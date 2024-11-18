---
title: 数据的使用
draft: true
---

# 数据的使用

在之前的两篇文章中，我们解释了LLVM中是如何对应数据区、寄存器和栈上的数据的。那么，这些数据定义了以后，该如何使用呢？

## 全局变量和栈上变量皆指针

下面，我们就需要讲怎样使用全局变量和栈上的变量。这两种变量实际上是类似的，LLVM IR把它们都看作指针。也就是说，对于全局变量：

```llvm
@global_variable = global i32 0
```

和栈上变量

```llvm
%local_variable = alloca i32
```

这两个变量实际上都是`ptr`指针，指向它们所处的一个`i32`大小的内存区域。所以，我们不能这样：

```llvm
%1 = add i32 1, @global_variable ; Wrong!
```

因为`@global_variable`只是一个指针。

如果要操作这些值，必须使用`load`和`store`这两个命令。如果我们要获取`@global_variable`的值，就需要

```llvm
%1 = load i32, ptr @global_variable
```

这个指令的意思是，把一个`ptr`指针`@global_variable`的`i32`类型的值赋给虚拟寄存器`%1`，然后我们就能愉快地

```llvm
%2 = add i32 1, %1
```

这样了。

类似地，如果我们要将值存储到全局变量或栈上变量里，会需要`store`命令：

```llvm
store i32 1, ptr @global_variable
```

这个代表将`i32`类型的值`1`赋给`ptr`类型的全局变量`@global_variable`所指的内存区域中。

## SSA

LLVM IR是一个严格遵守SSA(Static Single Assignment)策略的语言。SSA的要求很简单：每个变量只被赋值一次。也就是说，你不能

```llvm
%1 = add i32 1, 2
%1 = add i32 3, 4
```

对`%1`同时赋值两次是不被允许的。

SSA作为一个历史悠久的概念，已经有了相当成熟的相关技术。通过使用SSA，编译器可以进行更好的优化，应用更成熟的算法，得到更好的结果。这里因为个人能力有限，就不再多对SSA进行介绍。我们只需要知道，通过约束每个变量只被赋值一次，可以让LLVM更好地优化。

上面这个例子好做，直接把3加4的结果赋值给一个新的虚拟寄存器就好了。但是，并非所有的情况都这么简单。在一些复杂情况下，将值存储在栈上再取出来，或者使用`phi`指令（见之后控制语句一章），也是一个更好的选择。