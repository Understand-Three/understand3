---
title: 错误处理
draft: true
---

# 一、错误处理：Result、Option 以及  panic! 宏

## Rust 中的错误可以分为两种

Recoverable error：有返回类型

- 返回 Result 类型

- 返回 Option 类型

Unrecoverable type：没有返回类型，直接崩溃

- panic macro 将终止当前线程

## Result

- Result 是一个枚举类型，有两个变体： Ok 和 Err。它通常用于表示函数的执行结果，其中 Ok 表示成功的结果，Err 表示出现了错误

```rust 
pub enum Result<T,E>{
	Ok(T),
	Err(E)
}
```



## Option

- Option 也是一个枚举类型，有两个变体：Some 和 None
- 它通常表示一个可能为空的值

```rust
pub enum Option<T> {
	None,
	Some(T),
}
```

## panic!

当程序遇到无法继续执行的错误时，可以使用 `panic!` 宏来引发中断，中断会导致程序立即终止，并显示一条错误信息





```rust
use std::ops::Index;

fn divide(a: i32, b:i32) -> Result<f64,String>{ // 实际应该实现 error 特质
    if b == 0 {
        return Err(String::from("cannot be zero"));
    }
    let a = a as f64;
    let b = b as f64;
    Ok(a / b)
}

fn find_element(array:&[i32],target:i32) -> Option<usize>{
    for (index,element) in array.iter().enumerate() {
        if (*element) == target {
            return Some(index)
        }
    }
    None
}

fn main(){
    // result
    match divide(1,2) {
        Ok(number) => println!("{}",number),
        Err(err) => println!("{}",err)
    }
    // 0.5
    match divide(1,0) {
        Ok(number) => println!("{}",number),
        Err(err) => println!("{}",err)
    }
    // cannot be zero
    // -----------
    // option
    let arr = [1,2,3,4,5];
    match find_element(&arr,4) {
        None => println!("None"),
        Some(index) => println!("found in {}",index)
    }
    // found in 3
    match find_element(&arr,6) {
        None => println!("None"),
        Some(index) => println!("found in {}",index),
    }
    // None
    // ---------
    // panic!
    // let vec = [1,2,3,4,5];
    // vec[6]; // index out of bounds: the length is 5 but the index is 6
    // array 在编译的时候会确定长度，所以这是编译错误，而不是运行时错误
    //
    let vec = vec![1,2,3,4,5];
    vec[6];
    // 运行时错误
}
```





# 二、unwrap() 与 ?

## unwrap()

> [!NOTE]
>
> 注意该方法并不安全

`unwrap()` 是 Result 和 Option 类型提供的方法之一。它是一简便的方法，用于获取 Ok 或 Some 的值，如果是 Err 或 None 则会引发 panic

```rust
fn main(){
    let result_ok:Result<i32,&str> = Ok(32);
    let value = result_ok.unwrap();
    println!("ok {}",value);
    // ok 32
    let result_ok:Result<i32,&str> = Err("Error");
    let value = result_ok.unwrap();
    println!("error {}",value);
    // 触发 panic，程序终止  
}
```





## ? 运算符

- ？用于简化 Result 或 Option 类型的错误传播
- 它只能用于返回 Result 或 Option 的函数。
- 在函数内部可以像使用 `unwrap()` 一样访问 Ok 或 Some 的值，但是如果是 Err 或是 None 则会提前返回



```rust
use std::num::ParseIntError;
fn find_first_even(numbers:Vec<i32>) -> Option<i32> {
    let first_even = numbers.iter().find(|&num|num % 2 == 0)?;
    println!("Option");
    Some(*first_even)
}

// 传递错误
fn parse_numbers(input:&str) -> Result<i32,ParseIntError>{
    let val = input.parse::<i32>()?;
    Ok(val)
}

fn main() -> Result<(),Box<dyn std::error::Error>> {
    let result_ok:Result<i32,&str> = Ok(32);
    let value = result_ok.unwrap();
    println!("ok {}",value);
    // ok 32
    let result_ok:Result<i32,&str> = Ok(32);
    let value = result_ok?;
    println!("{}",value);
    // 32
    let numbers = vec![1,3,4,5];
    match find_first_even(numbers) {
        None => println!("no such number"),
        Some(number) => println!("first even {}", number),
    }
    // Option
    // first even 2
  
    // ---------------
    let numbers = vec![1,3,5];
    match find_first_even(numbers) {
        None => println!("no such number"),
        Some(number) => println!("first even {}", number),
    }
    // no such number
    match parse_numbers("str") {
        Ok(i) => println!("parsed {}",i),
        Err(err) => println!("failed to parse: {}",err)
    }
    // failed to parse: invalid digit found in string
    Ok(())

}
```



# 三、自定义一个 Error 类型

## 1. 自定义 Error 类型的三个步骤

1. 定义错误类型结构体：创建一个结构体来表示你的错误类型，通常包含一些字段来描述错误的详细信息
2. 实现 `std::fmt::Display` trait：实现这个 trait 以定义如何展示错误信息。这是为了使错误能够以人类可读的方式打印出来
3. 实现 `std::error::Error` trait：实现这个 trait 以满足 Rust 的错误处理机制的要求



```rust
use std::fmt::write;

#[derive(Debug)]
struct MyError{
    detail:String,

}

impl std::fmt::Display for MyError {
    fn fmt(&self,f:&mut std::fmt::Formatter<'_>) -> std::fmt::Result{
        write!(f,"Custom Error: {}",self.detail)
    }
}

impl std::error::Error for MyError{
    fn description(&self) -> &str {
       &self.detail
    }
    // 在 rust 中 &String 会自动转换为 &str
}

fn func() -> Result<(),MyError>{
    Err(MyError{
        detail: "Custom Error".to_owned()
    })
}

fn main(){
    match func() {
        Ok(_) => println!("function ok"),
        Err(err) => println!("Error: {}",err)
    }
    // Error: Custom Error: Custom Error
}
```





```rust
use std::fmt::write;

#[derive(Debug)]
struct MyError{
    detail:String,

}

impl std::fmt::Display for MyError {
    fn fmt(&self,f:&mut std::fmt::Formatter<'_>) -> std::fmt::Result{
        write!(f,"Custom Error: {}",self.detail)
    }
}

impl std::error::Error for MyError{
    fn description(&self) -> &str {
       &self.detail
    }
    // 在 rust 中 &String 会自动转换为 &str
}

fn func() -> Result<(),MyError>{
    Err(MyError{
        detail: "Custom Error".to_owned()
    })
}

fn main() ->Result<(),MyError>{
    func()?; // 在这里会抛出 error
    // Error: MyError { detail: "Custom Error" }
    println!("no"); // 不会打印
    Ok(())
}
```



```rust
use std::fmt::write;

#[derive(Debug)]
struct MyError{
    detail:String,

}

impl std::fmt::Display for MyError {
    fn fmt(&self,f:&mut std::fmt::Formatter<'_>) -> std::fmt::Result{
        write!(f,"Custom Error: {}",self.detail)
    }
}

impl std::error::Error for MyError{
    fn description(&self) -> &str {
       &self.detail
    }
    // 在 rust 中 &String 会自动转换为 &str
}

fn func() -> Result<(),MyError>{
    Err(MyError{
        detail: "Custom Error".to_owned()
    })
}

fn main() ->Result<(),Box<dyn std::error::Error>>{  // 也可以这样写
    func()?; // 在这里会抛出 error
    // Error: MyError { detail: "Custom Error" }
    println!("no"); // 不会打印
    Ok(())
}
```



```rust
use std::fmt::write;

#[derive(Debug)]
struct MyError{
    detail:String,

}

impl std::fmt::Display for MyError {
    fn fmt(&self,f:&mut std::fmt::Formatter<'_>) -> std::fmt::Result{
        write!(f,"Custom Error: {}",self.detail)
    }
}

impl std::error::Error for MyError{
    fn description(&self) -> &str {
       &self.detail
    }
    // 在 rust 中 &String 会自动转换为 &str
}

fn func() -> Result<(),MyError>{
    // Err(MyError{
    //     detail: "Custom Error".to_owned()
    // })
    Ok(())
}

fn main() ->Result<(),Box<dyn std::error::Error>>{
    func()?; // 返回 Ok
    println!("no"); // 会打印
    Ok(())
}
```







