---
title: 什么是 lib.rs
link: https://blog.csdn.net/vince1998/article/details/138371970
---

# 一、Rust lib.rs 文件有什么用

按文件描述，他就是一个库文件，整个 `package` 只能有一个，那实战中它到底有什么用？不要它行不行？

`lib.rs` 文件通常用于定义库的公共接口和模块结构

其实我认为，Rust 对 文件和函数 的视角和 Java、Golang 不太一样，把（文件，函数）都看成一个个（模块，模块条目），按（模块、模块条目）来设置可见性，类似public还是private的效果

那每一个模块和模块条目，能否被别的模块使用，我们就需要在lib.rs文件中进行定义引入，这样才，才，才可以使用引用的模块（文件）和模块条目（函数）

# 二、实战

我们来实战一下，先以一个最简单的例子，

## 1、案例一

一个package里面有三个文件，分别为`lib.rs`，`main.rs`，`main2.rs`。

假设，我们新建的文件是 `main2.rs`，里面我们写了新函数

```rust
pub fn Aoo() -> String{
	String::from("Aoo")
}
```

我现在想在 `main.rs` 中，调用这个 `Aoo` 函数，此时我们什么都不干，直接回到 `main.rs` 去尝试调用。

```rust
use hello_package::main2; // <-- Error
fn main(){

}
```

可以发现，是无法导入这个 `main2` 模块的，或者说 `main.rs` 无法看到 `main2` 这个模块，那我们应该怎么办？

这个时候 `lib.rs` 的作用就来了，我们在 `lib.rs` 声明有 `main2.rs` 这个模块，还可以声明 `main2.rs` 是公开的(这样哪怕是不同级别的模块也是可见的)

我们看看 `lib.rs` 文件的内容
```rust
pub mod main2;
pub fn Boo() -> String{
	String::from("Boo")
}
```

我们再回到main.rs中，看看能不能使用main2.rs中的函数

```rust
use hello_package::main2::{self,Aoo} // <-- OK
fn main(){
	Aoo();
}
```

这样我们就可以使用 `main2.rs` 新创建的函数了

## 2、案例2

按照案例1来看，难道我每次新创建一个文件都要去 `lib.rs` 去 `mod` 一下吗，万一我创建了很多，或者是我在一个目录下创建了很多新文件，每个文件下有很多新函数，难道我要一个个去 `mod` 吗？这太笨了吧？

假设是一个目录下，有很多新建的文件，我们可以在这个目录下，创建一个 `mod.rs` 文件，然后在 `mod.rs` 下，去声明，你需要公开该目录下的哪些模块，

举个例子，假设我有一个新目录 `my_house` ，目录下有 `mod.rs` 和两个新文件 `hostring.rs` 和 `serving.rs`

！！！！！！！！！注意
两个新文件 `hostring.rs` 和 `serving.rs` 我都想能被别的文件使用，那么我们需要这么做

（1）修改目录下mod.rs文件

```rust
pub mod serving;
pub mod hostring;
```

（2）修改 `lib.rs` 文件

首先导入目录这个 `mod`，mod 名称和目录名称一样，那么这里就是 `my_house`。

```rust
pub mod my_house;
```


这样就相当于我们引入了目录 `my_house`，在目录下 `my_house`，我们通过 `mod.rs` 去声明了我们要公开目录下的什么模块。这样完成的引入声明就完成了

我们在 `main.rs` 试试效果

```rust
use hello_package::main2;
use helo_package::my_house;
fn main(){

}
```
