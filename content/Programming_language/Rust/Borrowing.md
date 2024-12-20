---
title: Borrowing 借用 && Lifetime 生命周期
draft: true
---

# Borrowing && Borrow Checker && Lifetime

## Borrowing（引用的函数式的命名）

一个东西的两种描述

引用（Reference）：

1. 引用是一种变量的别名，通过 & 符号来创建。（非所有权）
2. 引用可以是不可变的（&T）或可变的（&mut T）
3. 引用允许在不传递所有权的情况下访问数据，他们是安全且低开销的。

借用（Borrowing）：

1. 借用是通过引用（Reference）来借用（Borrow）数据，从而在一段时间内访问数据而不拥有它
2. 借用分为可变借用和不可变借用。
    - 可变借用（&mut）允许修改数据，但在生命周期内只能有一个可变借用
    - 不可变借用（&）允许多个同事存在，但不允许修改数据



## Borrow Checker

- Borrow Checker 的规则

    1. 不可变借用规则：

        在任何给定的时间，要么有一个可变引用，要么有多个不可变引用，但是不能同时存在可变引用和不可变引用。这确保了在同一时间只有一个地方对数据进行修改，或者有多个地方同时读取数据

    2. 可变引用规则：

        在任何给定的时间，只能有一个可变引用来访问数据，这防止了并发修改相同数据的问题，从而防止了数据竞争。

    3. 生命周期规则：

        引用的生命周期必须在被引用的数据有效的时间范围内。这防止了悬垂引用，即引用的数据已经被销毁，但引用依旧存在

    4. 可变引用与不可变引用互斥：

        可以同时存在多个不可变引用，因为不可变引不会修改数据，不会影响到其他引用。但不可变引用与可变引用之间是互斥的

## 手动指定 Lifetime

生命周期参数在函数 / 结构体签名中指定：

- 一般情况下 Borrow Checker 会自行推断（随着Rust 版本的更新，会越来越强）
- 在函数 / 结构体签名中使用生命周期参数允许函数声明引用的有效范围



```rust
use std::fs::read_to_string;

fn main() {
    let mut s = String::from("Hello");
    // 不可变引用，可以同时修有多个不可变引用
    let r1 = &s;
    let r2 = &s;
    println!("r1 is {},\nr2 is {}",r1,r2);
    // r1 is Hello,
    // r2 is Hello
    let r3 = &mut s;
    println!("r3 is {}",r3);
    // r3 is Hello
    // println!("r1 is {},\nr2 is {}",r1,r2); //错误：immutable borrow later used here
    //
    let result:&str ; // 定义
    {
        result = "str"; // 这里是初始化
    }
    println!("result is {}",result);
    // result is str

    let result2:&str;
    {
        let r4 = &s;
        result2 = ff(r4);
    }
    // println!("r4 is {}",r4); // 超出生命周期
    println!("result2 is {}",result2);
    // result2 is Hello
}
fn ff<'a>(s:&'a str) -> &'a str{
    s
}

```





# Lifetime 与 函数

## 任何引用都是有生命周期的

大多数情况下，生命周期是隐式且被推断的

生命周期的主要目的是防止悬垂引用

关于“悬垂引用”的概念是指：引用指向的数据在代码结束后被释放，但引用仍然存在。

生命周期的引入有助于确保引用的有效性，防止程序在运行时出现悬垂引用的情况。通过生命周期的推断，Rust 能够在编译时检查代码，确保引用的有效性，而不是在运行时出现悬垂引用的错误。



## 生命周期与函数

编译器在没有显式注解的情况下，使用三个规则来推断这些生命周期：

1. 每个作为引用的参数都会得到它自己的生命周期参数。
2. 如果只有一个输入生命周期参数，那么该生命周期将被分配给所有输出生命周期参数（该生命周期将分配给返回值）
3. 如果有多个输入生命周期参数，但其中一个是对可变 self 或不可变self 的引用时，在这种情况下， self 的生命周期被分配给所有输出生命周期参数

```rust
use std::arch::aarch64::vaba_s16;

// 只有一个参数和返回值，不需要标注生命周期
fn no_need(s:&str) -> &str{
    s
}
// 有两个参数，需要标注生命周期
fn static_no_need(s1:&'static str,s2:&str) -> &'static str{
    // s1 // returning this value requires that `'1` must outlive `'static`
    s1
}

// 如果没有返回，不需要标注生命周期
fn no_return(s1:&str,s2:&str){
}
// 有返回 需要标记生命周期
fn longest<'a>(s1:&'a str,s2:&'a str) -> &'a str{ // 使用同一个生命周期
    if s1.len() > s2.len() {
        s1
    } else {
        s2
    }
}

// 使用不同的生命周期
// fn longest_lifetime<'a,'b>(s1:&'a str,s2:&'b str) -> &'a str{ // 使用同一个生命周期
//     if s1.len() > s2.len() {
//         s1
//     } else {
//         s2 // 返回 s2 的时候，生命周期报错： function was supposed to return data with lifetime `'a` but it is returning data with lifetime `'b`
//
//     }
// }


// 这样写性能会好一些
fn longest_diff_lifetime<'a,'b,'out>(s1:&'a str,s2:&'b str) -> &'out str
   where
    'a: 'out,
    'b: 'out, {
    if s1.len() > s2.len() {
        s1
    } else {
        s2
    }

}

fn main(){
    println!("no need {}",no_need("str"));
    // no need str
    println!("no need {}",static_no_need("string","str"));
    // no need string

    // ---------
    let s1 = "string";
    let s2 = "hello";
    println!("longest is {}",longest(s1,s2));
    // longest is string

    let result1:&str;
    {
        let result2 = "world";
        result1 = longest_diff_lifetime(result2,s1);
        println!("Longest string: {}",result1);
        // Longest string: string
    }
}
```





# 三、 Lifetime 与 Struct

## 结构体中的引用

在结构体中的引用需要标注生命周期

结构体的方法（&self 等）不需要标注生命周期



```rust
struct MyStruct<'a>{
    text: &'a str, // 不建议写 &str，因为属性被销毁的时候，这个结构体就不能用了，建议 String
}

impl <'a> MyStruct<'a> {
    fn get_length(&self) -> usize{
        self.text.len()
    }
    fn modify_data(&mut self){
        self.text = "string";
    }
}


struct StringHolder{
    data:String,
}
impl StringHolder{
    fn get_length(&self) -> usize {
        self.data.len()
    }
    fn get_refrence<'a>(&'a self) -> &'a String{
        &self.data
    }
    fn get_ref(&self) -> &String{ // 不用写生命周期，会自动推断
        &self.data
    }
}
fn main(){
    let str = String::from("value");
    let mut x = MyStruct{
        text:str.as_str(),
    };
    x.modify_data();
    println!("x is {}",x.text);
    // x is string

    let holder = StringHolder{
        data: String::from("Hello")
    };
    println!("string holder is {}",holder.get_refrence());
    // string holder is Hello
    println!("string holder is {}",holder.get_ref());
    // string holder is Hello
}
```

