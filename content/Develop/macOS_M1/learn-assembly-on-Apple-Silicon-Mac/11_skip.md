---
title: 跳转
draft: true
---

# 跳转

在我们日常编程的过程中，控制流的跳转是不可或缺的，如`if`-`else`语句、`while`和`for`循环等。这一类语句是怎样在汇编层面实现的呢？

## 标签

在介绍几种汇编层面的跳转之前，我们首先需要知道标签的概念。我们之前接触到的`_main:`就是一个标签。

在汇编语言中，标签往往不进行缩进，同时以`:`结尾。标签的作用是标记当前的地址。例如，我们最开始的汇编程序

```armasm
# 5-basic.s
    .section    __TEXT,__text
    .globl  _main
    .p2align    2
_main:
    mov    w0, #0
    ret
```

这个汇编程序中，`_main`标签标记了`mov    w0, #0`这条指令的地址，在接下来的任何指令中，如果用到`_main`这个标签（例如，跳转到`_main`标签所标记的位置。使用方法随后就会介绍），汇编器就会使用其地址来代替。

值得注意的是，这里使用了PC-relative的技巧。在[操作系统](4_Operating_system.md)一章中我们提到，为了充分随机化进程中的地址，我们需要编写Position-Independent Code。这里面要求，所有的指令不能涉及绝对地址。那么，如果直接将标签替换为相对应的绝对地址，是不满足PIC的要求的。所以如何处理我们的标签，才能正确编码相应的跳转指令，使得程序中不含有绝对地址呢？

我们可以注意到一件事，虽然一个进程在内存中的栈、堆、代码段等的基地址产生了随机化，但是其内部是不可以随机化的。例如，在代码段里，一条指令长32位。那么在执行这条指令时，`pc`寄存器的值加4，就一定是下一条指令的地址。也就是说，指令之间地址的距离是保持不变的。因此，我们可以使用「这个标签标记的位置距离这条指令的距离」来编码这个标签。这就是PC-relative的地址编码。

例如，有一条跳转指令，它的跳转目标是其之前的3条指令所在的位置（一条指令长32位），那么PC-relative的编码方式就可以是-12。

## 无条件直接跳转

所谓的无条件跳转，就是指执行这条语句后，控制流总是会前往指定的地方。C语言中的`goto`是一个比较直接的无条件直接跳转。在A64指令集中，无条件直接跳转使用`b`指令来表示。

例如，我们有以下汇编程序：

```armasm
foo:
    add    w0, w0, #1
    b      foo
```

那么这个程序就会陷入一个死循环，不断地给`w0`寄存器里的值加1。

我们在日常编程的过程中，什么时候会比较常用到这种无条件跳转呢？答案是在`switch`语句中。

考虑下面这个C语言程序片段：

```c
switch (a) {
    case 0: /* do something A */ break;
    case 1: /* do something B */ break;
}
// do something C
```

先不考虑`switch`本身的跳转怎么实现的，我们来看看`switch`之后的`break`该如何实现：

```armasm
    ; Decide whether to do something A, B or C by a's value
zero_case:
    ; Do something A
    b    after_switch
one_case:
    ; Do something B
    b    after_switch
after_switch:
    ; Do something C
```

使用无条件直接跳转来实现`break`语句是一个很直观的想法。

## PSTATE

在介绍条件跳转之前，我们首先需要了解AArch64的PSTATE机制。

在之前介绍基本的数据处理指令时，我们忽视了一个很重要的事：溢出。在[底层的整数](1_Underlying_integer.md)中我们提到，溢出是一个很严重的事情。因此，我们需要知道，我们进行的这个算术运算，会不会产生溢出。

我们在实现条件跳转的时候，也会思考，我们选择性跳转所依赖的「条件」，究竟可以是哪些条件？事实上，无外乎大于、小于等等。而这种大于小于的比较，我们也可以转化为一个算术运算：将两数相减，看结果是大于0，还是小于0。

因此，在我们进行算术运算的过程中，一些结果的“状态”对我们的编程是有意义的。这些状态，如是否溢出、是否小于0等，都是只有「是」或「否」两种可能。用来表示这种状态的，就是PSTATE机制。

在AArch64架构中，PSTATE（Process State）一种进程状态信息（Process State, PSTATE）。PSTATE存储了当前进程的状态，例如当前的异常级别、安全级别等等。此外，PSTATE还存储了一些条件位（Conditional Flags），被称为ALU标志位，其中包括：

* N位

   1表示结果为负，0表示结果非负
* Z位

   1表示结果为零，0表示结果非零
* C位

   1表示结果有进位，0表示结果无进位
* V位

   1表示结果有溢出，0表示结果无溢出

这些概念很抽象，那我们实际的指令是如何影响PSTATE的呢？

事实上，我们之前所讲的数据处理指令一般是默认不影响PSTATE的。这事因为大部分的数据处理指令的执行，并不会作为后续条件跳转的条件，从而可以节约计算成本。而如果我们需要使用可以影响PSTATE的指令，则需要在后面加上一个`s`。

例如，`adds`是`add`的一个变种，可以影响PSTATE。当结果相加为0，则会设立Z位。

但是，这些结尾加`s`的指令，从某种意义上讲，是「有副作用」的指令。因为这些指令，都需要一个目的操作数。也就是说，其需要将运算结果存储在目的寄存器中。但是，在大部分情况下，我们高级语言编写条件语句时，都仅仅是作一个大小的比较，并不需要得到实际的结果。因此，AArch64架构提供了更符合开发者语义的指令：`cmp`和`tst`。

`cmp    a, b`指令是`subs    wzr, a, b`的别名。也就是说，`cmp`指令将两数直接相减，并且不存储其相减的结果，同时设置PSTATE的ALU位。这就是最常见的比较指令。

`tst    a, b`指令是`ands    wzr, a, b`的别名。也就是说，`tst`指令将两数逐位相与，并设置PSTATE的ALU位。设计这个指令的目的是因为，在高级语言中，有非常非常多判断一个值是否为0的操作。与使用`cmp`，也就是减去0相比，更巧妙的方法是将这个值与自身相与，也就是`tst    a, a`。那么，这个值为0，当且仅当与自身相与的结果为0。

## 条件跳转

介绍了PSTATE机制之后，我们就可以了解条件跳转了。所谓条件跳转，就是指这种跳转需要依赖某种运行时的条件才能进行，也就是我们最常见的`if`语句。

### 条件分支指令

在AArch64架构下，这主要是由`b.{COND}`系列指令实现的（在ARMv8之前，几乎所有指令都可以条件执行。但是后续的基准测试表明，当前的分支预测器已经足够优秀，不需要再浪费额外编码空间来编码条件字段了。具体描述可以参考[Why are conditionally executed instructions not present in later ARM instruction sets?](https://newbedev.com/why-are-conditionally-executed-instructions-not-present-in-later-arm-instruction-sets)）。

所谓`b.{COND}`系列指令，其实和`b`指令类似，也需要后面跟着一个标签。但是，其`{COND}`部分则决定了其是否执行。

例如，`b.eq    foo`指令的意思就是，如果此时PSTATE的Z位为1（例如，之前执行了`cmp`指令，如果两个操作数相等，则相减结果为0，会将Z位置1），则跳转到`foo`标签所在的位置。

我们常见的`{COND}`部分包括：

* `eq`、`ne`

   表示是否相等。
   
   * `eq`表示相等，判断Z位是否为1：`Z == 1`
   * `ne`表示不等，判断Z位是否为0：`Z == 0`
* `hi`、`hs`、`ls`、`lo`

   表示无符号整数的比较。
   
   * `hi`表示大于，判断是否C位为1且Z位为0：`C == 1 && Z == 0`
   * `hs`表示大于等于，判断C位是否为1：`C == 1`
   * `ls`表示小于等于，判断是否C位为0或Z位为1：`!(C == 1 && Z == 0)`
   * `lo`表示小于，判断是否C位为0：`C == 0`
* `gt`、`ge`、`le`、`lt`

   表示有符号整数的比较。
   
   * `gt`表示大于，判断是否Z位为0且N位与V位相等：`Z == 0 && N == V`
   * `ge`表示大于等于，判断N位是否与V位相等：`N == V`
   * `le`表示小于等于，判断是否Z位为1或者N位与V位不等：`!(Z == 0 && N == V)`
   * `lt`表示小于，判断N位是否与V位不等：`N != V`

由此可见，巧妙地运用PSTATE的ALU位，就可以用来条件跳转。

### 条件选择指令

在我们日常使用高级语言进行开发的过程中，往往会有固定的代码片段。例如：

```c
int a;
if (condition()) {
    a = b;
} else {
    a = c;
}
// 等价于
// int a = condition() ? b : c;
```

鉴于这种代码片段的普遍性，AArch64架构下也有专门的指令来做这件事，这就是`csel`指令，其指令形式为

```plaintext
csel    dest_reg, src_reg1, src_reg2, {COND}
```

例如：

```plaintext
csel    w0, w1, w2, eq
```

这条语句的意思就是，如果当前PSTATE满足`eq`的条件（也就是`Z == 1`），那么就将`w1`赋值给`w0`，否则将`w2`赋值给`w0`。

## 常见的控制语句

在了解了无条件跳转与条件跳转之后，我们就可以写出常见控制语句的汇编形式了。

首先，以`if`语句为例：

```c
// int a, b;
if (a > b) {
    // do A
}
// do B
```

其对应的汇编代码为

```armasm
    ; a in w0, b in w1
    cmp    w0, w1
    b.le   do_b
    ; do A
do_b:
    ; do B
```

可以发现，在这种模式下，条件跳转的判断条件与C语言中的判断条件恰好相反。

类似地，我们也可以写出`for`循环的汇编代码：

```c
for (i = 0; i < a; /* do A */) {
    /* do B */
}
/* do C */
```

对应的汇编代码为：

```armasm
    ; i in w0, a in w1
    mov    w0, #0
compare:
    cmp    w0, w1
    b.ge   out
    ; do B
    ; do A
    b      compare
out:
    ; do C
```

见多了就会发现，这类控制语句转化为汇编语句时，最巧妙的往往是通过基本块的排列和判断条件的设置来尽可能少的减少跳转语句和基本块复杂度。

## 分支预测

### 运行时分支预测

随着人们对CPU要求越来越高，CPU设计者也在想方设法提高CPU的性能。在这些提升CPU性能的方法中，大部分都需要预先知道CPU后续需要执行的指令。例如，如果我在`mov    w0, #0`后是`mov    w1, #0`，那么这两条指令之间没有数据依赖关系，所以CPU可以调整这两条指令的执行顺序，也可以并行执行这两条指令。但是这一系列优化的前提是CPU需要知道后续执行的指令是什么。

在顺序执行中，CPU可以很方便地预测后续执行的指令是什么。但是如果程序中有条件跳转，那么只有真正运行到这条指令时，CPU才能知道后续执行的指令是哪一条。这极大地影响了CPU执行的效率。因此，现在大部分的CPU都有了分支预测器。分支预测器的工作，是通过大量的执行，训练出一个能够预测某条分支指令执行结果的模型。

但是，这种分支预测本身也耗时，有时候又会拖慢执行。在Rust的std源码中，有一个非常著名的例子（位于`library/core/src/iter/adapters/filter.rs`文件中）：

```rust
pub struct Filter<I, P> {
    iter: I,
    predicate: P,
}

impl<I: Iterator, P> Filter<I, P>
where
    P: FnMut(&I::Item) -> bool,
{
    // this special case allows the compiler to make `.filter(_).count()`
    // branchless. Barring perfect branch prediction (which is unattainable in
    // the general case), this will be much faster in >90% of cases (containing
    // virtually all real workloads) and only a tiny bit slower in the rest.
    //
    // Having this specialization thus allows us to write `.filter(p).count()`
    // where we would otherwise write `.map(|x| p(x) as usize).sum()`, which is
    // less readable and also less backwards-compatible to Rust before 1.10.
    //
    // Using the branchless version will also simplify the LLVM byte code, thus
    // leaving more budget for LLVM optimizations.
    #[inline]
    fn count(self) -> usize {
        #[inline]
        fn to_usize<T>(mut predicate: impl FnMut(&T) -> bool) -> impl FnMut(T) -> usize {
            move |x| predicate(&x) as usize
        }

        self.iter.map(to_usize(self.predicate)).sum()
    }
}
```

简单解释一下这个代码。这段片段中的`count`函数，其功能目的是实现下面这段代码片段：

```rust, ignore
let mut count = 0;
for element in collection {
    if some_condition(element) {
        count += 1;
    }
}
```

那么，`count`函数本身是怎么实现的呢？它实际上做了一个这样的事：

```rust, ignore
let mut count = 0;
for element in collection {
    count += some_condition(element) as usize
}
```

我们知道，`some_condition()`函数返回的是一个布尔值，而其在底层必然是一个整型0或者1。那么通过这种方法，确实可以实现`count`的目的。并且，通过这种方法，去除了这个`if`对应的条件跳转语句，从而也不需要分支预测器登场，更好地提升了效率。

### 编译期分支预测

上述的运行时分支预测中使用的技巧，是我们在日常编程中与分支预测关系最密切的一种了。那么，有没有编译期的分支预测呢？或者说，编译期的分支预测有什么意义呢？

在上面叙述常见控制语句对应的汇编代码时，我们没有讲`if`-`else`语句。下面我们来看看：

```c
// int a, b;
if (a > b) {
    // do A
} else {
    // do B
}
// do C
```

事实上，其可以对应两种汇编代码：

```armasm
    ; a in w0, b in w1
    cmp    w0, w1
    b.le   do_b
    ; do A
    b      do_c
do_b:
    ; do B
do_c:
    ; do C
```

和

```armasm
    ; a in w0, b in w1
    cmp    w0, w1
    b.gt   do_a
    ; do B
    b      do_c
do_a:
    ; do A
do_c:
    ; do C
```

这两种汇编语句，无外乎利用判断条件来对调一下`if`和`else`的基本块。那么，我们应该选择哪一种方案呢？这两种方案有何优劣呢？

事实上，在某些代码结构下，这两种方案的同一个分支（如`true`分支）的性能会有差别，例如[执行跳转对刷新CPU流水线有负面效果](https://kernelnewbies.org/FAQ/LikelyUnlikely)。因此，如果不进行跳转就可以到**更有可能被执行到的**基本块，那么总体而言对CPU的执行有利（具体的例子我们马上就可以见到）。

因此，我们有了一个非标准的`__builtin_expect`（[GCC](https://gcc.gnu.org/onlinedocs/gcc/Other-Builtins.html)和[Clang](https://clang.llvm.org/docs/LanguageExtensions.html#builtin-expect)都支持）和C++20标准里的[`likely`和`unlikely`属性](https://en.cppreference.com/w/cpp/language/attributes/likely)。

这里以`__builtin_expect`为例。在大部分大型C语言项目中，我们都可以见到如下的定义（例如在Linux内核中）：

```c
#define likely(x)       __builtin_expect(!!(x), 1)
#define unlikely(x)     __builtin_expect(!!(x), 0)
```

而具体使用的时候为：

```c
if (likely(a > b)) {
    // do A
} else {
    // do B
}
// do C
```

通过这个宏，编译器会得到用户提供的分支预测信息，也就是说，`a > b`的分支是更有可能被执行到的。以LLVM为例，在编译器编译分支语句时，对`true`分支和`false`分支各记录一个分支权重（[Branch Weight](https://llvm.org/docs/BranchWeightMetadata.html)）。我们通过`likely`和`unlikely`这样的宏可以**一定程度影响**这种分支权重。最终在生成分支语句时，LLVM会根据两个分支的分支权重来布局基本块位置。

下面举一个例子。我们有一个C语言代码（可以在[codes/11-likely.c](https://github.com/Evian-Zhang/learn-assembly-on-Apple-Silicon-Mac/blob/master/codes/11-likely.c)文件中看到）：

```c
#define likely(x)    __builtin_expect(!!(x), 1)
#define unlikely(x)  __builtin_expect(!!(x), 0)

extern void foo();
extern void bar();

void likely_pattern(int a) {
    if (likely(a > 0)) {
        foo();
    } else {
        bar();
    }
}

void unlikely_pattern(int a) {
    if (unlikely(a > 0)) {
        foo();
    } else {
        bar();
    }
}
```

其中`likely_pattern`和`unlikely_pattern`中除了`likely`和`unlikely`宏的使用外没有任何区别。

我们使用Clang生成相应的汇编文件：

```bash
clang 11-likely.c -O1 -S -o 11-likely.s
```

我们查看`11-likely.s`文件，可以看到以下关键代码（已省略无关代码）：

```armasm
_likely_pattern:
    ; ...
    cmp    w0, #1
    b.lt   LBB0_2
    bl     _foo
    ; ...
    ret
LBB0_2:
    bl     _bar
    ; ...
    ret

_unlikely_pattern:
    ; ...
    cmp    w0, #1
    b.ge   LBB1_2
    bl     _bar
    ; ...
    ret
LBB1_2:
    bl     _foo
    ; ...
    ret
```

其中`bl    _foo`和`bl    _bar`的意思分别对应C语言中对`foo()`和`bar()`函数的调用。

我们可以看到，在分别使用`likely`和`unlikely`后，这两个函数内部的条件跳转语句的分支基本块的布局发生了变化。以`likely_pattern`为例，我们告知编译器，这个分支语句更有可能走`true`分支。因此，如果我们在汇编层面走`true`分支的话，就会发现，`b.lt    LBB0_2`并没有发生跳转。而我们之前提到，发生跳转对CPU执行效率不利。因此，这种分支布局更有利于CPU执行效率。

## 间接跳转

间接跳转的意思是指，跳转的地址不再是编译期给定的静态的地址，而是存储在寄存器中的地址。其对应的汇编指令是`br`。例如：

```armasm
br    x0
```

就是指，跳转到`x0`寄存器中存储的地址。

这个有什么用呢？

我们在学习C语言的过程中，一定看过一个说法：`switch`语句的效率比多个`if`-`else`语句串在一起要高。那究竟为什么会这样呢？我们不妨写一个C语言的程序（源码位于[codes/11-switch.c](https://github.com/Evian-Zhang/learn-assembly-on-Apple-Silicon-Mac/blob/master/codes/11-switch.c)文件）：

```c
switch (a) {
    case 0: foo0(); break;
    case 1: foo1(); break;
    case 2: foo2(); break;
    case 3: foo3(); break;
}
```

我们将其编译为汇编语言，其关键部分的代码为：

```armasm
    ; C Variable a is in x8
    str    x8, [sp]
    subs   x8, x8, #3
    b.hi   LBB0_6
    ldr    x11, [sp]
    adrp   x10, lJTI0_0@PAGE
    add    x10, x10, lJTI0_0@PAGEOFF
Ltmp0:
    adr    x8, Ltmp0
    ldrsw  x9, [x10, x11, lsl #2]
    add    x8, x8, x9
    br     x8
LBB0_2:
    bl     _foo0
    b      LBB0_6
LBB0_3:
    bl     _foo1
    b      LBB0_6
LBB0_4:
    bl     _foo2
    b      LBB0_6
LBB0_5:
    bl     _foo3
    b      LBB0_6
LBB0_6:
    ; ...
    ret

    .p2align    2
lJTI0_0:
    .long  LBB0_2-Ltmp0
    .long  LBB0_3-Ltmp0
    .long  LBB0_4-Ltmp0
    .long  LBB0_5-Ltmp0
```

我们首先可以发现，它生成了一个位于`LJTI0_0`标签处的全局变量。

下面，以`a`为2为例，看看这是怎么运行的。

1. 最开始时，将判断`a`是否大于3（采用`hi`这种无符号比较的话，同时也可以将所有负数排除在外），如果大于3则直接跳转到`LBB0_6`，也就是不进入`switch`语句。
2. 随后，执行到`ldrsw  x9, [x10, x11, lsl #2]`时，由于`x10`是`LJTI0_0`的地址，`x11`是`a`的值，因此`x9`是`LJTI0_0 + 2 * 4`处的值，也就是`LBB0_4 - Ltmp0`。
3. 接下来，`x8`的值是`Ltmp0`的地址，因此将`x8`与`x9`相加，得到的就是`LBB0_4`的地址（这么做是为了PIC）。
4. 最后，`br    x8`就能正确地跳转到`LBB0_4`处了。

由此可见，`switch`语句在底层，会生成一个**跳转表**。我们可以通过一个算术运算，加上间接跳转，实现真正的跳转。这种方案与级联`if`-`else`语句相比，效率高出了许多（因为后者会每一个case都进行一个比较和跳转）。
