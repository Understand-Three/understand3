---
title: 泛型
draft: true
---
泛型主要目的是为程序员提供编程的便利，减少代码的臃肿，同时可以极大地丰富语言本身的表达能力，为程序员提供了一个合适的炮管。想想，一个函数，可以代替几十个，甚至数百个函数，是一件多么让人兴奋的事情。

我们在编程中，经常有这样的需求：用同一功能的函数处理不同类型的数据，例如两个数的加法，无论是整数还是浮点数，甚至是自定义类型，都能进行支持。

# 加法示例

## 不使用泛型

在不支持泛型的编程语言中，通常需要为每一种类型编写一个函数：

```rust
fn add_i8(a:i8, b:i8) -> i8 {
    a + b
}
fn add_i32(a:i32, b:i32) -> i32 {
    a + b
}
fn add_f64(a:f64, b:f64) -> f64 {
    a + b
}

fn main() {
    println!("add i8: {}", add_i8(2i8, 3i8));
    println!("add i32: {}", add_i32(20, 30));
    println!("add f64: {}", add_f64(1.23, 1.23));
}
```

输出:

```bash
add i8: 5  
add i32: 50  
add f64: 2.46
```

## 使用泛型

> 这段代码虽然很简洁，但是并不能编译通过，这只是泛型的思想，（但是你可以在其他同样支持泛型的语言中使用），这里无法编译通过的原因是需要写为 `fn add<T: std::ops::Add<Output = T>>(a:T, b:T) -> T {`
> 简单解释一下：因为 `T` 可以是任何类型，但是不是所有类型都可以相加，所以还需要一个限制，以保证不会发生错误，标准库`std` 下的 `ops` 中提供了一个 `Add` 类型，这个类型完美支持了相加的操作

```rust
fn add<T>(a:T, b:T) -> T {
    a + b
}

fn main() {
    println!("add i8: {}", add(2i8, 3i8));
    println!("add i32: {}", add(20, 30));
    println!("add f64: {}", add(1.23, 1.23));
}
```

输出：

```bash
add i8: 5  
add i32: 50  
add f64: 2.46
```

可以看到，他们的输出完全一致，在使用泛型的情况下，但是代码量少了很多。

# 结构体泛型

## Generic

泛型是编程语言的特性，它允许在代码中使用参数化类型，以便在不同地方使用相同的代码逻辑处理多种数据类型，而无需为每种类型编写单独的代码

作用：

1. 提高代码的重用性、
2. 提高代码的可读性
3. 提高代码的抽象度



## 泛型的应用类型

1. 泛型定义结构体 / 枚举
2. 泛型定义函数
3. 泛型与特质

## 相同的类型
```rust
#[derive(Debug)]

struct Point <T> {
    x:T,
    y:T,
}
fn main() {
    let c1 = Point{ x:1.0, y:2.0, }; 
    let c2 = Point{ x:'x', y:'y', };
    // let error = Point{x: 1, y: 1.0}; // 两个类型不同，会报错
    
    println!("c1 is {:?}, \nc2 is {:?} \n",c1,c2);
    // println!{"error is {:?}",error}
    
    // c1 is Point { x: 1.0, y: 2.0 },
    // c2 is Point { x: 'x', y: 'y' }
    // Error:  expected integer, found floating-point number
}
```

## 不同的类型

```rust
#[derive(Debug)]
struct PointTwo <T,E> {
    x:T,
    y:E,
}
fn main() {

    let c3 = PointTwo{ x:1.0, y:'y', };
    let c4 = PointTwo{ x: 30, y:'😂'};
    println!("c3 is {:?}",c3);
    println!("c4 is {:?}",c4);
    // c3 is PointTwo { x: 1.0, y: 'y' }
    // c4 is PointTwo { x: 30, y: '😂' }
}
```


# 枚举泛型

提到枚举类型，`Option` 永远是第一个应该被想起来的，在之前的章节中，它也多次出现：

```rust
enum Option<T> {
    Some(T),
    None,
}
```

`Option<T>` 是一个拥有泛型 `T` 的枚举类型，它第一个成员是 `Some(T)`，存放了一个类型为 `T` 的值。得益于泛型的引入，我们可以在任何一个需要返回值的函数中，去使用 `Option<T>` 枚举类型来做为返回值，用于返回一个任意类型的值 `Some(T)`，或者没有值 `None`。

对于枚举而言，卧龙凤雏永远是绕不过去的存在：如果是 `Option` 是卧龙，那么 `Result` 就一定是凤雏，得两者可得天下：

```rust
enum Result<T, E> {
    Ok(T),
    Err(E),
}
```

这个枚举和 `Option` 一样，**主要用于函数返回值**，与 `Option` 用于值的**存在与否**不同，`Result` 关注的主要是值的**正确性**。

如果函数正常运行，则最后返回一个 `Ok(T)`，`T` 是函数具体的返回值类型，如果函数异常运行，则返回一个 `Err(E)`，`E` 是错误类型。例如打开一个文件：如果成功打开文件，则返回 `Ok(std::fs::File)`，因此 `T` 对应的是 `std::fs::File` 类型；而当打开文件时出现问题时，返回 `Err(std::io::Error)`，`E` 对应的就是 `std::io::Error` 类型。


# 函数泛型

```rust
struct Point<T> {
    x: T,
    y: T,
}

impl<T> Point<T> {
    fn x(&self) -> &T {
        &self.x
    }
}

fn main() {
    let p = Point { x: 5, y: 10 };

    println!("p.x = {}", p.x());
}
```

使用泛型参数前，依然需要提前声明：`impl<T>`，只有提前声明了，我们才能在`Point<T>`中使用它，这样 Rust 就知道 `Point` 的尖括号中的类型是泛型而不是具体类型。需要注意的是，这里的 `Point<T>` 不再是泛型声明，而是一个完整的结构体类型，因为我们定义的结构体就是 `Point<T>` 而不再是 `Point`。

除了结构体中的泛型参数，我们还能在该结构体的方法中定义额外的泛型参数，就跟泛型函数一样：

```rust
struct Point<T, U> {
    x: T,
    y: U,
}

impl<T, U> Point<T, U> {
    fn mixup<V, W>(self, other: Point<V, W>) -> Point<T, W> {
        Point {
            x: self.x,
            y: other.y,
        }
    }
}

fn main() {
    let p1 = Point { x: 5, y: 10.4 };
    let p2 = Point { x: "Hello", y: 'c'};

    let p3 = p1.mixup(p2);

    println!("p3.x = {}, p3.y = {}", p3.x, p3.y);
}
```

这个例子中，`T,U` 是定义在结构体 `Point` 上的泛型参数，`V,W` 是单独定义在方法 `mixup` 上的泛型参数，它们并不冲突，说白了，你可以理解为，一个是结构体泛型，一个是函数泛型。

## 为具体的泛型类型实现方法

对于 `Point<T>` 类型，你不仅能定义基于 `T` 的方法，还能针对特定的具体类型，进行方法定义：

```rust
impl Point<f32> {
    fn distance_from_origin(&self) -> f32 {
        (self.x.powi(2) + self.y.powi(2)).sqrt()
    }
}

```

这段代码意味着 `Point<f32>` 类型会有一个方法 `distance_from_origin`，而其他 `T` 不是 `f32` 类型的 `Point<T>` 实例则没有定义此方法。这个方法计算点实例与坐标`(0.0, 0.0)` 之间的距离，并使用了只能用于浮点型的数学运算符。

这样我们就能针对特定的泛型类型实现某个特定的方法，对于其它泛型类型则没有定义该方法。

# const 泛型

在之前的泛型中，可以抽象为一句话：针对类型实现的泛型，所有的泛型都是为了抽象不同的类型，那有没有针对值的泛型？可能很多同学感觉很难理解，值怎么使用泛型？不急，我们先从数组讲起。

在[数组](https://course.rs/basic/compound-type/array.html)那节，有提到过很重要的一点：`[i32; 2]` 和 `[i32; 3]` 是不同的数组类型，比如下面的代码：

```rust
fn display_array(arr: [i32; 3]) {
    println!("{:?}", arr);
}
fn main() {
    let arr: [i32; 3] = [1, 2, 3];
    display_array(arr);

    let arr: [i32; 2] = [1, 2];
    display_array(arr);
}
```

运行报错：

```error
error[E0308]: mismatched types // 类型不匹配
  --> src/main.rs:10:19
   |
10 |     display_array(arr);
   |                   ^^^ expected an array with a fixed size of 3 elements, found one with 2 elements
                          // 期望一个长度为3的数组，却发现一个长度为2的
```

结合代码和报错，可以很清楚的看出，`[i32; 3]` 和 `[i32; 2]` 确实是两个完全不同的类型，因此无法用同一个函数调用。

首先，让我们修改代码，让 `display_array` 能打印任意长度的 `i32` 数组：

```rust
fn display_array(arr: &[i32]) {
    println!("{:?}", arr);
}
fn main() {
    let arr: [i32; 3] = [1, 2, 3];
    display_array(&arr);

    let arr: [i32; 2] = [1, 2];
    display_array(&arr);
}
```

很简单，只要使用数组切片，然后传入 `arr` 的不可变引用即可。

接着，将 `i32` 改成所有类型的数组：

```rust
fn display_array<T: std::fmt::Debug>(arr: &[T]) {
    println!("{:?}", arr);
}
fn main() {
    let arr: [i32; 3] = [1, 2, 3];
    display_array(&arr);

    let arr: [i32; 2] = [1, 2];
    display_array(&arr);
}
```

也不难，唯一要注意的是需要对 `T` 加一个限制 `std::fmt::Debug`，该限制表明 `T` 可以用在 `println!("{:?}", arr)` 中，因为 `{:?}` 形式的格式化输出需要 `arr` 实现该特征。

通过引用，我们可以很轻松的解决处理任何类型数组的问题，但是如果在某些场景下引用不适宜用或者干脆不能用呢？你们知道为什么以前 Rust 的一些数组库，在使用的时候都限定长度不超过 32 吗？因为它们会为每个长度都单独实现一个函数，简直。。。毫无人性。难道没有什么办法可以解决这个问题吗？

好在，现在咱们有了 const 泛型，也就是针对值的泛型，正好可以用于处理数组长度的问题：

```rust
fn display_array<T: std::fmt::Debug, const N: usize>(arr: [T; N]) {
    println!("{:?}", arr);
}
fn main() {
    let arr: [i32; 3] = [1, 2, 3];
    display_array(arr);

    let arr: [i32; 2] = [1, 2];
    display_array(arr);
}
```

如上所示，我们定义了一个类型为 `[T; N]` 的数组，其中 `T` 是一个基于类型的泛型参数，这个和之前讲的泛型没有区别，而重点在于 `N` 这个泛型参数，它是一个**基于值**的泛型参数！因为它用来替代的是数组的长度。

`N` 就是 const 泛型，定义的语法是 `const N: usize`，表示 const 泛型 `N` ，它基于的值类型是 `usize`。

在泛型参数之前，Rust 完全不适合复杂矩阵的运算，自从有了 const 泛型，一切即将改变。

## const 泛型表达式

假设我们某段代码需要在内存很小的平台上工作，因此需要限制函数参数占用的内存大小，此时就可以使用 const 泛型表达式来实现：

```rust
// 目前只能在nightly版本下使用
#![allow(incomplete_features)]
#![feature(generic_const_exprs)]

// 定义一个断言枚举，用于存储编译时常量
pub enum Assert<const CHECK: bool> {}

// 定义一个 IsTrue trait，用于提供默认实现
pub trait IsTrue {}

// 为 Assert<true> 提供 IsTrue 的实现
impl IsTrue for Assert<true> {}

// 定义 something 函数，它接受一个泛型参数 T
// 其中 Assert<{ size_of::<T>() < 768 }> 必须为 IsTrue 类型
fn something<T>(val: T)
where
    Assert<{ std::mem::size_of::<T>() < 768 }>: IsTrue,
{
    // 函数体
}

fn main() {
    something([0u8; 0]); // ok
    something([0u8; 512]); // ok
    // something([0u8; 1024]); // 编译错误，数组长度超过了768字节的限制
}
```

运行命令参考

```bash

# 临时使用夜版
rustup run nightly cargo run

# 修改默认使用夜版
rustup default nightly

# 安装夜班
rustup install nightly

# 使用稳定版（默认的版本）
rustup default stable
```


## const fn

在讨论完 `const` 泛型后，不得不提及另一个与之密切相关且强大的特性：`const fn`，即常量函数。`const fn` 允许我们**在编译期对函数进行求值**，从而实现更高效、更灵活的代码设计。

### 为什么需要 const fn
通常情况下，函数是在运行时被调用和执行的。然而，在某些场景下，我们希望在编译期就计算出一些值，以提高运行时的性能或满足某些编译期的约束条件。例如，定义数组的长度、计算常量值等。

有了 `const fn`，我们可以在编译期执行这些函数，从而将计算结果直接嵌入到生成的代码中。这不仅以高了运行时的性能，还使代码更加简洁和安全。

## const fn 的基本用法

要定义一个常量函数，只需要在函数声明前加上 `const` 关键字。例如：

```rust
const fn add(a: usize, b: usize) -> usize {
    a + b
}

const RESULT: usize = add(5, 10);

fn main() {
    println!("The result is: {}", RESULT);
}
```

## const fn 的限制

虽然 `const fn` 提供了很多便利，但是由于其在编译期执行，以确保函数能在编译期被安全地求值，因此有一些限制，例如，不可将随机数生成器写成 `const fn`。

无论在编译时还是运行时调用 `const fn`，它们的结果总是相同，即使多次调用也是如此。唯一的例外是，如果你在极端情况下进行复杂的浮点操作，你可能会得到（非常轻微的）不同结果。因此，不建议使 `数组长度 (arr.len())` 和 `Enum判别式` 依赖于浮点计算。

## 结合 const fn 与 const 泛型

将 `const fn` 与 `const 泛型` 结合，可以实现更加灵活和高效的代码设计。例如，创建一个固定大小的缓冲区结构，其中缓冲区大小由编译期计算确定：

```rust
struct Buffer<const N: usize> {
    data: [u8; N],
}

const fn compute_buffer_size(factor: usize) -> usize {
    factor * 1024
}

fn main() {
    const SIZE: usize = compute_buffer_size(4);
    let buffer = Buffer::<SIZE> {
        data: [0; SIZE],
    };
    println!("Buffer size: {} bytes", buffer.data.len());
}
```

在这个例子中，`compute_buffer_size` 是一个常量函数，它根据传入的 `factor` 计算缓冲区的大小。在 `main` 函数中，我们使用 `compute_buffer_size(4)` 来计算缓冲区大小为 4096 字节，并将其作为泛型参数传递给 `Buffer` 结构体。这样，缓冲区的大小在编译期就被确定下来，避免了运行时的计算开销。















---


1. 泛型与函数
2. 泛型与结构体中的方法

```rust
// 交换
fn swap<T>(a:T, b:T) -> (T,T){
    (b,a)
}

struct Point<T>{
    x:T,
    y:T,
}

impl<T> Point<T> {
    fn new(x:T,y:T) -> Self { // 可以不用再次声明 T
        Point{x,y}
    }
    fn get_coordinates(&self) -> (&T,&T){
        (&self.x,&self.y)
    }
}

fn main(){
    let number = swap(0,1);
    println!("swap {:?}",number);
    // swap (1, 0)

    let f_number = swap::<f64>(0.1,2.0);
    println!("swap f_number is {:?}",f_number);
    // swap f_number is (2.0, 0.1)

    let ff_number:(f64,f64) = swap(0.1,2.0);
    println!("swap f_number is {:?}",ff_number);
    // swap f_number is (2.0, 0.1)

    //-------------
    let str = swap("front","end");
    println!("str is {:?}",str);
    // str is ("end", "front")
    let str = swap(str.0,str.1);
    println!("str 0 is {} \nstr 1 is {}",str.0,str.1);
    //str 0 is front
    // str 1 is end

    let i32_point = Point::new(2,3);
    let f64_point = Point::new(2.0,3.0);
    let (x1,y1) = i32_point.get_coordinates();
    let (x2,y2) = f64_point.get_coordinates();
    println!("i32 point is x = {}, y = {}",x1,y1);
    // i32 point is x = 2, y = 3
    println!("f46 point is x = {}, y = {}",x2,y2);
    // f46 point is x = 2, y = 3

    // 给结构体的用 String 不要用 &str 字面量
    let string_point = Point::new("x_str".to_string(),"y_str".to_string());
    println!("string point x = {}, y = {}",string_point.x,string_point.y);
    // string point x = x_str, y = y_str
}
```



