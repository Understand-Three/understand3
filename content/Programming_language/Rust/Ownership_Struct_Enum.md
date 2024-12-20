---
title: 所有权、结构体、枚举
draft: true
---


# 所有权机制、结构体与枚举

## Ownership

类型基础类型、数组、元组和 string 数据类型的不同，string是一种复杂类型，它的变量赋值会导致所有权的转移

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



# Rust 的内存管理模型

> stop the world
>
> 这是与垃圾回收（Garbage Collection）相关的术语，它指的是在进行垃圾回收的时候，系统暂停程序的运行
>
> 这个术语主要用于描述一种全局的暂停，即：所有应用程序线程都被停止，以便六级回收器能够安全地进行工作，这种全局性的停止会导致一些潜在的问题，特别是对于需要低延迟和高性能的应用程序
>
> 需要注意的是，并非所有的六级回收算法都需要“Stop the world”，有一些现代的垃圾回收器采用了一些技术来减少全局停顿的影响，比如并发垃圾回收和增量垃圾回收



> C/C++ 内存错误大全
>
> 1. 内存泄漏（Memory Leaks）
>     ```c
>     int* ptr = new int;
>     // 忘记释放内存
>     // delete ptr
>     ```
>
> 2. 悬空指针（Danagling Pointers）
>     ```c
>     int* ptr = new int;
>     delete ptr;
>     // ptr 现在是悬空的指针
>     ```
>
> 3. 重复释放 （Double Free）
>     ```c
>     int* ptr = new int;
>     delete ptr;
>     delete ptr;
>     ```
>
> 4. 数组越界（Array out of bounds）
>     ```c
>     int arr[5];
>     arr[5] = 10;
>     ```
>
> 5. 野指针
>
>     ```c
>     int* ptr;
>     *ptr = 10; // 野指针
>     ```
>
> 6. 使用已经释放的内存（Use After Free）
>      ```c
>      int* ptr = new int;
>      delete ptr;
>      *ptr = 10; // 使用已经释放的内存
>      ```
> 7. 堆栈溢出（Stack overflow）
>	
>     递归堆栈
>
> 8. 不匹配的 new / delete 或 malloc / free



- 所有权系统（Ownership system）

- 借用（Borrowing）
    - 不可变引用（借用）
    - 可变引变（可变借用）
- 生命周期（Lifetimes）
- 引用计数（Reference Counting）

```rust
fn get_length(str:String){
    println!("string is {}",str);
    // string is string
    // 函数结束之后销毁传入的参数
}

fn get_length_no_ownership(str:String) -> usize{ // usize 是返回类型
    println!("string is {}",str);
    // string is string
    str.len() // 返回
    // 函数结束之后，不销毁参数
}
fn main() {
    // copy  and move
    // copy
    let c1 = 1;
    // 如果是基础类型，会执行 copy 操作
    let _c2 = c1; // c1 仍然存在，
    println!("c1: {}",c1);
    // c1: 1

    let str1 = String::from("string");
    let str2 = str1; // str1 的所有权会转移给 str2， 所以 str1 就不存在了
    println!("str2 is {}",str2);
    // str2 is string
    // println!("str1 is {}",str1); //错误: value borrowed here after move
    let str3 = str2.clone(); // 执行 clone，所有权没有转移
    println!("str2 is {}",str2);
    // str2 is string
    println!("str3 is {}",str3);
    // str3 is string

    get_length(str2); // str2 的所有权被转移到了函数里面, 函数结束之后，str2 被销毁了
    // println!("str2 is {}",str2);// 错误: this parameter takes ownership of the value
    let str3_len = get_length_no_ownership(str3);
    println!("str3's length is {}",str3_len);
    // str3's length is 6

    let back = first_word("hello world");
    println!("one back is {}",back);
    let back  = first_word("we are the world");
    println!("two back is {}",back);


    // move
}

// 不能直接返回一个引用，所有权机制不明确
// fn dangle() -> &str{ // expected named lifetime parameter
//     // 因为无法确定生命周期
//     // 进而无法确定所有权什么时候销毁
// }

// 解决一
// 返回类型
fn dangle_owner() -> String {
    "string".to_owned()
}

// 解决二
// 静态的生命周期，在整个程序的运行期间都会存在
fn dangle_static() -> &'static str{
    "string"
}

// 传入一个切片引用，传出的也是一个切片引用
// String 与 &str vector u8 ref
fn first_word(s:&str) -> &str{
    let bytes = s.as_bytes();
    for(i,&item) in bytes.iter().enumerate(){
        if item == b' '{
            return &s[0..i];
        };
    }
    &s[..]
}
```



# String 与 &str

在 Rust 中表示字符串的两种类型， `String` 和 `&str`

- String 是一个堆分配的可变字符串类型

    源码:

    ```rust
    pub struct String {
    	vec: Vec<u8>
    }
    ```

- `&str` 是指字符串切片引用，是在栈上分配的
    - 不可变引用，指向存储在其他地方的 UTF-8 编码的字符串数据
    - 由指针和长度构成

> [!NOTE]
>
> 注意 String 是具有私有权的，而 &str 没有

- `Struct` 中属性使用 `String`
    - 如果不使用显式声明生命周期，无法使用 `&str`
    - 不只是麻烦，还有更多的隐患
- 函数参数推荐使用 `&str`（如果不想交出所有权）
    - &str 为参数，可以传递 `&str` 和 `&String`
    - `&String` 为参数，只能传递 `&String` 不能传递 `&str`


字面量 to String

```rust
fn main(){
    // String to &str 的三种方法
    // String::from() 一
    // .to_string() 二
    // .to_owned() 三
    let name = String::from("Value C++");
    let course = "Rust".to_owned(); // 方法一： 从字面量转 String
    let new_name = name.replace("C++","CPP");
    println!("name: {name} \ncourse: {course} \nnew_name: {new_name}");
    // Value C++
    // Rust
    // Value CPP

    let rust = "\x52\x75\x73\x74"; // ASCII
    println!("ASCII is {rust}")
    // ASCII is Rust
}
```

字符串的字面量实际上就是一个切片引用

Struct

```rust
// 结构体
struct Person_v1 {
    // gender:&str,// 生命周期未指定错误：Missing lifetime specifier [E0106]
    name:String,
    color:String,
    age: i32
}

struct Person<'a> {
    name:&'a str, // 表示字面量的生命周期和结构体的生命周期是一样的  // 传入字面量
    color:String,// 传入字符串类型
    age: i32
}

fn main(){
		// Struct
    let color = "green".to_string();
    let people = Person{
        name: "john", // 字面量
        color:color, // 字符串
        age:89,
    };
}
```

Function

```rust
// 可以传入 &String 字符串 和 &str 字面量
fn print(data:&str){
    println!("data: {data}")
}

// 只能传入 &String 字符串
fn print_string_borrow(data:&String){
    println!("borrow data: {}",data);
}
fn main(){
    let value = "value".to_string();
    // print(value); // 类型错误：mismatched types [E0308] expected `&str`, found `String`
    print(&value); // 传入 String 的引用
    // data: value
    print("the date"); // 传入字面量
    // data: the date

    // print_string_borrow("the data borrow");// 类型错误：mismatched types [E0308] expected `&String`, found `&str`
    print_string_borrow(&value); // 传入 String 的引用
    // borrow data: value
}
```





# 枚举与匹配模式

- 枚举（enums）是一种用户自定义的数据类型，用于表示具有一组离散可能值的变量
    - 每种可能值都被称为 “variant”（变体）
    - `枚举名::变体名`
- 枚举的好处
    - 可以使你的代码更严谨、更易读
    - More robust programs

```rust
enum Shape{
	Circle(f64),
  Rectangle(f64,f64),
  Square(f64),
}
```

## 常用的枚举类型

-  Option  返回值的内容或者没有值

```rust
pub enum Option<T> {
	None,
  Some<T>
}
```

- Result  返回成功或失败原因

```rust
pub enum Result<T,E>{
	OK(T),
  Err(E)
}
```





## 匹配模式

1. `match` 关键字实现
2. 必须覆盖所有的变体
3. 可以使用 `_` 、 `..=`  、三元`if` 等来进行匹配

```rust
match number {
	0 => println!(""Zero), // 仅匹配 0
  1 | 2 => println!("One or Tow"), // 匹配 1 或 2
  3..=9 => println!("From Three to Nine"), // 范围 3～9 匹配
  n if n % 2 == 0 => println!("Even number"), // 三元匹配 如果为 true 执行 print 操作
  _ => println!("Other"), // 匹配剩余的所有
}
```



```rust
enum Color{
    Red,
    Yellow,
    Blue,
    Black
}

fn print_color(my_color:Color){
    match my_color {
        Color::Red => println!("Red"),
        Color::Yellow => println!("Yellow"),
        Color::Blue => println!("Blue"),
        _ => println!()
    }
}

fn main(){
    print_color(Color::Red);
    // Red

    print_color(Color::Black);
    // 未匹配到， 什么都不做

    let a = Color::Red;
    print_color(a);
    // let b = a; // 错误：Use of moved value // a 的所有权已经被转移给之前传入的函数了
}
```

在枚举中使用关联函数

```rust
enum BuildingLocation{
    Number(i32),
    Name(String), // 不要用 &str
    Unknown, // 没有任何信息
}

// 关联函数
impl BuildingLocation {
    fn print_location(&self){ // 如果不使用 &self 则在调用的时候为 BuildingLocation::print_location()
        match self {
            BuildingLocation::Number(c) => println!("building number {}",c), // 使用 BuildingLocation(3) 此时的 c 就是 3
            BuildingLocation::Name(s) => println!("building name {}",*s),//使用 buildingLocation("ok".to_string())
            BuildingLocation::Unknown => println!("Unknown")
        }
    }
}
fn main(){
    let house = BuildingLocation::Name("bud".to_string());
    house.print_location();
    // building name bud
    let house2 = BuildingLocation::Number(12);
    house2.print_location();
    // building number 12

    let house3 = BuildingLocation::Unknown;
    house3.print_location();
    // Unknown
}
```



# 结构体、方法、关联函数、关联变量

## 结构体

结构体是一种用户定义的数据类型，用于创建自定义的数据结构。

```rust
struct Point{
	x:i32,
  y:i32,
}
```

每条数据（x 和 y）称为属性（字段 field），通过`.` 来访问结构体中的属性



### 结构体中的方法

结构体中的方法是指，通过实例调用（self、&mut self、self）

```rust
impl Point{
	fn distace(&self,other:&Point) -> {
  	let dx = (self.x - other.x) as f64;
  	let dy = (self.y - other.y) as f64;
  	(dx * dx + dy * dy).sqrt()
  }
}
```

### 结构体中的关联函数

关联函数是与类型相关联的函数，调用时为  `结构体名::函数名`

```rust
impl Point {
	fn new (x: u32, y: u32) -> Self{ // Self 大写，指的是 Piont
		Point {x,y}
	}
}
```

### 结构体中的关联变量

这里的关联变量是指，和结构体类型相关的变量，也可以在特质或是枚举中

```rust
impl Point {
	const PI:f64 = 3.14;
}
```

调用时使用 `Point::PI`



```rust
enum Flavor {
    Spicy,
    Sweet,
    Fruity,
}

struct Drink{
    flavor:Flavor,
    price:f64,
}

fn print_drink(drink:Drink) {
    match drink.flavor {
        Flavor::Fruity => println!("fruity"),
        Flavor::Spicy => println!("spocy"),
        Flavor::Sweet => println!("sweet"),
    }
    println!("{}", drink.price);
}

impl Drink{
    // 关联变量
    const MAX_PRICE: f64 = 10.0;

    // 方法
    fn buy(&self){
        // if self.price > Self::MAX_PRICE{
        if self.price > Drink::MAX_PRICE{
            println!("I am poor");
            // return
        }else {
            println!("buy it");
        }
    }
    // 关联函数
    fn new(price:f64) -> Self{
        Drink{
            flavor:Flavor::Fruity,
            price,

        }
    }
}

fn main() {
    let sweet  = Drink{
        flavor: Flavor::Sweet,
        price:6.0,
    };
    println!("{}",sweet.price);
    print_drink(sweet); // 所有权丧失了， sweet 被销毁了

    let sweet2 = Drink{
        flavor: Flavor::Sweet,
        price: 10.0,
    };
    sweet2.buy();

    let sweet3 = Drink::new(12.0);
    sweet3.buy()
}
```





# 所有权机制

## 规则

每个值在 Rust 中都必须有一个 owner

他们一在每个时刻都只能有一个 owner

值在超出作用域的时候会被自动销毁



## value passing semantocs 值传递语义

每当将值从一个位置转移到另一个位置时 ，borrow checker 都会重新评估所有权

1. Immutable Borrow 使用**不可变的借用**，值的所有权仍然归发送者所有，接收方直接接收对该值的引用，而是不该值的副本。但是，他们不能使用该引用来修改它指向的值，编译器不允许这样做，释放资源的责任仍然由发送者承担。仅当发送人本身超出范围时，才会删除该值
2. Mutable Borrow 使用**可变的借用**，所有权和删除值的责任也由发送中承担，但是接收方能够通过他们接收的引用来修改该值
3. Move 这是所有权从一个地方转移到另一个地方，borrow checker 关于释放该值的决定将由该值的接收者（而不是发送者）通知。由于所有权已经从发送方转移到接收方，因此发送方在将引用转移到另一个上下文之后不能再使用该值引用，发送方在移动后对 value 的任何操作都会导致错误



## 结构体中关联函数的参数

```rust
&self (self: &Self) // 不可变引用

&mut self (self: &mut Self)  // 可变借用

self self(self: Self)   // Move

impl Point{
	get (self: Self) -> i32{
		self.x
	}
}
```

`self` 参数相当于 `Point::get(point)` 调用后丧失所有权（point 为实例对象）

`&self` 参数相当于对 `Point::get(&point)` ,

`&mut self` 参数相当于 `Point::get(&mut point)`



```rust
struct Counter{
    number: i32,

}
impl Counter{
    fn new(number:i32) -> Self{
        Self{number}
    }

    // 不可变借用
    fn get_number(&self) -> i32{ // 相当于： Counter::get_number(self,&Self)
        self.number
    }


    // 可变借用
    fn add(&mut self, increment: i32){ // 相当于：Counter::add(self: &mut self,increment)
        self.number += increment;
    }

     // move
    fn give_up(self){
         println!("free {}",self.number);
     }
    // Move
    fn combine(c1:Self, c2:Self) -> Self{
        Self{
            number:c1.number + c2.number,
        }
    }
}
fn main(){
    let  mut c1 = Counter::new(0);
    println!("c1's value is {}",c1.get_number());
    println!("c1's value is {}",c1.get_number());
    println!("c1's value is {}",c1.get_number()); // 可以多次操作， 所有权仍然在 c1 上
    // c1's value is 0
    c1.add(2);
    println!("c1's value is {}",c1.get_number());
    println!("c1's value is {}",c1.get_number());
    println!("c1's value is {}",c1.get_number()); // 可以多次操作， 仍然没有丧失所有权
    // c1's value is 2
    c1.give_up();
    // println!("c1's value is {}",c1.get_number()); // 错误：value borrowed here after move >>所有权已经丧失了

    let c2 = Counter::new(2);
    let c3 = Counter::new(1);
    let c4 = Counter::combine(c2,c3);
    // println!("c1's value is {}",c2.get_number()); // value borrowed here after move  >> c2 已经不存在了
    // println!("c1's value is {}",c3.get_number()); // value borrowed here after move  >> c3 已经不存在了
    println!("c1's value is {}",c4.get_number()); // c2 和 c3 的所有权转移到了 c4， c4 是值新创建值
}
```





# 堆栈、cpoy 和 clone

## 堆 heap

1. 堆的规律性较差，当你把一些东西放到你请求的堆上时，此时你请求空间，会返回一个指针（智能指针/ box），这是该位置的地址
2. 长度不确定

## 栈 stack

1. 堆栈将按照获取值的顺序存储值，并以相反的顺序删除值（先进后出）
2. 操作高效，函数作用域就是的栈上
3. 堆栈存储的所有数据都必须具有已知的固定大小数据

## Box

Box 是一个智能指针，它提供对堆分配内存的所有权。它允许你将数据存储在堆上而不是栈上，并且在复制或移动时保持对数据的唯一拥有权。使用 Box 可以避免一些内存问题，例如悬垂指针和重复释放

1. 所有权转移
2. 释放内存
3. 解引用
4. 构建递归数据结构



## copy 与 clone

Move：所有权转移

Clone：深拷贝

Copy：Copy 是在 Clone 的基础上建立的 marker trait （Rust 中最类似继承的关系）

1. trait（特质）是一种定义共享行为的机制。Clone 也是特质
2. marker trait 是一个没有任何方法的 trait， 它主要用于向编译器传递某些信息，以改变类型的默认行为

## 堆和栈 与 copy和move

stack

1. 基础类型
2. tuple 和 arrry
3. struct 与枚举也是存储在栈上；如果在 struct 中的属性有 string 等在堆上的数据类型，那么这个 struct 会指向堆



heap

Box Rc String/Vec 等（集合类）

一般来说在栈上的数据类型都是默认 copy，在赋值的时候会产生一个新的值。

 struct 和枚举等默认为 move，需要 copy 只需要设置数据类型实现 copy 特质即可，或是调用 clone 函数（需要 clone 特质）



 Box

```rust
struct Point{
    x:i32,
    y:i32,
}

fn main(){
    let boxed_point = Box::new(Point{x:10,y:20}); // 放在堆上
    // Box 是个智能指针
    println!("x:{},y:{}",boxed_point.x,boxed_point.y);
    //x:10,y:20
    // 在调用属性和实例是一样的，会默认解掉
    //
    let mut boxed_point_mut = Box::new(32);
    println!("{}",boxed_point_mut);
    // 32
    //
    // 修改值
    // boxed_point_mut += 10; // 不能直接对直接加 10
    *boxed_point_mut += 10; // 需要先解引用
    println!("{}",boxed_point_mut);
    // 42
}
```



copy and move

```rust
struct Book{
    page:i32,
    rating: f64,
}
#[derive(Debug,Copy,Clone)] // 派生了 Debug、Copy 和 Clone 三个特性（traits）
struct BookDebug {
    page:i32,
    rating: f64,
}

#[derive(Debug,Clone,Copy)] // 派生了 Debug、Copy 和 Clone 三个特性（traits）
struct BookString {
    page:i32,
    rating: f64,
    name:String, // this field does not implement `Copy` // 需要自己实现 copy
}
fn main(){
    // 存储在堆上的
    let x = vec![1,2,3];
    let y = x;
    println!("{:?}",y);
    // [1, 2, 3]
    // println!("{:?}",x); // 错误：value borrowed here after move  // 所有权已经被转移到 y 了
    //
    let z = y.clone(); // clone
    println!("{:?}",z);
    // [1, 2, 3]
    println!("{:?}",y);
    // [1, 2, 3]

    // ---------------
    //
    let x = "ss".to_string();
    let y = x;
    // println!("{:?}",x); // 错误：value borrowed here after move  // 所有权被转移了
    // 建议的解决方案：
    // let y = x.clone();
    //           ++++++++

    // -------------
    let b1 = Book{
        page: 1,
        rating:0.1,
    };
    let b2 = b1;
    // println!("{:?}",b1); // 错误：value borrowed here after move  // 所有权已经被转移
    // ------------
    let b3 = BookDebug {
        page: 1,
        rating:0.1,
    };
    let b4 = b3;
    println!("{:?}",b3); // 派生了 Debug、Copy 和 Clone 三个特性（traits）所以可用
    // ------------

}
```

