---
title: 流程控制
draft: true
---

# 1. 流程控制

Execution Flow（流程）

1. 代码执行从上到下 line-by-line
2. 而我们执行操作时，控制流程可能会改变

主要的流程控制结构

1. 顺序结构（Sequential Structure）：程序按照代码的顺序一步一步执行，没有跳过或循环
2. 选择结构（Selection Structure）：根据条件不同的路径执行，常见的选择结构有：
    - if 语句：根据条件执行不同的代码块
    - switch 语句（在某些编程语言中）：根据不同的条件值执行不同的代码块
3. 循环结构（Iteration）：重复执行一段代码，直到满足某个条件为止，常见的循环结构有：
    - for 循环：按照指定的次数重复执行一段代码
    - while 循环：在条件为真的情况下重复执行一段代码
    - do-while 循环：类似于 while 循环，但是保证至少执行一次循环体
4. 跳转结构：控制程序的执行流程跳转到指定的位置，常见的跳转结构有：
    - break 语句：终止循环或 switch 语句的执行
    - continue 语句：跳过当前循环中的剩余代码，进入下一次迭代
    - goto 语句（在某些编程语言中）：直接跳转到指定的标签处



## 1.1 if

代码一行行执行

执行流程会被 `if (else)`改变

可以嵌套使用，但容易引起可读性问题

```rust
fn main(){
    let age = 50;
    if age < 50 {
        println!("You are young");
    } else {
        println!("You are old");
        // You are old
    }
    
    // 类三元表达式，可以返回值
    let msg = if age > 50 {"old"} else {"young"};
    println!("You are {}",msg);
    // You are young

    let scores = 70;
    // if 的表达能力非常弱
    if scores > 90 {
        println!("Good !!!");
    } else if scores > 60 {
        println!("You are OK!");
        // You are OK!
    }else{
        println!("Bad !!!!")
    }
}
```



## 1.2 match 表达式

- `match` 用于模式匹配，允许更复杂的条件和分支
- 可以处理多个模式，提高代码的表达力
- `match` 是表达式，可以返回值

```rust
match value{
  pattern1 => {代码块}// 如果匹配到 pattern1 则执行这个代码块
  pattern2 if condition => {代码块}// 如果匹配到 pattern2 并且 condition 为 true 则执行这个代码块
  _ => {代码块} // 其他任意一种没有被其中匹配到的的情况，执行这个代码块
}
```



```rust
fn main(){
    //
    let num = 90;
    match num {
        80 => println!("80"),
        90 => println!("90"),
        // 90
        _ => println!("Some else"),
    }
    match num{
        25..=50 => println!("25 ... 50"),
        // 51 ... 100
        51..=100 => println!("51 ... 100"),
        _ => println!("Some else"),
    }
    match num {
        25 | 50 | 75 => println!("25 or 50 or 75"),
        100 | 200 => println!("100 or 200"),
        _ => println!("Some else"),
        // Some else
    }
    // if score
    match num {
        x if x<60 => println!("bad !"),
        x if x == 60 => println!("luck"),
        _ => println!("Some else")
        // Some else
    }

    // 返回值
    let num = 60;
    let res = match num {
        x if x < 60 => "bad".to_string(),
        x if x == 60 => "luck".to_string(),
        _ => "Some else".to_owned(),
    };
    println!("{}", res);
    // luck
}
```



## 1.3 if 流程控制与 match 表达式对比

复杂性：`if` 适用于**简单**的条件判断，而 `match` 更适用于**复杂**的模式匹配

表达力：`match` 更灵活，可以处理多个条件和模式，使代码更清晰

返回值：两者都是表达式，可以返回值，但 `match` 通常用于表达更复杂的场景 



# 2. 循环与 break comtinue 以及与迭代的区别

## 2.1 Rust 中的循环

Rust 提供了几种循环结构，其中最常见的是 `loop`、`while` 和 `for`

### 2.1.1 `loop` 循环

```rust
loop{
  // 无限循环的代码块
}
```

`loop` 创建一个无限循环，可以通过 `break` 语句来中断循环

### 2.1.2 `while` 循环：

```rust
while condition{
  // 条件为真时执行的代码块
}
```

`while` 循环在每次迭代之前检查一个条件，只有在条件为真时才执行循环体

### 2.1.3 `for`  循环：

```rust

for item in iterable {
  // 便利可迭代对象执行的代码块
}
```

    `for` 循环常用于迭代集合或范围，执行代码块来处理每个元素

## 2.2 break 和 continue

- break 关键字用于立即终止循环，并跳出循环体
    - 可以使用跳出指定标签循环
- continue 关键字用于立即跳过当前循环中剩余的代码，直接进入下一次循环





## 2.3 迭代

Rust 的迭代主要是通过迭代器（iterators）来实现。迭代器是一个抽象，它提供了一种访问集合元素的统一方式。

从实现上讲，在 Rust 中迭代器是一种实现了 Iterator trait 的类型

简化源码：

```rust
pub trait Iterator{
  type Item;
  fn next(&mut self) -> Option<Self::Item>;
}
```



## 2.4 循环与迭代的不同

循环适用于需要明确控制循环流程的情况，而迭代器则提供了一种更抽象的方式来处理集合元素。通常，推荐使用迭代器，因为它们可以提高代码的可读性和表达力。

for 循环是一种语法结构，用于遍历集合中的元素，它依赖于集合类型实现 Iterator trait

在Rust 中，迭代器提供了一系列用于遍历集合元素的方法，比如 `next()`、`map()` 、` filter()`等，可以让我们的代码更具有表达性



loop

```rust
use std::os::unix::raw::time_t;
use std::time;

fn main(){
    loop {
        println!("Ctrl + C");
        // Ctrl + C
        // Ctrl + C
        // Ctrl + C
        // Ctrl + C
        // ......
        std::thread::sleep(std::time::Duration::from_secs(1));
    }
}
```



while

```rust
fn main(){
    let mut i = 0;
    while i < 10 {
        println!("{}",i);
        i += 1;
        // 0
        // 1
        // 2
        // ......
        // 9
    }
}
```





for

```rust
fn main(){
    let arr = [1,2,3,4,5,6,7,8];
    // 打印数组元素
    for element in arr {
        println!("{}",element);
        // 1
        // 2
        // 3
        // ......
        // 8
    }
    // 输出 0 ～ 9
    for i in 0..10{
        println!("{}",i);
        // 0
        // 1
        // 2
        // ......
        // 9
    }
    // 输出 0 ～ 10
    for i in 0..=10{
        println!("{}",i);
        // 0
        // 1
        // 2
        // ......
        // 10
    }
}
```





break 和 continue

```rust
fn main(){
    let arr = [1,2,3,4,5,6,7,8,9,10,11];
    // 打印所有的元素
    for element in arr {
        print!("{} ",element);
        // 1 2 3 4 5 6 7 8 9 10 11 
    }
    // 打印到 10 以前的元素
    for element in arr {
        if element == 10 {
            break;
        }
        print!("{} ",element);
        // 1 2 3 4 5 6 7 8 9
    }
    // 打印 10 以外的所有元素
    for element in arr {
        if element == 10 {
            continue;
        }
        print!("{} ",element);
        // 1 2 3 4 5 6 7 8 9 11 
    }
}
```



break 标签

```rust
fn main(){
    let arr = [1,2,3,4,5,6,7,8,9,10,11];
    loop{
        println!("outer");
        loop{
            println!("inner");
            break; // 跳出 inner 循环, 但是不会跳出 outer 循环
        }
    };
    // outer
    // inner
    // outer
    // inner
    // outer
    // inner
    // outer
    // ......
    

    'outer: loop{
        println!("outer");
        loop{
            println!("inner");
            break 'outer; // 跳出 outer 循环

        }
    }
    // outer
    // inner
}
```



迭代与循环

```rust
fn main () {
    // 把所有的值乘以二
    let numbers = [1,2,3,4,5,6,7,8,9];
    // 循环的写法
    let mut for_numbers = Vec::new();
    for &number in numbers.iter() {
        let item = number * number;
        for_numbers.push(item);
    }
    println!("for : {:?}",for_numbers);
    // for : [1, 4, 9, 16, 25, 36, 49, 64, 81]

    // 迭代的写法
    let numbers = [1,2,3,4,5,6,7,8,9].to_vec();
    let iter_number : Vec<_>= numbers.iter().map(|&x|x*x).collect();
    println!("for : {:?}",for_numbers);
    // iter : [1, 4, 9, 16, 25, 36, 49, 64, 81]
}
```





# 函数基础与 copy 值参数传递

## 函数的基础知识

1. 函数的定义：在 Rust 中，你可以使用 `fn` 关键字声明和定义函数，而 `main` 是程序的入口点，是一种特殊的函数

2. 参数和返回值

    函数可以接受零个或多个参数，每个参数都需要指定类型

    函数可以有返回值，使用 `->` 指定返回类型。如果函数没有返回值，可以使用 `-> ()` 或省略这部分

3. 调用函数：调用函数时，使用函数名和传递给函数的实际参数



## Copy by value

- 如果数据类型实现 copy 特质，则在函数传参时会实现 copy by value 操作
- 会将实参拷贝为形参，形参改变并不会影响实参
- 如果要改变形参要加上 `mut`
- Struct、枚举、集合等并没有实现 copy trait，会实现 move 操作而失去所有权
- 为数据类型实现 copy trait，就可实现 copy by value





基础数据类型实现 copy

```rust
fn add(x:i32,y:i32) -> i32{
    x+y // 不加分号，会作为返回值被返回
}

fn no_change_i32(mut x:i32){
    x = x + 4;
    println!("fn: {}",x)
    // fn: 5
}

fn modify_i32(y:&mut i32){
    *y += 4;
}
fn main(){
    let a = 1;
    let b = 2;
    let c = add(a,b);
    println!("c: {c}");
    // c: 3
    let x = 1;
    no_change_i32(x); // 基础类型传的是 copy
    println!("x: {}",x);
    // x: 1

    let mut y = 3;
    modify_i32(&mut y);
    println!("y: {}",y);
    // y: 7
}
```



结构体 - 未实现 copy

```rust
struct Point {
    x: i32,
    y: i32,
}
fn print_point(point: Point){
    println!("point x {}",point.x);
}
fn main(){
    let s = Point{x:1,y:2};
    print_point(s);// 所有权已经消失了
    // println!("{}",s.x);// 错误：value borrowed here after move
}
```

结构体 - 实现 copy

```rust
#[derive(Copy,Clone)] // 实现 copy，实现 copy 需要先实现 clone）
struct Point {
    x: i32,
    y: i32,
}
fn print_point(point: Point){
    println!("point x {}",point.x);
}
fn main(){
    let s = Point{x:1,y:2};
    print_point(s);
    // point x 1
}
```





# 函数值参数传递、不可变借用参数传递、可变借用参数传递

## 函数值参数传递

函数的代码本身通常是存储在可执行文件的代码段，而在调用时函数会在栈上开辟一个新的 stack frame（栈空间），用于存储函数的局部变量、参数和返回值地址等信息，而当函数结束后会释放该空间

而当传入 non-copy value（Vec、String等）

传入函数时实参会转移 value 的所有权给形参，实参会失去 value 的所有权，而在函数结束时，value 的所有权会释放

## 不可变借用

- 如果不像失去 value 的所有权，你又没有修改 value 的需求，你可以使用不可变借用
- 在 Rust 中，你可以将不可变借用作为函数的参数，从而在函数内部访问参数值，但不能修改它。这有助于确保数据的安全性，防止在多处同时对数据进行写操作，从而避免数据竞争
- 如何应用不可变借用
    - `Use * to deference` 去获取其值

## 可变借用

- 如果你有修改值的需求，你可以石笋可变借用，以允许在函数内部修改战书的值，者允许函数对参数进行写操作，但是在同一时间只能有一个可变引用

- 需要在形参前加 `&mut`

- 如何应用可变借用

    - 同样使用 `Use * to deference` 去获取其值

    

```rust
fn move_func(p1:i32, p2:String){
    println!("p1 is {}",p1);
    // p1 is 12
    println!("p2 is {}",p2);
    // p2 is string
}

// 这里是 borrow 而不是 copy
fn print_value(value: &i32){
    println!("{}",value);
    // 12
}

fn string_func_borrow(s:&String){
    println!("{}",(*s).to_string()); // 这里可以不加"*", 默认是解引用的
    // string
}

#[derive(Debug)] // Debug 表示可以打印
struct Point{
    x: i32,
    y:i32,
}


fn modify_point(point:&mut Point){
    (*point).x += 2;
    point.y += 2; // 默认是解引用的，可以不加 "*"
}
fn main(){
    let n = 12;
    let s = String::from("string");
    move_func(n,s); // "string" 的所有权在函数结束的时候被销毁了
    println!("n is {}",n);
    // n is 12
    // println!("s is {}",s); // 错误：value borrowed here after move // 所有权被转移了
    let x= 12;
    let y = String::from("string");

    // 不可变借用
    print_value(&x);
    print_value(&n);
    string_func_borrow(&y);
    println!("s is {}",y);
    // s is string

    // 可变借用
    let p = Point{x:0, y:0};
    println!("{:?}",p); // ":?" 使用了 debug 的特质来进行打印
    // Point { x: 0, y: 0 }
    let mut q = Point{x:0,y:0};
    modify_point(&mut q);
    println!("{:?}",q);
    // Point { x: 2, y: 2 }
}
```





# 函数的返回值与所有权机制

## 返回 copy 与 non-copy

copy 与 non-copy 都可以返回，但是要注意 non-copy 是在堆上的

性能：在一般情况下，返回 copy 类型的值通常具有更好的性能。这是因为 copy 的值是通过复制进行返回的，而不涉及堆上内存的分配和释放，通常是在栈上分配。这样的操作比涉及堆上内存分配和释放更为高效。



## 返回引用

- 在只有传入一个引用参数，只有一个返回引用时，生命周期不需要声明
- 其他情况下需要声明引用的声明周期
- 慎用 `'static`

```rust
fn func_copy_back() -> i32{
    let n = 42;
    n
}

fn func_non_copy_back() -> String{
    let s = String::from("hello");
    s
}


fn get_mess(mark: i32) -> &'static str{
    if mark == 0 {
        "string"
    }else{
        "string too"
    }
}
fn main(){
    let i = func_copy_back();
    println!("{}",i);
    // 42
    let s = func_non_copy_back();
    println!("{}",s);
    // hello
    println!("{}",get_mess(i));
    // string too
}
```



# 六、高阶函数：函数作为参数与返回值

## 1. 高阶函数（Higher-Order Functions）

Rust 允许使用高阶函数，即函数可以作为参数传递给其他函数，或者函数可以返回其他函数

高阶函数也是函数式编程的重要特性



## 2. 高阶函数与集合

1. map 函数：`map` 函数可以用于对一个集合中的每个元素应用一个函数，并返回包含结果的新集合
2. filter 函数：`filter`函数用于过滤集合中的元素，根据一个谓词函数的返回值
3. fold：`fold` 函数（有时也称为 `reduce`）可以用于迭代集合的每个元素，并将它们积累到一个单一的结果中



```rust
fn  func_twice(f:fn(i32) -> i32, x: i32) -> i32{
    f(f(x))
}

fn mul(x:i32) -> i32{
    x * x
}

fn add(x:i32) -> i32 {
    x + 10
}

fn main(){
    let result = func_twice(mul,3);
    println!("result is {result}");
    // result is 81
    let res = func_twice(add,10);
    println!("res is {}",res);
    // res is 30

    // 数学计算：集合操作
    let numbers = vec![1,2,3,4,5,6,7,8,9];
    let res:Vec<_> = numbers.iter().map(|&x|x+x).collect();
    println!("{:?}",res);
    // [2, 4, 6, 8, 10, 12, 14, 16, 18]

    // filter
    let nums = vec![1,2,3,4,5,6,7,8,9];
    // ref ref_mut move
    let evens= numbers.into_iter().filter(|&x|x % 2 == 0).collect::<Vec<_>>(); // .collect::<Vec<_>>() 等同于 .collect()
    println!("{:?}",evens);
    // [2, 4, 6, 8]

    // reduce
    let nums2 = vec![1,2,3,4,5,6,7,8,9];
    let sum  = nums2.iter().fold(0,|acc,&x|acc + x);
    println!("Sum: {}",sum);
    // Sum: 45
}
```



