---
title: 寄存器和栈
draft: true
---

# 寄存器和栈

这两种数据我选择放在一起讲。我们知道，大多数对数据的操作，如加减乘除、比大小等，都需要操作的是寄存器内的数据。那么，我们为什么需要把数据放在栈上呢？主要有两个原因：

* 寄存器数量不够
* 需要操作内存地址

如果我们一个函数内有三四十个局部变量，但是家用型CPU最多也就十几个通用寄存器，所以我们不可能把所有变量都放在寄存器中。因此我们需要把一部分数据放在内存中，栈就是一个很好的存储数据的地方；此外，有时候我们需要直接操作内存地址，但是寄存器并没有通用的地址表示，所以只能把数据放在栈上来完成对地址的操作。

因此，在不操作内存地址的前提下，栈只是寄存器的一个替代品。有一个很简单的例子可以解释这个概念。我们有一个很简单的C程序：

```c
// max.c
int max(int a, int b) {
    if (a > b) {
        return a;
    } else {
        return b;
    }
}

int main() {
    int a = max(1, 2);
    return 0;
}
```

我们将其编译成汇编文件。我们首先来看`max(1, 2)`是如何调用的：

```x86asm
movl    $1, %edi
movl    $2, %esi
callq   max
```

将参数`1`和`2`分别放到了寄存器`edi`和`esi`里。那么，`max`函数又是如何操作的呢？

```x86asm
    pushq   %rbp
    movq    %rsp, %rbp
    movl    %edi, -8(%rbp)        # Move data stored in %edi to stack at -8(%rbp)
    movl    %esi, -12(%rbp)       # Move data stored in %esi to stack at -12(%rbp)
    movl    -8(%rbp), %eax        # Move data stored in stack at -8(%rbp) to register %eax
    cmpl    -12(%rbp), %eax       # Compare data stored in stack at -12(%rbp) with data stored in %eax
    jle     .LBB0_2               # If compare result is less than or equal to, then go to label LBB0_2
    movl    -8(%rbp), %eax        # Move data stored in stack at -8(%rbp) to register %eax
    movl    %eax, -4(%rbp)        # Move data stored in %eax to stack at -4(%rbp)
    jmp     .LBB0_3               # Go to label LBB0_3
.LBB0_2:
    movl    -12(%rbp), %eax       # Move data stored in stack at -12(%rbp) to register %eax
    movl    %eax, -4(%rbp)        # Move data stored in %eax to stack at -4(%rbp)
.LBB0_3:
    movl    -4(%rbp), %eax        # Move data stored in stack at -4(%rbp) to register %eax
    popq    %rbp
    retq
```

考虑到篇幅，我将这个汇编每一个重要步骤所做的事都以注释形式写在了代码里面。这个看上去很复杂，但实际上做的是这样的事：

1. 把`int a`和`int b`看作局部变量，分别存储在栈上的`-8(%rbp)`和`-12(%rbp)`上
2. 为了比较这两个局部变量，将一个由栈上导入寄存器`eax`中
3. 比较`eax`寄存器中的值和另一个局部变量
4. 将两者中比较大的那个局部变量存储在栈上的`-4(%rbp)`上（由于x86_64架构不允许直接将内存中的一个值拷贝到另一个内存区域中，所以得先把内存区域中的值拷贝到`eax`寄存器里，再从`eax`寄存器里拷贝到目标内存中）
5. 将栈上`-4(%rbp)`这个用来存储返回值的区域的值拷贝到`eax`中，并返回

这看上去真是太费事了。但是，这也是无可奈何之举。这是因为，在不开优化的情况下，一个C的函数中的局部变量（包括传入参数）和返回值都应该存储在函数本身的栈帧中，所以，我们得把这简单的两个值在不同的内存区域和寄存器里来回拷贝。

那么，如果我们优化一下会怎样呢？我们使用

```shell
clang -O1 -S max.c
```

之后，我们的`max`函数的汇编代码是：

```x86asm
movl    %esi, %eax
cmpl    %esi, %edi
cmovgl  %edi, %eax
retq
```

那么长的一串代码竟然变的如此简洁了。这个代码翻译成伪代码就是

```pseudocode
function max(register a, register b) {
    register c = register b
    if (register a >= register c) {
        register c = register a
    }
    return register c
}
```

很简单的事，并且把所有的操作都从对内存的操作变成了对寄存器的操作。

因此，由这个简单的例子我们可以看出来，如果寄存器的数量足够，并且代码中没有需要操作内存地址的时候，寄存器是足够胜任的，并且更加高效的。

## 寄存器

正因为如此，LLVM IR引入了虚拟寄存器的概念。在LLVM IR中，一个函数的局部变量可以是寄存器或者栈上的变量。对于寄存器而言，我们只需要像普通的赋值语句一样操作，但需要注意名字必须以`%`开头：

```llvm
%local_variable = add i32 1, 2
```

此时，`%local_variable`这个变量就代表一个寄存器，它此时的值就是`1`和`2`相加的结果。我们可以写一个简单的程序验证这一点：

```llvm
; register_test.ll
define i32 @main() {
    %local_variable = add i32 1, 2
    ret i32 %local_variable
}
```

我们查看其编译出的汇编代码，其主函数为：

```x86asm
main:
    movl    $2, %eax
    addl    $1, %eax
    retq
```

确实这个局部变量`%local_variable`变成了寄存器`eax`。

关于寄存器，我们还需了解一点。在不同的ABI下，会有一些callee-saved register和caller-saved register。简单来说，就是在函数内部，某些寄存器的值不能改变。或者说，在函数返回时，某些寄存器的值要和进入函数前相同。比如，在System V的ABI下，`rbp`, `rbx`, `r12`, `r13`, `r14`, `r15`都需要满足这一条件，这在System V的ABI下被称作callee-saved registe。由于LLVM IR是面向多平台的，所以我们需要一份代码适用于多种ABI。因此，LLVM IR内部自动帮我们做了这些事。如果我们把所有没有被保留的寄存器都用光了，那么LLVM IR会帮我们把这些被保留的寄存器放在栈上，然后继续使用这些被保留寄存器。当函数退出时，会帮我们自动从栈上获取到相应的值放回寄存器内。

那么，如果所有通用寄存器都用光了，该怎么办？LLVM IR会帮我们把剩余的值放在栈上，但是对我们用户而言，实际上都是虚拟寄存器，用户是感觉不到差别的。

因此，我们可以粗略地理解LLVM IR对寄存器的使用：

* 当所需寄存器数量较少时，直接使用caller-saved register，即不需要保留的寄存器
* 当caller-saved register不够时，将callee-saved register原本的值压栈，然后使用callee-saved register
* 当寄存器用光以后，就把多的虚拟寄存器的值压栈

因此，我们还可以注意到，如果在调用别的函数的过程中，如果调用方的非callee-saved register中存有一些后续需要用到的数据，需要将这些数据放入栈上，在函数调用结束后，再从栈上将这些值放回相应的寄存器中。

我们可以写一个简单的程序验证。对于x86_64架构下，我们只需要使用15个虚拟寄存器就可以验证这件事。鉴于篇幅，我就不把代码放在文章中了，如果想看详细代码可以去我的GitHub仓库中查看`many_registers_test.ll`。我们将其编译成汇编语言之后，可以看到在函数开头就有

```x86asm
pushq    %r15
pushq    %r14
pushq    %r13
pushq    %r12
pushq    %rbx
```

也就是把那些需要保留的寄存器压栈。然后随着寄存器用光，第15个虚拟寄存器就会使用栈：

```x86asm
movl    $2, %eax
addl    $1, %eax
movl    %eax, -4(%rsp)
```

## 栈

我们之前说过，当不需要操作地址并且寄存器数量足够时，我们可以直接使用寄存器。而LLVM IR的策略保证了我们可以使用无数的虚拟寄存器。那么，在需要操作地址以及需要可变变量（之后会提到为什么）时，我们就需要使用栈。

LLVM IR对栈的使用十分简单，直接使用`alloca`指令即可。如：

```llvm
%local_variable = alloca i32
```

就可以声明一个在栈上的变量了。关于栈上变量的操作，我会在之后提到，目前我们对栈上变量的了解只需这么多。