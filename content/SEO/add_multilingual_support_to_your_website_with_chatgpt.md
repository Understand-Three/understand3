---
title: 养网站防老第6步：利用ChatGPT给网站增加多语言支持
original: https://mp.weixin.qq.com/s/b3_lY793bgiVcuZ2TREF2w
aliases:
  - 养网站防老第6步：利用ChatGPT给网站增加多语言支持
tags:
  - 哥飞SEO教程
draft: true
---
原创 我是哥飞 哥飞 _2023年10月21日 08:01_ _广东_

大家好，我是哥飞。

网站养老系列，哥飞已经更新了7篇了：

[养网站防老：网站可以做成一生的事业](http://mp.weixin.qq.com/s?__biz=MjM5OTIzMzYyMA==&mid=2650080601&idx=1&sn=676b0fff888c93fd63b283e87a3c75d2&chksm=bf3f34628848bd74e4a6ebac72806e89be8bbc9440196edf14cf4f08837f3a81970070a21da2&scene=21#wechat_redirect)

[养网站防老第1步，挖掘出第1个需求](http://mp.weixin.qq.com/s?__biz=MjM5OTIzMzYyMA==&mid=2650080669&idx=1&sn=baf814d85976df09a85c44d9a45a943b&chksm=bf3f34a68848bdb065889163a3b58f10566b937769d679fa50b25768351d55ea4ef24271cae4&scene=21#wechat_redirect)

[养网站防老第2步：分析搜索意图](http://mp.weixin.qq.com/s?__biz=MjM5OTIzMzYyMA==&mid=2650080680&idx=1&sn=4ee04f6579aaa40acefb96318310cbcc&chksm=bf3f34938848bd850bcd811892f9b71c7a51512f9d010ab7aae46487eb045559ac55e9bd70ed&scene=21#wechat_redirect)

[养网站防老第1.5步：用一个公式来判断关键词是否值得做，让你选择关键词不再犹豫](http://mp.weixin.qq.com/s?__biz=MjM5OTIzMzYyMA==&mid=2650080690&idx=1&sn=b6b8b6fbcbc1a57e476d61e574f5c1a1&chksm=bf3f34898848bd9f107fff59df18264e792c3161734b71abc48713e49c9845ec02daa243f596&scene=21#wechat_redirect)

[养网站防老第3步：根据搜索意图使用ChatGPT的GPT4生成网页](http://mp.weixin.qq.com/s?__biz=MjM5OTIzMzYyMA==&mid=2650080699&idx=1&sn=153560f607edada80e68d0804cf70ef7&chksm=bf3f34808848bd968c8fdd5962789ef58311ab109703d7244dd51a2df89359ee2332ccb4ae2c&scene=21#wechat_redirect)

[养网站防老第4步：手动调整布局和样式](http://mp.weixin.qq.com/s?__biz=MjM5OTIzMzYyMA==&mid=2650080715&idx=1&sn=51a41252ac6f2c8bb9d543f9f39bb31b&chksm=bf3f34f08848bde6a1b0602352384a66e4b14e3599469ddf6c4ba75a01556fbc9a9f6ef51124&scene=21#wechat_redirect)

[养网站防老第5步：内页和内链建设](http://mp.weixin.qq.com/s?__biz=MjM5OTIzMzYyMA==&mid=2650080739&idx=1&sn=1685ea0a11d983c256820d49ef197446&chksm=bf3f34d88848bdcea3546d50ac8a8ee5cbafda8b0b9f71e4368a3f2492905091faa41f1035f5&scene=21#wechat_redirect)  

在此前的步骤中，我们把首页和内页都做好了，但是只有英文一种语言，今天我们借助ChatGPT给网站增加多语言支持。

大家可能会发现，哥飞在一些步骤中推荐大家使用ChatGPT，这是因为这次网站养老系列教程，更主要的读者是初学者。

哥飞希望通过这个教程，让完全不懂海外网站开发，甚至有一点技术基础但是对于前端不太熟悉的同学，也能够顺利地跟着教程学会如何开发海外网站。

所以使用ChatGPT，不仅仅可以提高效率，还可以让初学者也能做出及格线以上水平的网站。  

那么到底要做哪些语言呢？我们用数据说话，打开Semrush，查看这个关键词各个国家的搜索量。  

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/LBrX00GQeictH7no4jU2gUUAZZVLJDyRYaNbM9nDUtZ9icUdneezu9w2UIXibg7xI5vPicuQYjk0MUL9xWRjfWNEew/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

排名前六的分别是：GH 、US 、NG 、UK、IN、PH，我们通过询问ChatGPT，可以得到这些国家信息和主要语言。

```
GH、US、NG、UK、IN、PH 分别是哪些国家，说什么语言？
```

GPT4的回答：

```
这些是国家的缩写，以下是对应的国家及其主要官方语言：
```

刚好挺巧的，这些国家都会说英语，也就是其实我们这个网站只需要有英文就足够了，但是我们今天为了给大家讲解如何给网站增加多语言支持，所以我们以印地语和菲律宾语为例来说明。

我们需要先问一下GPT4，印地语和菲律宾语一般缩写是什么。  

```
印地语和菲律宾语一般缩写是什么？
```

GPT4的回答：

```
为了网站多语言支持，通常我们会采用语言代码作为子目录的命名。
```

所以，我们需要在网站根目录，也就是 index.html 的同级，创建两个子目录，分别是“hi”和“tl”，创建好之后我们网站目前的目录结构如下：

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/LBrX00GQeictH7no4jU2gUUAZZVLJDyRYb8bpGs4ia57XqDNtribDFbIPHMoYYic1Ll2gsQNmYcpMAQRF6M44EYuEw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

然后，我们需要在原先的页面中增加语言切换按钮，同样，先问GPT4:  

```
如果我要在网站增加语言切换按钮，英文我用 English ，那么 hi 和 tl 用什么名称？
```

GPT4回答：  

```
在为网站添加语言切换按钮时，我们通常会使用该语言的自称来表示。
```

哥飞继续问：

```
如果用 Filipino ，那么简称用 tl 合适吗？
```

GPT4回答：  

```
"Filipino" 是基于"塔加洛语" (Tagalog) 的官方标准版本，用于菲律宾的官方事务和教育。
```

所以我们语言名称用“Filipino”，简称用“tl”是完全没问题的。

在 logo 和 country-list 中间增加一个 language-list ：  

```
<div class="language-list">
```

对应的 css 如下：  

```
.language-list{
```

效果如下，没有过多美化，直接在右侧增加了三个语言的列表，当前语言加粗加黑：

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/LBrX00GQeictH7no4jU2gUUAZZVLJDyRYxWYKWDYVjMLhetAxiafXcgxsKBficL1h5NST8sdPRDQ1jGK89IMpjqgQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

我们这个网站，默认是英语，所以给英语增加了“curr”类。

接着去修改 china-phone-number-generator.html 文件，依然是把语言切换放进去，跟首页有些小区别的是，因为用户当前在中国手机号页面，所以切换时也需要保持继续在这个页面，对应的代码如下：

```
<div class="language-list">
```

其它页面按照同样的方法处理。

接着，我们把所有处理好的 .html 文件复制，然后分别粘贴到 /hi/ 和 /tl/ 目录，做完之后，我们网站目前的目录结构如下：

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/LBrX00GQeictH7no4jU2gUUAZZVLJDyRY7icOG3TaEw2GHwzAkYkR6tW7vuyhtnq3EKztJPV5EWqF4FzmQQOmxWw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

注意，styles.css 是不用复制的，因为这是公共通用文件。  

但是子目录内的链接就需要调整一下了。  

以下我们都以 /hi/ 目录的文件为例，tl目录方法类似。  

修改 /hi/ 所有文件的第二行：

```
从下面这样：
```

修改 /hi/ 所有文件的 styles.css 引用路径，指向到上一层目录下的styles.css：  

```
从下面这样：
```

修改 /hi/ 首页位置，也就是印地语的首页指向 /hi/ 目录 ：  

```
从下面这样：
```

修改 /hi/ 首页语言列表对应的链接，首页对应代码如下：  

```
<div class="language-list">
```

看出区别了吗？因为我们目前在 /hi/ 的 index.html 页面，所以curr要放在第二个。如果要切换到英语，需要回到上一层级，所以用了“../”来回到上一层。同理，要切换到菲律宾语，也需要回到上一层级，然后再进入 /tl/ 目录，所以用“../tl/”。

再看 /hi/china-phone-number-generator.html 文件，语言列表这里就需要改为如下代码：

```
<div class="language-list">
```

请注意观察，跟英语对应的同名文件，这里写法上的区别。

有没有发现，这里写起来还是挺繁琐的？这是因为我们目前这个网站采用的是纯静态文件的形式制作。如果用上动态生成页面技术，就不用这么麻烦了。  

但是对于初学者来讲，如果通过这个有些麻烦的方法，能够学会并理解，也是值得的。

并且对于初学者，如果不懂后端开发的话，麻烦就麻烦，先手工方式做好第一个网站再说，从第二个网站开始，再来想办法提升效率。

接下来，回到 /hi/index.html 文件，我们目前网页上的文字还是英语呢，需要让 GPT4 帮忙翻译为印地语。  

```
请把下面翻译为印地语：
```

翻译结果为：

```
<title>फ़ोन नंबर जनरेटर, चीन, भारत, अमेरिका, इंडोनेशिया, ब्राज़िल, पाकिस्तान, नाइजीरिया, बांग्लादेश, रूस, जापान</title>
```

为了确认翻译质量，我们可以新开一个窗口让GPT4把印地语再翻译为英语：

```
请把下面的印地语翻译为英语：
```

翻译结果看起来没问题，也就说明印地语没多大问题：

```
Phone number generator, China, India, America, Indonesia, Brazil, Pakistan, Nigeria, Bangladesh, Russia, Japan
```

接着翻译导航栏：

```
请把下方html代码中的 title 和标签内英语翻译为印地语：
```

翻译结果如下：

```
<div class="country-list">
```

再接着翻译首页的section，以第一个 china 为例：

```
以下html代码，除了 url 不翻译，其它该翻译的地方都翻译为印地语：
```

翻译结果如下：

```
<section>
```

全部翻译完成后的印地语首页效果如下：

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/LBrX00GQeictH7no4jU2gUUAZZVLJDyRYVhtiaeKoX5sCpDiaUz6kVxJezJmD652V2mExdCchY7icp411MGytpyiacw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

大家按照上面的方法继续把剩下所有页面都翻译好，那么我们的多语言支持就做好了。

注意，本来这些页面都需要再做移动端适配的，我们暂时不做处理，先继续往下走。

明天哥飞带着大家进行下一步，注册域名，然后部署到Vercel，并且用 Cloudflare 包一层。

到时候，网站就可以对外访问了，然后就可以提交到谷歌Search Console后台，并且增加谷歌统计代码。

欢迎关注哥飞公众号，及时收到连载推送：  

![](http://mmbiz.qpic.cn/mmbiz_png/LBrX00GQeicsQIcEZg1UMapobh9KDpNHpFI7CNXVq0Z4zQD6zVia7KGl8iacciaFNPCa3Cic1TKp4h7tYY9doIQ3eRg/300?wx_fmt=png&wxfrom=19)

**哥飞**

哥飞，出海鼓励师，SEO专家，Adsense玩家，AI工具出海创业者。V: gefei55

326篇原创内容

公众号

哥飞从7月2日开始发起了一个付费社群，群友们都是人才：  

[入群100天，哥飞的朋友们手握百万流量，支付订单滚滚来](http://mp.weixin.qq.com/s?__biz=MjM5OTIzMzYyMA==&mid=2650080648&idx=1&sn=25928bc955f2bc06289016100e9cfeeb&chksm=bf3f34b38848bda51564715addd3d46d1e7100727f30e0db51b95c0539cb8a956ced1e4626cf&scene=21#wechat_redirect)

哥飞还提出了养网站防老概念《[养网站防老：网站可以做成一生的事业](http://mp.weixin.qq.com/s?__biz=MjM5OTIzMzYyMA==&mid=2650080601&idx=1&sn=676b0fff888c93fd63b283e87a3c75d2&chksm=bf3f34628848bd74e4a6ebac72806e89be8bbc9440196edf14cf4f08837f3a81970070a21da2&scene=21#wechat_redirect)》：[](http://mp.weixin.qq.com/s?__biz=MjM5OTIzMzYyMA==&mid=2650080648&idx=1&sn=25928bc955f2bc06289016100e9cfeeb&chksm=bf3f34b38848bda51564715addd3d46d1e7100727f30e0db51b95c0539cb8a956ced1e4626cf&scene=21#wechat_redirect)  

> 6、做网站就像是种树一样，先种下第一棵树，再种下第二棵树，慢慢你就有了一个小果园，收成会越来越好； 
> 
> 7、尽量多种几种不同品种的果树，既可以使得一年四季都有水果吃，又可以防止“病虫害”导致同种果树死亡；
> 
> 8、网站可以做成一生的事业，只要碳基生命还存在，就还会有网站的需求，我们就还能靠网站来赚钱； 
> 
> 9、养儿防老不如养网站防老。
> 
> 我是哥飞，公众号：哥飞[养网站防老：网站可以做成一生的事业](https://mp.weixin.qq.com/s?__biz=MjM5OTIzMzYyMA==&mid=2650080601&idx=1&sn=676b0fff888c93fd63b283e87a3c75d2&chksm=bf3f34628848bd74e4a6ebac72806e89be8bbc9440196edf14cf4f08837f3a81970070a21da2&scene=21#wechat_redirect)

哥飞也给大家说了《[2023年了，为什么还要做网站？为的是可控的流量，可控的用户，可控的收入。](http://mp.weixin.qq.com/s?__biz=MjM5OTIzMzYyMA==&mid=2650079683&idx=1&sn=091f793f74b58d107a6c3adc93870974&chksm=bf3f30f88848b9ee3879f5236c1b0d3be457abd39088ad7cb916f4e7db0a54795d3dd95cefef&scene=21#wechat_redirect)》  

哥飞的社群就是围绕着“养网站防老”话题，带着大家一起做网站赚钱，让每一位朋友都能够慢慢有一个自己的小果园。  

社群目前暂时是微信群形态，有一个配套的网站，已上线第一版，社群内朋友可见。

社群主要面向技术开发者、产品经理、设计师等人群，大家一起讨论独立开发、出海产品、流量获取、流量变现等话题。

社群讨论的话题主要是围绕着网站来的，用网站来承接流量，然后变现。  
那么就要考虑做什么网站，所以需要去挖掘需求。

然后去搞流量，可以是SEO，也可以是发帖宣传推广，还可以是付费软文。

有了流量之后就得考虑如何变现，可以是广告变现，也可以是联盟导购，更可以直接向用户收费。

目前有两个群，一群定价888元一年，目前450多人了，二群按照人数调整价格，目前92人，所以500元优惠价只剩8个位置。  

社群从加入日期开始计时，365天后到期。

群里讨论很活跃，行动很迅速，大家已经做了几十个产品了。

这个社群7月2号开始运营的，到今天3个多月时间里，主要讨论了以下话题：

1、建站基础，如何快速做一个网站；  
2、SEO基础，如何优化网站；  
3、推广基础，如何宣传推广网站；  
4、运营基础，如何运营好一个网站；  
5、Adsense基础，如何靠谷歌Adsense赚广告费；  
6、一些工具使用经验分享，如Semrush分析别的网站流量和出入站链接，Similarweb如何看流量；  
7、基于Semrush、Similarweb等工具，如何去发掘新需求，发现新网站；  
8、实战经验，如何去抓住新词热词做网站，从搜索引擎获取流量。  

以及其他更多相关话题，欢迎加哥飞微信 qiayue 加入社群大家一起出海赚钱，养网站防老。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/LBrX00GQeicsG8Pro6O9Hu75bIIiafZVPs3qlYeaNNJ1BpqNplEGgibL5m1bcq8a1N1rzoI5lia8aJjtHfgiaAADJJQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1&tp=webp)

​

养网站防老130

出海47

ChatGPT19

seo50

养老1

养网站防老 · 目录

上一篇养网站防老第5步：内页和内链建设下一篇养网站防老第7步：注册域名，解析域名，部署上线

​

![](https://mp.weixin.qq.com/mp/qrcode?scene=10000004&size=102&__biz=MjM5OTIzMzYyMA==&mid=2650080755&idx=1&sn=27c8b30bcbf77d6e9aeea6469ca3c118&send_time=)

微信扫一扫  
关注该公众号