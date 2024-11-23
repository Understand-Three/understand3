---
title: 搜索引擎如何工作的以及你为什么要在意？
aliases:
  - 搜索引擎如何工作的以及你为什么要在意？
original: https://ahrefs.com/blog/zh/how-do-search-engines-work/
tags:
  - ahrefs
  - SEO
draft: true
---
搜索引擎通过使用叫做蜘蛛的爬虫程序来进行抓取工作。这些网络爬虫能有效地跟踪页面之间的链接，以查找要添加到索引中的新内容。使用搜索引擎时，将从索引中提取相关结果，并使用算法对其进行排名。

如果听起来很复杂，那是因为事实如此。但是，如果你想[在搜索引擎中排名更高](https://ahrefs.com/blog/zh/how-to-rank-higher-on-google/)以使你的网站获得更多点击量，则需要对搜索引擎是如何查找、索引、排名的原理有基本的了解。

这就是你将在本指南会学到的内容。


# 一、搜索引擎基础

在介绍技术之前，首先要确保我们了解搜索引擎的真正含义，它们为什么存在、以及为什么它很重要。

## 搜索引擎是什么？

搜索引擎是用于查找和排名与用户搜索匹配的 Web 内容的工具。 

每个搜索引擎都包含两个主要部分：

1. **搜索索引**，有关网页信息的数字图书馆。
2. **搜索算法**，匹配搜索并进行排名的计算机程序。

热门搜索引擎有 Google、Bing、以及 DuckDuckGo。

## 搜索引擎的目的是什么？

每个搜索引擎都旨在为用户提供最佳、最相关的结果。至少从理论上讲，这就是他们获取或维持市场份额的方式。

![img](https://ahrefs.com/blog/zh/wp-content/uploads/2021/06/01-how-search-engines-work-zh.png)

## 搜索引擎如何盈利？

搜索引擎具有两种类型的搜索结果：

- **自然排名结果**，你无法付费获取。
- **付费排名结果**，你可以付费获取。

![img](https://ahrefs.com/blog/zh/wp-content/uploads/2021/06/02-how-search-engines-work-zh.png)

每次有人点击付费搜索结果时，广告客户都会向搜索引擎付费。这就是所谓的按点击付费（[PPC](https://docs.pingcode.com/ask/326952.html)）广告。

这就是为什么市场份额很重要。更多的用户意味着更多的广告点击和更多的收入。

## 你为什么要关心搜索引擎的工作方式？

了解搜索引擎如何查找内容，索引、排名可以帮助你更好的对关键词进行优化、排名。

如果你可以在这些搜索中排名靠前，则你的内容将获得更多点击和自然流量。

![img](https://ahrefs.com/blog/zh/wp-content/uploads/2021/06/02-seo-basics-zh.png)

## 哪个是最受欢迎的搜索引擎？

谷歌，[它拥有92％的市场份额](https://gs.statcounter.com/search-engine-market-share)。

![img](https://ahrefs.com/blog/zh/wp-content/uploads/2021/06/03-how-search-engines-work-zh.png)

Google 是大多数 SEO 专业人员和站长最关心的搜索引擎，因为与其他任何搜索引擎相比，Google 都有可能以更多的方式给你带来流量。

> [!NOTE] 进阶
> - [7个替代谷歌的搜索引擎](https://ahrefs.com/blog/alternative-search-engines/)
> - [SEO与PPC：你应该使用哪个？](https://ahrefs.com/blog/zh/seo-vs-ppc/)






# 二、搜索引擎是如何建立索引的

最著名的搜索引擎，例如 Google 和 Bing，其搜索索引中有数万亿个页面。因此，在讨论排名算法之前，让我们更深入地研究用于构建和维护 Web 索引的机制。

这是 [Google 提供的基本流程](https://developers.google.com/search/docs/guides/javascript-seo-basics)：

![img](https://ahrefs.com/blog/zh/wp-content/uploads/2021/06/04-how-search-engines-work-zh.png)

分解之后就是：

1. URL
2. 抓取
3. 处理 & 渲染
4. 索引

小提示：

 这个过程专门适用于 Google，但对于其他网络搜索引擎（如 Bing）来说，可能非常相似。还有其他类型的搜索引擎，例如 Amazon，YouTube 和 Wikipedia，它们仅显示其内部的页面结果。

## 步骤 1：URL

一切都始于已知的 URL 列表。 Google 通过各种方法发现了这些，但是最常见的三种是：

### 通过外链

Google 已经有一个包含数万亿个网页的索引库。如果某人在这些页面中添加了一个链接指向了自己的网站，那么 Google 可以从那些页面中找到链接。

你可以使用 [Ahrefs Webmaster Tools](https://ahrefs.com/zh/webmaster-tools)（Ahrefs 站长）中免费的 [Site Explorer](https://ahrefs.com/zh/site-explorer)（网站分析）去查看网站的外链。

1. 注册免费的 Ahrefs Webmaster Tools（Ahrefs站长）账号
2. 将你的网站放入 [Site Explorer](https://ahrefs.com/zh/site-explorer)（网站分析）
3. 进入**外链**报告。

![img](https://ahrefs.com/blog/zh/wp-content/uploads/2021/06/1-ahrefs-site-explorer.jpg)

我们的爬虫程序是[第二活跃的仅次于 Google](https://www.imperva.com/blog/most-active-good-bots/)。因此你应该在此处看到相当完整的[外链](https://ahrefs.com/blog/zh/what-are-backlinks/)数据报告。

### 来自网站地图

站点地图列出了你网站上的所有重要页面。如果你将站点地图提交给 Google，则可以帮助他们更快地找到你的网站。

### 来自 URL 提交

Google 还允许通过 Google Search Console 提交单个 URL。

## 步骤 2：抓取

抓取是一种称为蜘蛛的抓取程序（例如 [Googlebot](https://developers.google.com/search/docs/advanced/crawling/googlebot)）访问并下载发现的页面的地方。

重要的是要注意，Google 并不总是按照发现页面的顺序对其进行抓取。

Google 会根据以下因素对要抓取的 UR L进行排序，其中包括：

- URL 的 PageRank
- URL 多久更改一次
- 是否是新的

这很重要，因为这意味着搜索引擎可能会在某些页面之前对其他页面进行抓取和索引。如果你的网站很大，搜索引擎可能需要一段时间才能完全抓取它。

## 步骤 3：处理

Google 会在处理过程中从抓取的页面中提取关键信息。 Google 以外的人都不知道有关此过程的细节，但是我们认位重要部分是提取链接和存储内容并进行索引。

Google 必须渲染页面以对其进行完全处理，而 Google 会运行页面的代码以了解外观对用户的影响。

也就是说，在渲染之前和之后都会进行一些处理——如你在图中所看到的。

## 步骤 4：索引

索引是将抓取页面中的信息添加到叫做搜索索引的大型数据库中。本质上，这是一个由数万亿个网页组成的数字图书馆，Google 的搜索结果都来自于此。

这是重要的一点。当你在搜索引擎中搜索时，你并不是直接匹配互联网上的结果。而是在搜索搜索引中进行匹配的。如果网页不在搜索索引中，则搜索引擎用户将找不到它。这就是为什么让你的网站在 Google 和 Bing 等主要搜索引擎中建立索引如此重要。 

>[!NOTE] 进阶
> - [什么是外链](https://ahrefs.com/blog/zh/what-are-backlinks/)
> - [如何创建 XML 网站地图](https://ahrefs.com/blog/zh/how-to-create-a-sitemap/)
> - [PageRank: 入门指南](https://ahrefs.com/blog/zh/google-pagerank/) 


# 搜索引擎如何对网页进行排名

发现，抓取和索引内容仅仅是流程的第一部分。搜索引擎还需要一种在用户执行搜索时匹配结果的排名的方法。这是就搜索引擎算法用处。

每个搜索引擎都有用于对网页进行排名的独特算法。但是，由于 Google 是迄今为止使用最广泛的搜索引擎（至少在西方世界），因此在本指南的其余部分中，我们将重点关注该引擎。

Google 有 200 多个排名因素。

没有人知道所有的这些排名因素，但是关键因素却是已知的。

让我们讨论其中的一部分：

- 外链
- 相关性
- 新鲜度
- 话题权威性
- 页面速度
- 移动友好

## 外链

外链是 Google 最重要的排名因素之一。

Google 的搜索质量高级策略师 Andrey Lipattsev 在2016年的一次在线网络研讨会上证实了这一点。当被问到两个最重要的排名因素时，他的[回答](https://youtu.be/l8VnZCcl9J4?t=1827)很简单：**内容**和**链接**。

> 可以。我可以告诉你它们是什么（排名前两个的因素）。一个是内容。一个是它是指向你网站的链接.

自 1997 年链接引入 PageRank 以来，它一直是 Google 中重要的排名因素，PageRank 是一种根据指向外链**数量**和**质量**来判断网页价值的公式。

![img](https://ahrefs.com/blog/zh/wp-content/uploads/2021/06/05-how-search-engines-work-zh.png)

我们[分析了](https://ahrefs.com/blog/zh/search-traffic-study/)超过 10 亿个页面，并发现链接到该页面的网站数量与它从 Google 获得的自然流量之间有着明显的相关性。

![img](https://ahrefs.com/blog/zh/wp-content/uploads/2021/06/06-how-search-engines-work-zh.png)

但是，这并不只关乎数量，因为并非所有外链都是一样的。具有少量高质量外链的页面完全有可能胜过具有许多低质量外链的页面。

良好的外链具有六个关键属性。

![img](https://ahrefs.com/blog/zh/wp-content/uploads/2021/06/07-how-search-engines-work-zh.png)

让我们仔细研究一下两个最重要的部分：**权重**和**相关性**。

### 链接权重

来自高权威页面外链通常对排名影响最大。

你如何定义权重？在 SEO 中，有权重的页面和网站是具有许多外链（或“投票”）。

![img](https://ahrefs.com/blog/zh/wp-content/uploads/2021/06/08-how-search-engines-work-zh.png)

在 Ahrefs 中，我们有两个指标来估算网站和页面的相对权重：

- **网站评分（Domain Rating）**: 网站的权重指标，范围为 0–100。
- **网址评分 （URL Rating）**: 页面的权重指标，范围为 0–100。

你可以在 Ahrefs [Site Explorer](https://ahrefs.com/zh/site-explorer)（网站分析）中检查任何网站或网页的权重。

![img](https://ahrefs.com/blog/zh/wp-content/uploads/2021/06/2-seo-tips.png)

### 链接相关性

来自相关网站和网页的链接通常是最有价值的。

![img](https://ahrefs.com/blog/zh/wp-content/uploads/2021/06/09-how-search-engines-work-zh.png)

Google 在讨论[搜索是如何工作的时候](https://www.google.com/intl/en_us/search/howsearchworks/)，就说到了相关性对页面影响。



> 如果**该主题**上的其他知名的网站都链接到了该页面，则表明该页面上的信息是高质量的。

如果你想知道相关性为何重要，请考虑一下现实世界中的事物是如何运作的。在寻找最好的意大利餐厅时，你可能会相信厨师朋友的建议而不是兽医朋友的建议。但是，如果你正在寻找猫粮推荐，那就另当别论了。

## 相关性

Google 有很多确定页面相关性的方法。 

最基本的，它将查找包含与搜索词相同的关键词的页面。

![img](https://ahrefs.com/blog/zh/wp-content/uploads/2021/06/3-google-guidelines.png)

但是相关性不仅仅只有关键词匹配。

Google 还使用交互数据来评估搜索结果是否与搜索词相关。换句话说，就是用户觉得页面对自己有帮助吗？

![img](https://ahrefs.com/blog/zh/wp-content/uploads/2021/06/4-google-guidelines.png)

例如 “苹果” 的所有排名靠前的结果都与技术公司有关，而不是水果。 Google 从互动数据中知道大多数用户正在寻找前者而不是后者的信息。

不过，互动数据远非 Google 做到这一点的唯一方法。

Google 已经投资了许多技术来帮助理解诸如人、地点、事物之类的实体之间的关系。知识图谱是这些技术之一，本质上是一个巨大的实体之间关系的知识库。

苹果（水果）和苹果（技术公司）都是知识图中的实体。

Google 使用实体之间的关系来更好地了解页面的相关性。谈论橙子、香蕉的“苹果”的匹配结果显然是关于水果的。但是谈论 iPhone、iPad、和iOS的人显然是关于这家技术公司的。

归功于“知识图谱”，Google 可以超越关键词匹配的限制。

有时，你甚至可能会看到搜索结果中没有提及搜索中看似重要的关键词。例如，以 “apple paper app” 的第二个结果为例，该结果在页面上的任何地方都没有提及 “apple” 一词。

![img](https://ahrefs.com/blog/zh/wp-content/plugins/a3-lazy-load/assets/images/lazy_placeholder.gif)

谷歌之所以知道这是一个相关的结果，部分是因为它在知识图谱中提到了与苹果密切相关的实体，例如 iPhone，以及 iPad。

小提示.

 互动数据和知识图谱并不是 Google 用来了解页面与搜索词相关性的唯一技术。许多工作是使用诸如 BERT 和 RankBrain 之类的技术来理解搜索词本身背后的含义和意图来完成的。

## 新鲜度

新鲜度是基于搜索词的排名因素，这意味着它对某些结果的影响比对其他结果的影响更大。

对于 “what’s new on amazon prime” 这样的搜索，新鲜度很重要。因为搜索者想了解最近添加的电影和电视节目。这可能就是 Google 给新发布或新更新的页面排名更高的原因。

![img](https://ahrefs.com/blog/zh/wp-content/plugins/a3-lazy-load/assets/images/lazy_placeholder.gif)

对于诸如 “best headphones” 之类的搜索，新鲜度也重要，但不是最重要的。因此 2015 年的页面可能不太适合，但是 2–3 个月前发布的帖子仍然有用。

Google 知道这一点，并显示了在过去几个月中更新或发布的结果。

![img](https://ahrefs.com/blog/zh/wp-content/plugins/a3-lazy-load/assets/images/lazy_placeholder.gif)

也有一些查询结果的新鲜度与无关，例如 “how to tie a tie”。因为方法没有任何变化，因此搜索结果是昨天还是 1998 年都无关紧要。Google 知道这一点，并且对多年前发布的文章进行排名没有任何问题。

![img](https://ahrefs.com/blog/zh/wp-content/uploads/2021/06/8-how-to-tie-a-tie.png)

## 话题权威性

Google 希望对具有该话题权威的网站的内容进行排名。这意味着 Google 可能会将网站本生视为评价搜索结果质量的标准。 

Google 在[其专利中](https://www.seobythesea.com/2017/05/how-does-google-look-for-authoritative-search-results/)谈到了这一点：



> 搜索系统是否认为网站具有权威性通常取决于搜索词。 `[…]` 搜索系统可以将疾病控制中心（cdc.gov）的站点视为 “CDC mosquito stop bites” 搜索的权威站点，但可能不会将其视为对 “restaurant recommendations” 搜索的权威站点。

尽管这只是 Google 申请的众多专利之一，但我们发现有证据表明，对于许多搜索而言，“话题权威性” 在搜索结果中很重要。 

只需查看 “sous vide vacuum sealer” 的结果就知道。 

![img](https://ahrefs.com/blog/zh/wp-content/uploads/2021/06/9-sous-vide-vacuum-sealer.png)

在这里，我们看到了两个小型的利基网站，其排名都超过了《纽约时报》。

尽管毫无疑问，这里还有其他因素在起作用，但 “话题权威性” 应该是这些网站排名的原因之一。

这可能就是为什么 Google 的 [SEO 入门指南](https://developers.google.com/search/docs/beginner/seo-starter-guide)告诉站长：

> *在特定领域内以专业知识和可信赖度赢得声誉。*

## 页面速度

没有人喜欢等待页面加载，而 Google 知道这一点。因此，他们将网页速度列为 [2010](https://webmasters.googleblog.com/2010/04/using-site-speed-in-web-search-ranking.html) 年台式机搜索和 [2018](https://webmasters.googleblog.com/2018/01/using-page-speed-in-mobile-search.html) 年移动搜索的排名因素。

许多人执迷于页面速度，值得注意的是，你的页面排名无需闪电般快速。谷歌表示，只有你页面速度过慢时才需要考虑速度问题。

换句话说，在网站上节省几毫秒的时间不太可能提高排名。它只需要足够快就不会对用户产生负面影响。

你可以在 [PageSpeed Insights](https://developers.google.com/speed/pagespeed/insights/) 中检查任何网页的速度，同时还有速度优化的建议。

![img](https://ahrefs.com/blog/zh/wp-content/uploads/2021/06/10-pagespeed-insights.png)

PageSpeed Insights 还显示了有关[核心页面指标](https://ahrefs.com/blog/zh/core-web-vitals/)信息。

核心页面指标由三个指标组成，用来评估网页的加载性能、交互性、以及视觉稳定性。谷歌已经确认，核心页面指标将在 [2021 年 6 月](https://developers.google.com/search/blog/2021/04/more-details-page-experience)成为排名要素之一。

你可以使用 Google Search Console 中的核心页面指标报告查看网站上所有页面的效果。 

![img](https://ahrefs.com/blog/zh/wp-content/uploads/2021/06/11-google-search-console.png)

如果许多 URL 的性能不佳或需要改进，请及时与开发人员联系。

## 移动端友好

65％ 的 Google [搜索发生在移动设备上](https://www.seroundtable.com/google-mobile-searches-now-65-of-all-searches-28003.html)。因此，自2015年以来，移动设备友好性就成为移动设备搜索排名的一个重要因素。

自 2019 年以来，由于 Google 改用[移动设备优先索引](https://developers.google.com/search/mobile-sites/mobile-first-indexing)技术，移动设备友好性也是成为了桌面搜索的排名因素。这意味着 Google 在所有设备上 “主要将内容的移动版本用于索引和排名”。

换句话说，移动不友好性可能会影响排名。

你可以使用 Google 的[移动设备友好测试工具](https://search.google.com/test/mobile-friendly)或 Google Search Console 中的**移动设备可用性**报告来检查任何网页的移动设备友好性问题。

![img](https://ahrefs.com/blog/zh/wp-content/uploads/2021/06/12-mobile-usability.png)

> [!NOTE] 进阶
> - [10个不容忽视的 Google 排名因素](https://ahrefs.com/blog/zh/google-ranking-factors/)
> - [Google 知识图详解](https://ahrefs.com/blog/google-knowledge-graph/)
> - [核心网页指标详解](https://ahrefs.com/blog/zh/core-web-vitals/)
> - [如何在20分钟内提升 WordPress 网站的速度](https://ahrefs.com/blog/zh/speed-up-wordpress/)




# 搜索引擎是如何个性化搜索结果的

搜索引擎了解不同的结果会吸引不同的人。这就是为什么他们为每个用户量身定制了搜索结果。

如果你曾经在多个设备或浏览器上搜索相同的内容，则可能已经看到了这种个性化的效果。结果通常会根据各种因素而出现在不同的位置。

由于这种个性化，如果你要进行 SEO，最好使用 Ahrefs [Rank Tracker](https://ahrefs.com/zh/rank-tracker)（排名跟踪）之类的专用工具来跟踪排名。这些工具中所报告的排名位置可能更接近真实情况，因为它们不太可能会产生个性化的结果。

搜索引擎如何个性化结果的？

Google [指出](https://www.google.com/intl/en_uk/search/howsearchworks/algorithms/)：“诸如你的地理位置、过去的搜索历史、和搜索设置之类的信息都可以帮助 [我们] 用最有用和最相关的信息来定制你的结果。

让我们详细说这三点：

## 1. 位置

如果你搜索 “italian restaurant” 之类的内容，则地图包中的所有结果均为本地的餐厅。

![img](https://ahrefs.com/blog/zh/wp-content/uploads/2021/06/13-italian-restaurant.jpg)

Google 之所以这么推荐，是因为你不太可能飞到另一头去吃午饭。

Google 也会使用你的位置来个性化除地图之外的搜索结果。如果我们向下搜索 “italian restaurant”，甚至 TripAdvisor 的结果都是个性化的，并且我们看到许多排名高的搜索结果都是本地餐厅的网站。

![img](https://ahrefs.com/blog/zh/wp-content/uploads/2021/06/14-italian-restaurant.jpg)

对于类似 “buy a house” 这样的搜索，情况与此类似。 Google 会返回本地的列表而不是其他国家的列表页面，因为你太可能迁移到其他国家/地区。

![img](https://ahrefs.com/blog/zh/wp-content/uploads/2021/06/15-buy-a-house.png)

你的位置会极大地影响本地查询的结果，以至于从两个不同的位置搜索同一词时几乎没有相同的结果。

## 2. 语言

Google 知道向西班牙用户显示英语结果毫无意义。因此，Google 分别对[ YouTube SEO 教程](https://ahrefs.com/blog/zh/youtube-seo/)文章的英语版（英语搜索）和西班牙语版（西班牙语）进行排名。

![img](https://ahrefs.com/blog/zh/wp-content/plugins/a3-lazy-load/assets/images/lazy_placeholder.gif)
![](https://ahrefs.com/blog/zh/wp-content/uploads/2021/06/16-youtube-seo.png)

![](https://ahrefs.com/blog/zh/wp-content/uploads/2021/06/17-seo-en-youtube.png)

![img](https://ahrefs.com/blog/zh/wp-content/plugins/a3-lazy-load/assets/images/lazy_placeholder.gif)

但是，谷歌在某种程度上依赖于网站站长去做分割。如果你有多种语言的网页，除非你告诉 Google，否则 Google 可能不会意识到这种情况。 

你可以使用称为 [hreflang](https://ahrefs.com/blog/zh/hreflang-tags/) 的 HTML 属性来执行此操作。 

Hreflang 有点复杂，远远超出了本指南的范围。原理上，它只是一小段代码，用于指示同一页面的不同语言版本之间的关系。

## 3. 搜索历史

Google 会使用搜索历史记录来个性化搜索结果。最明显的例子可能是，当下次运行相同的搜索时，它会将先前点击的搜索结果 “排名” 更高。

当然它并非总是会发生，但它似乎很普遍——特别是如果你在短时间内多次单击或访问该页面。

# 总结

了解搜索引擎的工作方式是迈向获取更高的 Google  排名、并获得更多流量的第一步。如果搜索引擎无法找到、抓取、索引你的页面，那么你可能一开始就失败了。

如果你想知道如何开始针对 SEO 优化你的网站，请阅读我们的[SEO基础指南](https://ahrefs.com/blog/zh/seo-basics/)。

有问题吗？在 [Twitter](https://twitter.com/joshuachardwick?lang=en) 上找我吧。 

*译者，**[Park Cheng](https://park.mobayke.com/)**，魔贝课凡联合创始人。*

![Joshua Hardwick](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20210%20140%22%3E%3C/svg%3E)

文章作者

Joshua Hardwick

贡献者

![Patrick Stox](https://ahrefs.com/blog/zh/wp-content/plugins/a3-lazy-load/assets/images/lazy_placeholder.gif)

![Sam Oh](https://ahrefs.com/blog/zh/wp-content/plugins/a3-lazy-load/assets/images/lazy_placeholder.gif)

Ahrefs内容营销总监。他负责确保我们发布的每篇文章都是神作。

搜索

中文

© 2024 [Ahrefs Pte Ltd.](https://ahrefs.com/)

PICK A TOPIC

SEO

- [SEO 总汇](https://ahrefs.com/blog/zh/category/general-seo/)
- [关键词研究](https://ahrefs.com/blog/zh/category/keyword-research/)
- [页面 SEO](https://ahrefs.com/blog/zh/category/on-page-seo/)
- [链接建设](https://ahrefs.com/blog/zh/category/link-building/)
- [技术 SEO](https://ahrefs.com/blog/zh/category/technical-seo/)
- [本地 SEO](https://ahrefs.com/blog/zh/category/local-seo/)

市场营销

- [营销总汇](https://ahrefs.com/blog/zh/category/marketing/)
- [内容营销](https://ahrefs.com/blog/zh/category/content-marketing/)
- [分销营销](https://ahrefs.com/blog/zh/category/affiliate-marketing/)
- [付费营销](https://ahrefs.com/blog/zh/category/paid-marketing/)
- [视频营销](https://ahrefs.com/blog/zh/category/video-marketing/)

[数据与研究 ](https://ahrefs.com/blog/zh/category/data-studies/)

AHREFS TOOLS

Core Tools

- [网站分析](https://ahrefs.com/zh/site-explorer)
- [关键词分析](https://ahrefs.com/zh/keywords-explorer)
- [内容分析](https://ahrefs.com/zh/content-explorer)
- [网站诊断](https://ahrefs.com/zh/site-audit)
- [排名监控](https://ahrefs.com/zh/rank-tracker)

Free Tools

- [外链检查](https://ahrefs.com/zh/backlink-checker)
- [网站权威检查](https://ahrefs.com/zh/website-authority-checker)
- [关键词排名检测](https://ahrefs.com/zh/keyword-rank-checker)
- [失效链接检查](https://ahrefs.com/zh/broken-link-checker)
- [SERP 检查](https://ahrefs.com/zh/serp-checker)
