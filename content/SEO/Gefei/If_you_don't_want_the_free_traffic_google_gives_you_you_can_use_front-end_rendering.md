---
title: 如果不想要谷歌给的免费流量，你就用前端渲染吧
aliases:
  - 如果不想要谷歌给的免费流量，你就用前端渲染吧
tags:
  - 哥飞SEO教程
  - SEO
original: https://mp.weixin.qq.com/s/ibWT766ftLAq2LrH4wMUWw
draft: true
---
原创 我是哥飞 哥飞 _2024年04月07日 23:16_ _广东_

![图片](https://mmbiz.qpic.cn/sz_mmbiz_jpg/LBrX00GQeicvnbd7dnZUiaqnxhTlzdMzuWNlwOnnreD5nDvkFOhlBFYmP97Gl4TZwxJarTjL7DZWSxh1jzOcg8KQ/640?wx_fmt=jpeg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

大家好，我是哥飞。

最近不少朋友都遇到这个问题，本来要后端渲染的页面，结果在开始开发之前，没有跟工程师说清楚要求，最后上线了一个前端渲染的网站。

这种情况就属于哥飞讲过的，如果建站之初就没想好，那么最后很有可能就要推倒重来。

虽然说把一个前端渲染的网站改成后端渲染，工作量不算太大，但是开发工程师可能也会埋怨你，为什么不在一开始就说清楚？！

所以如果你的网站想要从谷歌等搜索引擎获取到免费流量，那就一定要去适应这些搜索引擎的规则。  

哥飞知道，有人会说，谷歌也不是不能渲染JS，最后得到渲染后的内容。

但是哥飞想跟大家说的是，可以先照照镜子看看自己的脸够不够大吧。

如果我们的脸不够大，谷歌凭啥给我们的小网站额外耗费资源去渲染JS页面？

所以，别做他想，赶紧改成后端渲染吧。  

那么要怎么判断一个网页到底是前端渲染还是后端渲染呢？  

很简单，打开谷歌浏览器，打开任意一个你要检查的网页，鼠标点在网页空白的地方，右键，选择查看网页源代码。  

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/LBrX00GQeicvnbd7dnZUiaqnxhTlzdMzuW0lC7EjhZ33rzl8ho4ibuzjzDWOF1HVibaGvoIkcrbjFFfTp6ZKRZia6HA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

谷歌浏览器会打开一个新页面，网址前面有 `view-source:`，表示我们正在查看这个网页的 html 代码。  

然后你再用 `Ctrl + F` 打开网页搜索小工具，去搜索网页里显示出来的一些文字是否出现在 html 代码里。  

如果没有出现，那么必然是前端渲染的页面了。

如果出现了，还需要看出现在哪里，如果出现在 json 数据里，这种也算前端渲染。

只有出现在 html 标签里的，才算后端渲染。

好，判断方法讲完了，今天文章也就差不多讲完了。

哥飞再次回答一下，什么是后端渲染？

也就是需要网页主体内容跟随 html 代码一起返回的，才算。

再回答一下，为什么要后端渲染？

因为谷歌爬虫抓取 html 代码，不会运行 js，而是直接经过一些处理后提取网页主体内容。

所以如果你的内容需要js运行之后才会显示到网页里的，谷歌爬虫一般情况下都获取不到。  

也就是如果你的网页是前端渲染的，谷歌都抓取不到网页内容，当然就无法把你的网页拿去参与排名了。  

也就当然无法从谷歌获取到免费的流量了。  

好了，今天的文章到此就真的结束了。  

如果你还想学习更多SEO知识，想要跟着哥飞做出海网站赚美元养老，请加入哥飞的朋友们社群。

关于社群的更多介绍，请看《[是时候给大家好好介绍一下哥飞的社群了，毕竟刚被二十年站长大佬夸过](http://mp.weixin.qq.com/s?__biz=MjM5OTIzMzYyMA==&mid=2650082450&idx=1&sn=b33f52d905edd76782d85eb06163f312&chksm=bf3f3da98848b4bf8214219c775293b397bdda48f14975f88e55a5bbe7efa75e4b11d93010a5&scene=21#wechat_redirect)》。  

  

先给大家看看已经在社群里的其他朋友怎么评价的吧。

  

![图片](https://mmbiz.qpic.cn/sz_mmbiz_jpg/LBrX00GQeictfJNjePhchkZYLuBwKPcJl2yZPhaRV7VWHg1Fe9tIs05v9QTFBq1oCZjVn9qB08LszWxrFibHHeMQ/640?wx_fmt=other&wxfrom=5&wx_lazy=1&wx_co=1&tp=webp)

![图片](https://mmbiz.qpic.cn/sz_mmbiz_jpg/LBrX00GQeicsc3DNibdfcSLWyEGZBZSXSUbPuaibAobt9LPMO3wygibBF21OuH0mCYZU6Hn3qgz5Zvxml98F9dKnrQ/640?wx_fmt=other&wxfrom=5&wx_lazy=1&wx_co=1&tp=webp)

  

![图片](https://mmbiz.qpic.cn/sz_mmbiz_jpg/LBrX00GQeicu0ohJ2AspibworASbayGLjNicts7f15fE789SLz4EI2yZgzHicU6KCsqDNVgkpOwdulS8sGWaSXSRVg/640?wx_fmt=other&wxfrom=5&wx_lazy=1&wx_co=1&tp=webp)

那么这到底是一个什么样的社群呢？  

  

一句话介绍，这是一个教你出海做网站赚美元的社群。  

  

哥飞知道，肯定会有人说，教人赚钱最赚钱。  

  

但是，哥飞这个社群，你学了，是真的能够赚美元的。

  

因为哥飞不是教你做一个类似的社群去赚别人的钱。  

  

哥飞教你怎么挖掘需求，怎么搞SEO，怎么搞流量，怎么把流量变现。

  

或者说，哥飞其实是在给大家做微培训。

  

如果想更多了解社群，或者想加入社群，请加哥飞的微信 qiayue 。  

  

当然，即使你现在不加社群，也可以先关注哥飞的公众号，多看几篇文章，你会有收获的。  

  

![](http://mmbiz.qpic.cn/mmbiz_png/LBrX00GQeicsQIcEZg1UMapobh9KDpNHpFI7CNXVq0Z4zQD6zVia7KGl8iacciaFNPCa3Cic1TKp4h7tYY9doIQ3eRg/300?wx_fmt=png&wxfrom=19)

**哥飞**

哥飞，出海鼓励师，SEO专家，Adsense玩家，AI工具出海创业者。V: gefei55

326篇原创内容

公众号

  

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

  

养网站防老130

seo50

养网站防老 · 目录

上一篇【哥飞SEO教程】从 TDK 到 TDH下一篇哥飞的朋友网站接入支付三天，用户付费2500+美元

​

![](https://mp.weixin.qq.com/mp/qrcode?scene=10000004&size=102&__biz=MjM5OTIzMzYyMA==&mid=2650082690&idx=1&sn=5c053eecd24c0f0b156cd7fcb9869a02&send_time=)

微信扫一扫  
关注该公众号