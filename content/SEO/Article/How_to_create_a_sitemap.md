---
title: 如何创建 XML 网站地图 (并向 Google 提交)
original: https://ahrefs.com/blog/zh/how-to-create-a-sitemap/
tags:
  - SEO
  - ahrefs
draft: true
author: Joshua Hardwick
date: 2024-01-22
---

在没有地图的情况下找到没有去过的地方很困难，同时，没有网站地图，Google 也会迷路。

幸运的是，创建和提交 XML 网站地图并不复杂。

接下来，我们会一步一步地学习如何操作。

但是首先，我们需要了解一些基本知识。

(已经熟悉了基本知识？[点击这里可以直接跳转到网站地址的创建教程。](https://ahrefs.com/blog/zh/how-to-create-a-sitemap/#section4))

# 什么是网站地图（sitemap）？

网站地图是一个 XML 文件，用于罗列网站上的重要内容。任何你希望能够出现在搜索引擎的页面或文件都应该出现在网站地图中。

>[!NOTE] 有趣的事实
>
>网站地图不能罗列超过 50,000 个 URL，且体积必须在 50mb 以下。如果你的网站地图超出其中任一指标，你就需要多创建几个了。

# XML 网站地图的形式是怎样的？

XML 网站地图是为搜索引擎——而不是用户——创建的。如果你之前没有见过网站地图，那么他们乍看起来可能会令你心生畏惧。
```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
	<url>
		<loc>https://ahrefs.com/</loc>
		<lastmod>2019-08-21T16:12:20+03:00</lastmod>
	</url>
	<url>
		<loc>https://ahrefs.com.com/blog/</loc>
		<lastmod>2019-07-31T07:56:12+03:00</lastmod>
	</url>
</urlset>
```


我们现在慢慢展开。

## XML 声明

```xml
<?xml version="1.0" encoding="UTF-8"?>
```

这则片段会告诉搜索引擎他们在抓取的是一个 XML 文件。同时这也声明了 XML 的版本和所用的字符编码。对于网站地图来说，版本**应该**为 1.0，编码**必须**为 UTF‑8。

## URL 组

```xml
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
```

这个容器包含了网站地图中所有的 URL。同时它还会告诉网络爬虫应该使用何种协议标准。大多数网站地图会指定使用 0.90 的协议标准，包括 Google、Yahoo! 和微软在内的各类搜索引擎都支持该标准。

## URL

```xml
<url>
<loc>https://ahrefs.com/</loc>
<lastmod>2019-08-21T16:12:20+03:00</lastmod>
</url>
```

这是每个 URL 的父标签。你必须在一个嵌套的标签 `<loc>` 中指定 URL 的位置。这些 URL 必须是绝对的 —— 而非相对的 —— 权威链接。

尽管该标签是这里唯一的强制标签，你还可以使用一些可选的属性：

- `<lastmod>`: 用于声明文件最后一次修改的时间。其格式必须符合 [W3C Datetime](https://www.w3.org/TR/NOTE-datetime) 格式。例如你在 2019 年 9 月 25 日更新了某篇帖文，该属性应为 `2019–09-25`。你还可以在其中指定时间，但这不是强制的。
- `<priority>`**:** 用于指明该 URL 较网站其他 URL 的优先级。数值在 `0.0` 到 `1.0` 之间。数值越高表明越重要。
- `<changefreq>`**:** 用于指明该页面可能更新的频率。它的作用是告诉搜索引擎应该多久回头抓取一次这个 URL。它的值可以是总是、每小时、每天和每周。

这些可选的标签对 SEO 来说并没有那么重要。

说到  `<lastmod>` 标签，Google 的 Gary Ilyes [曾经表示](http://stackoverflow.com/questions/31349345/how-to-properly-format-last-modified-lastmod-time-for-xml-sitemaps?stw=2)他们会无视这个标签，因为“站长在保证这个标签数据的准确性方面做得太差了。” 大多数的网站地图生成器都会将所有页面的日期设置成当前日期，而不是该页面上次被编辑的日期。原因显而易见。

至于 `<priority>`标签，Google [曾表示](https://www.seroundtable.com/google-sitemap-priority-field-a-bag-of-noise-23645.html)，因为这些标签会带来“大量噪音”，所以他们会选择无视。

而`<changefreq>`标签，John Mueller [指出](https://www.seroundtable.com/google-priority-change-frequency-xml-sitemap-20273.html)“优先级和改动频率已经退出网站地图的舞台了。”


# 我为什么需要网站地图？

Google 通过爬行网站来探索新的内容。当搜索引擎的爬虫爬行某个页面时，他们会同时关注页面的内外链。当他们发现某个 URL 不在索引中时，就会试图解析其中的内容，并在适当的位置索引他们。

但是 Google 无法通过这种方式找到所有的内容。如果某个页面没有来自其他页面的链接，那么 Google 就没有办法找到这些页面。

这个时候网站地图就可以发挥作用了。

网站地图可以告诉 Google（以及其他搜索引擎）应该去网站的哪些位置寻找最重要的页面，这样爬虫就可以抓取并索引它们。这很重要因为引擎只有事先索引了你的页面，才可以对它进行排名。

# 如何创建网站地图

部分内容管理系统可以帮你生成网站地图。当你向网站添加或移除页面的时候，这些网站地图会自动更新。如果你的内容管理系统本身不自带这个功能，那么通常情况下会有相关的插件可以做到。

## 在 WordPress 中创建网站地图

即使 ＷordPress [驱动了全球 34.5% 的网站](https://w3techs.com/technologies/history_overview/content_management/all)，然而它却不会为你自动生成网站地图。你可以借助 Yoast SEO 这样的[插件](https://ahrefs.com/blog/zh/best-seo-plugins-for-wordpress/)来生成网站地图。

要安装 Yoast SEO，首先登录 WordPres 后台。

依次进入插件（Plugins）> 添加（Add New）：

![add new plugin wordpress](https://ahrefs.com/blog/wp-content/uploads/2020/01/add-new-plugin-wordpress.png)

搜索 Yoast SEO。

点击现在安装（Install now）然后激活（Activate）：

![yoast seo search](https://ahrefs.com/blog/wp-content/uploads/2020/01/yoast-seo-search.png)

前往 `SEO` > `通用设置`，确保 `XML 网站地图` 开关处于打开状态。

![xml sitemap yoast](https://ahrefs.com/blog/wp-content/uploads/2020/01/xml-sitemap-yoast.png)

现在你应该可以在 yourdomain.com/sitemap.xml 或者 yourdomain.com/sitemap_index.xml 中看到网站地图（或者网站地图的索引）了。

![ahrefs sitemap](https://ahrefs.com/blog/wp-content/uploads/2020/01/ahrefs-sitemap.png)

小提示.

 如果你的 WordPress 是安装在子目录或者子域名下的，那么你的网站地图也会处于这个位置。例如，我们博客的网站地图就可以通过 ahrefs.com/blog/sitemap_index.xml 来访问。 

提示

如果你想在网站地图中囊括或者排除一些特定的内容（如标签页面、类目页面等），就需要前往“搜索展示”（“Search Appearance”）设置。 

![category pages exclude yoast](https://ahrefs.com/blog/wp-content/uploads/2020/01/category-pages-exclude-yoast.png)

你还可以通过编辑器的“高级”（“Advanced”）元选项框单独排除博文或页面。

![yoast noindex post](https://ahrefs.com/blog/wp-content/uploads/2020/01/yoast-noindex-post.png)

**重要提示.** 只有当你不想要某些页面出现在搜索结果中时，才从网站地图中移除他们。

你可以从我们的 [WordPress SEO 指南](https://ahrefs.com/blog/zh/wordpress-seo/)中了解更多。

## 在 Wix 中创建网站地图

Wix 会自动为网站创建网站地图。你可以通过访问 _yourwixsite.com/sitemap.xml_ 找到它。

不幸的是，对于网站地图包含哪些页面，不包含哪些页面，你并没有太多控制。如果你想要排除某个页面，就前往该页面的的“SEO (Google)”设置板块并关闭“在搜索结果中展示该页面”（“Show this page in search results”）选项。

![wix noindex](https://ahrefs.com/blog/wp-content/uploads/2020/01/wix-noindex.png)

注意这样会给该页面加入一个 noindex 元标签，它就不会显示在搜索结果中了。

小提示.

 如果你在 Wix 将某个 URL权威化，它并不会从网站地图中消失。尽管这对大多数用户来说无关紧要，但是记住在网站地图中包含权威页面并不是最好的办法，这样做会向 Google 发送混淆的信号。 

## 在 Squarespace 中创建网站地图

Squarespace 也会自动创建网站地图。你可以在 _yoursquarespacesite.com/sitemap.xml_ 中找到它。

在 Squarespace 中你没有办法手动编辑网站地图，但是你可以在“SEO”标签中将那些无需索引的页面排除。

![seo squarespace](https://ahrefs.com/blog/wp-content/uploads/2020/01/seo-squarespace.png)

这样他们也会从你的网站地图中消失。

## 在 Shopify 中创建网站地图

Shopify 会自动生成网站地图，地址为 _youtstore.com/sitemap.xml_。

然而，想要在 Shopify 中要将一些页面排除在索引之外没那么简单。你必须直接编辑 .liquid 文件。

## 不使用内容管理系统创建网站地图

如果你网站的页面不足 300 个，可以安装免费版的 [Screaming Frog](https://www.screamingfrog.co.uk/seo-spider/)。

安装完成后，前往 模式（_Mode_）> 爬虫（_Spider_）。

将你首页的 URL 粘贴进标有“向抓虫提供 URL”（“Enter URL to spider”）的文本框内。

点击“开始”（“Start”）。

![screaming frog sitemap](https://ahrefs.com/blog/wp-content/uploads/2020/01/screaming-frog-sitemap.png)

小提示.

 确保你使用了网站首页的权威（主要）版本。如如果使用了其他版本，Screaming Frog 将只会的抓取一个 URL。 

抓取任务结束后，查看屏幕的右下角。

会看到下图所示的信息：

![sf total scrape](https://ahrefs.com/blog/wp-content/uploads/2020/01/sf-total-scrape.png)

如果数量小于等于 499，就可以去到网站地图（_Sitemaps_）> XML 网站地图（_XML sitemap_）。

因为 Google 基本会忽略  
`<lastmod>`, `<changefreq>`, 和`<priority>`,  
我们建议将这些片断排除出网站地图文件。

![screaming frog sitemap settings](https://ahrefs.com/blog/wp-content/uploads/2020/01/screaming-frog-sitemap-settings.png)

点击“下一步”并将网站地图保存到本地。完成。

若数量显示为“500 of 500”，就没有必要将网站地图导入了。为什么？因为这意味着 Screaming Frog 在抓取到网站的所有页面之前已经达到了数量上限。亦即此时导出的网站地图中可能会遗失数百个页面——这样就没有意义了。

有一种解决办法是寻找免费的网站地图生成器。这样的工具有很多。

可惜的是，他们中的大部分都很不可靠。

我们测试了许多流行的网站地图生成工具，发现其中的大部分包含了非权威的 URL，无需索引的页面以及重定向。这是非常糟糕的 SEO 实践。

|生成工具|包含非权威的URLs?|包含无需索引的URLs?|包含重定向(301 redirects)?|
|---|---|---|---|
|xml-sitemaps.com|Yes ❌|No ✅|No ✅|
|web-site-map.com|Yes ❌|No ✅|No ✅|
|xmlsitemapgenerator.org|Yes ❌|No ✅|No ✅|
|smallseotools.com/xml-sitemap-generator|Yes ❌|Yes ❌|Yes ❌|
|freesitemapgenerator.com|Yes ❌|Yes ❌|Yes ❌|
|duplichecker.com/xml-sitemap-generator.php|Yes ❌|Yes ❌|Yes ❌|
|xsitemap.com|Yes ❌|Yes ❌|Yes ❌|

那么应该如何解决呢？

如果 Screaming Frog 未能成功抓取整个网站，可以使用 Ahrefs 的[网站诊断](https://ahrefs.com/zh/site-audit)（Site Audit）工具。

小提示.

 验证你的网站后，抓取速度会变快。[这里有操作方法](https://help.ahrefs.com/en/articles/1431155-how-do-i-finish-crawling-my-website-faster-in-site-audit)。

一旦抓取完成，可以前往页面分析（Page Explorer）板块，添加以下过滤条件。

![](https://ahrefs.com/blog/zh/wp-content/uploads/2020/01/page-explorer-1-1536x665-1.png)

点击导出（_Export_）> 当前表格视图（_Current table view_）。

打开 CSV 文件，接着将 URL 一栏中的所有链接复制粘贴到[这个工具](https://timestampgenerator.com/tools/xml-sitemap-from-list)中。

点击“加入队列”（“Add to queue”），然后再点击“将队列导出为 sitemap.xml”（“Export queue as sitemap.xml”）。

这个导出的文件就是完整版的网站地图了。

# 如何向 Google 提交网站地图

首先，你需要知道网站地图的位置。

如果你使用了插件，那么很有可能网站地图会存放在 domain.com/sitemap.xml

如果你的网站地图是手动生成的，那么请将它命名为类似 `sitemap.xml` 这样的文件名，然后上传到网站根目录。这样你就可以通过 domain.com/sitemap.xml 来访问它了。

>[!NOTE] 小提示
>当然你也可以自由选择网站地图的文件名，但最好还是坚持用 `sitemap.xml`。当你有多个网站地图的时候，可以使用 `sitemap_1.xml`，`sitemap_2.xml` 这样的模式。 

接着去到 Google 站长工具（_Google Search Console）_> 网站地图（_Sitemaps_）> 粘贴网站地图的地址 > 点击“提交”(“Submit”)

![sitemap search console](https://ahrefs.com/blog/wp-content/uploads/2020/01/sitemap-search-console.png)

这样就可以了。

>[!TIPS] 提示
>
>把网站地图的 URL 添加到 [robots.txt文件](https://ahrefs.com/blog/zh/robots-txt/)上也是一种不错的实践。
>
>你可以在网站服务器的根目标找到这个文件。要在其中加入网站地图，只需要打开该文件，并将以下这行粘贴进去：
>```xml
>Sitemap: https://www.yourdomain.com/sitemap.xml
>```
> 
>记得将上面的示例 URL 换成你自己网站地图的网址。
>
>如果你有多个网站地图，只需要批量将他们加入。
>
>```xml
>Sitemap: https://www.asos.com/sitemap_1.xml
>Sitemap: https://www.asos.com/sitemap_2.xml
>```


# 修复影响网站地图的错误

Google 站长工具可以告诉你与网站地图相关的大多数技术错误。

比如，在以下的例子中，我们提交的一个 URL 被 [robots.txt文件](https://ahrefs.com/blog/zh/robots-txt/)屏蔽了，Google 站长工具给出了警告：

![submitted url blocked by robots](https://ahrefs.com/blog/wp-content/uploads/2020/01/submitted-url-blocked-by-robots.png)

点击[此处](https://support.google.com/webmasters/answer/7440203?hl=en)，你可以了解这些问题的更多信息，以及如何修复他们。

话虽如此，有一些问题并不在 Google 站长工具的警告之列。

以下我们罗列出了一些更常见的问题，以及如何修复他们。

## 网站地图包含无用的、低质量的页面

网站地图中的每一个页面都必须是索引的权威版本。

然而，这并不意味着所有页面都是高质量的。如果你的网站内容较多，那么一些低质量的页面就有可能混入你的网站地图。

例如，我们来看一下某电商网站的这两个页面。 

![ecommerce 2](https://ahrefs.com/blog/wp-content/uploads/2020/01/ecommerce-2.png)

![ecommerce 2 1](https://ahrefs.com/blog/wp-content/uploads/2020/01/ecommerce-2-1.png)

他们对搜索用户来说没有任何价值，却依然出现在了这个网站的网站地图中，Google 也索引了这两个页面。

![indexed near duplicate 2](https://ahrefs.com/blog/wp-content/uploads/2020/01/indexed-near-duplicate-2.png)

![indexed near duplicate 1](https://ahrefs.com/blog/wp-content/uploads/2020/01/indexed-near-duplicate-1.png)

要找出这些页面，可以前往网站诊断（Site Audit）> 重复内容 (Duplicate Content)

你需要找出那些重复的或者准重复的没有权威版本的页面。他们在 Ahrefs 中会以橙色方框表示。点击其中的某个可以看到存在该类问题的所有页面。  

![](https://ahrefs.com/blog/zh/wp-content/uploads/2020/01/duplicate-content.png)

查看这些页面，看他们是否有价值。

网站包含低质量页面非常不好，主要有以下三个原因：

- **他们浪费了抓取的配额**：让 Google 浪费时间和资源去抓取无用的、低重的页面是很不理想的。他们应该花时间去抓取那些更重要的页面。_（声明，[Google](https://webmasters.googleblog.com/2017/01/what-crawl-budget-means-for-googlebot.html) 表示“大部分内容发布者都无需担心”抓取配额。）_
- **他们偷取了更重要的页面的链接权威度**：页面的权威度和他们的排名有着[清晰的关系](https://ahrefs.com/blog/zh/search-traffic-study/)。指向低质量页面的[内链](https://ahrefs.com/blog/zh/internal-links-for-seo/)只会稀释那些本可以流向更重要的页面的权威度。（_有趣的是，[在我们移除了 Ahrefs 博客几乎 ⅓ 的内容后](https://ahrefs.com/blog/zh/content-audit/)，流量不降反增）_
- **他们会导致糟糕的用户体验**：这些页面的访客无法从中获取任何价值。点击这些页面对于访客来说是恼人的，如果网站因此得到了低质量和无人看管的名声，那么最后访客很有可能跳出。

总体来说，最好的行动方案是从网站和网站地图中先后移除低质量的内容。如果你正在开展这项工作，那么不要忘了连指向那些页面的内部链接也一并删除。否则，你会把一个问题（低质量页面）变成另外一个问题（[无效链接](https://ahrefs.com/blog/fix-broken-links/)）。

除了重复和接近重复的内容，你还应该把那些单薄的内容找出来。

查看网站诊断板块中的“页面”(“On page”)报告，注意那些带有“字数较少”（“Low word count”）警告的页面。

![low word count pages](https://ahrefs.com/blog/wp-content/uploads/2020/01/low-word-count-pages.png)

## 意外地被排除在网站地图外的页面

如果你按照上文中推荐的某种方法创建了网站地图，那么带有 noindex 或者权威标签（非自我参照）的页面则不会被包含在内。

这是一件好事。你的网站地图不应该包含权威链接或者无需索引的页面。

话虽如此，如果你网站包含了粗制烂造的 noindex 标签，页面可能会意外地被排除在外。

你可以前往网站诊断板块的“可索引性”(“Indexibility”)报告并点击“Noindex 页面”警告，就可以看到所有没有被索引的页面。

![noindex pages](https://ahrefs.com/blog/wp-content/uploads/2020/01/noindex-pages.png)

这些页面中的大部分可能都是被有意排除的，但是仍然有必要好好浏览这个列表，仔细检查。粗制烂造的 noindex 标签很容易被发现，因为他们会贯穿网站的某一分部。

如果你发现了不应该被排除的页面，那就应该从页面中移除 noindex 标签，并将这个页面（的链接）加入网站地图。如果你使用了内容管理系统或者插件，那么第二步会自动发生。

> [!NOTE] 专业提示
>
>除此之外还有必要去查看武断的权威标签和重定向。为此，你需要前往页面分析（Page Explorer）板块并加入以下过滤条件。
>
>![](https://ahrefs.com/blog/zh/wp-content/uploads/2020/01/page-explorer-canonical-1536x751-1.png)
>
>查看武断的权威标签。
>
![](https://ahrefs.com/blog/zh/wp-content/uploads/2020/01/page-explorer-redirects-1536x688-1.png)
>
>查看武断的重定向。
>
>删除所有武断的权威标签和重定向，并将受其影响的页面（链接）添加进网站地图。

# 常见问题

以下是对一些关于网站地图常见问题的解答。如果你还有其他问题，请告诉我们，我们会把他们（连同答案）添加进来。

## 加速移动页面（AMP）需要网站地图吗？

不需要。

> [@Kfowler325](https://twitter.com/Kfowler325?ref_src=twsrc%5Etfw) No need for sitemaps for AMP pages — the rel=amphtml link is enough for us.— 🍌 John 🍌 (@JohnMu) [13 October 2016](https://twitter.com/JohnMu/status/786588362706673664?ref_src=twsrc%5Etfw)

## 如何为电商网站创建网站地图？

为电商网站添加网站地图的操作和其他网站一样。话虽如此，考虑到分面导航在电商网站中的普及度， 大量的重复和准重复页面经常会成为漏网之鱼，需要仔细检查。

# 结语

创建网站地图并不是很复杂的事情，尤其是当你可以借助插件来完成繁琐步骤的时候。从无到有创建网站地图也没有很难——抓取你的网站页面并为 URL 结果列表设置合适的格式即可。

话虽这样说，非常重要的一点是你要记得 Google 并不是一定要索引你的网站地图中的页面。并且网站地图和网站排名没有什么关系。

如果你想知道如何在 Google 中取得高排名，可以[看看这篇文章](https://ahrefs.com/blog/zh/how-to-rank-higher-on-google/)。

有任何问题，请在评论区或者[在 Twitter 上](https://twitter.com/joshuachardwick?lang=en)告诉我们。

_译者：Alex Wang, Not Soup Yet 创始人_