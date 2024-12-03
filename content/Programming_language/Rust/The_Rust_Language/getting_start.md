---
title: 开始
draft: true
---
## Linux 或 macOS 上安装 `rustup`

打开终端并输入下面命令：

```bash
$ curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh
```

这个命令将下载一个脚本并开始安装 `rustup` 工具，此工具将安装 Rust 的最新稳定版本。可能会提示你输入管理员密码。

如果安装成功，将出现下面这行：

`Rust is installed now. Great!`

OK，这样就已经完成 Rust 安装啦。

## 更新

要更新 Rust，在终端执行以下命令即可更新：

`$ rustup update`

## 卸载

要卸载 Rust 和 `rustup`，在终端执行以下命令即可卸载：# 

```bash
rustup self uninstall
```

## 检查安装是否成功

检查是否正确安装了 Rust，可打开终端并输入下面这行，此时能看到最新发布的稳定版本的版本号、提交哈希值和提交日期：

```bash
$ rustc -V rustc 1.56.1 (59eed8a2a 2021-11-01)  $ cargo -V cargo 1.57.0 (b2e52d7ca 2021-10-21)
```


# IDE

使用 `VSCode` 编辑器和 `Rust` 插件以及 `rust-analyzer` 插件

## 安装其它好用的插件

在此，再推荐大家几个好用的插件：

1. `Even Better TOML`，支持 .toml 文件完整特性
2. `Error Lens`, 更好的获得错误展示
3. `One Dark Pro`, 非常好看的 VSCode 主题
4. `CodeLLDB`, Debugger 程序

好了，至此，VSCode 的配置就已经全部结束，是不是很简单？下面让我们来用 `Cargo` 创建一个 Rust 项目，然后用 VSCode 打开。