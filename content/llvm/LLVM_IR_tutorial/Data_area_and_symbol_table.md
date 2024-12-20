---
title: 数据区与符号表
draft: true
---

# 数据区与符号表

我们知道，数据区里的数据，其最大的特点就是，能够给整个程序的任何一个地方使用。同时，数据区里的数据也是占静态的二进制可执行程序的体积的。所以，我们应该只将需要全程序使用的变量放在数据区中。而现代编程语言的经验告诉我们，这类全局静态变量应该越少越好。

同时，由于LLVM是面向多平台的，所以我们还需要考虑的是该怎么处理这些数据。一般来说，大多数平台的可执行程序格式中都会包含`.data`分区，用来存储这类的数据。但除此之外，每个平台还有专门的更加细致的分区，比如说，Linux的ELF格式中就有`.rodata`来存储只读的数据。因此，LLVM的策略是，让我们尽可能细致地定义一个全局变量，比如说注明其是否只读等，然后依据各个平台，如果平台的可执行程序格式支持相应的特性，就可以进行优化。

一般来说，在LLVM IR中定义一个存储在数据区中的全局变量，其格式为：

```llvm
@global_variable = global i32 0
```

这个语句定义了一个`i32`类型的全局变量`@global_variable`，并且将其初始化为`0`。

如果是只读的全局变量，也就是常量，我们可以用`constant`来代替`global`：

```llvm
@global_constant = constant i32 0
```

这个语句定义了一个`i32`类型的全局常量`@global_constant`，并将其初始化为`0`。

## 符号与符号表

讲到了数据区，就顺便讲讲符号表。在LLVM IR中，所有的全局变量的名称都需要用`@`开头。我们有一个这样的LLVM IR：

```llvm
; global_variable_test.ll
@global_variable = global i32 0

define i32 @main() {
    ret i32 0
}
```

也就是说，在之前最基本的程序的基础上，新增了一个全局变量`@global_variable`。我们将其直接编译成可执行文件：

```shell
clang global_variable_test.ll -o global_variable_test
```

然后，我们使用`nm`命令查看其符号表：

```shell
nm global_variable_test
```

我们可以在输出中找到一行：

```plaintext
000000000000402c B global_variable
```

我们注意到，出现了`global_variable`这个字段。这表明，直接定义的全局变量，其名称会出现在符号表之中。那么，怎么控制这个行为呢？首先，我们需要简单地了解一下符号与符号表。

在传统的C语言编译模型中，编译器将每个`.c`文件（也称为「编译单元」）编译为一个`.o`目标文件，然后链接器将这些`.o`文件链接为一个可执行文件。这么做的好处是，如果一个项目特别大，编译器就不需要将所有`.c`文件都读入内存中一起处理，而是可以并行地、高效地单独处理每个`.c`文件（这也是著名前端框架React不选择使用TypeScript的原因之一，参见[为什么 React 源码不用 TypeScript 来写？ - Cat Chen的回答 - 知乎](https://www.zhihu.com/question/378470381/answer/1079675543)）。对于动态链接的程序而言，在程序加载、运行时，也会由动态链接器将相应的库动态链接进程序之中。

也就是说，编译器生成的结果，需要给链接器和动态链接器进行处理。在这一过程中，就需要「符号表」出马了。在上述的过程中，编译器的输入是一个编译单元，而输出是一个目标文件。那么如果我们在源代码中，在一个`.c`文件中调用了别的文件中实现的函数，编译器并不知道别的函数在哪。因此，编译器选择的策略是将这个函数的调用用一个符号代替，在将来链接以及动态链接的时候，再进行替换。

粗略来讲，整体的符号处理的过程为：

1. 编译器对源代码按文件进行编译。对于每个文件中的未知函数，记录其符号；对于这个文件中实现的函数，暴露其符号
2. 链接器收集所有的目标文件，对于每个文件而言，将其记录下的未知函数的符号，与其他文件中暴露出的符号相对比，如果找到匹配的，就成功地解析（resolve）了符号
3. 部分符号在程序加载、执行时，由动态链接库给出。动态链接器将在这些阶段，进行类似的符号解析

这一流程粗粒度地来看，非常的简单。但是仔细来看，就需要更多的处理。

一个符号本身，就是一个字符串。那么我们在写一个C语言的项目时，如果希望有的函数在别的文件中被调用，按照上述过程，似乎就是暴露一下符号就行。但是，一个C语言的项目，往往会链接很多第三方库。如果我们想暴露的函数名与其他第三方库里的函数名重复了，会怎样呢？如果不加处理，链接器会直接报错。那难道我们起一个名字，需要注意与别的所有的库里的函数都不重复吗？此外，一个程序会有成千上万个符号，一些简单的，只在一个文件里用到的符号，比如说`cmp`、`max`，难道也要放在符号表中吗？

在LLVM IR中，解决这些问题，与两个概念密切相关：链接与可见性，LLVM IR也提供了[Linkage Type](https://llvm.org/docs/LangRef.html#linkage-types)和[Visibility Styles](https://llvm.org/docs/LangRef.html#visibility-styles)这两个修饰符来控制相应的行为。

### 链接类型

对于链接类型，我们常用的主要有什么都不加（默认为`external`）、`private`和`internal`。

什么都不加的话，就像我们刚刚那样，直接把全局变量的名字放在了符号表中。这样的话，这个函数可以在链接时被其他编译单元看到。

用`private`，则代表这个变量的名字不会出现在符号表中。我们将原来的代码改写成

```llvm
@global_variable = private global i32 0
```

那么，用`nm`查看其编译出的可执行文件，这个变量的名字就消失了。

用`internal`则表示这个变量是以局部符号的身份出现（全局变量的局部符号，可以理解成C中的`static`关键词）。我们将原来的代码改写成

```llvm
@global_variable = internal global i32 0
```

那么，再次将其编译成可执行程序，并用`nm`查看，可以看到这个符号。但是，在链接过程中，这个符号并不会参与符号解析。

### 可见性

可见性在实际使用中则比较少，主要分为三种`default`, `hidden`和`protected`，这里主要的区别在于符号能否被重载。`default`的符号可以被重载，而`protected`的符号则不可以；此外，`hidden`则不将变量放在动态符号表中，因此其它的模块不可以直接引用这个符号。

### 可抢占性

在我们日常看到的LLVM IR中，会经常见到`dso_local`这样的修饰符，在LLVM中被称作[运行时抢占性修饰符](https://llvm.org/docs/LangRef.html#runtime-preemption-specifiers)。如果需要深入理解这个概念，可以参考国人大神写的[ELF interposition and `-Bsymbolic`](https://maskray.me/blog/2021-05-16-elf-interposition-and-bsymbolic)、[`-fno-semantic-interposition`](https://maskray.me/blog/2021-05-09-fno-semantic-interposition)。简单来说，`dso_local`保证了程序像我们想象中的一样运行。

举个例子：

```c
// interposition1.c
void f(void) {
    printf("From interposition1\n");
}

// interposition2.c
void f(void) {
    printf("From interposition2\n");
}

void g(void) {
    f();
}

// interposition-main.c
void g();

int main() {
    g();
    return 0;
}
```

我们想把`interposition1.c`和`interposition2.c`分别编译为动态链接库，并给`main`来调用。最简单的做法是：

```shell
clang -fPIC interposition1.c --shared -o libinterposition1.so
clang -fPIC interposition2.c --shared -o libinterposition2.so
clang -L. -linterposition1 -linterposition2 interposition-main.c -o interposition
```

我们运行这个程序，常理告诉我们，正常来说，得是输出"From interposition2"吧？但是，我们真正运行这个程序，会输出"From interposition1"。

我们如果看`interposition2`的汇编代码，会发现，`g`函数的实现为

```x86asm
g:
    pushq    %rbp
    movq     %rsp, %rbp
    callq    f@PLT
    popq     %rbp
    retq
```

虽然`f`在同一个文件内，但它居然默认是去PLT表找实现！！

这不仅极其愚蠢（可能仅仅对通过`LD_PRELOAD`来hook API有帮助），而且效率还低。

但如果我们这样子来编译：

```shell
clang -fPIC interposition1.c --shared -o libinterposition1.so
clang -fPIC -fno-semantic-interposition interposition2.c --shared -o libinterposition2.so
clang -L. -linterposition1 -linterposition2 interposition-main.c -o interposition
```

仅仅在编译`libinterposition2.so`时增加了`-fno-semantic-interposition`这个选项，再运行程序，输出就对了！

如果我们查看生成的`interposition2.ll`，可以发现：

```llvm
define dso_local void @f() {
  %1 = call i32 (ptr, ...) @printf(ptr noundef @.str)
  ret void
}

define dso_local void @g() {
  call void @f()
  ret void
}
```

`f`和`g`都有了`dso_local`的修饰符。`dso_local`就是告诉链接器，这个不许抢占，在生成动态链接库的时候，直接调用，别去PLT表找了。

当我们使用`clang -O3`等级别进行优化编译时，不需要加`-fno-semantic-interposition`就可以达成一样的效果。

根据Fedora社区的尝试[Changes/PythonNoSemanticInterpositionSpeedup](https://fedoraproject.org/wiki/Changes/PythonNoSemanticInterpositionSpeedup)和cpython对应的issue [Compile libpython with -fno-semantic-interposition](https://github.com/python/cpython/issues/83161)，仅仅是增加这个选项，就可以让cpython快1.3倍。

### C的例子

关于符号和符号表，这些还是挺抽象的，我们不如用一个具体的C语言的例子来看看效果：

```c
int a;
extern int b;
static int c;
void d(void);
void e(void) {}
static void f(void) {}
```

首先我们先理解一下这个C语言代码各个符号的含义：

* `a`

   定义在当前文件中的全局变量，别的文件也可以使用这个符号
* `b`

   定义在别的文件中的全局变量，当前文件需要使用这个符号
* `c`

   定义在当前文件中的全局变量，别的文件不可以使用这个符号
* `d`

   定义在别的文件中的函数，当前文件需要使用这个符号
* `e`

   定义在当前文件中的函数，别的文件也可以使用这个符号
* `f`

   定义在当前文件中的函数，别的文件不可以使用这个符号

以上六种，是我们在C语言编程中最常见的符号形式。

我们使用Clang将其编译为LLVM IR，是什么样子的呢？

```llvm
@a = dso_local global i32 0, align 4
@b = external global i32, align 4
@c = internal global i32 0, align 4

declare void @d()

define dso_local void @e() {
  ret void
}

define internal void @f() {
  ret void
}
```

我们可以发现几件事（在默认的编译选项下）：

* C语言中的`static`，也就是当前文件中定义，别的文件不可以用的，都会加上`internal`修饰符
* C语言中的`extern`，也就是别的文件中定义的，全局变量会加上`external`修饰符，函数会使用`declare`
* C语言中定义的，可以给别的文件使用的全局变量或函数，不会加上链接类型修饰符，并且会加上`dso_local`保证不会被抢占