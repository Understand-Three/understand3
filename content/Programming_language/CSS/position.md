---
title: 定位
draft: true
---

# 一、position 的四个值：static、relative、absolute、fixed。

绝对定位：`absolute` 和 `fixed` 统称为绝对定位

相对定位：`relative`

默认值：`static`

# 二、`relative` 定位与 `absolute` 定位的区别

## 实例

HTML代码：
```html
<body>
	<div class="box1">box1box1box1box1box1box1box1box1</div>
	<div class="box2">box2box2box2box2box2box2box2box2</div>
	<div class="box3">box3box3box3box3box3box3box3box3</div>
	<div class="box4">box4box4box4box4box4box4box4box4</div>
	<div class="box5">box5box5box5box5box5box5box5box5</div>
</body>
```

![img](https://www.runoob.com/wp-content/uploads/2018/04/1523584580-4835-20160715090740904-628130236.png)

css代码：


![img](https://www.runoob.com/wp-content/uploads/2018/04/1523584580-2724-20160715090904592-318989579.png)

初始效果：

![img](https://www.runoob.com/wp-content/uploads/2018/04/1523584580-2255-20160715091039576-2001316532.png)

**1、relative：相对于原来位置移动，元素设置此属性之后仍然处在文档流中，不影响其他元素的布局**

给第二个box设置relative：

元素相对于原来位置偏移，宽高都没变，撑大了容器。

![img](https://www.runoob.com/wp-content/uploads/2018/04/1523584580-4801-20160715092724232-191432888.png)

![img](https://www.runoob.com/wp-content/uploads/2018/04/1523584580-5788-20160715092656576-1570070204.png)

**2、absolute:元素会脱离文档流，如果设置偏移量，会影响其他元素的位置定位**

只给第五个box设置absolute：

说明：元素在没有定义宽度的情况下，宽度由元素里面的内容决定，效果和用float方法一样。

![img](https://www.runoob.com/wp-content/uploads/2018/04/1523584581-7423-20160715092354670-413530609.png)

![img](https://www.runoob.com/wp-content/uploads/2018/04/1523584581-6332-20160715092255795-618371335.png)

 **absolute定位原理剖析：**

**1.在父元素没有设置相对定位或绝对定位的情况下，元素相对于根元素定位（即html元素）（是父元素没有）。**

现在给box5偏移值来验证：

![img](https://www.runoob.com/wp-content/uploads/2018/04/1523584581-6635-20160715093702826-936517517.png)

![img](https://www.runoob.com/wp-content/uploads/2018/04/1523584581-9960-20160715093416842-596966947.png)

**2.父元素设置了相对定位或绝对定位，元素会相对于离自己最近的设置了相对或绝对定位的父元素进行定位（或者说离自己最近的不是static的父元素进行定位，因为元素默认是static）。**

**补充：网上有人解释为元素会相对于第一个不是static的父元素定位，我觉得这很容易让人产生误解。以上是我自己的定义。**

现在给body元素一个绝对定位（body元素设置为了absolute，整个容器的宽度由最长div决定，宽度变小了）：

此时的box5现在相对于body元素定位

![img](https://www.runoob.com/wp-content/uploads/2018/04/1523584582-1064-20160715094045654-1511816828.png)

我把上面相对于html元素定位和相对于body定位的两张图放在一起，对比可以看到下面的图，相对于body定位的box5距离文字box1要远一点。所以在没有父元素设置相对定位或绝对定位的情况下，设置了absolute的元素会相对于html根元素定位。

![img](https://www.runoob.com/wp-content/uploads/2018/04/1523584582-5040-20160715095522670-154523685.png)

![img](https://www.runoob.com/wp-content/uploads/2018/04/1523584583-5661-20160715094045654-1511816828.png)

css代码：

![img](https://www.runoob.com/wp-content/uploads/2018/04/1523584583-7776-20160715094628654-1347263129.png)

再来验证这句话：**父元素设置了相对定位或绝对定位，元素会相对于离自己最近的设置了相对或绝对定位的父元素进行定位**

**现在给box们套三个父容器，如下：**

html代码：

![img](https://www.runoob.com/wp-content/uploads/2018/04/1523584583-9859-20160715110450873-1313192754.png)

三个父容器的css样式如下：

![img](https://www.runoob.com/wp-content/uploads/2018/04/1523584583-6738-20160715110612186-436678631.png)

 **现在的样子，现在的box5并不是所说的相对于第一个不是static的元素定位（按这句话的说法，现在我的box5应该相对于最外层容器1偏移才对），而是相对于离自己最近的一层的设置了相对或绝对定位的父元素定位：**

![img](https://www.runoob.com/wp-content/uploads/2018/04/1523584583-8411-20160715110701982-1661555829.png)

**现在把第二个容器和第三个容器的position注释掉（没有position，设置top、left、bottom、right值都没有效），结果如下：**

现在box5的外层设置了相对或绝对的父元素只有最外层容器1，所以box5现在相对于最外层容器1定位。（明显box5移动了）

![img](https://www.runoob.com/wp-content/uploads/2018/04/1523584584-7950-20160715112636107-225201441.png)

**现在只注释掉第三个容器的position**

原理也是一样，现在相对于第二个容器定位（top：50px，离自己最近的设置了相对或绝对定位的父元素）：

![img](https://www.runoob.com/wp-content/uploads/2018/04/1523584584-8858-20160715113341592-1309127001.png)

 **上面第二个和第三个容器都设置的是相对定位，现在改成绝对定位：**

**css代码：**

![img](https://www.runoob.com/wp-content/uploads/2018/04/1523584584-7869-20160715114052701-1904279669.png)

原理和把第二、第三个容器设置为relative一样，只是设置为absolute了之后，第三个容器包含着内容一起脱离了文档，所以没有撑开外面两层容器的宽度

现在的效果：

![img](https://www.runoob.com/wp-content/uploads/2018/04/1523584585-4382-20160715113941139-2051731118.png)

 **外面再添一个容器，来验证上面第一、第二没有被撑开的效果**

![img](https://www.runoob.com/wp-content/uploads/2018/04/1523584585-5206-20160715133241545-396105562.png)

**宽度受到上一层的父容器的宽度限制，现在拉宽第一层的容器的宽度，第二层和第三层随之变宽，效果如下：**

 ![img](https://www.runoob.com/wp-content/uploads/2018/04/1523584585-3475-20160715132441467-557437036.png)

但是如果容器里面有长的div，容器仍然可以被撑开，效果如下：

![img](https://www.runoob.com/wp-content/uploads/2018/04/1523584585-1232-20160715132039217-177646130.png)

 补充：

box2设置为absolute定位之后，脱离文档流，box3向上移，左边被box2遮盖了。

 ![img](https://www.runoob.com/wp-content/uploads/2018/04/1523584586-7671-20160715102324686-1388696339.png)

 在上面的基础上，box3设置absolute，box3脱离文档流（就好像box3浮起来了一样，浮在了box2上面），box4往上移，box3盖住box2，和部分box4.

![img](https://www.runoob.com/wp-content/uploads/2018/04/1523584586-1308-20160715102353123-1422841831.png)

 同理如果box4设置了绝对定位，就会浮起来盖住box3和box2。

### 总结



**relative：定位是相对于自身位置定位**（设置偏移量的时候，会相对于自身所在的位置偏移）。设置了relative的元素仍然处在文档流中，元素的宽高不变，设置偏移量也不会影响其他元素的位置。最外层容器设置为relative定位，在没有设置宽度的情况下，宽度是整个浏览器的宽度。

**absolute：定位是相对于离元素最近的设置了绝对或相对定位的父元素决定的，如果没有父元素设置绝对或相对定位，则元素相对于根元素即html元素定位**。设置了absolute的元素脱了了文档流，元素在没有设置宽度的情况下，宽度由元素里面的内容决定。脱离后原来的位置相当于是空的，下面的元素会来占据位置。

> 原文链接：http://www.cnblogs.com/yy95/p/5672440.html