---
title: 内置函数、属性和元数据
draft: true
---

# 内置函数、属性和元数据

在LLVM IR中，除了基础的数据表示、控制流之外，还有内置函数、属性和元数据等，能够影响二进制程序生成的功能。

## 内置函数

我们回顾一下，LLVM IR的作用实际上是将编译器前端与后端解耦合。编程语言的前端开发者，负责将输入的编程语言代码进行解析，生成LLVM IR；指令集架构的后端开发者，负责将输入的LLVM IR生成为目标架构的二进制指令。因此，LLVM IR提供了若干非常基础的指令，如`add`、`br`、`call`等。这样做的好处在于：

* 对前端开发者而言，这些指令语义足够全，使用方法也和常见高级语言类似。
* 对后端开发者而言，这些指令相对数目比较少，提供的功能也相对较为独立，在大部分常见的指令集中都有类似的指令与其对应。

但是，这样的策略也有其弊端：

* 对前端开发者而言，仍然有部分通用的语义无法被单个指令所涵盖
* 对后端开发者而言，对一些通用指令的优化无法针对LLVM IR指令来做

### `memcpy`

以内存拷贝为例。熟悉AMD64或者AArch64的开发者一定知道，在这些支持向量操作的指令集架构中，大规模的内存拷贝往往是通过向量指令来实现的，Glibc中的`memcpy`就是这样实现的。

但是对于通用编程语言来说，标准库往往不喜欢直接调用libc中的函数，会产生一些不必要的依赖。并且，`memcpy`用向量操作来实现已经是一个非常通用的方案了，所以能不能复用一些逻辑呢？

对于此类，LLVM IR指令过于基础，但是却非常广泛地使用同一套实现逻辑的情况，LLVM IR提供了「[内置函数](https://llvm.org/docs/LangRef.html#intrinsic-functions)」（Intrinsic Functions）功能来解决。

所谓内置函数，我们可以理解成一些可以像普通的LLVM IR函数一样调用的函数，但这些函数不需要开发者自己实现，LLVM的后端开发者提供了这些函数的实现。

例如，LLVM IR提供了[`llvm.memcpy`](https://llvm.org/docs/LangRef.html#llvm-memcpy-intrinsic)内置函数，以提供内存的拷贝操作。前端开发者只需要调用这个函数，就可以实现内存拷贝功能了。

我们熟知的Rust语言，在利用LLVM生成二进制程序时，就是使用的这个函数，可以参考其封装的[`LLVMRustBuildMemCpy`](https://github.com/rust-lang/rust/blob/90c541806f23a127002de5b4038be731ba1458ca/compiler/rustc_llvm/llvm-wrapper/RustWrapper.cpp#L1448-L1456)与调用者[`memcpy`](https://github.com/rust-lang/rust/blob/90c541806f23a127002de5b4038be731ba1458ca/compiler/rustc_codegen_llvm/src/builder.rs#L871-L896)。

### 静态分支预测

LLVM IR提供的内置函数有许多，这里，我们再以静态分支预测为例，介绍一个常见内置函数。

我们在阅读一些大规模项目源码时，例如Linux内核源码、QEMU源码等，往往会注意到大量使用的`likely`与`unlikely`，如：

```c
if (likely(x > 0)) {
    // Do something
}
```

这个`likely`是什么？它是干什么用的？事实上，`likely`与`unlikely`往往是通过宏定义实现的，它们的作用是静态分支预测。

我们知道，对于C语言等常见的编程语言的`if`语句，在生成二进制程序的时候，我们可以交换它的两个分支的位置。紧接着`cmp`等判断语句的分支，在执行时，不会发生跳转，而另一个分支则需要设置PC寄存器来跳转。这种跳转往往会造成一定程度的性能损耗，这些具体的我在「[在 Apple Silicon Mac 上入门汇编语言](https://github.com/Evian-Zhang/learn-assembly-on-Apple-Silicon-Mac)」中的[编译期分支预测](https://evian-zhang.github.io/learn-assembly-on-Apple-Silicon-Mac/11-跳转.html#编译期分支预测)一节中有详细阐述。总之，我们需要给编译器一些信息，来排布不同的分支布局。

对于Clang来说，这是通过[内置`expect`指令](https://llvm.org/docs/BranchWeightMetadata.html#built-in-expect-instructions)来实现的，也就是说：

```c
#define likely(x)       __builtin_expect(!!(x), 1)
#define unlikely(x)     __builtin_expect(!!(x), 0)
```

而`__builtin_expect`这个内置指令，就会翻译为LLVM IR中的[`llvm.expect`](https://llvm.org/docs/LangRef.html#llvm-expect-intrinsic)内置函数，从而实现了静态分支预测。

## 属性

在C语言中，我们会遇到一个函数的修饰符：`inline`。这个修饰符会提示编译器，建议编译器在遇到这个函数的调用时，内联这个函数。这类的信息，LLVM会将其看作函数的「[属性](https://llvm.org/docs/LangRef.html#function-attributes)」（Attribtues）。

在之前，我们也提到过，我们可以：

```llvm
define void @foo() attr1 attr2 attr3 {
    ; ...
}
```

如果有多个函数有相同的属性，我们可以用一个属性组的形式来复用：

```llvm
define void @foo1() #0 {
    ; ...
}
define void @foo2() #0 {
    ; ...
}
attributes #0 = { attr1 attr2 attr3 }
```

LLVM支持的函数属性有多种，我们来看看几个比较容易理解的，由函数属性控制的优化：

### 内联

函数内联是一个非常复杂的概念，这里我们只是简单地来看一下，下面这个C语言代码：

```c
inline int foo(int a) __attribute__((always_inline));

int foo(int a) {
    if (a > 0) {
        return a;
    } else {
        return 0;
    }
}
```

这里声明了`foo`函数，并且用了一个扩展语法`__attribute__((always_inline))`，这个语法实际上的作用就是给函数加上`alwaysinline`的属性。

我们查看其生成的LLVM IR：

```llvm
define dso_local i32 @foo(i32 noundef %0) #0 {
  ; ...
}

attributes #0 = { alwaysinline nounwind uwtable "frame-pointer"="all" "min-legal-vector-width"="0" "no-trapping-math"="true" "stack-protector-buffer-size"="8" "target-cpu"="x86-64" "target-features"="+cx8,+fxsr,+mmx,+sse,+sse2,+x87" "tune-cpu"="generic" }
```

可以看到，其确实有了`alwaysinline`这个属性。

### 帧指针清除优化

我们再来看一个属性控制的优化：帧指针清除优化（Frame Pointer Elimination）。

在讲这个之前，先讲一个比较小的优化。我们将一个非常简单的C程序

```c
void foo(int a, int b) {}
int main() {
    foo(1, 2);
    return 0;
}
```

编译为汇编程序，可以发现，`foo`函数的汇编代码为：

```x86asm
foo:
    pushq   %rbp
    movq    %rsp, %rbp
    movl    %edi, -4(%rbp)
    movl    %esi, -8(%rbp)
    popq    %rbp
```

与我们常识有些违背。为啥这里栈不先增加（也就是对`rsp`寄存器进行`sub`），就直接把`edi`, `esi`的值移入栈内了呢？`-4(%rbp)`和`-8(%rbp)`的内存空间此刻似乎并不属于栈。

这是因为，在System V关于amd64架构的标准中，规定了`rsp`以下128个字节为red zone。这个区域，信号和异常处理函数均不会使用。因此，一个函数可以放心使用`rsp`以下128个字节的内容。

同时，我们对栈指针进行操作，一个很重要的原因就是为了进一步函数调用的时候，使用`call`指令会自动将被调用函数的返回地址压栈，那么就需要在调用`call`指令之前，保证栈顶指针确实指向栈顶，否则压栈就会覆盖一些数据。

但此时，我们的`foo`函数并没有调用别的函数，也就不会产生压栈行为。因此，如果在栈帧不超过128个字节的情况下，编译器自动为我们省去了这样的操作。为了验证这一点，我们做一个小的修改：

```c
void bar() {}
void foo(int a, int b) { bar(); }
int main() {
    foo(1, 2);
    return 0;
}
```

这时，我们再看编译出的`foo`函数的汇编代码：

```x86asm
foo:
    pushq   %rbp
    movq    %rsp, %rbp
    subq    $16, %rsp
    movl    %edi, -4(%rbp)
    movl    %esi, -8(%rbp)
    callq   bar
    addq    $16, %rsp
    popq    %rbp
    retq
```

确实增加了对`rbp`的`sub`和`add`操作。而此时的`bar`函数，也没有对`rsp`的操作。

接下来，就要讲帧指针清除优化了。经过我们上述的讨论，一个函数在进入时会有一些固定动作：

1. 把`rbp`压栈
2. 把`rsp`放入`rbp`
3. 减`rsp`，预留栈空间

在函数返回之前，也有其相应的操作：

1. 加`rsp`，回收栈空间
2. 把`rbp`最初的值弹栈回到`rbp`

我们刚刚讲的优化，使得没有调用别的函数的函数，可以省略掉进入时的第3步和返回前的第1步。那么，是否还可以继续省略呢？

那么，我们就要考虑为什么需要这些步骤。这些步骤都是围绕`rbp`进行的，而正是因为`rbp`经常进行这种操作，所以我们把`rbp`称为帧指针。之所以要进行这些操作，是因为我们在函数执行的过程中，栈顶指针随着不断调用别的函数，会不断移动，导致我们根据栈顶指针的位置，不太方便确定局部变量的位置。而如果我们在一开始就把`rsp`的值放在`rbp`中，那么局部变量的位置相对`rbp`是固定的，就更好确认了。注意到我们这里说根据`rsp`的值确认局部变量的位置只是不方便，但并不是不能做到。所以，我们可以增加一些编译器的负担，而把帧指针清除。

帧指针清除在LLVM IR层面其实十分方便，就是什么都不写。我们可以观察

```llvm
define void @foo(i32 %a, i32 %b) {
    %1 = alloca i32
    %2 = alloca i32
    store i32 %a, ptr %1
    store i32 %b, ptr %2
    ret void
}
```

这个函数在编译成汇编语言之后，是：

```x86asm
foo:
    movl    %edi, -4(%rsp)
    movl    %esi, -8(%rsp)
    retq
```

不仅没有了栈的增加减少（之前提过的优化），也没有了对`rbp`的操作（帧指针清除）。

要想恢复这一操作也十分简单，在函数参数列表后加上一个属性`"frame-pointer"="all"`：

```llvm
define void @foo(i32 %a, i32 %b) "frame-pointer"="all" {
    %1 = alloca i32
    %2 = alloca i32
    store i32 %a, ptr %1
    store i32 %b, ptr %2
    ret void
}
```

其编译后的汇编程序就是：

```x86asm
foo:
    pushq   %rbp
    movq    %rsp, %rbp
    movl    %edi, -4(%rbp)
    movl    %esi, -8(%rbp)
    popq    %rbp
    retq
```

恢复了往日的雄风。

## 元数据

函数的属性可以在前后端之间传递函数的信息，例如，前端发现某个函数需要后端的特殊处理，就给这个函数加一个自定义的属性。而在LLVM的整个管线中的任意一个位置，我们往往都能读到这个属性，从而可以依据是否有这个属性来做特殊的处理/优化。正因如此，之所以函数要有属性，是因为函数是LLVM的优化过程中一个非常重要的基础单元，因此需要保留各种信息。

除此之外，我们有时也会希望每一条指令，或者每一个翻译单元，都可以有类似属性一样的信息，可以在管线中传递/过滤，从而能获得一些信息。这在LLVM IR中被称为「[元数据](https://llvm.org/docs/LangRef.html#metadata)」（Metadata）。

### 调试信息

说了这么多，元数据具体有什么用处呢？元数据的语法又是怎样的呢？我们来看一个具体的例子。

我们知道，在Clang中，传入`-g`选项可以生成调试信息。那么，调试信息是怎么在LLVM IR中体现的呢？

我们这样一个`debug.c`文件：

```c
int sum(int a, int b) {
    return a + b;
}
```

我们使用

```shell
clang debug.c -g -S -emit-llvm
```

生成LLVM IR文件，其一部分如下：

```llvm
; ...
; Function Attrs: noinline nounwind optnone uwtable
define dso_local i32 @sum(i32 noundef %0, i32 noundef %1) #0 !dbg !10 {
  %3 = alloca i32, align 4
  %4 = alloca i32, align 4
  store i32 %0, ptr %3, align 4
  call void @llvm.dbg.declare(metadata ptr %3, metadata !15, metadata !DIExpression()), !dbg !16
  store i32 %1, ptr %4, align 4
  call void @llvm.dbg.declare(metadata ptr %4, metadata !17, metadata !DIExpression()), !dbg !18
  %5 = load i32, ptr %3, align 4, !dbg !19
  %6 = load i32, ptr %4, align 4, !dbg !20
  %7 = add nsw i32 %5, %6, !dbg !21
  ret i32 %7, !dbg !22
}

; ...

!llvm.dbg.cu = !{!0}
!llvm.module.flags = !{!2, !3, !4, !5, !6, !7, !8}
!llvm.ident = !{!9}

!0 = distinct !DICompileUnit(language: DW_LANG_C11, file: !1, producer: "Homebrew clang version 16.0.6", isOptimized: false, runtimeVersion: 0, emissionKind: FullDebug, splitDebugInlining: false, nameTableKind: None)
!1 = !DIFile(filename: "debug.c", directory: "...", checksumkind: CSK_MD5, checksum: "...")
; ...
!10 = distinct !DISubprogram(name: "sum", scope: !1, file: !1, line: 1, type: !11, scopeLine: 1, flags: DIFlagPrototyped, spFlags: DISPFlagDefinition, unit: !0, retainedNodes: !14)
!11 = !DISubroutineType(types: !12)
!12 = !{!13, !13, !13}
!13 = !DIBasicType(name: "int", size: 32, encoding: DW_ATE_signed)
!14 = !{}
!15 = !DILocalVariable(name: "a", arg: 1, scope: !10, file: !1, line: 1, type: !13)
!16 = !DILocation(line: 1, column: 13, scope: !10)
!17 = !DILocalVariable(name: "b", arg: 2, scope: !10, file: !1, line: 1, type: !13)
!18 = !DILocation(line: 1, column: 20, scope: !10)
!19 = !DILocation(line: 2, column: 12, scope: !10)
!20 = !DILocation(line: 2, column: 16, scope: !10)
!21 = !DILocation(line: 2, column: 14, scope: !10)
!22 = !DILocation(line: 2, column: 5, scope: !10)
```

我们可以看到，在生成的LLVM IR中，出现了大量以`!`开头的符号，这就是元数据的语法。

具体而言，我们看到其中的

```llvm
!12 = !{!13, !13, !13}
!13 = !DIBasicType(name: "int", size: 32, encoding: DW_ATE_signed)
```

这里，`!13 = ...`生成了一个元数据，其内容为一个给定的结构体`DIBasicType`，而`!12`这个元数据的内容，则并不是一个给定的结构体，而是由三个`!13`这个元数据组成的结构。也就是说，元数据的组织相对比较灵活。

在`sum`函数体中，我们可以看到，几乎每条指令后都附加了一个元数据，在代码下半部分找到对应的元数据，其实就是这行指令对应C语言中源代码里的位置，也就是调试信息中的location。

此外，我们还可以看到`llvm.dbg.declare`内置函数的调用。这个函数的作用是标记源代码中变量的地址。例如：

```llvm
store i32 %0, ptr %3, align 4
call void @llvm.dbg.declare(metadata ptr %3, metadata !15, metadata !DIExpression()), !dbg !16
```

这里就是指，源代码中位于`!15`元数据处的变量，也就是`a`，其在生成的二进制程序中，位于`%3`变量。

LLVM中的调试信息非常全面且复杂，具体可以看官方文档[Source Level Debugging with LLVM](https://llvm.org/docs/SourceLevelDebugging.html)。

### 控制流完整性

元数据的另一个用途，就在于控制流完整性保护。当一个攻击者攻击一个二进制程序的时候，最低级的攻击者只是让它崩溃，造成DoS攻击。高级的攻击者，往往想让这个程序执行自己想让它执行的命令。而这一途径，在现代攻击环境下，往往是通过函数指针覆盖来实现的。

举一个例子来说，在前几年，有一个非常著名的漏洞[checkm8](https://twitter.com/axi0mX/status/1177542201670168576?s=20)。这个漏洞可以攻击苹果的大部分iPhone设备，并且由于代码处于ROM中，所以被认为无法修复。其具体的分析可以看[Technical analysis of the checkm8 exploit](https://habr.com/en/companies/dsec/articles/472762/)和[iPhone史诗级漏洞checkm8攻击原理浅析 - Gh0u1L5的文章 - 知乎](https://zhuanlan.zhihu.com/p/87456653)。我们这里只需要了解一点，它的核心是，Apple代码中有一个结构体

```c
struct usb_device_io_request {
    void *callback;
    // ...
};
```

这里`callback`是一个函数指针，在程序执行中会被调用。攻击者通过某种方法，强行覆盖了这个函数指针的值，从而让程序执行自己想要执行的函数。

为了抵御这种攻击，我们往往会采用控制流完整性（Control Flow Integrity, CFI）策略。最简单的思路是，我们在写程序时，函数指针所指向的函数，肯定是有限个确定的函数。那么，我们可以在执行函数指针所对应的间接调用时，检查调用目标是否是那有限个确定的函数，就可以保证不会出现之前的这种问题了。

但是，如何确定这个函数指针究竟能指向哪些函数呢？这个问题非常复杂，编译器往往是做不到这件事的。因此，现在一般会使用比较弱化的控制流完整性策略。在LLVM中，我们可以通过传递`-fsanitize=cfi-icall`来启用LLVM-CFI所提供的控制流完整性策略（需要同时通过`-flto`开启LTO），例如，我们有以下程序：

```c
typedef void (*f)(void);

void foo1(void) {}
void foo2(void) {}
void bar(int a) {}

void baz(f func) {
    func();
}
```

将其保存为`cfi.c`，然后在命令行中使用

```shell
clang cfi.c -flto -fsanitize=cfi-icall -S -emit-llvm
```

可以生成一个开启了LLVM-CFI策略的LLVM IR代码。

那么，LLVM-CFI策略是什么呢？由于其相对比较复杂，具体可以参考[Control Flow Integrity Design Documentation](https://clang.llvm.org/docs/ControlFlowIntegrityDesign.html)，我们这里只是非常粗略地讲。

在上述代码中，`baz`函数接收一个函数指针，然后调用了这个函数指针。这个函数指针的类型是，不接收参数，也没有返回值。而LLVM-CFI采用的策略则是，只要满足这个类型的函数，都被认为是可以被函数指针所指向的。反之，如果不满足，则被拒绝。也就是说，在这个代码中，`foo1`、`foo2`都是满足的，而`bar`函数，因为它接收一个`int`类型的参数，所以不满足。

那么，具体是怎么实现的呢？我们来看看它的LLVM IR代码，其一部分为：

```llvm
; Function Attrs: noinline nounwind optnone uwtable
define dso_local void @foo1() #0 !type !9 !type !10 {
  ret void
}

; Function Attrs: noinline nounwind optnone uwtable
define dso_local void @foo2() #0 !type !9 !type !10 {
  ret void
}

; Function Attrs: noinline nounwind optnone uwtable
define dso_local void @bar(i32 noundef %0) #0 !type !11 !type !12 {
  %2 = alloca i32, align 4
  store i32 %0, ptr %2, align 4
  ret void
}

; Function Attrs: noinline nounwind optnone uwtable
define dso_local void @baz(ptr noundef %0) #0 !type !13 !type !14 {
  %2 = alloca ptr, align 8
  store ptr %0, ptr %2, align 8
  %3 = load ptr, ptr %2, align 8
  %4 = call i1 @llvm.type.test(ptr %3, metadata !"_ZTSFvvE"), !nosanitize !15
  br i1 %4, label %6, label %5, !nosanitize !15

5:                                                ; preds = %1
  call void @llvm.ubsantrap(i8 2) #3, !nosanitize !15
  unreachable, !nosanitize !15

6:                                                ; preds = %1
  call void %3()
  ret void
}

!9 = !{i64 0, !"_ZTSFvvE"}
!10 = !{i64 0, !"_ZTSFvvE.generalized"}
!11 = !{i64 0, !"_ZTSFviE"}
!12 = !{i64 0, !"_ZTSFviE.generalized"}
```

可以看到，在`baz`函数中，在调用这个函数指针，也就是`call void %3()`之前，被插入了一部分代码：

```llvm
  %3 = load ptr, ptr %2, align 8
  %4 = call i1 @llvm.type.test(ptr %3, metadata !"_ZTSFvvE"), !nosanitize !15
  br i1 %4, label %6, label %5, !nosanitize !15
5:                                                ; preds = %1
  call void @llvm.ubsantrap(i8 2) #3, !nosanitize !15
  unreachable, !nosanitize !15
```

在这里，首先调用了`llvm.type.test`这个内置函数。这个内置函数的作用是查看`ptr %3`这个函数的类型，是否是`!"_ZTSFvvE"`这个元数据所代表的类型，如果不是的话，就跳转，调用`llvm.ubsantrap`报告错误。而我们可以看到，`foo1`、`foo2`、`bar`都被附加了一些元数据，查看代码的下半部分，可以看到，`foo1`、`foo2`的元数据是`!"_ZTSFvvE"`，而`bar`的元数据是`!"_ZTSFviE"`。因此，如果攻击者想让这个间接调用前往`bar`函数，就会被拒绝，从而保护了控制流的完整性。