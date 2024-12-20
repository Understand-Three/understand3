---
title: 浏览器是如何渲染页面的？
aliases:
  - How_does_the_browser _render_the_page?
  - 浏览器是如何渲染页面的？
original: https://juejin.cn/post/7167927579867873311
---
>[!NOTE] 线程与进程
>一台电脑可以运行多个程序，这里的程序是一个进程，一个程序的多个工作，这个工作是线程


# 前言

浏览器的主要功能总结起来就是一句话：将用户输入的 `URL` 转变成可视化的图像。

1. 从 `URL` 到 `DOM` 树；
2. 从 `DOM` 树到可视化图像；
3. 这两个过程之间的关系并没有那么明确，我们可以统称这两个过程为页面的渲染；

# 1. 网页的解析过程

- 思考一下：一个网页从 `url` 输入到浏览器，经历过怎样的解析过程？

![[Pasted image 20241119232841.png]]

- 要想深入理解下载的过程，我们还要先理解，一个 `index.html` 被下载下来后是如何被解析和显示在浏览器上的；

# 2. 浏览器的功能与组成

## 2.1 浏览器内核

1. `Trident` （ 三叉戟）： IE、 360 安全浏览器、 UC 浏览器
2. `Gecko`（ 壁虎） ： Mozilla Firefox
3. `Presto`（急板乐曲） -> Blink （眨眼）： Opera
4. `Webkit` ： Safari、 360 极速浏览器、搜狗高速浏览器、移动端浏览器（Android、 iOS）
5. `Webkit` -> `Blink` ： Google Chrome， Edge

![[Pasted image 20241119233115.png]]

> 浏览器的内核相当于汽车的发动机，是最核心的存在，它负责将代码转换成用户眼中的界面。

- 我们经常说的 浏览器内核 指的是 浏览器的排版引擎：
    - 排版引擎 (layout engine)：也称为浏览器引擎 (browser engine)、页面渲染引擎 (rendering engine) 或样版引擎；
- 也就是一个网页下载下来后，就是由我们的渲染引擎来帮助我们解析的；

## 2.2 进程与线程

- 进程与线程的解释：
    - 进程：程序的一次执行，它占有一片独有的内存空间，是操作系统执行的基本单元；
    - 线程：是进程内的一个独立执行单元，是 CPU 调度的最小单元；
- 浏览器： 多进程、多线程模型
    - `Browser` 进程：
        - 浏览器的主进程，负责浏览器界面的显示，和各个页面的管理；
        - 浏览器中所有其他类型进程的祖先，负责其他进程的的创建和销毁，它有且只有一个！
    - `Renderer` 进程：
        - 网页渲染进程，负责页面的渲染，可以有多个渲染进程的数量，不一定是打开页面的数量；
    - `GPU Process`：负责 GPU 相关；
    - `Plugin Process`：负责控制一个网页用到的 `Plugin`；

![[Pasted image 20241119233128.png]]

# 3. 浏览器渲染流程

## 3.1 渲染引擎解析过程

- 渲染引擎在拿到一个页面后，如何解析整个页面并且最终呈现出我们的网页呢？
    - 我们通过下面的这幅图，让我们更加详细的学习它的过程；

![[Pasted image 20241119233142.png]]

## 3.2 渲染引擎主要模块

- 一个渲染引擎主要包括：`HTML` 解析器，`CSS` 解析器，`javascript` 引擎，布局 `layout` 模块，绘图模块；
    - `HTML` 解析器：解释 HTML 文档的解析器，主要作用是将 HTML 文本解释成 DOM 树；
    - `CSS` 解析器：它的作用是为 DOM 中的各个元素对象计算出样式信息，为布局提供基础设施；
    - `Javascript` 引擎：使用 Javascript 代码可以修改网页的内容，也能修改 css 的信息，javascript 引擎能够解释 javascript 代码，并通过 DOM 接口和 CSS 树接口来修改网页内容和样式信息，从而改变渲染的结果；
    - 布局 (`layout`)：在 DOM 创建之后，Webkit 需要将其中的元素对象同样式信息结合起来，计算他们的大小位置等布局信息，形成一个能表达这所有信息的内部表示模型；
    - 绘图模块 (`paint`)：使用图形库将布局计算后的各个网页的节点绘制成图像结果；

# 4. 渲染页面的详细流程

> 浏览器渲染页面的整个过程：浏览器会从上到下解析文档。

![[Pasted image 20241119233154.png]]

## 4.1 HTML 解析过程

> 遇见 `HTML` 标记，调用 `HTML` 解析器解析为对应的 `token` （一个 `token` 就是一个标签文本的序列化）并构建 `DOM` 树（就是一块内存，保存着 `tokens`，建立它们之间的关系）

![[Pasted image 20241119233206.png]]

## 4.2 生成 CSS 规则

> 遇见 `style/link` 标记调用解析器处理 `CSS` 标记并构建 `CSS` 样式树。

![[Pasted image 20241119233216.png]]

## 4.3 构建 Render Tree

> 当有了 `DOM Tree` 和 `CSSOM Tree` 后，就可以两个结合来构建 `Render Tree` 了

![[Pasted image 20241119233225.png]]

- **注意一**： `link` 元素不会阻塞 `DOM Tree` 的构建过程，但是会阻塞 `Render Tree` 的构建过程
    - 这是因为 `Render Tree` 在构建时，需要对应的 `CSSOM Tree`；
- **注意二**： `Render Tree` 和 `DOM Tree` 并不是一一对应的关系
    - 比如对于 `display` 为 `none` 的元素，压根不会出现在 `render tree` 中；

## 4.4 布局 (layout) 和绘制 (Paint)

- 第四步是：在渲染树（Render Tree）上运行**布局（Layout）** 来计算每个节点的几何体。
    - 渲染树会表示显示哪些节点以及其他样式，但是不表示每个节点的尺寸、位置等信息；
    - 布局是确定呈现树中所有节点的宽度、高度和位置信息；
- 第五步是：将每个节点绘制（Paint）到屏幕上。
    - 在绘制阶段，浏览器将布局阶段计算的每个 frame 转为屏幕上实际的像素点；
    - 包括将元素的可见部分进行绘制，比如文本、颜色、边框、阴影、替换元素（比如 img）

![[Pasted image 20241119233236.png]]

# 5. 重绘和回流解析

## 5.1 重绘（Repaint）

- 第一次渲染内容称之为绘制（paint）
  
    - 之后重新渲染称之为重绘
- 重绘不会带来重新布局，所以并不一定伴随重排。
  
    - 浏览器会根据元素的新属性重新绘制，使元素呈现新的外观
- 什么属性会导致重绘呢？
  
    - `color background box-shadow..` (比如修改背景色、文字颜色、边框颜色、样式等)

## 5.2 回流/重排（reflow）

理解回流 `reflow` ：也可以称之为**重排**

- 第一次确定节点的大小和位置，称之为布局（layout）
  
    - 之后对节点的大小、位置修改重新计算称之为回流
- "重排/回流"必然导致"重绘"
  
    - 比如改变一个网页元素的位置，就会同时触发"重排"和"重绘"，因为布局改变了
    - 所以**回流是一件很消耗性能的事情**
- 什么属性会导致回流呢？
  
    - `width top position..` （比如 DOM 结构发生改变 / 修改了布局）

## 5.3 常见的触发"回流/重排"操作

- `Reflow(回流)` 的成本比 `Repaint(重绘)` 的成本高得多的多。
- 所以在开发中要尽量避免发生回流：
    1. 修改样式时尽量一次性修改
       
        - 将多次**改变样式属性的操作合并成一次操作**
        - 预先定义好 class，然后修改 DOM 的 className
    2. 尽量避免频繁的操作 `DOM`
       
        - 我们可以在一个 `DocumentFragment` 或者父元素中将要操作的 `DOM` 操作完成，再一次性的操作；
    3. 尽量避免通过 `getComputedStyle` 获取尺寸、位置等信息；
       
    4. 对某些元素使用 `position` 的 `absolute` 或者 `fixed`
       
        - 并不是不会引起回流，而是开销相对较小，不会对其他元素造成影响。

## 5.4 合成和性能优化

- 绘制的过程，可以将布局后的元素绘制到多个合成图层中
    - 这是浏览器的一种优化手段
- 默认情况下，标准流中的内容都是被绘制在同一个图层（Layer）中的
- 而一些特殊的属性，会创建一个新的合成层（ CompositingLayer ），并且新的图层可以利用 GPU 来加速绘制
    - 因为**每个合成层都是单独渲染**的
- 那么哪些属性可以形成新的合成层呢? 常见的一些属性:
    - 3D transforms
    - video、 canvas、 iframe
    - opacity 动画转换时
    - position: fixed
    - will-change：一个实验性的属性，提前告诉浏览器元素可能发生哪些变化
    - animation 或 transition 设置了 opacity、 transform
- 分层确实可以提高性能，但是它以内存管理为代价，因此不应作为 web 性能优化策略的一部分过度使用

![[Pasted image 20241119233249.png]]

## 5.5 script 元素和页面解析的关系

- 我们现在已经知道了页面的渲染过程，但是 `JavaScript` 在哪里呢？
    - 事实上，浏览器在解析 `HTML` 的过程中，遇到了 `script` 元素是不能继续构建 `DOM` 树的；
    - 它会停止继续构建，首先下载 `JavaScript` 代码，并且执行 `JavaScript` 的脚本；
    - 只有等到 `JavaScript` 脚本执行结束后，才会继续解析 `HTML`，构建 `DOM` 树；
- 为什么要这样做呢？
    - 这是因为 `JavaScript` 的作用之一就是操作 `DOM`，并且可以修改 `DOM`；
    - 如果我们等到 `DOM` 树构建完成并且渲染再执行 `JavaScript`，会造成严重的回流和重绘，影响页面的性能；
    - 所以会在遇到 `script` 元素时，优先下载和执行 `JavaScript` 代码，再继续构建 `DOM` 树；
- 但是这个也往往会带来新的问题，特别是现代页面开发中：
    - 在目前的开发模式中（比如 `Vue`、 `React`），脚本往往比 `HTML` 页面更“重”，处理时间需要更长；
    - 所以会造成页面的解析阻塞，在脚本下载、执行完成之前，用户在界面上什么都看不到；
- 为了解决这个问题， `script` 元素给我们提供了两个属性（`attribute`）： `defer` 和 `async`。

# 6. defer 和 async 属性

## 6.1 defer 属性

- `defer` 属性：告诉浏览器**不要等待脚本下载**，而**继续解析 HTML**，**构建 DOM Tree**。
    - 脚本会由浏览器来进行下载，但是不会阻塞 `DOM Tree` 的构建过程；
    - 如果脚本提前下载好了，它会等待 `DOM Tree` 构建完成，在 `DOMContentLoaded` 事件之前先执行 `defer` 中的代码；
- **所以 DOMContentLoaded 总是会等待 defer 中的代码先执行完成**。

![[Pasted image 20241119233300.png]]

- 另外多个带 `defer` 的脚本是可以保持正确的顺序执行的。
    - 从某种角度来说， `defer` 可以提高页面的性能，并且推荐放到 `head` 元素中；
    - 注意： `defer` 仅适用于外部脚本，对于 `script` 默认内容会被忽略。

## 6.2 async 属性

- `sync` 特性与 `defer` 有些类似，**它也能够让脚本不阻塞页面**。
- **async 是让一个脚本完全独立的：**
    - 浏览器不会因 `async` 脚本而阻塞（与 `defer` 类似）；
    - `async` 脚本不能保证顺序，它是独立下载、独立运行，不会等待其他脚本；
    - **async 不会能保证在 DOMContentLoaded 之前或者之后执行**

![[Pasted image 20241119233312.png]]

- `defer` 通常用于需要在文档解析后操作 DOM 的 JavaScript 代码，并且对多个 script 文件有顺序要求的；
- `async` 通常用于独立的脚本，对其他脚本，甚至 DOM 没有依赖的；