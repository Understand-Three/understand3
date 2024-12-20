---
title: 迭代器
draft: true
---

# 一、迭代与循环

## 循环（Loop）

定义：循环是一种控制流结构，它会反复执行一组语句，直到满足某个条件

控制条件：循环通常包含一个条件表达式，只有在条件为真时，循环中的雨局才会执行

退出条件：循环执行直到条件不再满足或是通过 `break` 语句显式中断

使用场景：适用于需要反复执行某个操作直到满足某个条件的情况



## 迭代（Iteration）

定义：迭代是对序列中的元素进行逐个访问的过程

控制条件：迭代通常使用迭代器（Iterator）来实现，迭代器提供了对序列元素的访问和操作

退出条件：通常不需要显式的退出条件，迭代器会在处理完所有元素后自动停止

使用场景：适用于需要便利数据结构中的元素的情况，例如：数组、切片、集合等

## 区别

1. 迭代是一个种数据结构，它反复执行一组语句
2. 迭代是对序列中的元素进行逐个访问的过程，通常使用迭代器实现
3. 循环可以是有限的（通过设置退出条件）或无限的（使用 `loop` 关键字）
4. Dodd器提供了一个更抽象的方法来处理序列，使得代码更具可读性和灵活性

在 Rust 中，迭代和循环的差距可能会取决于具体的使用情况，和编译器的优化。在绝大多数情况下，Rust 的迭代器是经过优化的，可以达到或接近手动编写最优循环的性能水平。

```rust
use std::sync::Barrier;

fn sum_with_loop(arr:&[i32]) -> i32 {
     let mut sum = 0;
     for &item in arr {
         sum += item;
     }
     sum
 }

 fn sum_with_iter(arr:&[i32]) -> i32 {
     arr.iter().sum()
 }


fn main(){
    const ARRAY_SIZE: usize = 10000;
    let arrry:Vec<i32> = (1..ARRAY_SIZE as i32).collect();
    let sum1 = sum_with_loop(&arrry);
    println!("sum loop {}",sum1);
    // sum loop 49995000

    let sum2 = sum_with_iter(&arrry);
    println!("sum iter {}",sum2);
    // sum iter 49995000
}
```





# 二、IntoIterator、Iterator、Iter之间的关系

## IntoIterator Trait

IntoIterator 是一个 Rust Trait，它定义了一种将类型转换为迭代器的能力

该 Trait 包含一个方法 into_iter，该方法返回一个实现了 Iterator Trait 的迭代器

通常，当你有一个类型，希望能够对其进行迭代时，你会实现 IntoIterator Trait 来提供将类型转换为迭代器的方法



## Iterator Trait

Itrator 是 Rust 标准库种的 Trait， 定义了一种访问序列元素的方式

它包含了一系列方法，如 `next`、`map` 、 `filter` 、 `sum` 等，用于对序列进行不同类型的操作

通过实现 `Iterator` Trait，你可以创建自定义的迭代器，以定义如何迭代你的类型种的元素

```rust
pub trait Iterator{
	type Item;
	fn next(&mut self) -> Option<Self::Item>;
}
```



## 源码种经常出现的 Iter

- Iter 是 Iterator Trait 的一个具体实现，通常用于对集合中的元素进行迭代。
- 在 Rust 中，你经常会看到 `Iter`，特别是在对数组、切片等集合类型进行迭代时
- 通过 IntoItertor Trait，你可以获取到一个特定类型的迭代器，比如 Iter，然后可以使用 Iterator Trait 的方法进行操作

```rust
fn main(){
    // vector
    let v = vec![1,2,3,4,5]; // intoIterator 特质， into_iter
    // 转换为迭代器
    let iter = v.into_iter(); // move 所所有权转移了, 类型 Iter Iterator 的特质对象
    let sum:i32 = iter.sum();
    println!("vector sum is {}",sum);
    // vector sum is 15
    // println!("{:?}",v); // value borrowed here after move
    // ------------------------
    // array
    let array = [1,2,3,4,5];
    let iter:std::slice::Iter<'_,i32> = array.iter();
    let sum: i32 = iter.sum();
    println!("array sum is {}",sum);
    println!("{:?}",array);
    // [1, 2, 3, 4, 5]

    // array sum is 15
    // --------------
    // char
    let text = "hello, world";
    let iter = text.chars(); // 会返回 iter()
    let uppercase = iter.map(|c|c.to_ascii_uppercase()).collect::<String>(); // 这是不可变引用，否则会性能非常差
    println!("char uppercase is {}",uppercase);
    // char uppercase is HELLO, WORLD
    println!("{:?}",text);
    // "hello, world"
}
```





# 三、获取迭代器的三种方法iter()、iter_mut() 和 Into_iter()

## Iter() 方法

iter() 方法返回一个不可变引用的迭代器，用于只读访问集合的元素

该方法适用于你希望在不修改集合的情况下迭代元素的场景



## itet_mut() 方法

iter_mut() 方法返回一个可变引用的迭代器，用于允许修改集合中的元素。

该方法适用于你希望在迭代过程中修改集合元素的场景



## into_iter() 方法

into_iter() 方法返回一个拥有所有权的迭代器，该迭代器会消耗集合本身，将所有权转移到迭代器。

该方法适用于你希望在迭代过程中拥有集合的所有权，以便进行消耗性的操作，如移除元素

```rust
fn main(){
    let vec = vec![1,2,3,4,5];
    // iter()  不可变
    for &iter  in vec.iter(){
        println!("iter() {}",iter);
        // iter() 1
        // iter() 2
        // iter() 3
        // iter() 4
        // iter() 5
    }
    println!("vec {:?}",vec);
    // vec [1, 2, 3, 4, 5]

    // iter_mut() 可变
    let mut vec2 = vec![1,2,3,4,5];
    for item in vec2.iter_mut(){
        *item *= 2;
        println!("iter_mut() {}",item);
        // iter_mut() 2
        // iter_mut() 4
        // iter_mut() 6
        // iter_mut() 8
        // iter_mut() 10
    }
    println!("vec2 {:?}",vec2);
    // vec2 [2, 4, 6, 8, 10]

    // 所有权转移
    let vec3 = vec![1,2,3,4,5];
    for item in vec3.into_iter(){
        println!("into_iter() {}",item);
        // into_iter() 1
        // into_iter() 2
        // into_iter() 3
        // into_iter() 4
        // into_iter() 5
    }
    // println!("vec3 is {:?}",vec3); // 错误：value borrowed here after move // 所有权已经被转移了
}
```





# 四、自定义类型实现 iter()、iter_mut() 和 into_iter()



```rust
#[derive(Debug)]
struct Stack<T>{
    items:Vec<T>
}

impl<T> Stack<T> {
    // 创建
    fn new() -> Self{
        Stack{items:Vec::new()}
    }
    // 入栈
    fn push(&mut self,item:T){
        self.items.push(item)
    }
    // 出栈
    fn pop(&mut self) -> Option<T>{
        self.items.pop()
    }
    // 不可变引用
    fn iter(&mut self) -> std::slice::Iter<T>{
        self.items.iter()
    }
    // 可变引用
    fn iter_mut(&mut self) -> std::slice::IterMut<T>{
        self.items.iter_mut()
    }
    fn into_iter(self) -> std::vec::IntoIter<T>{ // vector
        self.items.into_iter()
    }
}

fn main(){
    let mut my_stack = Stack::new();
    my_stack.push(1);
    my_stack.push(2);
    my_stack.push(3);

    for item in my_stack.iter(){
        println!("iter {}",item);
        // iter 1
        // iter 2
        // iter 3
    }
    println!("my_stack {:?}",my_stack);
    // my_stack Stack { items: [1, 2, 3] }

    // 可变引用
    for item in my_stack.iter_mut(){
        *item *= 2;
        println!("iter_mut {}",item);
        // iter_mut 2
        // iter_mut 4
        // iter_mut 6
    }
    println!("my_stack {:?}",my_stack);
    // my_stack Stack { items: [2, 4, 6] }
    //
    for item in my_stack.into_iter(){
        println!("into_iter() {}",item);
        // into_iter() 2
        // into_iter() 4
        // into_iter() 6
    }
    // println!("my_stack {:?}",my_stack); // value borrowed here after move
}
```

