---
title: 技术 SEO 初学者指南
aliases:
  - 技术 SEO 初学者指南
original: https://ahrefs.com/blog/zh/technical-seo/
tags:
  - SEO
  - ahrefs
draft: true
---
技术 SEO 曾经是 SEO 中最重要的部分。页面需要可被抓取，可索引，才有机会获得排名。但与内容和链接相比，现在许多的要素对SEO的影响微乎其微。

我们编写了这份初学者指南，以帮助你了解一些基础知识，以及最好将时间花在那些能最大程度地发挥影响的要素上。整篇文章链接了很多其他资源，最后还有更多资源供你了解更多信息。

让我们开始吧。



# 一、技术 SEO 基础

由于这是初学者指南，让我们从基础开始。

## 什么是技术 SEO

技术 SEO 是优化你的网站以帮助 Google 等搜索引擎查找、抓取、理解和索引你的网页。目标是让搜索引擎找到并提高排名。

## 技术 SEO 有多复杂？ 

看情况。基础知识并不难掌握，但技术 SEO 可能很复杂且难以理解。我将通过本指南使事情尽可能的简单。

---

![](https://ahrefs.com/blog/wp-content/uploads/svg/spider_icon.svg)

Part 2

# 二、理解抓取

在本章中，我们将介绍如何确保搜索引擎能够有效地抓取你的内容。

## 抓取的工作原理

爬虫从页面抓取内容并使用这些页面上的链接来查找更多页面。这让他们可以在互联网上找到更多内容。这个过程中有一些机制需要讨论。

![](https://ahrefs.com/blog/zh/wp-content/uploads/2021/07/Untitled-75.png)

来源：[Google](https://developers.google.com/search/docs/guides/javascript-seo-basics)

### URL 来源

爬虫必须从某个地方开始。通常，他们会创建一个列表，列出他们通过页面找到的所有 URL。另外一个机制就是通过用户或具有页面列表的各种系统创建的[站点地图](https://ahrefs.com/blog/zh/how-to-create-a-sitemap/)来查找更多 URL。

### 抓取队列

所有需要爬取或重新爬取的 URL 都会被安排优先级并加入到爬取队列中。这基本上是 Google 想要抓取的 URL 的有序列表。

### 爬虫

抓取页面内容的机制。

### 处理

这些是规范化的处理机制，渲染页面，就像浏览器加载页面一样，并处理页面以获取更多要抓取的 URL，我们后面会讨论这些机制。

### 渲染

渲染就是像浏览器一样加载页面，加载 JavaScript 和 CSS 文件。这样做是为了让 Google 可以看到大多数用户会看到的内容。

### 索引

用于储存 Google 向用户显示的页面。

## 抓取控制

有几种方法可以控制在你的网站上可被抓取的内容。

### Robots.txt

Robots.txt 文件会告诉搜索引擎他们可以和不可以访问的页面。 

需要说明的是，如果链接指向这些页面，即使 Google 不可以访问该页面，但也可能会将它们编入索引。这可能会令人困惑，但如果你想防止页面被索引，请查看[本指南和流程图](https://ahrefs.com/blog/zh/remove-urls-from-google/)。

### 抓取频率

你可以在 robots.txt 中使用一个 crawl-delay 指令，许多抓取工具都支持该指令，你可以设置它们抓取页面的频率。不幸的是，谷歌并不支持。对于 Google，你需要按照[此处](https://support.google.com/webmasters/answer/48620?hl=en)所述在 Google Search Console 中更改抓取速度。. 

### 访问限制

如果你希望某些用户可以访问该页面，但搜索引擎不能访问该页面，那么你可能想要的是以下三个情况之一：

- 某些登录页面;
- [HTTP 认证](https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication) （需要密码才能访问的地方）;
- IP 白名单 （只允许特定的 IP 地址访问页面）

这种类型的设置最适用于内部网络、会员限定的内容、测试、或开发中的站点。它允许一组用户访问该页面，但搜索引擎将无法访问它们并且不会索引这些页面。

## 如何查看抓取活动

特别是对于 Google，查看他们正在抓取的内容的最简单方法是使用 [Google Search Console 抓取统计报告](https://search.google.com/search-console/settings/crawl-stats)，该报告为你提供有关抓取你网站的更多信息。

如果你想查看网站上的所有抓取活动，则需要访问服务器日志并需要使用工具来更好地分析数据。如果你的主机有一个像 cPanel 这样的控制面板，你应该可以通过一些工具例如 Awstats 和 Webalizer 访问原始日志。

![](https://ahrefs.com/blog/zh/wp-content/uploads/2021/07/Untitled-78.png)

## 抓取调整

每个网站都有不同的抓取预算，这是 Google 抓取网站的频率以及你的网站允许抓取的数量的组合。更受欢迎的页面和经常更改的页面将被更频繁地抓取，而看起来不受欢迎或链接不多的页面抓取频率会比较低。

如果抓取工具在抓取网站时有压力，它们通常会减慢速度甚至停止抓取，直到条件改善。

页面被抓取后，它们会被渲染，然后送到索引。索引就是储存搜索结果的列表。

我们来谈谈指数。

![Advanced learning](https://ahrefs.com/blog/zh/wp-content/themes/Ahrefs-4/images/advanced_learning.svg)

- [如何创建 XML 站点地图](https://ahrefs.com/blog/zh/how-to-create-a-sitemap/ "How to Create an XML Sitemap")

- [Robots.txt 和 SEO：你需要知道的一切](https://ahrefs.com/blog/zh/robots-txt/ "Robots.txt and SEO: Everything You Need to Know")

- [如何从 Google 搜索中移除网址](https://ahrefs.com/blog/zh/remove-urls-from-google/ "How to Remove URLs From Google Search")

---

![](https://ahrefs.com/blog/wp-content/uploads/svg/index_icon.svg)

Part 3

# 三、理解索引

在本章中，我们将讨论如何确保你的页面被索引并检查它们是如何被索引的。

## 爬虫指令

爬虫标记是一个 HTML 片段，它告诉搜索引擎如何抓取或索引某个页面。它被放置在网页的 `<head>` 部分，如下所示：

`<meta name="robots" content="noindex" />`

## 规范化

当同一页面有多个版本时，Google 会选择一个存储在它们的索引中。此过程称为规范化，选择为规范的 URL 将是 Google 在搜索结果中显示的 URL。他们使用许多不同的信号来选择规范 URL，包括：

- [规范标签](https://ahrefs.com/blog/zh/canonical-tags/)
- [重复页面](https://ahrefs.com/blog/duplicate-content/)
- [内部链接](https://ahrefs.com/blog/zh/internal-links-for-seo/)
- [跳转](https://ahrefs.com/blog/zh/301-redirects/)
- [网站地图 URL](https://ahrefs.com/blog/zh/how-to-create-a-sitemap/)

查看 Google 如何将页面编入索引的最简单方法是使用 Google Search Console 中的 [URL 检查工具](https://search.google.com/search-console?action=inspect)。它将显示 Google 选择的规范网址是什么。

![](https://ahrefs.com/blog/zh/wp-content/uploads/2021/07/Untitled-80.png)

![Advanced learning](https://ahrefs.com/blog/zh/wp-content/themes/Ahrefs-4/images/advanced_learning.svg)

- [10 种方法让网站加入 Google 索引](https://ahrefs.com/blog/zh/google-index/ "10 Ways to Get Google to Index Your Site")

- [移动优先索引：你需要了解的内容](https://ahrefs.com/blog/zh/mobile-first-indexing/ "Mobile-First Indexing: What You Need to Know")

- [Robots Meta 标签 和 X‑Robots-Tag：你需要知道的一切](https://ahrefs.com/blog/meta-robots/ "Robots Meta Tag & X‑Robots-Tag: Everything You Need to Know")

- [规范标签：简单的初学者指南](https://ahrefs.com/blog/zh/canonical-tags/ "Canonical Tags: A Simple Guide for Beginners")

---

![](https://ahrefs.com/blog/wp-content/uploads/svg/win.svg)

Part 4

# 四、技术 SEO 速胜要素

对于 SEO 来说，最难的事情之一是确定优先级。有很多最佳做法，但有些变化会对你的排名和流量产生的影响比其他的更大。以下是我建议优先考虑的一些要素。

## 检查索引

确保你希望人们看到的页面已被 Google 编入索引。前两章讲了爬行和索引，目的就在于此。

你可以在 [Site Audit](https://ahrefs.com/zh/site-audit)（网站诊断）中查看可见度报告以查找无法编入索引的页面及其原因。这个报告在 [Ahrefs Webmaster Tools](https://ahrefs.com/zh/webmaster-tools)（Ahrefs 站长工具）中是免费的。

![](https://ahrefs.com/blog/zh/wp-content/uploads/2021/07/Untitled-82.png)

## 回收丢失的链接

网站运行期间，往往会更改其 URL。在许多情况下，这些旧 URL 包含来自其他网站的链接。如果它们没有被重定向到当前页面，那么这些链接就会丢失并且不再计入你的页面。通过重定向可以快速收回丢失的链接。这也是一个快速获取链接的技巧。

[Site Explorer](https://ahrefs.com/site-explorer) -> yourdomain.com -> Pages -> Best by Links -> add a “404 not found” HTTP response filter. I usually sort this by “Referring Domains”.

[Site Explorer](https://ahrefs.com/zh/site-explorer)（网站分析） -> 你的域名 -> 页面 -> Best by Links（按反链数量排序） -> 添加“404 not found” HTTP 响应过滤器。我通常会按 Referring Domains（引用域）进行排序。

  

这是检测 1800flowers.com 网站的结果：

![](https://ahrefs.com/blog/zh/wp-content/uploads/2021/07/Untitled-84.jpg)

在 archive.org 中查看第一个 URL，我看到这以前是关于母亲节页面。通过将该页面重定向到当前版本，你可以回收来自 59 个不同网站的 225 个链接，其他页面也有很多类似的情况。

你需要用 [301 跳转](https://ahrefs.com/blog/zh/301-redirects/)，将旧 URL 重定向到当前页面以收回丢失的权重。

## 加入内链

内部链接是从你网站上的一个页面到你网站上另一个页面的链接。它们有助搜索引擎于找到你的页面，并帮助页面更好地排名。我们在 [Site Audit](https://ahrefs.com/zh/site-audit)（网站诊断）中有一个称为**链接机会**的报告，可帮助你快速找到这些机会。

## 添加架构标记

架构标记是一种代码，可帮助搜索引擎更好地理解你的内容，并提供许多功能，可帮助你的网站在搜索结果中脱颖而出。 谷歌的[搜索库](https://developers.google.com/search/docs/guides/search-gallery)可以显示网站符合条件所需的各种搜索功能和架构。

![Advanced learning](https://ahrefs.com/blog/zh/wp-content/themes/Ahrefs-4/images/advanced_learning.svg)

- [301 重定向：你需要知道的一切](https://ahrefs.com/blog/zh/301-redirects/ "301 Redirects for SEO: Everything You Need to Know")

- [SEO 内部链接：可操作指南](https://ahrefs.com/blog/zh/internal-links-for-seo/ "Internal Links for SEO: An Actionable Guide")

- [什么是架构标记？如何将其用于 SEO](https://ahrefs.com/blog/zh/schema-markup/ "What Is Schema Markup? How to Use It for SEO")

---

![](https://ahrefs.com/blog/wp-content/uploads/svg/2.svg)

Part 5

# 五、附加技术要素

我们将在本章中讨论的要素都是值得关注的，但与上一章中的速胜要素相比，它们可能需要更多的工作并且收益更少。这并不意味着你不需要做，只是为了帮助你了解如何确定工作的优先级。

## 页面体验信号

这些是次要的排名因素，但为了你的用户，你仍然希望查看这些内容。它们涵盖了影响用户体验 (UX) 的网站方面。

![](https://ahrefs.com/blog/zh/wp-content/uploads/2021/07/Untitled-84-2.jpg)

### 核心页面指标

[核心页面指标](https://ahrefs.com/blog/zh/core-web-vitals/)是速度指标，是 Google 用于衡量用户体验的页面体验信号的一部分。这些指标测量是：最大内容绘制速度 (LCP)、累积布局偏移速度 (CLS) 、以及首次输入延迟时间 (FID) 。

### HTTPS

[HTTPS](https://ahrefs.com/blog/zh/what-is-https/) 保护你的浏览器和服务器之间的通信不被攻击者拦截和篡改。这为当今绝大多数互联网流量提供了机密性、完整性和身份验证。你更希望你的页面通过 HTTPS 而不是 HTTP 加载。

任何在地址栏中显示锁型图标的网站都在使用 HTTPS。

![](https://ahrefs.com/blog/zh/wp-content/uploads/2021/07/Untitled-86.png)

### 移动友好

简而言之，这会检查网页是否正确显示并且是否可以被移动设备上的人们轻松使用。

你如何知道你的网站对移动设备的友好程度如何？检查 [Google Search Console](https://ahrefs.com/blog/google-search-console/) 中的 “移动可用性” 报告即可。

![](https://ahrefs.com/blog/zh/wp-content/uploads/2021/07/Untitled-88.png)

此报告会告诉你网页是否存在移动友好性问题。

### 安全浏览

这些检查是为了确保页面没有欺骗性内容、不包含恶意软件、并且没有任何恶意下载。

### 插页式广告

[插页式广告](https://developers.google.com/search/blog/2016/08/helping-users-easily-access-content-on)会阻止内容被看到。这些弹出窗口会阻碍用户阅读主要页面内容。

## Hreflang — 用于多语言

Hreflang 是一个 HTML 属性，用于指定网页的语言和地理定位。如果你有不同语言的同一页面的多个版本，你可以使用 hreflang 标签将这些变体告知 Google 等搜索引擎。这有助于他们向用户提供正确的版本。

## 维护/网站健康

这些任务不太可能对你的排名产生太大影响，但通常是改善用户体验的好事情。

### 失效的链接

失效的链接是你网站上指向不存在资源的链接——这些链接可以是内部的（即指向你网站域中的其他页面），也可以是外部的（即指向其他网站中的页面）。

你可以使用 [Site Audit](https://ahrefs.com/zh/site-audit)（网站诊断）中的链接报告快速找到网站上的失效的链接。它 [Ahrefs Webmaster Tools](https://ahrefs.com/zh/webmaster-tools)（Ahrefs 站长工具）中是免费的。

![](https://ahrefs.com/blog/zh/wp-content/uploads/2021/07/Untitled-90.png)

 

### 重定向链

重定向链是发生在初始 URL 和目标 URL 之间的一系列重定向。 

你可以使用 [Site Audit](https://ahrefs.com/zh/site-audit)（网站诊断）中的“重定向”报告快速找到重定向链。它 [Ahrefs Webmaster Tools](https://ahrefs.com/zh/webmaster-tools)（Ahrefs 站长工具）中是免费的。

![](https://ahrefs.com/blog/zh/wp-content/uploads/2021/07/Untitled-92.png)

![Advanced learning](https://ahrefs.com/blog/zh/wp-content/themes/Ahrefs-4/images/advanced_learning.svg)

- [核心页面要素：页面速度现在对 SEO 更为重要](https://ahrefs.com/blog/zh/core-web-vitals/ "Core Web Vitals: Page Speed Is Now More Important for SEO")

- [如何从头到尾提高页面速度（高级指南）](https://ahrefs.com/blog/zh/advanced-pagespeed-guide/ "How to Improve Page Speed from Start to Finish (Advanced Guide)")

- [什么是HTTPS？你需要知道的一切](https://ahrefs.com/blog/zh/what-is-https/ "What is HTTPS? Everything You Need to Know")

- [Hreflang：简单的初学者指南](https://ahrefs.com/blog/zh/hreflang-tags/ "Hreflang: The Easy Guide for Beginners")

---

![](https://ahrefs.com/blog/wp-content/uploads/guide/ch6.svg)

Part 6

# 六、技术 SEO 优化工具

这些工具可帮助你改进网站的 SEO 技术方面。

## [Google Search Console](https://search.google.com/search-console/about)

![](https://ahrefs.com/blog/zh/wp-content/uploads/2021/07/Untitled-94.png)

Google Search Console 是 Google 提供的一项免费服务，可帮助你监控网站在搜索结果中的表现并对其进行故障排除。

使用它来查找和修复技术错误、提交站点地图、查看结构化数据问题等。

[Bing](https://www.bing.com/toolbox/webmaster) 和 [Yandex](https://webmaster.yandex.com/welcome/) 也有自己的工具，Ahrefs 也是如此。[Ahrefs Webmaster Tools](https://ahrefs.com/zh/webmaster-tools)（Ahrefs 站长工具）是一款免费工具，可帮助你提高网站的 SEO 性能。它允许你：

- 监控你网站的 SEO 健康状况
- 检查 100 多个 SEO 问题
- 查看所有反向链接
- 查看你排名的所有关键词
- 了解你的网页获得了多少流量
- 寻找内部链接机会
- 这是弥补了 Google Search Console 的局限性。

## [谷歌移动友好测试](https://search.google.com/test/mobile-friendly)

![](https://ahrefs.com/blog/zh/wp-content/uploads/2021/07/Untitled-93.png)

Google 的移动友好测试可检查访问者在移动设备上使用你的页面的难易程度。它还可以识别特定的移动可用性问题，例如文本太小而无法阅读、使用不兼容的插件等。

测试会显示 Google 在抓取页面时看到的内容。你还可以使用[富搜索结果测试](https://search.google.com/test/rich-results)来查看 Google 在你的桌面或移动设备上看到的内容。

## [Chrome 开发者工具](https://developers.google.com/web/tools/chrome-devtools/)

![](https://ahrefs.com/blog/zh/wp-content/uploads/2021/07/Untitled-97.jpg)

Chrome 开发者工具是 Chrome 的内置网页调试工具。使用它来调试页面速度问题、提高网页渲染性能等。

从技术 SEO 的角度来看，它有无穷无尽的用途。

## [Ahrefs](https://ahrefs.com/zh/seo-toolbar) [Toolbar](https://ahrefs.com/zh/seo-toolbar)（Ahrefs SEO工具栏）

![](https://ahrefs.com/blog/zh/wp-content/uploads/2021/07/Untitled-99.png)

Ahrefs SEO Toolbar （Ahrefs SEO工具栏）是支持 [Chrome](https://chrome.google.com/webstore/detail/ahrefs-seo-toolbar/hgmoccdbjhknikckedaaebbpdeebhiei) 和 [Firefox](https://addons.mozilla.org/en-US/firefox/addon/ahrefs-seo-toolbar/) 的免费扩展程序，可提供有关你访问的页面和网站的有用 SEO 数据。

它的免费功能是：

- 页面SEO报告
- 使用 HTTP 标头重定向跟踪器
- 失效的链接查询
- 链接高亮
- SERP排位

此外，作为 Ahrefs 用户，你可以获得：

- 你访问的每个网站和页面以及 Google 搜索结果的 SEO 指标
- 在 SERP 中的关键词指标，例如搜索量和关键词难度
- SERP结果报告导出

## [PageSpeed Insights](https://developers.google.com/speed/pagespeed/insights/)

![](https://ahrefs.com/blog/zh/wp-content/uploads/2021/07/Untitled-97.png)

PageSpeed Insights 分析网页的加载速度。除了性能得分外，它还显示了可操作的建议，以加快页面加载速度。

# 总结

所有这些只是技术 SEO 的皮毛。这应该可以帮助你了解基础知识，并且许多部分都有其他链接供你进一步深入了解。本指南中有未涵盖的主题，因此如果你想了解更多信息，我们也给你准备了一个清单。

**具体重点**

- [PDF SEO](https://ahrefs.com/blog/zh/seo-for-pdfs/)
- [图片 SEO](https://ahrefs.com/blog/image-seo/)
- [JavaScript SEO](https://ahrefs.com/blog/zh/javascript-seo/)

**基础设施相关的**

- [状态代码](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)
- [重定向](https://ahrefs.com/blog/zh/301-redirects/)
- [HTTP/2/3](https://blog.cloudflare.com/http-3-vs-http-2/)
- [CDNs](https://en.wikipedia.org/wiki/Content_delivery_network)
- [负载均衡](https://en.wikipedia.org/wiki/Load_balancing_(computing))
- [HTTP 标题](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers)

**网站相关的**

- [页面速度](https://ahrefs.com/blog/zh/advanced-pagespeed-guide/)
- [加速移动页面 (AMP)](https://amp.dev/)
- [渐进式网络应用程序(PWAs)](https://web.dev/progressive-web-apps/)
- [移动版网址](https://developers.google.com/search/mobile-sites/mobile-seo/separate-urls)
- [参数处理](https://en.wikipedia.org/wiki/Query_string)
- [分面导航](https://en.wikipedia.org/wiki/Faceted_search)
- [分页](https://ahrefs.com/blog/rel-prev-next-pagination/)
- [站点链接](https://ahrefs.com/blog/zh/sitelinks/)
- [抓取预算](https://developers.google.com/search/blog/2017/01/what-crawl-budget-means-for-googlebot)
- [Edge SEO / serverless SEO](https://www.searchenginejournal.com/edge-seo-get-started/325931/)
- [移除网址](https://ahrefs.com/blog/zh/remove-urls-from-google/)
- [网站结构](https://ahrefs.com/blog/zh/website-structure/)
- [URLs](https://ahrefs.com/blog/zh/seo-friendly-urls/)

**流程**

- [技术SEO审核](https://www.youtube.com/watch?v=G_9-AkZch4k)
- [迁移](https://www.contentkingapp.com/academy/website-migrations/)
- [自动化 / python](https://www.seopythonistas.com/)
- [Log file分析](https://www.suganthan.com/blog/logfile-analysis-seo/)
- [SEO测试](https://seotesting.com/blog/seo-testing-guide)

**其他**

- [Regex](https://www.onely.com/blog/principles-regular-expressions-seo/)
- [用户代理](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/User-Agent)

享受探索和学习的乐趣吧，有任何问题可以在 [Twitter](https://twitter.com/patrickstox) 上找我。

_译者，__[Park Cheng](https://park.mobayke.com/)__，魔贝课凡联合创始人。_

![](https://ahrefs.com/blog/zh/wp-content/themes/Ahrefs-4/images/authors/PatrickStox.jpg "Patrick Stox")

文章作者

[

Patrick Stox

](https://ahrefs.com/blog/zh/author/patrick-stox/ "Posts by Patrick Stox")

Patrick Stox 是 Ahrefs 的产品顾问，技术 SEO 和品牌大使。他是罗利（美国城市）SEO 聚会、SEO 大会、啤酒和 SEO 聚会和 Finadability 大会的组织者之一，同时也是 /r/TechSEO 的版主。

[](https://patrickstox.com/)[](https://twitter.com/patrickstox)[](https://facebook.com/patrickstox)[](https://linkedin.com/in/patrickstox)

搜索

中文

© 2024 [Ahrefs Pte Ltd.](https://ahrefs.com/)

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

[数据与研究](https://ahrefs.com/blog/zh/category/data-studies/) 

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