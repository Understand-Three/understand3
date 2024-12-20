---
title: 再聊多语言：为什么不建议使用子域名而更建议使用子目录
aliases:
  - 再聊多语言：为什么不建议使用子域名而更建议使用子目录
tags:
  - SEO
  - 哥飞SEO教程
draft: true
original: https://mp.weixin.qq.com/s/UEx5DT7m_pGYQYclnTqxgg
---

原创 我是哥飞 哥飞 _2024年02月17日 19:02_ _广东_

大家好，我是哥飞。  

上一篇文章还是大年初二写的，之后一直在休息，昨天回到深圳了，今天初八，开工了。  

先祝大家开工大吉，万事顺意，出海起飞，流量多多，美元多多！  

关于多语言，其实哥飞之前写了好几篇文章了：  

1. [他给博客增加多语言支持后，访问量增加了10倍](http://mp.weixin.qq.com/s?__biz=MjM5OTIzMzYyMA==&mid=2650080629&idx=1&sn=7cb843cbd5e1c673d1e10583465b1edd&chksm=bf3f344e8848bd58e467bd56210a13e0024218491b654b92d556dce2956ce8181d2efa77da4b&scene=21#wechat_redirect)  
    
2. [【6000字详解】养网站防老第6步：利用ChatGPT给网站增加多语言支持](http://mp.weixin.qq.com/s?__biz=MjM5OTIzMzYyMA==&mid=2650080755&idx=1&sn=27c8b30bcbf77d6e9aeea6469ca3c118&chksm=bf3f34c88848bddeedc07dc6529718c8a05b2befb5432b6907bd4a3bbbd44f451c9bcf4c32d5&scene=21#wechat_redirect)  
    
3. [从一个月访问量7.8亿的网站告诉你子域名和子目录该如何选择](http://mp.weixin.qq.com/s?__biz=MjM5OTIzMzYyMA==&mid=2650080225&idx=1&sn=15d079557ecf072df36e6b078085d384&chksm=bf3f32da8848bbcc930c56986384a5e2ae0adf2e99bcebc5974efcd51c07d08fe609a5028a55&scene=21#wechat_redirect)  
    
4. [【5800字长文】从网站站内优化到部署上线再到推广运营一篇文章让你学明白](http://mp.weixin.qq.com/s?__biz=MjM5OTIzMzYyMA==&mid=2650080101&idx=1&sn=477191907e388aff6df3f16c915056d8&chksm=bf3f325e8848bb48e682193cc0bef2c42e25900fb2ca02987b5a854892bb3cb88c540e9492b6&scene=21#wechat_redirect)
    
5. [别人做过的产品我还能不能做？哥飞告诉你，还能做](http://mp.weixin.qq.com/s?__biz=MjM5OTIzMzYyMA==&mid=2650080128&idx=1&sn=1e3008e113c5e1a537057f361a0aa017&chksm=bf3f32bb8848bbad590c3a20757db7330f3136bf825d64a2a7cd915b8503a8a681b24c02200c&scene=21#wechat_redirect)
    
6. [为什么俄罗斯版妙鸭相机即使拿下1840万月访问量，也主要只在几个国家火？哥飞告诉你答案](http://mp.weixin.qq.com/s?__biz=MjM5OTIzMzYyMA==&mid=2650080214&idx=1&sn=6bec8257bc6b77b8fdc3a33272bc0cc1&chksm=bf3f32ed8848bbfb1303701b2f64b2b20667812727d3367f2edb7707c257f0596815f9662e90&scene=21#wechat_redirect)  
    

  

最近社群里的有新朋友继续提问，为什么不建议用子域名做多语言？

哥飞的回答是，谷歌其实会把每一个域名当作一个独立的网站，同一个域名下的多个子域名也会当成不同的网站。每一个网站在谷歌那里都是从零开始积累权重的，如果我们用子域名做多语言，如果有10个语言需要支持，就相当于你需要从零开始冷启动10个网站，相对于子目录形式，你的难度和工作量立马乘10。  

假设域名是 abc.com ，那么甚至 abc.com 和 www.abc.com 在谷歌眼里也是两个网站，所以我们需要选定一个域名作为我们网站的主域名，然后把另一个域名301跳转到主域名。  

哥飞建议大家选择 abc.com 作为主域名，然后把 www.abc.com 301 跳转到 abc.com 。

为什么呢？

因为现在大多数用户已经习惯了输入无 www 的域名直接访问了，在别的地方介绍你的产品给你留下链接时也会直接留下无 www 的形式。  

那么在谷歌眼里，是无 www 形式的网站反向链接加一，也就是 abc.com 的权重增加了，如果你的主域名就是 abc.com ，那么权重直接就加到了你的网站上。

而假设你选择的主域名是 www.abc.com ，那么虽然 abc.com 通过 301 跳转把权重传递过来了一部分，但是也不可能全部传递，所以你的反向链接带来的效果其实就打了折扣了，换句话说就是你的反向链接被浪费掉了。

那么有人可能会问，你怎么证明你这个猜测呢？为什么你会认为每一个子域名在谷歌眼里都是单独积累权重的呢？

其实举三个例子就很容易明白了。  

**第一个例子**，Ahrefs 的反向链接检测工具检测的就是你输入的域名的反向链接，当你输入 abc.com 时，www.abc.com 的链接不会出现在结果列表里。  

https://ahrefs.com/backlink-checker/

**第二个例子**，Google Search Console 里，每一个子域名都需要单独添加，你可以同时添加 abc.com 和 www.abc.com 。  

甚至同一个子域名的 http 和 https 在谷歌眼里也是两个不同的网站，所以我们也需要把 http 通过 301 跳转到 https 。

**第三个例子**，假设所有的子域名共享权重，那么会乱套的。

这里哥飞拿 github.io 这个域名来举例说明，这是 Github 提供给开发者使用的免费域名，所有的 Github pages 部署的网站，都默认有一个 github.io 的子域名。

有很多 Github pages 网站都已经运行很多年了，拿到了很多反向链接，假设谷歌默认所有子域名都共享反向链接权重，那么我现在如果想要拿到某个词的排名，直接去创建一个新的 Github pages 站点，就相当于在高权重域名下做一个新词，很容易就因为高权重而拿到了排名，这不就乱套了吗。  

综上所述，谷歌不可能会共享不同子域名的权重，所以我们做多语言时，就需要用子目录形式，而不是子域名形式。

另外多说一句哈，对于一些特别高权重的域名的子域名，谷歌的确也会给一个初始的权重，但不会太高。如维基百科开了一个新的子域名做的网站，谷歌默认就会比较信任这个网站。  

另外再说一句，既然高权重域名的子域名不行，那么高权重域名的内页是否可行呢？  

哥飞告诉你，这是可行的，并且哥飞之前就跟社群里朋友们详细介绍了这种用法。

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

除了以上平台，还有哪些平台能够让我们创建内页呢？  

欢迎加入哥飞的付费社群“哥飞的朋友们”，里边就会有你想要的答案。

社群目前暂时是微信群形态，有一个配套的网站，已上线第一版，社群内朋友可见。

  

社群主要面向技术开发者、产品经理、设计师等人群，大家一起讨论独立开发、出海产品、流量获取、流量变现等话题。

  

社群讨论的话题主要是围绕着网站来的，用网站来承接流量，然后变现。

  

 那么就要考虑做什么网站，所以需要去挖掘需求。

  

然后去搞流量，可以是SEO，也可以是发帖宣传推广，还可以是付费软文。

  

有了流量之后就得考虑如何变现，可以是广告变现，也可以是联盟导购，更可以直接向用户收费。

  

社群目前超过1000人，新的一期开始了，这期哥飞将带着大家实战，每个月都会安排任务，推着大家前进，让大家能够赚钱。

  

目前888元优惠价已经结束，前两天已经正式涨价为999元了。

  

社群按照365天计时，也就是你今天加入后，明年今日到期。

  

前两期讨论很活跃，行动很迅速，大家已经做了上百个产品了。 

  

有的几人小团队已经用几个月时间从零开始做到了月收入4万美元以上，还有的单人实现了月收入几千美元。

  

这个社群7月2号开始运营的，到今天7个多月时间里，主要讨论了以下话题：

1、建站基础，如何快速做一个网站；

2、SEO基础，如何优化网站；

3、推广基础，如何宣传推广网站；

4、运营基础，如何运营好一个网站；

5、Adsense基础，如何靠谷歌Adsense赚广告费；

6、一些工具使用经验分享，如Semrush分析别的网站流量和出入站链接，Similarweb如何看流量；

7、基于Semrush、Similarweb等工具，如何去发掘新需求，发现新网站；

8、实战经验，如何去抓住新词热词做网站，从搜索引擎获取流量。

  

以上所有讨论都沉淀到了社群配套网站 web.cafe 上，所以第三期大家一进群就可以看到前两期的精华内容，以及其他更多相关话题。

  

欢迎加哥飞微信 qiayue 加入社群大家一起出海赚美元。

  

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

  

养网站防老130

养网站防老 · 目录

上一篇【哥飞推荐】假期可以带着孩子们一起玩的编程小游戏，培养逻辑思维能力，养网站防老从娃娃抓起下一篇推荐一个能让你在 Sora API 发布之前就上线网站接住泼天流量的开源 Sora Web 客户端 SoraWebui

​

![](https://mp.weixin.qq.com/mp/qrcode?scene=10000004&size=102&__biz=MjM5OTIzMzYyMA==&mid=2650082091&idx=1&sn=c067c1b413e900726c8598529c2c0bdc&send_time=)

微信扫一扫  
关注该公众号