---
title: 深入理解浏览器渲染
aliases:
  - 深入理解浏览器渲染
original: https://www.51cto.com/article/717431.html
---
# 图解浏览器渲染原理及流程

作者：GUOZE2022-08-30 09:01:11


我们打包出来的 HTML、CSS、JavaScript 等文件，经过浏览器运行之后就会显示出页面，这个过程就是浏览器的渲染进程来操作实现的，渲染进程的主要任务就是将静态资源转化为可视化界面。

大家好，我是 CUGGZ。

今天来分享一下浏览器的渲染原理及流程。

## 前言

先来看看 Chrome 浏览器的多进程架构：

![图片](https://s8.51cto.com/oss/202208/30/481f13621017872b31d062ee5f6dccaf6ec94f.png "图片")

通常，我们打包出来的 HTML、CSS、JavaScript 等文件，经过浏览器运行之后就会显示出页面，这个过程就是浏览器的渲染进程来操作实现的，渲染进程的主要任务就是将静态资源转化为可视化界面：

![图片](https://s2.51cto.com/oss/202208/30/9721fe44347407e8cc9865cfd54a41217b85d8.png "图片")

对于中间的浏览器，它就是一个黑盒，下面就来看看这个黑盒是如何将静态资源转化为前端界面的。由于渲染机制比较复杂，所以渲染模块在执行过程中会被划分为很多子阶段，输入的静态资源经过这些子阶段，最后输出页面。我们将一个处理流程称为渲染流水线，其大致流程如下图所示：

![图片](https://s4.51cto.com/oss/202208/30/6969b9e80b155a87bf02856005e18123f9126b.png "图片")

这里主要包含五个过程：

1. **DOM （文档对象模型）树构建**：渲染引擎使用HTML解析器（调用XML解析器）解析HTML文档，将各个HTML元素逐个转化成 DOM 节点，从而生成 DOM 树。
2. **CSSOM （CSS 对象模型）树构建**：CSS 解析器解析 CSS，并将其转化为 CSS 对象，将这些 CSS 对象组装起来，构建 CSSOM 树。
3. **渲染树构建**：DOM 树和 CSSOM 树都构建完成以后，浏览器会根据这两棵树构建出一棵渲染树。
4. **页面布局**：渲染树构建完毕之后，元素的位置关系以及需要应用的样式就确定了，这时浏览器会计算出所有元素的大小和绝对位置。
5. **页面绘制**：页面布局完成之后，浏览器会将根据处理出来的结果，把每一个页面图层转换为像素，并对所有的媒体文件进行解码。

对于这五个流程，每一阶段都有对应的产物：DOM 树、CSSOM 树、渲染树、盒模型、界面。

下图为渲染引擎工作流程中各个步骤所对应的模块：

![图片](https://s7.51cto.com/oss/202208/30/4207a7a493a3e2960c8238f76acb1d2f38ea0e.png "图片")

从图中可以看出，渲染引擎主要包含的模块有：

- **HTML 解析器**：解析HTML文档，主要作用是将HTML文档转换成DOM树。
- **CSS 解析器**：将DOM中的各个元素对象进行计算，获取样式信息，用于渲染树的构建。
- **JavaScript 解释器**：使用JavaScript可以修改网页的内容、CSS规则等。JavaScript解释器能够解释JavaScript代码，并通过DOM接口和CSSOM接口来修改网页内容、样式规则，从而改变渲染结果。
- **页面布局**：DOM创建之后，渲染引擎将其中的元素对象与样式规则进行结合，可以得到渲染树。布局则是针对渲染树，计算其各个元素的大小、位置等布局信息。
- **页面绘制**：使用图形库将布局计算后的渲染树绘制成可视化的图像结果。

## DOM树构建

在说构建DOM树之前，我们需要知道，为什么要构建 DOM 树呢？ 这是因为，浏览器无法直接理解和使用 HTML，所以需要将HTML转化为浏览器能够理解的结构——DOM树。

了解过数据结构的小伙伴对于树结构应该不陌生，树是由结点或顶点和边组成的且不存在着任何环的一种数据结构。一棵非空的树包括一个根结点，还有多个附加结点，所有结点构成一个多级分层结构。下面通过一张图来看看什么是树结构：

![图片](https://s8.51cto.com/oss/202208/30/a45e8e058a80037f2c736575d51aca60fe1c3d.png "图片")

对于上面的三个结构，前两个都是树，他们都只有唯一的根节点，而且不存在环结构。而第三个存在环，所以就不是一个树结构。

在页面中，每个HTML标签都会被浏览器解析成文档对象。HTML 本质上就是一个嵌套结构，在解析时会把每个文档对象用一个树形结构组织起来，所有的文档对象都会挂在document上，这种组织方式就是HTML最基础的结构——文档对象模型（DOM），这棵树的每个文档对象就叫做 DOM 节点。

在渲染引擎中，DOM 有三个层面的作用：

- 从页面的视角来看，DOM 是生成页面的基础数据结构。
- 从 JavaScript 脚本视角来看，DOM 提供给 JavaScript 脚本操作的接口，通过这套接口，JavaScript 可以对 DOM 结构进行访问，从而改变文档的结构、样式和内容。
- 从安全视角来看，DOM 是一道安全防护线，一些不安全的内容在 DOM 解析阶段会被拒之门外。

在渲染引擎内部，HTML 解析器负责将 HTML 字节流转换为 DOM 结构，其转化过程如下：

![图片](https://s3.51cto.com/oss/202208/30/93a376b25d55fdd1a219384b8f8e302cc9a8f6.png "图片")

### 1、字符流 → 词（token）

HTML结构会首先通过分词器将字节流拆分为词（token）。Token分为Tag Token 和文本 Token。下面来看一个HTML代码是如何被拆分的：

复制

```html
<body>
    <div>
        <p>hello world</p>
    </div>
</body>
```

对于这段代码，可以拆成词：

![图片](https://s2.51cto.com/oss/202208/30/a9e082e976cce78b64243209aa1f476d768256.png "图片")

可以看到，Tag Token 又分 StartTag 和 EndTag，`<body>`、`<div>`、`<p>` ​就是 `StartTag` ，`</body>`、`</div>`、`</p>` 就是 `EndTag`，分别对应图中的蓝色和红色块，文本 Token 对应绿色块。

这里会通过状态机将字符拆分成token，所谓的状态机就是将每个词的特征逐个拆分成独立的状态，然后再将所有词的特征字符合并起来，形成一个连通的图结构。那为什么要使用状态机呢？因为每读取一个字符，都要做一次决策，这些决策都和当前的状态有关。

实际上，状态机的作用就是用来做词法分析的，将字符流分解为词（token）。

### 2、词（token）→ DOM树

接下来就需要将 Token 解析为 DOM 节点，并将 DOM 节点添加到 DOM 树中。这个过程是通过**栈结构**来实现的，这个栈主要用来计算节点之间的父子关系，上面步骤中生成的token会按顺序压入栈中，该过程的规则如下：

- 如果分词器解析出来是 **StartTag Token**，HTML 解析器会为该 Token 创建一个 DOM 节点，然后将该节点加入到 DOM 树中，它的父节点就是栈中相邻的那个元素生成的节点。
- 如果分词器解析出来是**文本Token**，那么会生成一个文本节点，然后将该节点加入到 DOM 树中，文本 Token 是不需要压入到栈中，它的父节点就是当前栈顶 Token 所对应的 DOM 节点。
- 如果分词器解析出来的是**EndTag Token**，比如是 EndTag div，HTML 解析器会查看 Token 栈顶的元素是否是 StarTag div，如果是，就将 StartTag div从栈中弹出，表示该 div 元素解析完成。

通过分词器产生的新 Token 就这样不停地入栈和出栈，整个解析过程就这样一直持续下去，直到分词器将所有字节流分词完成。

下面来看看这的Token栈是如何工作的，有如下HTML结构：

```html
<html>
    <body>
        <div>hello juejin</div>
        <p>hello world</p>
    </body>
</html>
```

开始时，HTML解析器会创建一个根为 document 的空的 DOM 结构，同时将 StartTag document 的Token压入栈中，然后再将解析出来的第一个 StartTag html 压入栈中，并创建一个 html 的DOM节点，添加到 document 上，这时 Token 栈和 DOM树 如下：

![图片](https://s9.51cto.com/oss/202208/30/682db1a968009f663d487316a4eab905d14ed8.png "图片")

接下来 `body` 和 `div` 标签也会和上面的过程一样，进行入栈操作：

![图片](https://s2.51cto.com/oss/202208/30/16a36a119055ff5af45744969caf730c0c1888.png "图片")

随后就会解析到 `div` 标签中的文本 `Token`，渲染引擎会为该 `Token` 创建一个文本节点，并将该 `Token` 添加到 `DOM` 中，它的父节点就是当前 `Token` 栈顶元素对应的节点：

![图片](https://s3.51cto.com/oss/202208/30/d54799531d0dde48ed0141ba1069d7800592ff.png "图片")

接下来就是第一个 `EndTag div`，这时 HTML 解析器会判断当前栈顶元素是否是 `StartTag div`，如果是，则从栈顶弹出 `StartTag div`，如下图所示：

![图片](https://s7.51cto.com/oss/202208/30/f6b97f252c30e158a3071023df009dba8d0b52.png "图片")

再之后的过程就和上面类似了，最终的结果如下：

![图片](https://s9.51cto.com/oss/202208/30/e137b13562b8f731574374dea1a19302391b11.png "图片")

## CSSOM 树构建

上面已经基本了解了 DOM 的构建过程，但是这个 DOM 结构只包含节点，并不包含任何的样式信息。下面就来看看，浏览器是如何把 CSS 样式应用到 DOM 节点上的。

同样，浏览器也是无法直接理解 CSS 代码的，需要将其浏览器可以理解的 CSSOM 树。实际上。浏览器在构建 DOM 树的同时，如果样式也加载完成了，那么 CSSOM 树也会同步构建。CSSOM 树和 DOM 树类似，它主要有两个作用：

- 提供给 JavaScript 操作样式的能力。
- 为渲染树的合成提供基础的样式信息。

不过，CSSOM 树和 DOM 树是独立的两个数据结构，它们并没有一一对应关系。DOM 树描述的是 HTML 标签的层级关系，CSSOM 树描述的是选择器之间的层级关系。可以在浏览器的控制台，通过document.styleSheets命令来查看CSSOM树：

![图片](https://s8.51cto.com/oss/202208/30/41af69187d099705ab628477252d938de81c90.jpg "图片")

那CSS样式的来源有哪些呢？

![图片](https://s8.51cto.com/oss/202208/30/a18061a810abfec544b712b918a72eedebbfe6.png "图片")

CSS样式的来源主要有三种：

- 通过 link 引用的外部 CSS 样式文件。
- <style>标签内的CSS样式。
- 元素的style属性内嵌的CSS。

在将CSS转化为树形对象之前，还需要将样式表中的属性值进行标准化处理，比如，当遇到以下CSS样式：

复制

```
body { font-size: 2em }
p {color:blue;}
div {font-weight: bold}
div p {color:green;}
div {color:red; }
```

可以看到上面CSS中有很多属性值，比如2em、blue、red、bold等，这些数值并不能被浏览器直接理解。所以，需要将所有值转化为浏览器渲染引擎容易理解的、标准化的计算值，这个过程就是属性值标准化。经过标准化的过程，上面的代码会变成这样：

复制

```
body { font-size: 32px }
p {color: rgb(0, 0, 255);}
div {font-weight: 700}
div p {color: (0, 128, 0);}
div {color: (255, 0, 0); }
```

可以看到，2em被解析成了32px，blue被解析成了rgb(255, 0, 0)，bold被解析成700。现在样式的属性已被标准化了，接下来就需要计算 DOM 树中每个节点的样式属性了，这就涉及到 CSS 的继承规则和层叠规则。

#### （1）样式继承

在 CSS 中存在样式的继承机制，CSS 继承就是每个 DOM 节点都包含有父节点的样式。比如在 HTML 上设置“font-size:20px;”，那么页面里基本所有的标签都可以继承到这个属性了。

在CSS中，有继承性的属性主要有以下几种：

1. **字体系列属性**

- font-family：字体系列。
- font-weight：字体的粗细。
- font-size：字体的大小。
- font-style：字体的风格。

2. **文本系列属性**

- text-indent：文本缩进。
- text-align：文本水平对齐。
- line-height：行高。
- word-spacing：单词之间的间距。
- letter-spacing：中文或者字母之间的间距。
- text-transform：控制文本大小写（就是uppercase、lowercase、capitalize这三个）。
- color：文本颜色。

3. **元素可见性**

- visibility：控制元素显示隐藏。

4. **列表布局属性**

- list-style：列表风格，包括list-style-type、list-style-image等。

5. **光标属性**

- cursor：光标显示为何种形态。

#### （2）样式层叠

样式计算过程中的第二个规则是样式层叠。层叠是 CSS 的一个基本特征，它是一个定义了 如何合并来自多个源的属性值的算法。它在 CSS 处于核心地位，CSS 的全称“层叠样式表”正是强调了这一点。这里不再多说。

总之，样式计算阶段的目的是为了计算出 DOM 节点中每个元素的具体样式，在计算过程 中需要遵守 CSS 的继承和层叠两个规则。这个阶段最终输出的内容是每个 DOM 节点的样 式，并被保存在 ComputedStyle 的结构内。

对于以下代码：

复制

```
<html>
 <head>
  <link href="./style.css">
        <style>
            .juejin {
                width: 100px;
                height: 50px;
                background: red;
            }

            .content {
                font-size: 25px;
                line-height: 25px;
                margin: 10px;
            }
        </style>
 </head>
    <body>
        <div class="juejin">
         <div>CUGGZ</div>
        </div>
        <p style="color: blue" class="content">
            <span>hello world</span>
            <p style="display: none;">浏览器</p>
        </p>
    </body>
</html>
```

最终生成的CSSOM树大致如下：

![图片](https://s4.51cto.com/oss/202208/30/a98caa8912a73abefba952780e25ccc23d1cf7.png "图片")

## 渲染树构建

在 DOM 树和 CSSOM 树都渲染完成之后，就会进入渲染树的构建阶段。渲染树就是 DOM 树和 CSSOM 树的结合，会得到一个可以知道每个节点会应用什么样式的数据结构。这个结合的过程就是遍历整个 DOM 树，然后在 CSSOM 树里查询到匹配的样式。

在不同浏览器里，构建渲染树的过程不太一样：

- 在 Chrome 里会在每个节点上使用 attach() 方法，把 CSSOM 树的节点挂在 DOM 树上作为渲染树。
- 在 Firefox 里会单独构造一个新的结构， 用来连接 DOM 树和 CSSOM 树的映射关系。

那为什么要构建渲染树呢？在上面的示例中可以看到，DOM树可能包含一些不可见的元素，比如head标签，使用display:none;属性的元素等。所以在显示页面之前，还要额外地构建一棵只包含可见元素的渲染树。

下面来看看构建渲染树的过程：

![图片](https://s4.51cto.com/oss/202208/30/5303c800772f4c99fb71884dac29cbdb78b1d4.png "图片")

可以看到，DOM树中不可见的节点都没有包含到渲染树中。为了构建渲染树，浏览器上大致做了如下工作：遍历DOM树中所有可见节点，并把这些节点加到布局中，而不可见的节点会被布局树忽略掉，如 head 标签下面的全部内容，再比如 p.p 这个元素，因为它的属性包含 dispaly:none​，所以这个元素也没有被包含进渲染树中。如果给元素设置了visibility: hidden属性，那这个元素会出现在渲染树中，因为具有这个样式的元素是需要占位的，只不过不需要显示出来。

这里在查找的过程中，出于效率的考虑，会从 CSSOM 树的叶子节点开始查找，对应在 CSS 选择器上也就是从选择器的最右侧向左查找。所以，不建议使用标签选择器和通配符选择器来定义元素样式。

除此之外，同一个 DOM 节点可能会匹配到多个 CSSOM 节点，而最终的效果由哪个 CSS 规则来确定，就是样式优先级的问题了。当一个 DOM 元素受到多条样式控制时，样式的优先级顺序如下：内联样式 > ID选择器 > 类选择器 > 标签选择器 > 通用选择器 > 继承样式 > 浏览器默认样式​。

CSS常见选择器的优先级如下：

|   |   |   |
|---|---|---|
|**选择器**|**格式**|**优先级权重**|
|id选择器|#id|100|
|类选择器|.classname|10|
|属性选择器|a[ref=“eee”]|10|
|伪类选择器|li:last-child|10|
|标签选择器|div|1|
|伪元素选择器|li:after|1|
|相邻兄弟选择器|h1+p||
|子选择器|ul>li||
|后代选择器|li a||
|通配符选择器|*||

对于选择器的优先级：

- 标签选择器、伪元素选择器：1。
- 类选择器、伪类选择器、属性选择器：10。
- id 选择器：100。
- 内联样式：1000。

#### 注意：

- !important声明的样式的优先级最高。
- 如果优先级相同，则最后出现的样式生效。
- 继承得到的样式的优先级最低。

## 页面布局

经过上面的步骤，就生成了一棵渲染树，这棵树就是展示页面的关键。到现在为止，已经有了需要渲染的所有节点之间的结构关系及其样式信息。下面就需要进行页面的布局。

通过计算渲染树上每个节点的样式，就能得出来每个元素所占空间的大小和位置。当有了所有元素的大小和位置后，就可以在浏览器的页面区域里去绘制元素的边框了。这个过程就是布局。这个过程中，浏览器对渲染树进行遍历，将元素间嵌套关系以盒模型的形式写入文档流：

![图片](https://s5.51cto.com/oss/202208/30/62290dd140cbcab669c542ab61d67e86cc8dc2.png "图片")

盒模型在布局过程中会计算出元素确切的大小和定位。计算完毕后，相应的信息被写回渲染树上，就形成了布局渲染树。同时，每一个元素盒子也都携带着自身的样式信息，作为后续绘制的依据。

## 页面绘制

### 1、构建图层

经过布局，每个元素的位置和大小就有了，那下面是不是就该开始绘制页面了？答案是否定的，因为页面上可能有很多复杂的场景，比如3D变化、页面滚动、使用z-index进行z轴的排序等。所以，为了实现这些效果，渲染引擎还需要为特定的节点生成专用的图层，并生成一棵对应的图层树。

那什么是图层呢？我们可以在Chrome浏览器的开发者工具中，选择Layers标签（如果没有，可以在更多工具中查找），就可以看到页面的分层情况，以掘金首页为例，其分层情况如下：

![图片](https://s7.51cto.com/oss/202208/30/29953091476285611df139b64d2566f8437010.png "图片")

可以看到，渲染引擎给页面分了很多图层，这些图层会按照一定顺序叠加在一起，就形成了最终的页面。这里，将页面分解成多个图层的操作就成为分层， 最后将这些图层合并到一层的操作就成为合成， 分层和合成通常是一起使用的。Chrome 引入了分层和合成的机制就是为了提升每帧的渲染效率。

通常情况下，并不是渲染树上的每个节点都包含一个图层，如果一个节点没有对应的图层，那这个节点就会属于其父节点的图层。那什么样的节点才能让浏览器引擎为其创建一个新的图层呢？需要满足以下其中一个条件：

#### （1）拥有层叠上下文属性的元素

我们看到的页面通常是二维的平面，而层叠上下文能够让页面具有三维的概念。这些 HTML 元素按照自身属性的优先级分布在垂直于这个二维平面的 z 轴上。下面是盒模型的层叠规则：

![图片](https://s8.51cto.com/oss/202208/30/d2d00a679a77fe9b465488f26f9f753673e245.png "图片")

对于上图，由上到下分别是：

- 背景和边框：建立当前层叠上下文元素的背景和边框。
- 负的z-index：当前层叠上下文中，z-index属性值为负的元素。
- 块级盒：文档流内非行内级非定位后代元素。
- 浮动盒：非定位浮动元素。
- 行内盒：文档流内行内级非定位后代元素。
- z-index:0：层叠级数为0的定位元素。
- 正z-index：z-index属性值为正的定位元素。

**注意:** 当定位元素z-index:auto，生成盒在当前层叠上下文中的层级为 0，不会建立新的层叠上下文，除非是根元素。

#### （2）需要裁剪的元素

什么是裁剪呢？假如有一个固定宽高的div盒子，而里面的文字较多超过了盒子的高度，这时就会产生裁剪，浏览器渲染引擎会把裁剪文字内容的一部分用于显示在 div 区域。当出现裁剪时，浏览器的渲染引擎就会为文字部分单独创建一个图层，如果出现滚动条，那么滚动条也会被提升为单独的图层。

### 2、绘制图层

在完成图层树的构建之后，渲染引擎会对图层树中的每个图层进行绘制，下面就来看看渲染引擎是怎么实现图层绘制的。

渲染引擎在绘制图层时，会把一个图层的绘制分成很多绘制指令，然后把这些指令按照顺序组成一个待绘制的列表：

![图片](https://s2.51cto.com/oss/202208/30/07122a630a92f608a18976fe85ead42992f2ef.png "图片")

可以看到，绘制列表中的指令就是一系列的绘制操作。通常情况下，绘制一个元素需要执行多条绘制指令，因为每个元素的背景、边框等属性都需要单独的指令进行绘制。所以在图层绘制阶段，输出的内容就是绘制列表。

在Chrome浏览器的开发者工具中，通过Layer标签可以看到图层的绘制列表和绘制过程：

![图片](https://s3.51cto.com/oss/202208/30/8133354925490396ad046434ec865e4fe9ecdd.png "图片")

绘制列表只是用来记录绘制顺序和绘制指令的列表，而绘制操作是由渲染引擎中的合成线程来完成的。当图层绘制列表准备好之后，主线程会把该绘制列表提交给合成线程。

注意：合成操作是在合成线程上完成的，所以，在执行合成操作时并不会影响到主线程的执行。

很多情况下，图层可能很大，比如一篇长文章，需要滚动很久才能到底，但是用户只能看到视口的内容，所以没必要把整个图层都绘制出来。因此，合成线程会将图层划分为图块，这些图块的大小通常是 256x256 或者 512x512。合成线程会优先将视口附近的图块生成位图。实际生成位图的操作是在光栅化阶段来执行的，所谓的光栅化就是按照绘制列表中的指令生成图片。​

当所有的图块都被光栅化之后，合成线程就会生成一个绘制图块的命令，浏览器相关进程收到这个指令之后，就会将其页面内容绘制在内存中，最后将内存显示在屏幕上，这样就完成了页面的绘制。

至此，整个渲染流程就完成了，其过程总结如下：

1. 将HTML内容构建成DOM树。
2. 将CSS内容构建成CSSOM树。
3. 将DOM 树和 CSSOM 树合成渲染树。
4. 根据渲染树进行页面元素的布局。
5. 对渲染树进行分层操作，并生成分层树。
6. 为每个图层生成绘制列表，并提交到合成线程。
7. 合成线程将图层分成不同的图块，并通过栅格化将图块转化为位图。
8. 合成线程给浏览器进程发送绘制图块指令。
9. 浏览器进程会生成页面，并显示在屏幕上。

## 扩展

### 1、重排和重绘

说完浏览器引擎的渲染流程，再来看两个重要的概念：重排（Reflow）和重绘（Repaint）。

我们知道，渲染树是动态构建的，所以，DOM节点和CSS节点的改动都可能会造成渲染树的重新构建。渲染树的改动就会造成页面的重排或者重绘。下面就来看看这两个概念，以及它们触发的条件和减少触发的操作。

#### （1）重排

当我们的操作引发了 DOM 树中几何尺寸的变化（改变元素的大小、位置、布局方式等），这时渲染树里有改动的节点和它影响的节点都要重新计算。这个过程就叫做重排，也称为回流。在改动发生时，要重新经历页面渲染的整个流程，所以开销是很大的。

以下操作都会导致页面重排：

- 页面首次渲染。
- 浏览器窗口大小发生变化。
- 元素的内容发生变化。
- 元素的尺寸或者位置发生变化。
- 元素的字体大小发生变化。
- 激活CSS伪类。
- 查询某些属性或者调用某些方法。
- 添加或者删除可见的DOM元素。

在触发重排时，由于浏览器渲染页面是基于流式布局的，所以当触发回流时，会导致周围的DOM元素重新排列，它的影响范围有两种：

- 全局范围：从根节点开始，对整个渲染树进行重新布局。
- 局部范围：对渲染树的某部分或者一个渲染对象进行重新布局。

#### （2）重绘

当对 DOM 的修改导致了样式的变化、但未影响其几何属性（比如修改颜色、背景色）时，浏览器不需重新计算元素的几何属性、直接为该元素绘制新的样式（会跳过重排环节），这个过程叫做重绘。简单来说，重绘是由对元素绘制属性的修改引发的。

当我们修改元素绘制属性时，页面布局阶段不会执行，因为并没有引起几何位置的变换，所以就直接进入了绘制阶段，然后执行之后的一系列子阶段。相较于重排操作，重绘省去了布局和分层阶段，所以执行效率会比重排操作要高一些。

下面这些属性会导致回流：

- color、background 相关属性：background-color、background-image 等。
- outline 相关属性：outline-color、outline-width 、text-decoration。
- border-radius、visibility、box-shadow。

**注意：**当触发重排时，一定会触发重绘，但是重绘不一定会引发重排。

相对来说，重排操作的消耗会比较大，所以在操作中尽量少的造成页面的重排。为了减少重排，可以通过以下方式进行优化：

- 在条件允许的情况下尽量使用 CSS3 动画，它可以调用 GPU 执行渲染。
- 操作DOM时，尽量在低层级的DOM节点进行操作。
- 不要使用table​布局， 一个小的改动可能会使整个table进行重新布局。
- 使用CSS的表达式。
- 不要频繁操作元素的样式，对于静态页面，可以修改类名，而不是样式。
- 使用 absolute 或者 fixed，使元素脱离文档流，这样他们发生变化就不会影响其他元素。
- 避免频繁操作DOM，可以创建一个文档片段documentFragment，在它上面应用所有DOM操作，最后再把它添加到文档中。
- 将元素先设置display: none，操作结束后再把它显示出来。因为在display属性为none的元素上进行的DOM操作不会引发回流和重绘。
- 将DOM的多个读操作（或者写操作）放在一起，而不是读写操作穿插着写。这得益于浏览器的渲染队列机制。

浏览器针对页面的回流与重绘，进行了自身的优化——渲染队列， 浏览器会将所有的回流、重绘的操作放在一个队列中，当队列中的操作到了一定的数量或者到了一定的时间间隔，浏览器就会对队列进行批处理。这样就会让多次的回流、重绘变成一次回流重绘。

### 2、JavaScript 对 DOM 的影响

当解析器解析HTML时，如果遇到了script标签，判断这是脚本，就会暂停 DOM 的解析，因为接下来的 JavaScript 脚本可能会修改当前已经生成的 DOM 结构。

来看一段代码：

复制

```
<html>
    <body>
        <div>hello juejin</div>
        <script>
            document.getElementsByTagName('div')[0].innerText = 'juejin yyds'
        </script>
        <p>hello world</p>
    </body>
</html>
```

这里，当解析完div标签后，就会解析script标签，这时的DOM结构如下：

![图片](https://s5.51cto.com/oss/202208/30/2517a8085381b47911e5947288b9b2c3aa5230.png "图片")

这时，HTML解析器就会暂停工作，JavaScript引擎就会开始工作，并执行script标签中的脚本内容。由于这段脚本修改了第一个div的内容，所以执行完这个脚本之后，div中的文本就变成了“juejin yyds”，当脚本执行完成之后，HTML解析器就会恢复解析过程，继续解析后面的内容，直至生成最终的DOM。

上面我们说的JavaScript脚本是通过script标签直接嵌入到HTML中的。当在页面中引入JavaScript脚本时，情况就会变得复杂。比如：

复制

```
<html>
    <body>
        <div>hello juejin</div>
        <script type="text/javascript" src='./index.js'></script>
        <p>hello world</p>
    </body>
</html>
```

其实这里的执行流程和上面时一样的，当遇到script标签时，HTML解析器都会暂停解析并去执行脚本文件。不过这里执行 JavaScript 脚本时，需要先下载脚本。脚本的下载过程会阻塞 DOM 的解析，而通常下载又是非常耗时的，会受到网络环境、JavaScript 脚本文件大小等因素的影响。

经过上面的分析可知，JavaScript 线程会阻塞 DOM 的解析，我们可以通过CDN、压缩脚本等方式来加速 JavaScript 脚本的加载。如果脚本文件中没有操作DOM的相关代码，就可以将JavaScript脚本设置为异步加载，可以给script标签添加 async 或 defer 属性来实现脚本的异步加载。两者的使用方式如下：

复制

```
<script async type="text/javascript" src='./index.js'></script>
<script defer type="text/javascript" src='./index.js'></script>
```

下图可以直观的看出异步加载和直接加载的区别:

![图片](https://s5.51cto.com/oss/202208/30/d8a426942a6870f423f059d335c1c73480a4b9.png "图片")

其中蓝色代表脚本下载，红色代表脚本执行，绿色代表HTML解析，灰色表示HTML解析暂停。

> 当初始HTML文档已完全加载和解析时，将触发DOMContentLoaded事件，而不需要等待样式表，图像和子框架页面加载。该事件可以用来检测HTML页面是否完全加载完毕。

defer 和 async属性都是去异步加载外部的JS脚本文件，它们都不会阻塞页面的解析，其区别如下：

- **执行顺序：**多个带async属性的标签，不能保证加载的顺序；多个带defer属性的标签，按照加载顺序执行。
- **脚本是否并行执行：**async属性，表示**后续文档的加载和执行与js脚本的加载和执行是并行进行的**，即异步执行；defer属性，加载后续文档的过程和js脚本的加载(此时仅加载不执行)是并行进行的(异步)，JavaScript 脚本需要等到文档所有元素解析完成之后才执行，DOMContentLoaded事件触发执行之前。

再来看另外一种情况：

复制

```
<html>
    <head>
   <style src='./style.css'></style>
    </head>
    <body>
        <div>hello juejin</div>
        <script>
            const ele = document.getElementsByTagName('div')[0];
            ele.innerText = 'juejin yyds';    // 操作DOM
            ele.style.color = 'skyblue';      // 操作CSSOM
        </script>
        <p>hello world</p>
    </body>
</html>
```

上面的代码中，第9行是操作DOM的，而第10行是操作CSSOM的，所以在执行 JavaScript 脚本之前，还需要先解析 JavaScript 语句之上所有的 CSS 样式。所以如果代码里引用了外部的 CSS 文件，那么在执行 JavaScript 之前，还需要 等待外部的 CSS 文件下载完成，并解析生成 CSSOM 对象之后，才能执行 JavaScript 脚本。而 JavaScript 引擎在解析 JavaScript 之前，是不知道 JavaScript 是否操纵了 CSSOM 的，所以渲染引擎在遇到 JavaScript 脚本时，不管该脚本是否操纵了 CSSOM，都会执行 CSS 文件下载，解析操作，再执行 JavaScript 脚本。

所以，JavaScript 会阻塞 DOM 生成，而样式文件又会阻塞 JavaScript 的执行，我们在开发时需要格外注意这一点。

最后再来看一种情况，示例代码如下：

复制

```
<html>
    <head>
        <style src='./style.css'></style>
    </head>
    <body>
        <div>hello juejin</div>
        <script type="text/javascript" src='./index.js'></script>
        <p>hello world</p>
    </body>
</html>
```

这段HTML代码中包含了CSS外部引用和JavaScript外部文件，在接收到 HTML 数据之后的预解析过程中，HTML 预解析器识别出来了有 CSS 文件和 JavaScript 文件需要下载，就会同时发起两个文件的下载请求。

责任编辑：姜华来源： [前端充电宝](https://mp.weixin.qq.com/s/9GMk0kFTHyTW_UrL0svNpQ)

[浏览器渲染](https://so.51cto.com/?keywords=%E6%B5%8F%E8%A7%88%E5%99%A8%E6%B8%B2%E6%9F%93)[前端](https://so.51cto.com/?keywords=%E5%89%8D%E7%AB%AF)

![](https://s5-media.51cto.com/cms/client/img/zanpc.bd208a1.png)

![](https://s5-media.51cto.com/cms/client/img/weixin.23cd8b3.png)分享到微信

![](https://s5-media.51cto.com/cms/client/img/weibo.16d6b4f.png)分享到微博

相关推荐

[![](https://s4.51cto.com/oss/202011/06/ce62932046665495581a3cf51b66dcec.png?x-oss-process=image/resize,m_fixed,w_142,h_82)](https://www.51cto.com/article/631121.html)

[_浏览器__渲染__原理_](https://www.51cto.com/article/631121.html)

[本文从浏览器角度来告诉你，URL后输入后按回车，浏览器内部究竟发生了什么。](https://www.51cto.com/article/631121.html)

2020-11-06 15:20:45

[浏览器](https://so.51cto.com/?keywords=%E6%B5%8F%E8%A7%88%E5%99%A8)[前端](https://so.51cto.com/?keywords=%E5%89%8D%E7%AB%AF)[架构](https://so.51cto.com/?keywords=%E6%9E%B6%E6%9E%84)

[_浏览器_的_渲染__原理_简介](https://www.51cto.com/article/398315.html)

[看到这个标题大家一定会想到这篇神文《HowBrowsersWork》，这篇文章把浏览器的很多细节讲得很细，而且也被翻译成了中文。](https://www.51cto.com/article/398315.html)

2013-06-14 13:56:29

[浏览器](https://so.51cto.com/?keywords=%E6%B5%8F%E8%A7%88%E5%99%A8)[渲染原理](https://so.51cto.com/?keywords=%E6%B8%B2%E6%9F%93%E5%8E%9F%E7%90%86)

[_浏览器_的_渲染__原理_简介](https://www.51cto.com/article/395281.html)

[《HowBrowsersWork》，这篇文章把浏览器的很多细节讲得很细，而且也被翻译成了中文。但是，这篇文章太长了，阅读成本太大，不能一口气读完，而且似乎对工作没什么帮助。本文主要是解决这两个难题。](https://www.51cto.com/article/395281.html)

2013-05-23 16:01:56

[浏览器](https://so.51cto.com/?keywords=%E6%B5%8F%E8%A7%88%E5%99%A8)

[_浏览器_如何_渲染_文本](https://www.51cto.com/article/417787.html)

[浏览器是我们最常用的软件之一，文本又是网页中最主要的元素，在浏览器显示文本的过程中有许多有趣的细节，值得展开来讲讲，或许能减少一些误解。这是一个比较粗略的，概括性的介绍，尽可能不涉及过多的技术细节和具体实现，而立足于给Web开发者和设计师提供一些正确的概念。](https://www.51cto.com/article/417787.html)

2013-11-18 14:42:53

[浏览器](https://so.51cto.com/?keywords=%E6%B5%8F%E8%A7%88%E5%99%A8)[渲染](https://so.51cto.com/?keywords=%E6%B8%B2%E6%9F%93)

[前端百题斩之神奇的_浏览器__渲染__流程_](https://www.51cto.com/article/674467.html)

[下面一起来看看浏览器的渲染流程，主要包含构建DOM树、样式计算、布局阶段、分层、图层绘制、分块、栅格化操作、合成和显示。其整个渲染阶段流程如下图所示。](https://www.51cto.com/article/674467.html)

2021-07-26 05:01:55

[浏览器](https://so.51cto.com/?keywords=%E6%B5%8F%E8%A7%88%E5%99%A8)[渲染](https://so.51cto.com/?keywords=%E6%B8%B2%E6%9F%93)[流程](https://so.51cto.com/?keywords=%E6%B5%81%E7%A8%8B)

[_浏览器_解析_渲染_以及页面优化](https://www.51cto.com/article/564176.html)

[浏览器对页面的加载、解析以及渲染是一个非常复杂的话题，这里我只对这个过程做一个非常概括的总览，以初步了解这些过程，对于前端编程如何优化页面给予一些原理性的支撑。](https://www.51cto.com/article/564176.html)

2018-01-19 14:39:53

[浏览器](https://so.51cto.com/?keywords=%E6%B5%8F%E8%A7%88%E5%99%A8)[页面](https://so.51cto.com/?keywords=%E9%A1%B5%E9%9D%A2)[优化](https://so.51cto.com/?keywords=%E4%BC%98%E5%8C%96)

[![](https://s1.51cto.com/wyfs02/M00/08/12/wKiom1na89LC7V2rAAC7l-QsRvQ67.jpeg?x-oss-process=image/resize,m_fixed,w_142,h_82)](https://www.51cto.com/article/553498.html)

[_浏览器__渲染_过程与性能优化](https://www.51cto.com/article/553498.html)

[用户在使用浏览器访问一个网站时需要先通过HTTP协议向服务器发送请求，之后服务器返回HTML文件与响应信息。这时，浏览器会根据HTML文件来进行解析与渲染(该阶段还包括向服务器请求非内联的CSS文件与JavaScript文件或者其他资源)，最终再将页面呈现在用户面前。](https://www.51cto.com/article/553498.html)

2017-10-09 13:39:26

[浏览器](https://so.51cto.com/?keywords=%E6%B5%8F%E8%A7%88%E5%99%A8)[渲染](https://so.51cto.com/?keywords=%E6%B8%B2%E6%9F%93)[服务器](https://so.51cto.com/?keywords=%E6%9C%8D%E5%8A%A1%E5%99%A8)

[![](http://s1.51cto.com/wyfs01/M01/32/B6/wKioOVKMTaXxdbpmAAAHFCnORnU136.jpg?x-oss-process=image/resize,m_fixed,w_142,h_82)](https://www.51cto.com/article/418106.html)

[了解_浏览器_如何工作—_渲染_引擎](https://www.51cto.com/article/418106.html)

[从基础架构上我们也可以看到浏览器的重头戏其实在于渲染引擎(又称排版引擎)，很多页面兼容性问题的根源可以说也皆来源于此。好了，那我们深入到渲染引擎内部仔细看一下吧。](https://www.51cto.com/article/418106.html)

2013-11-20 13:47:43

[浏览器](https://so.51cto.com/?keywords=%E6%B5%8F%E8%A7%88%E5%99%A8)[渲染引擎](https://so.51cto.com/?keywords=%E6%B8%B2%E6%9F%93%E5%BC%95%E6%93%8E)

[![](http://s2.51cto.com/wyfs02/M02/8E/62/wKiom1i_VLyROKffAABReCjfc3I009.jpg?x-oss-process=image/resize,m_fixed,w_142,h_82)](https://www.51cto.com/article/534098.html)

[理解_浏览器_关键的_渲染_路径](https://www.51cto.com/article/534098.html)

[当浏览器接收到从服务器发送过来的HTML页面信息，在将其绘画渲染到屏幕上之前会有许多的步骤要做。浏览器绘制页面需要做的这一系列行为我们称为关键渲染路径。](https://www.51cto.com/article/534098.html)

2017-03-08 08:31:48

[浏览器](https://so.51cto.com/?keywords=%E6%B5%8F%E8%A7%88%E5%99%A8)[渲染](https://so.51cto.com/?keywords=%E6%B8%B2%E6%9F%93)[路径](https://so.51cto.com/?keywords=%E8%B7%AF%E5%BE%84)

[_图解_IE_浏览器_升级演变史](https://www.51cto.com/article/247897.html)

[随着IE9的即将发布，人们对IE的争论也越来越多。下面我们就来看下IE这款浏览器从1.0版升级到9.0版的演变过程。从图片中真真切切的感受下IE浏览器的成长过程。](https://www.51cto.com/article/247897.html)

2011-03-08 10:40:42

[IE9正式版](https://so.51cto.com/?keywords=IE9%E6%AD%A3%E5%BC%8F%E7%89%88)

[![](https://s3.51cto.com/oss/201901/03/21a41730e171c6e516ad90c6facd52cb.png?x-oss-process=image/resize,m_fixed,w_142,h_82)](https://www.51cto.com/article/589699.html)

[_浏览器_缓存_原理_总结](https://www.51cto.com/article/589699.html)

[浏览器在加载资源时，先根据这个资源的一些httpheader判断它是否命中强缓存，强缓存如果命中，浏览器直接从自己的缓存中读取资源，不会发请求到服务器。](https://www.51cto.com/article/589699.html)

2019-01-03 13:09:58

[浏览器](https://so.51cto.com/?keywords=%E6%B5%8F%E8%A7%88%E5%99%A8)[缓存](https://so.51cto.com/?keywords=%E7%BC%93%E5%AD%98)[原理](https://so.51cto.com/?keywords=%E5%8E%9F%E7%90%86)

[C#调用_浏览器_的_原理__及_实现浅析](https://www.51cto.com/article/149562.html)

[C调用浏览器的原理的探讨呢，其实就是通过一个小例子向你介绍了C调用浏览器的实质就是一个单独的程序，那么如何实现呢？本文就向你介绍这些具体内容。](https://www.51cto.com/article/149562.html)

2009-09-04 10:05:16

[C#调用浏览器](https://so.51cto.com/?keywords=C%23%E8%B0%83%E7%94%A8%E6%B5%8F%E8%A7%88%E5%99%A8)[浏览器的原理](https://so.51cto.com/?keywords=%E6%B5%8F%E8%A7%88%E5%99%A8%E7%9A%84%E5%8E%9F%E7%90%86)

[![](http://s4.51cto.com/wyfs02/M00/8E/8A/wKioL1jEs-jTbd8TAAAf5-6uuq0246.jpg?x-oss-process=image/resize,m_fixed,w_142,h_82)](https://www.51cto.com/article/534456.html)

[_浏览器_的关键_渲染_路径深入解析](https://www.51cto.com/article/534456.html)

[在in面试被CTO问到的问题，谨以此翻译来表达对自己知识匮乏的鄙视。](https://www.51cto.com/article/534456.html)

2017-03-12 10:15:18

[浏览器](https://so.51cto.com/?keywords=%E6%B5%8F%E8%A7%88%E5%99%A8)[DOM树](https://so.51cto.com/?keywords=DOM%E6%A0%91)[CSSOM树](https://so.51cto.com/?keywords=CSSOM%E6%A0%91)

[Windows 10_浏览器_采用新_渲染_引擎](https://www.51cto.com/article/466787.html)

[2月27日，微软周四披露了为所有Windows10设备中共同采用的ProjectSpartan浏览器专门设计的新渲染引擎。微软同时还证实，Windows10操作系统中的IE浏览器也将会采用这一新渲染引擎。](https://www.51cto.com/article/466787.html)

2015-02-28 09:39:24

[Windows 10](https://so.51cto.com/?keywords=Windows+10)[Spartan](https://so.51cto.com/?keywords=Spartan)

[_浏览器_加载和_渲染_html的顺序](https://www.51cto.com/article/418084.html)

[前阵子，在组内给大家做了一次关于“浏览器加载和渲染HTML的顺序”的分享，这里再总结一下吧。](https://www.51cto.com/article/418084.html)

2013-11-20 10:47:57

[浏览器](https://so.51cto.com/?keywords=%E6%B5%8F%E8%A7%88%E5%99%A8)[渲染](https://so.51cto.com/?keywords=%E6%B8%B2%E6%9F%93)[html](https://so.51cto.com/?keywords=html)

[CSS3 3D 行星运转 && _浏览器__渲染__原理_](https://www.51cto.com/article/654925.html)

[本文通过一个3DWeb动画的实例，详细的捋一捋浏览器整个渲染页面的过程及原理。](https://www.51cto.com/article/654925.html)

2021-04-01 06:23:24

[CSS3](https://so.51cto.com/?keywords=CSS3)[3D](https://so.51cto.com/?keywords=3D)[3D Web 动画](https://so.51cto.com/?keywords=3D+Web+%E5%8A%A8%E7%94%BB)

[_图解_：百度_浏览器_内测版](https://www.51cto.com/article/248563.html)

[倍受关注的百度浏览器终于在3月8日揭开了它的神秘面纱，伴随着“百度浏览器Beta1.0”内测版本的发布，与其他浏览器不同的是，这一内测版包含杀手锏——APP应用，并与百度应用平台打通，此外，还可以智能搜索。百度宣称这一版本不带任何插件。从公布的截图看，内测版的界面色调以灰色为主，采用了当下流行的简洁布局风格。](https://www.51cto.com/article/248563.html)

2011-03-10 17:17:03

[_图解_五大_浏览器_性能测试](https://www.51cto.com/article/249327.html)

[随着IE9的加入“现代”浏览器大家庭终于已经完整，这些浏览器的共同特点是兼容W3C标准、快速的内容处理引擎和各种安全增强，它们的性能到底如何，ZDNet进行了一次测试，主要项目为V8、SunSpider、Peacekeeper和Kraken。](https://www.51cto.com/article/249327.html)

2011-03-16 10:19:21

[浏览器性能测试](https://so.51cto.com/?keywords=%E6%B5%8F%E8%A7%88%E5%99%A8%E6%80%A7%E8%83%BD%E6%B5%8B%E8%AF%95)

[![](http://s4.51cto.com/wyfs02/M01/8B/37/wKioL1hHc8yiDF2aAEGqPe8FGyI278.gif?x-oss-process=image/resize,m_fixed,w_142,h_82)](https://www.51cto.com/article/524338.html)

[CSS3 3D 行星运转以及_浏览器__渲染__原理_](https://www.51cto.com/article/524338.html)

[3Dtransform会启用GPU加速，例如translate3D,scaleZ之类，当然我们的页面可能并没有3D变换，但是不代表我们不能启用GPU加速，在非3D变换的页面也使用3Dtransform来操作，算是一种hack加速法。我们实际上不需要z轴的变化，但是还是假模假样地声明了，去欺骗浏览器。](https://www.51cto.com/article/524338.html)

2016-12-07 13:25:08

[CSS3](https://so.51cto.com/?keywords=CSS3)[3D](https://so.51cto.com/?keywords=3D)[渲染](https://so.51cto.com/?keywords=%E6%B8%B2%E6%9F%93)

[css的效率和_浏览器__渲染_的速度](https://www.51cto.com/article/418097.html)

[我承认我并不经常想这个问题......我们写的css的效率是怎么样的呢，浏览器渲染的速度又如何呢？](https://www.51cto.com/article/418097.html)

2013-11-20 13:04:41

[css](https://so.51cto.com/?keywords=css)[浏览器](https://so.51cto.com/?keywords=%E6%B5%8F%E8%A7%88%E5%99%A8)[渲染](https://so.51cto.com/?keywords=%E6%B8%B2%E6%9F%93)

### 相似话题

[

后端

](https://www.51cto.com/backend)[26228内容](https://www.51cto.com/backend)

[

开发工具

](https://www.51cto.com/tool)[7302内容](https://www.51cto.com/tool)

[

测试

](https://www.51cto.com/test)[511内容](https://www.51cto.com/test)

[

游戏开发

](https://www.51cto.com/game)[653内容](https://www.51cto.com/game)

[全部话题![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAAAAXNSR0IArs4c6QAAAERlWElmTU0AKgAAAAgAAYdpAAQAAAABAAAAGgAAAAAAA6ABAAMAAAABAAEAAKACAAQAAAABAAAAGKADAAQAAAABAAAAGAAAAADiNXWtAAACT0lEQVRIDZWUPYgTQRTHdzdR0yjRTgOKnViIvVYiooLIieTwQCLkC05UhAPRwlJETpRrjnwiEkSDqETwLARB0FoQwVIRsZOIEDxDEn9vbyZkc5O5zEDy3tv5z++9Nzuzfrlcvul53oUgCK7kcrmX+Nbhqg+gzQ8Gg739fr9ZKpUOW+lrk076APgTWYdNYFr1en3/Gsf876qXDhZ833+jcNu73e5KrVbbZcaHT530QbFY7MZisTMk+aigu3u93kqj0dhmSuKqlw68bDb7h9ZPkuSbxPgHOp3O82azuVni8eGiDxMIgMp+Aj5Okl8S4x9pt9sPsL7E42Na/TCBAFj0BXOKJH8lBn6uUqncEd80ptFHEgikUCh8EDBuX2L8BY7vZfFNYyP9ugQCobIXdHFpBHiPTs6OxBHXpjfur17Nrb1FB9dVvMppO8Ztf6fnx61Jb+xAL6T9G3TyUMVbOL5Les5kTXprAqr3+Q01JLN2bNLHTJXoZ6lU6jb+vIpli+ZarVZ4V7Rm1Jr0w+pGheLzUi9S0TXxKXyAOW/b/0l6Y8u8rBngT4GGBfApv5rP5+9LMtOw6dd1UK1WDwF5xE/P3bXBN9JHOuBC7WM73lP9DqkU/zHwObVF8igyptHrKj3EOwG91nBIb5PJZMYCn0ofJuD7vxXQK+B7VImfsDPpdPpfpGQVuOjjVL6JC/QM+EG1/nsikTiRyWR+m+Cu+jiQReBHBUYXbYzAf0g8YTjp40BnSSCsVY7jac765wng8LGrPmDBMiu/Ap+1XSSd1FX/H7GkjBB3TDEJAAAAAElFTkSuQmCC)](https://www.51cto.com/topic)

### 同话题下的热门内容

[npm 创始人再创业，全新前端工具来了！](https://www.51cto.com/article/801678.html)[20 个 Python 非常实用的自动化脚本](https://www.51cto.com/article/801582.html)[你必须掌握的 30 个 Python 代码，短小精悍，用处无穷](https://www.51cto.com/article/801660.html)[ISO C++委员会主席萨特，本周微软离职，已效力22年！揭秘C++26标准：白宫压力下历史上最大一次变革，C++在微软进展缓慢](https://www.51cto.com/article/801699.html)[Java多次启动一个线程究竟会发生什么？程序到底会不会崩？大部分程序员理解错误！！](https://www.51cto.com/article/801854.html)[SpringBoot 3.3.5 试用CRaC，启动速度提升3到10倍](https://www.51cto.com/article/801552.html)[SpringBoot 整合 Mail 轻松实现邮件自动推送，你学会了吗？](https://www.51cto.com/article/801698.html)[函数是怎么创建的，背后经历了哪些过程？](https://www.51cto.com/article/801823.html)

### 相关专题[更多](https://www.51cto.com/specials)

[

![2024年第十九届中国企业年终评选](https://s3.51cto.com/oss/202411/05/e7d3ccb174c0db8e6ef017cb259e1376c2d696.jpg)

2024年第十九届中国企业年终评选

](https://server.51cto.com/act/nzpx/2024)

[

![如何发挥数据的最大力量?](https://s8.51cto.com/oss/202409/11/52d2412495be0f336e45519df34c5b4fcd58c0.png)

如何发挥数据的最大力量?

2024-09-11 10:06:01



](https://cloud.51cto.com/act/dataflywheel/2024)[

![HarmonyOS创新探索与应用实践· 开发者系列沙龙](https://s2.51cto.com/oss/202408/29/540063f04ca45f992b52502dd7ad5362311af2.jpg)

HarmonyOS创新探索与应用实践· 开发者系列沙龙

2024-08-07 16:28:10



](https://cloud.51cto.com/act/hmos/202407)

我收藏的内容

[![](https://s5-media.51cto.com/cms/static/img/edit.jpg)](https://www.51cto.com/editor.html#article)

![点赞](https://s5-media.51cto.com/cms/client/img/zanpc10.eeddee9.png)

![收藏](https://s5-media.51cto.com/cms/client/img/collect.6dfb91c.png)

![分享](https://s5-media.51cto.com/cms/client/img/share.ca08f33.png)

### 51CTO业务

- 媒体
    
    [51CTO](https://www.51cto.com/)[CIOAge](https://www.cioage.com/)[HC3i](https://www.hc3i.cn/)[Techplur](https://www.51cto.com/techplur)
- 社区
    
    [51CTO博客](https://blog.51cto.com/)[软考社区](https://rk.51cto.com/)[鸿蒙开发者社区](https://ost.51cto.com/)[AI.x社区](https://www.51cto.com/aigc/)
- 教育
    
    [51CTO学堂](https://edu.51cto.com/)[精培](https://e.51cto.com/?utm_platform=pc&utm_medium=51cto&utm_source=zhuzhan&utm_content=sy_topbar&rtm_frd=4)[企业培训](https://b.51cto.com/index?utm_source=hometop)[CTO训练营](https://x.51cto.com/act/cto/camp)

[](https://weibo.com/51cto001?is_all=1)

### 关于我们&条款

- [关于我们](https://www.51cto.com/about/aboutus.html)
- [新闻动态](https://www.51cto.com/about/news.html)
- [站点地图](https://www.51cto.com/about/map.html)
- [意见反馈](https://www.51cto.com/about/aboutus.html#feedback)
- [English](https://www.51cto.com/about/aboutus_e.html)
- [用户协议](https://edu.51cto.com/center/other/service)
- [隐私协议](https://edu.51cto.com/center/other)

北京市海淀区中关村南1条甲1号ECO中科爱克大厦6-7层

北京市公安局海淀分局备案编号：110108002980号  
营业执照 [京ICP备09067568号](https://beian.miit.gov.cn/)

Copyright © 2005-2024 51CTO.COM 京ICP证060544 版权所有 未经许可 请勿转载

[![](https://s7.51cto.com/wyfs02/M02/73/FD/wKiom1YLhe6Rz4cRAAAXp7l7roQ463.jpg)](https://image.51cto.com/images/51cto-icp.jpg)

[营业执照](https://s2.51cto.com/media/license/zz.jpg) [出版物经营许可证](https://s2.51cto.com/media/license/xkz.jpg)

### 友情链接

[新浪科技](https://tech.sina.com.cn/)[腾讯科技](https://tech.qq.com/)[网易科技](https://tech.163.com/)[凤凰科技](https://tech.ifeng.com/)[驱动科技](https://www.mydrivers.com/)[科技行者](https://www.techwalker.com/)[TechWeb](http://www.techweb.com.cn/)[艾瑞网](https://www.iresearch.cn/)[站长之家](http://www.chinaz.com/)[速途网](https://www.sootoo.com/)[中国经济新闻网](http://www.cet.com.cn/)[IT之家](https://www.ithome.com/)[工联网](http://www.iitime.com.cn/)[极客公园](https://www.geekpark.net/)[236视频会议](https://www.263.net/)[中国IDC圈](http://www.idcquan.com/)[企业网D1Net](http://www.d1net.com/)[投资界](https://www.pedaily.cn/)[次方元](https://metafun-space.com/)[火山引擎](https://www.volcengine.com/?utm_campaign=51CTO_2024&utm_content=youlian&utm_medium=51CTO&utm_source=youlian_2024&utm_term=51CTO_youlian)

![](https://s5-media.51cto.com/cms/static/img/erweima.png)

51CTO技术栈公众号

51CTO技术栈公众号

![](https://s5-media.51cto.com/cms/static/img/video.jpg)

业务  
速览