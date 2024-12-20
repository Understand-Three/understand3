---
title: 变量与数据类型
draft: true
---

# 1. 变量与不可变性

## 变量

- 使用 let 声明变量

    `let x`

- Rust 支持类型推导，但你也可以显式地指定变量类型

    `let x:i32 = 5 # 显式地指定为 i32 类型`

- 变量名使用蛇形命名法 (snake_case)，而枚举和结构体使用帕斯卡命名法(PascalCase)

    `let user_name`

    `struct UserName`

- 如果变量没有使用，可以为其添加前置下划线，消除警告 

    `let _x`

- 强制类型转换 

    `let a = 3.1;  let b = a as i32`

- 打印变量   （`{}`与`{:?}` 需要实现特质，在之后的章节介绍，基础类型默认实现）

    `println!("val: {}, x")`

    `println!("val: {x}")`

## 不可变

不可变性时 Rust 实现其可靠性和安全性目标的关键

不可变性有助于防止数据竞争和并发问题

Shadowing Variables 并不是重新赋值

Rust 允许你隐藏一个变量，这意味着你可以声明一个与现有变量同名的新变量，从而有效地隐藏前一个变量

- 可以改变值
- 可以改变类型
- 可以改变可变性







```rust
fn main() {
    // 不可变
    let a = 10; // 自动推导为 i32 类型
    let b:i64 = 10; // 指定为 i64 类型

    let c = "before";
    println!("before c: {}",c);
    // c = 20; // 错误: Cannot assign twice to immutable variable [E0384]
    let mut c = "after";
    println!("after c: {}", c);
    // 可以重定义类型可变性

    // 声明可变
    let mut d = 10;
    d = 20; // mut 可以修改
    println!("use mut d: {}",d);
    // use mut d: 20
    // d = "string";// 但是 mut 只能改为相同类型, 错误: mismatched types [E0308] expected `i32`, found `&str`

    // 切变引用  在同一个作用域下，重新声明了不同类型的值，它覆盖了之前的值
    let e = 5;
    let e = 10;
    let e = "string";
    println!("final e: {}",e);
    // final e: string

    //shadowing
    let f = 10;
    { // 新的命名空间
        let f = 20; // 可以赋值
        println!("inner x : {}",f)
    }
    // 离开作用域后，内部的 e 被销毁了
    println!("outer x: {}",f);
    // inner x : 20
    // outer x: 10


    // 没有用到的变量使用 _ 使其不警告
    let _g = 10;
}
```





# 2. 常量与静态变量

## const 常量

- 常量的值必须是在编译时已知的常量表达式，必须指定类型与值

- 与 C 语言的宏定义（宏体替换）不同， Rust 的 const 常量的值直接被嵌入到生成的底层机器代码中，而不是进行简单的替换

- 常量名与静态变量名约定为全部大写，单词之间加入下划线 `USER_NAME`
- 常量的作用域是块级作用域 `{}`，它们只在声明它们的作用域内可见







## static 静态变量

- 与 const 常量不同，static 变量是在运行时分配内存的
- 并不是不可变的，可以使用 `unsafe` 修改
- 静态变量的声明周期为整个程序的运行时间





```rust
static MY_STATIC:i32 = 42;
static mut MY_MUT_STATIC:i32 = 42;

fn main() {
    // 常量 const
    const SECOND_HOUR: usize = 3_600; // 3600 的更易读的写法
    const SECOND_DAY: usize = 24 * SECOND_HOUR; //在编译的时候会被确定（类型和值）
    println!("{}",SECOND_DAY);
    // 86400

    // 块级作用域
    {
        const SE: usize = 1_000;
        println!("const scope: {SE}");// 常量只能在块级作用域内打印
        // scope: 1000
    }
    // println!("const {SE}");// 不可以在在块级作用域外打印块级作用域内的常量
    // error

    println!("static: {MY_STATIC}");
    // static: 42
    // No mut
    // MY_STATIC = 10; // 错误: Cannot assign twice to immutable variable [E0384]
    // Use mut
    // MY_MUT_STATIC = 10; // 错误: Use of mutable static is unsafe and requires unsafe function or block [E0133]
    // 必须使用 unsafe 访问 static mut 变量
    unsafe {
        // 可以修改
        MY_MUT_STATIC = 10;
        println!("inner: {MY_MUT_STATIC}")
        // inner: 10
    }
    //note: mutable statics can be mutated by multiple threads:
    // aliasing violations or data races will cause undefined behavior
    // println!("outer: {MY_MUT_STATIC}") // 错误: 不可以访问
}
```





# 3. 基础数据类型

- Integer types 默认推断为 `i32`
    - `i8`  `i16`  `i32`  `i64`  `i128`
- Unsigned Integer Types
    - `u8`  `u64`  `u32`  `u64`  `u128` 
- Paltform-Specific Integer Type （由平台决定）
    - usize
    - isize
- Float Types
    - `f32` 与 `f64`
    - 尽量使用 `f64` ，除非你清楚边界需要的空间，并且希望节省空间
- Boolean Value
    - true
    - false
- Character Types
    - Rust 支持 Unicode 字符 :laughing:
    - 表示 char 类型使用单引号



```rust
use std::{isize, usize};

fn main() {
    // 进制的字面量
    let a = -125; // 十进制
    let b = 0xFF; // 十六进制
    let c = 0o13; // 八进制
    let d = 0b10; // 二进制
    println!("Decimal {a},\n Hexadecimal: {b},\n Octal: {c},\n Binary: {d}");
    println!("u32 max: {}",u32::MAX);
    println!("u32 max: {}",u32::MIN);
    println!("u32 max: {}",i32::MAX);
    println!("u32 max: {}",i32::MIN);
    println!("usize max: {}",usize::MAX);
    println!("usize is {} bytes",std::mem::size_of::<usize>());
    println!("isize is {} bytes",std::mem::size_of::<isize>());
    println!("u64 is {} bytes",std::mem::size_of::<u64>());
    println!("i64 is {} bytes",std::mem::size_of::<i64>());
    println!("u32 is {} bytes",std::mem::size_of::<u32>());
    println!("i32 is {} bytes",std::mem::size_of::<i32>());

    // float
    let e:f32 = 1.2345;
    let f:f64 = 6.7809;
    println!("Float are {:.2}, {:.2}",e,f); // {:.2} // 在第二位四舍五入

    // bool
    let is_ok = true;
    let can_ok:bool = false;
    println!("is ok? {is_ok}\n can ok? {can_ok}");
    println!("is ok or can ok? {}\n can ok and is ok {}",is_ok || can_ok, is_ok && can_ok );

    // char
    let char_c = 'C';
    let emo_char ='😊';
    println!("You get {}, and  feel {}",char_c,emo_char);
    println!("emoji's unicode number is {}",emo_char as usize);
}
// 
Decimal -125,
 Hexadecimal: 255,
 Octal: 11,
 Binary: 2
u32 max: 4294967295
u32 max: 0
u32 max: 2147483647
u32 max: -2147483648
usize max: 18446744073709551615
usize is 8 bytes
isize is 8 bytes
u64 is 8 bytes
i64 is 8 bytes
u32 is 4 bytes
i32 is 4 bytes
Float are 1.23, 6.78
is ok? true
 can ok? false
is ok or can ok? true
 can ok and is ok false
You get C, and  feel 😊
emoji's unicode number is 128522

```









## 3.1 元组与数组

- 相同点

    - 元组和数组都是 compound types，而 vec 和map 都是 collection types

    - 元组和数组的长度都是固定的

- 不同点

    - Tuples 保存不同的数据类型

    - Arrays 保存相同的数据类型



### 3.1.1 数组

- 数组是长度固定的同构集合
- 创建方式
    - `[a, b, c]`放入每个元素
    - `[value; size]` 元素初始值；数量
- 获取元素 `arr [index]`
- 获取长度 `arr. len()`

### 3.1.2 元组

- 元组是固定长度的异构集合
- Empty Tuple ()
    - 为函数默认返回值
- 元组获取元素
    - `tup.index`
    - 没有 `len()`

```rust
use std::{isize, usize};

fn main() {
    let tup =(0,"str",2.3);
    println!("tup elements is {}, {}, {}",tup.0,tup.1,tup.2);
    // tup elements is 0, str, 2.3

    let mut tup2 = (0,"str", 2.3);
    println!("tup2 elements is {}, {}, {}",tup2.0,tup2.1,tup2.2);
    // tup2 elements is 0, str, 2.3
    // tup2.0 = 'f'; // 错误: mismatched types [E0308] expected `i32`, found `char`
    tup2.1 = "string";
    println!("tup2 elements is {}, {}, {}",tup2.0,tup2.1,tup2.2);
    // tup2 elements is 0, string, 2.3

    let tup3 = ();
    println!("tup3 is empty: {:?}",tup3); // {:?} 使其可以被打印
    // tup3 is empty: ()

    // Array
    let mut arr = [11,12,34];
    arr[0] = 99;
    println!("arr let {} first element is {}",arr.len(),arr[0]);
    // arr let 3 first element is 99

    for element in arr {
        println!("{}",element);
    }

    let ar = [2; 3]; // [2,2,2]
    for i in ar{
        println!("{}",i)
    }
}
```

# 4. 所有权机制

Ownership

类型基础类型与数组、元组

它们和 string 数据类型的不同

```rust
fn main() {
    // ownership
    let arr_item = [1,2,3];
    let tup_item = (2,"ff");
    println!("arr {:?}",arr_item);
    println!("tup {:?}",tup_item);

    let arr_ownership = arr_item;
    let tup_ownership = tup_item;
    println!("arr {:?}",arr_ownership);
    println!("tup {:?}",tup_ownership);

    let a = 3;
    let b = a;
    println!("{a}");
    // 变量赋值默认执行的是 copy 操作， 变量 a 在赋值结束后还是存在的
    println!("{b}");
    
    // move 赋值，会更改所有权 ownership
    let string_item = String::from("the string");
    let string_item_to = string_item; // String 类型就把 Ownership 进行了 Move 操作， string_item 就不存在了
    println!("string_item is {}",string_item); // 错误: value borrowed here after move 
}
```















