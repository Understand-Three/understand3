---
title: 养网站防老第5步：内页和内链建设
aliases:
  - 养网站防老第5步：内页和内链建设
tags:
  - SEO
  - 哥飞SEO教程
draft: true
original: https://mp.weixin.qq.com/s/X95UZmPEKHZZ4rNoBcaoJg
---


原创 我是哥飞 哥飞 _2023年10月20日 08:03_ _广东_

大家好，我是哥飞。  

昨天@damo 老板又来给大家报喜了，我们先恭喜他在订阅上走出了成绩。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_jpg/LBrX00GQeicvPAwKkOfBX8q9vDYjTpsZnkYuwRutAnR8HjEIZ0jWARtlWjIjWAicApmAD9oC5gGSpfPmucet2xOw/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

网站养老系列，哥飞已经更新了6篇了：  

[养网站防老：网站可以做成一生的事业](http://mp.weixin.qq.com/s?__biz=MjM5OTIzMzYyMA==&mid=2650080601&idx=1&sn=676b0fff888c93fd63b283e87a3c75d2&chksm=bf3f34628848bd74e4a6ebac72806e89be8bbc9440196edf14cf4f08837f3a81970070a21da2&scene=21#wechat_redirect)  

[养网站防老第1步，挖掘出第1个需求](http://mp.weixin.qq.com/s?__biz=MjM5OTIzMzYyMA==&mid=2650080669&idx=1&sn=baf814d85976df09a85c44d9a45a943b&chksm=bf3f34a68848bdb065889163a3b58f10566b937769d679fa50b25768351d55ea4ef24271cae4&scene=21#wechat_redirect)  

[养网站防老第2步：分析搜索意图](http://mp.weixin.qq.com/s?__biz=MjM5OTIzMzYyMA==&mid=2650080680&idx=1&sn=4ee04f6579aaa40acefb96318310cbcc&chksm=bf3f34938848bd850bcd811892f9b71c7a51512f9d010ab7aae46487eb045559ac55e9bd70ed&scene=21#wechat_redirect)  

[养网站防老第1.5步：用一个公式来判断关键词是否值得做，让你选择关键词不再犹豫](http://mp.weixin.qq.com/s?__biz=MjM5OTIzMzYyMA==&mid=2650080690&idx=1&sn=b6b8b6fbcbc1a57e476d61e574f5c1a1&chksm=bf3f34898848bd9f107fff59df18264e792c3161734b71abc48713e49c9845ec02daa243f596&scene=21#wechat_redirect)

[养网站防老第3步：根据搜索意图使用ChatGPT的GPT4生成网页](http://mp.weixin.qq.com/s?__biz=MjM5OTIzMzYyMA==&mid=2650080699&idx=1&sn=153560f607edada80e68d0804cf70ef7&chksm=bf3f34808848bd968c8fdd5962789ef58311ab109703d7244dd51a2df89359ee2332ccb4ae2c&scene=21#wechat_redirect)

[养网站防老第4步：手动调整布局和样式](http://mp.weixin.qq.com/s?__biz=MjM5OTIzMzYyMA==&mid=2650080715&idx=1&sn=51a41252ac6f2c8bb9d543f9f39bb31b&chksm=bf3f34f08848bde6a1b0602352384a66e4b14e3599469ddf6c4ba75a01556fbc9a9f6ef51124&scene=21#wechat_redirect)  

之前我们已经把首页做好了，今天我们来聊第5步，把内页也做好，同时教大家如何做内链建设。  

**一、首页小调整**

在此之前，我们先把首页稍微修改一下。  

**1.1、标题和描述**

标题和描述修改为：

```
<title>Phone Number Generator,China,India,US,Indonesia,Brazil,Pakistan,Nigeria,Bangladesh,Russia,Japan</title>
```

**1.2、首页h1**

首页h1的a标签增加title：  

```
<h1 class="logo">
```

**1.3、导航栏**

导航栏的a标签增加title：  

```
<div class="country-list">
```

**1.4、国家列表**

每一个h2的a标签也增加title：  

```
<section>
```

这样我们首页就给每个国家的内页都增加了2个链接，分别传递了“xxx Phone Number Generator”、“Generate xxx Phone Number”两个关键词的权重到对应的国家内页。  

**1.5、首页预览**  

调整完的首页长这样：

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/LBrX00GQeicvPAwKkOfBX8q9vDYjTpsZnfoF2yObeW6cAIqjQv3ia8PZNYXwSl8tPfQeZKCHkWHxuCW4icJhYnxGw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

**二、内页**  

**2.1、内页预览**

以“China Phone Number Generator”为例，先给大家看下内页长这样：

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/LBrX00GQeicvPAwKkOfBX8q9vDYjTpsZnobvNJ5ltiarHNXowFwle9ibCib1c0IGoDYfD6G1daFItianFvoWfpfNGAQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

**2.2、标题和描述**

先说标题和描述，先自己大概写一下：

```
<title>China Phone Number Generator, Generate China Phone Number</title>
```

然后让GPT4生成符合SEO要求的且更自然的标题和描述：  

```
<title>China Phone Number Generator - Generate Authentic & Random Chinese Numbers</title>
```

**2.3、内页h1**

内页 h1 如下：  

```
<section>
```

这里我们直接用了首页的 section 样式，在 main 的第一个 section 中写 h1 和一些介绍。  

**2.4、生成电话号码功能**  

接着第二个 section 提供生成电话号码功能：  

```
<section>
```

每点击一次按钮，就生成一个新的号码，并且不断添加到底部，也就是说可以生成一个号码列表，需要用 js 配合生成符合格式的号码：  

```
<script>
```

这里为了用户体验，还可以增加一次生成10个号码、50个号码的按钮，限于篇幅今天我们不放相关代码出来，有需要直接找GPT生成就可以。  

**2.5、增加更多关于关键词的h2**

在生成电话号码功能下方，我们让GPT基于我们提供的一些关键词，生成更多关于内页关键词的 seation ，每一个 section 都是一个 h2 。

我们先导出 Semrush 中跟当前内页关键词相关的更多关键词。  

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/LBrX00GQeicvPAwKkOfBX8q9vDYjTpsZn4KibiaxDCRUMezUDryUpQAA2OCbXxDW7LFJib7TBh3QQA5JtVvkNJicyfA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

然后提供关键词列表给GPT4，让AI生成指定格式的 section，部分生成后的代码如下：  

```
<section>
```

对应页面效果如下：

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/LBrX00GQeicvPAwKkOfBX8q9vDYjTpsZnhNIsDjwtqVYk9SSOuNrxpOS7d2zbn92lFAalYaQtkEplbjIhUkXicJg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

**2.6、生成更多内页**

按照同样的方法，生成其它9个国家的内页，注意每个国家的电话号码格式都不一样，直接让GPT生成相关js代码就好。  

我们举例说明的这个工具站页面结构更简单，只需要首页给每个内页增加内链，内页给首页给增加内链就行。  

至此我们的代码网站代码就都写完了，目前的语言默认是英文，下一步我们还需要给网站增加多语言支持，这部分内容在明天的推文中介绍。

再下一步是注册域名，然后部署到Vercel，并且用 Cloudflare 包一层，既能加速又能保护源站。

再下一步是提交到谷歌Search Console后台，并且增加谷歌统计代码。  

欢迎关注哥飞公众号，接收后续文章推送。

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

  

养网站防老130

出海47

ChatGPT19

seo50

养网站防老 · 目录

上一篇养网站防老：网站可以做成一生的事业下一篇【6000字详解】养网站防老第6步：利用ChatGPT给网站增加多语言支持

​

![](https://mp.weixin.qq.com/mp/qrcode?scene=10000004&size=102&__biz=MjM5OTIzMzYyMA==&mid=2650080739&idx=1&sn=1685ea0a11d983c256820d49ef197446&send_time=)

微信扫一扫  
关注该公众号