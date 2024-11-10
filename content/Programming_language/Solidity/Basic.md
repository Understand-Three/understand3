---
title: solidity 基础
draft: true
---
# 1. 环境准备
打开在线 IDE [Remix](https://remix.ethereum.org/) 编写代码，并测试环境是否正常

## 1.1 打开默认工作区

![[../../Images/remix-default-wokespace.png]]

这个按键的解释，[图片来源](https://www.wtf.academy/docs/solidity-101/HelloWeb3/)
![Remix 面板](https://www.wtf.academy/assets/images/1-1-59ec4df354181363259759212e42dad1.png)


## 1.2 创建文件 hello.sol

> 在 contracts 目录中创建 hello.sol 文件，（你可以删除 contracts 目录下的其他的三个文件，我这里已经删除了，也可以不删除）

![[../../Images/remix-create-file.png]]

## 1.3 写入 hello world 代码

```solidity title="hello.sol"
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.21;
contract HelloWorld{
    string public string = "Hello World!"; 
}
```

> 编译后会解释这段代码 `^_^`
## 1.4 编译文件

>[!ERROR] 错误
>
>```error
>Worker error: Uncaught NetworkError: Failed to execute 'importScripts' on 'WorkerGlobalScope': The script at 'https://solc-bin.ethereum.org/bin/soljson-v0.5.1+commit.c8a2cb62.js' failed to load.
>```

这是编译器加载失败，刷新一下页面试试，如果写了代码记得先保存到本地，如下为正常：

![[../../Images/remix-compiler.png]]


# 2. 测试环境 Hello World

在左侧的 “编译” 按钮上（`silidity compiler`）点击 `complie hello.sol` 按钮开始编译

![[../../Images/compile-hello.png]]

编译成功会在 “编译” 按钮上出现一个绿色的 `√`

## 2.1 部署页面

在 `DEPLOY & RUN TRANSACTIONS`  有一哥橙色的按钮 `deploy`，点击一下就可以部署

![[../../Images/remix-deploy.png]]

在下方会出现一个绿色的 `√` 表示部署成功，
## 2.2 测试合约

左侧下方有一个小三角，后面是方法名

![[../../Images/test-hello.png]]

点击小三角展开会出现变量名称，蓝色表示这是一个只读变量

点击后会出现 “hello world”，测试成功。

# 3. 解释代码

```solidity
// SPDX-License-Identifier: MIT
pragma solidity 0.8.7; // 使用 0.8.7 以上的版本 (0.8 版本内的)
contract HelloWorld {
string public myString = "hello world";
}
```


第一行：版权声明注释（不写会有警告）

```solidity
// SPDX-License-Identifier: MIT
```


第二行：指定编译器的版本

```solidity
pragma solidity ^0.8.7; // 使用 0.8.7 以上的版本 (0.8 版本内的)
```


第三行：定义一个合约

```solidity
contract HelloWorld {
string public myString = "hello world"; // 使用分号结尾
}
```

第四行：第一个变量

```solidity
string public myString = "hello world";
```


注释：
`//` : 单行注释

# 4. 中文 Solidity 资料推荐
1. [Solidity中文文档](https://docs.soliditylang.org/zh/v0.8.19/index.html)（官方文档的中文翻译）
2. [崔棉大师solidity教程](https://space.bilibili.com/286084162) web3技术教学博主，我看他视频学到了很多
3. [wtf](https://www.wtf.academy/docs/solidity-101/HelloWeb3/)