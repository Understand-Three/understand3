---
title: 分享几个实用的谷歌搜索高级语法
aliases:
  - 分享几个实用的谷歌搜索高级语法
tags:
  - SEO
  - 哥飞分享
draft: true
original: https://mp.weixin.qq.com/s/VXYBmRSevFwaLNKK1OvTzQ
date: 2023-09-25
---
大家好，我是哥飞。  

昨天哥飞发了《[ChatPDF.com 小调查，帮你梳理这个月访问量540万的AI产品是如何爆火的](http://mp.weixin.qq.com/s?__biz=MjM5OTIzMzYyMA==&mid=2650080375&idx=1&sn=7ecb6ccb7a834d43b0b4bd63ef7c2592&chksm=bf3f354c8848bc5ae9c686dbf8901a1aab7241c7e160a782c195f55db91a9845e20d73708778&scene=21#wechat_redirect)》，加上上次发的《[【5000字调查分析】建站20天拿下480万访问量，俄罗斯版的妙鸭相机是怎么做到的？](http://mp.weixin.qq.com/s?__biz=MjM5OTIzMzYyMA==&mid=2650079744&idx=1&sn=0d82dcd95fe435a6b46a53a642a6c4e4&chksm=bf3f333b8848ba2deee768dea94b0ed5c2101c5bbf689cf536967d6141910b14f55ba03ed5c9&scene=21#wechat_redirect)》，里边在定位数据时，都用到了一些谷歌的高级搜索语法，今天哥飞就给大家分享一下这些高级语法的用法和用途。  

**一、基础语法**

我们最常用的就是直接输入关键字进行搜索，如想搜索“Vercel”，直接在输入框里输入“Vercel”就可以了。  

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/LBrX00GQeicussgMr7orm3gGxh62PggiaXYfF1mR4DS9ibcLQoERulLZ0RKHHLRsVAMDl8VLqXkuSyh2FnF1icjz1A/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

有时候搜索的关键词包含多个词时，只会部分命中，如搜索“Vercel pricing”，谷歌会自动判断“Vercel”是一个网站，你想找这个网站的价格信息，所以给你展示“https://vercel.com/pricing”页面。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/LBrX00GQeicussgMr7orm3gGxh62PggiaXnkev6v9gA9zJ6hpMRMuG4SOyicuMSIibBDM7qib0jxTpHgHLQO6rlTSSQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

此时如果你把搜索词用双引号括住，再搜，出来的就是下面的结果了，官方页面没出来，出来的是别的完全命中了这两个关键词的网页。  

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/LBrX00GQeicussgMr7orm3gGxh62PggiaXFb8tM9v2Y1Oic4PT4e0K83OpzibnPkLOdt648KLhGPqsAtj5GqVvafnQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

所以双引号的作用就是告诉谷歌，你想得到完全匹配你的搜索词的结果。

  

**二、site 语法**  

这个语法我们站长最常用，用途是查询某个指定的域名的所有被收录页面，我们通常用来看我们的网站被收录了多少页面，以及某个页面是否被收录。

语法格式：  

```
site:[域名]
```

举例：  

```
site:vercel.com
```

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/LBrX00GQeicussgMr7orm3gGxh62PggiaX1WibCaw0MoyTMhA8oIibKVq5vicWKbia2EzsYNGIAefjrdPeSe1hibFiaw1A/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

其中GSC哥飞之前介绍过：《[如何清晰的知道我们网站在搜索引擎的表现：Google Search Console 使用入门讲解](http://mp.weixin.qq.com/s?__biz=MjM5OTIzMzYyMA==&mid=2650079678&idx=1&sn=28e2e1f0abf09872482549f66c214f0a&chksm=bf3f30858848b9934cc6ca69c172537ac676a04975ab475160e90b02d56cc6d5fe42df03a97f&scene=21#wechat_redirect)》。  

一般排序方式是首页>子域名>子目录>内页。  

  

**三、减号语法**  

减号的用途是排除，去除你不想要的搜索结果。  

如搜索“Vercel -site:vercel.com”，就是说搜索所有非vercel官方域名下的“Vercel”结果。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/LBrX00GQeicussgMr7orm3gGxh62PggiaXb8gWKIibcuR5kibz9okUlu2sFgV0BuXPpAos2nCoibzfXrnQCO4F7JJag/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

再举个例子，最近 iPhone 15 发售了，我们试试直接搜索“iPhone 15”结果是什么。  

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/LBrX00GQeicussgMr7orm3gGxh62PggiaXnYGF2GsPiaxIJQVGueA6CaTBgBsRXwIdqiaKdexiarZzANfH0k7iclibb1Q/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

可以看到会出现“iPhone 15”和“iPhone 15 Plus”和“iPhone 15 Pro”等结果。

如果我们只想要找“iPhone 15 Pro”的结果，就可以把“iPhone 15 Plus”给排除掉，那么搜索词是不是这么写“iPhone 15 Pro -iPhone 15 Plus”呢？  

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/LBrX00GQeicussgMr7orm3gGxh62PggiaXswiaiaVsS7OulQia34G27icJ7ALPI5grTRacbrwLicHicm3nZ1PRkjCF1ibUA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

你会发现找不到结果，想到为什么了吗？

因为把“iPhone”给排除掉了，那么我们想要排除“iPhone 15 Plus”，正确的写法是“iPhone 15 Pro -"iPhone 15 Plus"”，也就是用双引号把“iPhone 15 Plus”给全部括起来，就是当作一个词，那么排除时就只会排除“iPhone 15 Plus”。  

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/LBrX00GQeicussgMr7orm3gGxh62PggiaX9CGJo6dsqc8JY1ZhtRMf2ia2ILyuyfrlZmDQXfbozkeSNZZLmltdx1w/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

**四、intitle 语法**

用途是查询网页标题中含有指定关键词的网页。  

语法格式：  

```
intitle:[关键词]
```

举例，搜索“intitle:iPhone”结果如下：

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/LBrX00GQeicussgMr7orm3gGxh62PggiaXm8cBxqE9WwsbiaX89nRguagDXX0TaNrc1XhbzcyicSjawL66wxyFX8TQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

搜索“intitle:"iPhone 15 Pro"”结果如下：  

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/LBrX00GQeicussgMr7orm3gGxh62PggiaXCM56PDzmib1aAmoibsp0ogBaLjg8wDm9NlicE2vhSRHSyGZCb0HQDSoZA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

还可以多个语法结合使用，如“intitle:"iPhone 15 Pro" -site:apple.com”。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/LBrX00GQeicussgMr7orm3gGxh62PggiaXJljH9egJNiad5CG3S5yQJ7RxDibp7hIPoxyPKib2kVbS8273mxibJbju8g/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

或者“intitle:"iPhone 15 Pro" site:apple.com”。  

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/LBrX00GQeicussgMr7orm3gGxh62PggiaXIF3NXVgAJHiaU02GPibZSBWBtsQl2SWw6QhHXavfHlSAPJfYWWPSK2nQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

  

**五、inurl 语法**  

与intitle类似，inurl 用途是限定只搜索 url 中携带指定关键词的网页。  

如我们可以用“inurl:login”来找到各个网站的登录页面，这里排除维基百科是为了去掉百科中关于“login”的介绍结果页面。  

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/LBrX00GQeicussgMr7orm3gGxh62PggiaXmJnv2Mzv2hpVE4zlYiao6mRxS8dee4iaY2sicDqunmawcLuicdGzWKojibA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

**六、filetype 语法**  

用途是限定搜索结果的文件类型，如可以用“filetype:pdf Travel”来找到所有关于旅游相关的pdf文件。  

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/LBrX00GQeicussgMr7orm3gGxh62PggiaXQfsa0Qle26XyaeTrpN3zdI3aPBBsLW3ibO247EJWoVickibKdFHVupKUQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

支持 pdf、ppt、doc 等很多文件格式，具体见下方表格。

|文件类型|文件格式|
|---|---|
|Adobe Portable Document Format|pdf|
|Adobe PostScript|ps|
|Autodesk Design Web Format|dwf|
|Google Earth|kml, kmz|
|GPS eXchange Format|gpx|
|Hancom Hanword|hwp|
|HTML|htm, html|
|Microsoft Excel|xls, xlsx|
|Microsoft PowerPoint|ppt, pptx|
|Microsoft Word|doc, docx|
|OpenOffice presentation|odp|
|OpenOffice spreadsheet|ods|
|OpenOffice text|odt|
|Rich Text Format|rtf|
|Scalable Vector Graphics|svg|
|TeX/LaTeX|tex|
|Text|txt|
|Basic source code|bas|
|C/C++ source code|c, cc, cpp, cxx, h, hpp|
|C# source code|cs|
|Java source code|java|
|Perl source code|pl|
|Python source code|py|
|Wireless Markup Language|wml, wap|
|XML|xml|

  

刚才哥飞也给大家演示了，其实这些语法之间是支持搭配使用的，大家可以自由发挥，根据使用场景合理搭配。

好了，今天的文章就分享到这里了。