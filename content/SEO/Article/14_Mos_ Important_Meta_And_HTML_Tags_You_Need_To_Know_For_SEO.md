---
title: SEO 您需要了解的 14 个最重要的元和 HTML 标签
aliases:
  - SEO 您需要了解的 14 个最重要的元和 HTML 标签
original: https://www.searchenginejournal.com/important-tags-seo/156440/
date: 2024-06-18
authors: Aleh Barysevich
tags:
  - SEO
draft: true
---
使用有效的 Meta 和 HTML 标签提升您的 SEO。了解如何使用元标记优化您的网站以提高搜索引擎排名。

![14 Most Important Meta And HTML Tags You Need To Know For SEO](https://www.searchenginejournal.com/wp-content/uploads/2020/07/important-meta-tags-5f203655f1aa8.jpg)


很长一段时间以来，HTML 元标记一直被称为 [SEO](https://www.searchenginejournal.com/seo/) 最重要的方面之一。你知道吗？这仍然是正确的。


谷歌的约翰[·穆勒 （John Mueller） 表示](https://www.searchenginejournal.com/google-answers-if-meta-description-matters-for-rankings/449119/#:~:text=John%20Mueller%20answered%3A)，谷歌使用 HTML 元标记来形成 SERP 片段，而不是用于排名。在这段声明中，他还说一个好的搜索片段会让人们访问你的页面。因此，元标记绝对是您必须关心才能获得流量的内容。

但这不仅仅是关于 [SERP 片段](https://www.searchenginejournal.com/how-important-is-structured-data/257775/)。HTML 标记指定实体以及它们之间的关系。这对于 SEO 成功至关重要，因为它们以最易理解的方式告诉 Google 页面的内容。页面上的 HTML 元素和属性（如 H2 和图像 alt 标签）也是如此。

那么，让我们开始吧。以下是供您在网站上使用的前 14 个元标记和 [HTML 元素](https://www.searchenginejournal.com/important-tags-seo/156440/#html-elements)。仔细阅读并借鉴最佳实践。

# 元标记（Meta Tags ）

## 1. 标题标签（Title）

标题标签是您主要和最重要的锚点。

`<title>` 元素通常在搜索引擎结果页面 （Search Engine Results Page，SERP） 中显示为可点击的标题，也会显示在社交网络和浏览器中。


例如，如果查看本文的 HTML，则会看到标题为：

```html
<title>SEO 您需要了解的 14 个最重要的元和 HTML 标签</title>
```

标题标签放置在网页的 `<head>` 中，旨在提供页面内容的清晰而全面的概念。

但是，它们是否像过去多年来那样对排名产生重大影响？

在过去的几年里，[用户行为](https://www.searchenginejournal.com/google-analytics-user-behavior/202964/)因素经常被讨论为相关性的逻辑证明，因此也是一种排名信号——甚至 Google 代表也承认它们在这里和那里的影响。

页面的标题仍然是搜索者在 SERP 中看到的第一件事，它帮助他们确定该页面是否有可能回答搜索意图。

一个写得很好的可能会增加点击次数和流量，这至少对排名有一定影响。

一个简单的实验还可以表明，Google 不再需要你的标题标签包含完全匹配关键词来确定页面涵盖的主题。

例如，几年前，在 Google 上搜索 `[如何建立品牌知名度]` 会出现前 5 个结果中的两个，其中标题与您的查询完全匹配。

然而，今天我们看到了不同的画面：

![SERP example](https://www.searchenginejournal.com/wp-content/uploads/2024/03/meta_tags_1-854.png)
> 来自 Google 的搜索 `[如何建立品牌知名度]` 的屏幕截图，2024 年 4 月

没有一个完全匹配。

然而，也没有一个无关紧要的结果;这里给出的每一个页面都解释了如何建立知名度，标题也反映了这一点。

但是，请注意，Google 可能会根据标题长度或与搜索查询的相关性等因素[重写标题标签](https://www.searchenginejournal.com/google-is-rewriting-title-tags-in-serps/416793/)。为了最大限度地减少重写的可能性，请确保您的标题信息丰富、用户友好、反映页面的内容，并与页面上的 H1 标签匹配。

标题标签示例，该标签更有可能被重写，因为它包含关键字填充，并且未针对用户优化，而是针对搜索引擎进行优化：
```html
<title>简单健康美味的晚餐食谱 | 最好的健康晚餐食谱</title>
```


相反，我会将其更改为：

```html
<title>简单和健康的晚餐食谱快速，美味的饭菜在家里</title>
```


通过消除 `食谱` 的重复并去除不自然的分隔符 `|`，您可以使其阅读流畅。

请记住，搜索引擎会着眼于整体情况，并倾向于将页面的内容作为一个整体进行评估，但一本书的封面仍然很重要——尤其是在与搜索者的互动方面。

### 最佳实践

- 为每个页面指定一个唯一的标题，以简洁准确地描述页面的内容。
- 即使 Google [对标题长度没有限制](https://www.searchenginejournal.com/google-title-tag-length/400682/)，也请将其保持在 50-60 个字符以内，这样它们就不会在 SERP 中被截断，并且用户可以阅读整个含义。请记住，长标题在 SERP 上被缩短到大约 600-700 像素。
- 将[重要的关键词](https://www.searchenginejournal.com/seo/why-keywords-important-seo/)放在第一位，但要以自然的方式，就好像你首先为访问者写标题并避免关键词填充一样。
- 避免在标题中使用品牌名称，因为它们显示在 SERP 中每个搜索结果的上方。包含品牌名称将是多余的。相反，节省空间以包含页面可以排名的相关关键字。

### 提示：使用标题吸引注意力

`title` 标签很珍贵，不仅因为它是 SERP 的主要资产，还因为它在您的网络浏览器中用作标签标题。

这可用于吸引用户的注意力。例如：

[![title tag example](https://www.searchenginejournal.com/wp-content/uploads/2020/07/tab-title-browser-5f1a882fa204a.png)](https://www.searchenginejournal.com/wp-content/uploads/2020/07/tab-title-browser-5f1a882fa204a.png)
截图来自作者，2024 年 4 月

这是 Facebook 和 LinkedIn 用来向您展示您有通知的确切方法，并且可以产生良好的效果。

## 2. 元描述标签（Meta Description Tags）

元描述也位于网页的 `<head>` 中，通常（但并非总是）与标题和页面 URL 一起显示在 SERP 片段中。

例如，这是本文的[元描述](https://www.searchenginejournal.com/on-page-seo/optimize-meta-description/)：
```html
<meta name="description" content="HTML **tags** are crucial for **SEO** more than ever before. In this post, I’m sharing the top 10 HTML meta **tags** you need to know."/>
```

虽然元描述不是一个直接的排名因素，但它需要你的优化工作来吸引用户（和 Google）的注意力。

- 元描述是人们在搜索片段中看到的内容和标题，因此它是让他们决定你的页面是否值得点击的方面之一。
- 描述会影响您获得的点击次数，如果页面的内容符合承诺，还可能会提高点击率并降低[跳出率](https://www.searchenginejournal.com/ranking-factors/bounce-rate/)。这就是为什么描述必须既现实又吸引人，并清楚地反映内容。
- 如果您的描述包含搜索者在搜索查询中使用的关键字，它们将以**粗体**显示在 SERP 上。这对帮助你脱颖而出并告诉搜索者他们会在你的页面上找到什么大有帮助。
- 如果 Google 认为您的描述与您页面的内容不匹配，它可以以合适的方式生成自己的描述。因此，请确保您的元描述包含主要关键字并且与主题相关。

没有办法把你想要排名的每个关键词都放在元描述中，也没有真正的必要 —— 相反，写几个有凝聚力的句子来描述你的页面的要点，包括一些关键词。

与标题标签一样，Google 在大约 [70% 的情况下](https://www.searchenginejournal.com/google-rewrites-meta-descriptions-over-70-of-the-time/382140/)会重写元描述。

做一些竞争研究是弄清楚在你的元描述中写什么以及现在什么最适合你的特定主题的好方法。

查看排名靠前的竞争对手如何填写自己的描述，以了解每个特定情况下的最佳用例。

### 最佳实践

- 为每个页面提供唯一的[元描述](https://www.searchenginejournal.com/on-page-seo/optimize-meta-description/)，以清楚地反映该页面所具有的价值。
- Google 的片段通常最多包含 `150 ~ 160` 个字符（包括空格）。
- 包括你最重要的关键词，这样它们就可以在实际的 SERP 上得到突出显示，但要小心避免关键词填充。不要让您的描述只是您定位的关键词的组合。
- 或者，使用引人注目的号召性用语 （Call To Action，CTA）、您提供的独特主张或关于预期内容的其他提示 —— “学习”、“购买”结构等。
- 不要使用引号`""` `''`，因为 Google 会在那里剪切您的摘要。

### 元提示（Meta Tip）

元描述不必只是重复页面文本第一段的句子。

要有创意：添加 CTA 以鼓励相关行动，使用关键词变体（即不是您在标题中使用的关键词），并牢记搜索意图。

例如，如果你有一个关于扇贝的信息页面，那么将你的元描述作为扇贝的定义是个好主意。如果您的页面告诉您如何烹饪扇贝，那么请为您的食谱想一个美味的描述。

如果你是一个卖新鲜扇贝的鱼贩，请描述它们的新鲜程度，并鼓励人们尽快购买它们，并附上一些 CTA。

## **3. 机器人 Meta 标签** （Robots Meta Tag）

具有 content=“noindex” 属性的页面级 [robots 元标记](https://developers.google.com/search/reference/robots_meta_tag)指示搜索引擎不为任何给定页面编制索引。

```html
<meta name="robots" content="noindex">
```

nofollow 属性指示不要点击该页面上的任何链接。

```html
<meta name="robots" content="nofollow">
```

可以将**多个指令组合**在同一个 meta 标记中，例如：

```html
<meta name="robots" content="noindex,nofollow">
```

此外，还可以使用 “name” 属性指定爬网程序：

```html
<meta name="googlebot-news" content="noindex">
```

您想要使用 “noindex” 指令的一个示例场景是阻止搜索引擎对[精简内容](https://www.searchenginejournal.com/what-is-thin-content-how-to-fix-it/270583/)进行索引，因为这些是低质量的页面，这可能会导致 Google 的有用内容算法将站点范围的[分类器](https://www.searchenginejournal.com/google-clarifies-how-helpful-content-system-works/500010/)应用于网站并降低排名。

- **阅读：**[Google 的 Mueller 概述了受 Core Update 影响的网站的恢复之路](https://www.searchenginejournal.com/googles-mueller-outlines-path-to-recovery-for-sites-hit-by-core-update/515591/)


此外，可能有一些 “草稿” 或占位符页面需要在完全优化之前发布，并且您不希望在评估网站的整体质量时考虑这些页面。

在其他情况下，您可能希望某些页面远离 SERP，因为它们具有特殊交易，应该只能通过直接链接（例如，从时事通讯）或付费活动的登录页面访问。

此外，如果您在电子商务网站上有全站[搜索选项或分面](https://www.searchenginejournal.com/technical-seo/faceted-navigation/)，Google 建议关闭搜索结果页面，这些页面可以无限期地抓取，并且不会将搜索机器人的资源浪费在没有独特内容上。


用于机器人元标记的另一个重要规则是“`max-image-preview：large， max-snippet：-1， max-video-preview：-1`”，您可以将其组合为：

```html
<meta name="googlebot-news" content="index, follow, max-image-preview:large, max-snippet:-1, max-video-preview:-1">
```

这将帮助您改善网站在 [Google Discover](https://www.searchenginejournal.com/google-discover/361142/) 上的外观。

此规则指示 Google 在搜索结果中显示大图片预览、不限数量的文本摘要和完整的视频预览，这可以极大地帮助提高您在 Google 探索中的点击率。

但是，请注意，[Google 可能会绕过](https://twitter.com/g33konaut/status/1727968613364048210)这一点，仍然会提取小缩略图。

在上述情况下，讨论的元标记规则非常有用，因为它们可以让您对网站在搜索引擎中的外观进行一定的控制。

### 最佳实践

- 关闭内容薄弱、价值不大且无意出现在 SERP 中的不必要/未完成的页面。
- 关闭不合理浪费[抓取预算](https://www.searchenginejournal.com/technical-seo/crawl-budget/)的页面。
- 请仔细确保您不会错误地限制重要页面编入索引。

## 4. 规范链接标签（Canonical Link Tag）

rel=“canonical” 链接标签是一种告诉搜索引擎您认为页面的哪个版本是主要版本并希望被搜索引擎索引并被人们找到的方法。

```html
<link rel="canonical" href="https://www.example.com" />
```

它必须有一个 `meta` 标签，告诉搜索引擎应该在搜索结果页面中显示哪个版本的页面 URL，因为网页可以有无限数量的可访问 URL，而不会改变内容。


例如，具有 UTM 跟踪参数的 URL，如 ：`https://www.example.com/?utm_source=daily-newsletter&utm_medium=email&utm_campaign=blast-01`。

Google 将具有不同参数的每个 URL 视为唯一 URL，但它们都提供相同的内容。那么，Google 如何知道它应该在 SERP 中索引和服务哪一个呢？答案是规范的 `meta` 标记。

Google 通常遵循规范的 `meta` 标记，但这是一个[提示而不是规则](https://developers.google.com/search/docs/crawling-indexing/canonicalization)，这意味着 Google 可能仍会选择不同的版本。
 
例如，如果您使用 `https://www.example.com/?tracking=bottom-cta` 等查询参数在内部链接到某个网页，Google 可能更愿意将该版本而不是规范版本编入索引，因为内部链接在确定规范页面时对 Google 来说是一个强烈的信号。

所选 URL 被更频繁地抓取，而其他 URL 则被抛在后面。

另一个好处是，规范化页面可以更轻松地跟踪与内容相关的性能统计数据。

对重复内容使用 `rel=canonical` 有助于 Google 整合你的所有工作，并将链接信号从所有页面版本传递到首选版本。

这就是使用规范标签可以帮助您将 SEO 工作引导到一个方向的地方。

### 最佳 SEO 实践

- 在同一主题上具有相似内容的页面。
- 在多个 URL 下提供重复的页面。
- 具有会话 ID 或其他 URL 参数的同一页面版本，这些参数不会影响内容。
- 小心使用规范标签来处理接近重复的页面：如果由规范标签连接的两个页面在内容上差异太大，搜索引擎将简单地忽略该标签。

## 5. Social Media Meta Tags（社交媒体元标签）

Facebook 最初推出 Open Graph 是为了让您控制页面在社交媒体上分享时的外观。

Twitter 卡片提供类似的增强功能，但仅限于 X （Twitter）。

以下是主要的 Open Graph 标签：

### 1. `og:title`

在这里，您可以放置要在页面链接时显示的标题。

```html
<meta property="og:title" content="Search Engine Journal - Marketing News, Interviews and How-to Guides" />
```

### 2. `og:url`

在这里，你放置了你想要在页面链接时显示的标题。它通常与 canonical meta 标签具有相同的值。

```html
<meta property="og:url" content="https://www.example.com/"/>
```

### 3. og:description

页面的描述。请记住，Facebook 将仅显示大约 300 个字符的描述。

```html
<meta property="og:description" content="Best-in-industry guides and information while cultivating a positive community."/>
```

### 4. og:image

在这里，您可以放置您希望在页面链接到时显示的图像的 URL。

```html
<meta property="og:image" content="https://www.example.com/sample.jpg"/>
```

使用特定的社交媒体元标记来提升您的链接对您的关注者的显示效果。

这不是一个巨大的调整，也不会影响您在搜索引擎上的排名。

但是，通过配置指向页面的链接的外观，您可以大大提高 `CTR` 和 `UX` 指标。

### 最佳实践

- 使用 [Open Graph](http://ogp.me/) 协议添加基本和相关元数据，并[测试 URL](https://developers.facebook.com/tools/debug/) 以查看它们的显示方式。
- [设置 X（前 Twitter）卡片](https://developer.twitter.com/en/docs/tweets/optimize-with-cards/guides/getting-started)并在完成后[验证](https://cards-dev.twitter.com/validator)它们。

## 6. 视口元标记（Viewport Meta Tag）

`viewport meta` 标记是一个 HTML 元素，用于控制网页在不同设备上的布局和缩放。它告诉浏览器如何调整页面的尺寸和缩放比例以匹配正在使用的设备的屏幕大小。

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

此设置可确保视区的宽度与设备的宽度匹配，从而使页面具有响应性。`initial-scale=1.0` 确保页面以 `1：1` 的比例加载，这意味着在页面首次加载时不会放大或缩小内容。

### 最佳实践

- 允许用户放大和缩小对于辅助功能非常重要。避免使用 `user-scalable=no`，这会禁用缩放。如果未设置，[Google Search Console](https://www.searchenginejournal.com/google-search-console-guide/209318/) 将引发错误 “viewport not set”。
- 确保您的 CSS 和 HTML 是响应式的。viewport meta 标记只是响应式设计的一部分；您的布局、[图像](https://www.searchenginejournal.com/on-page-seo/image-optimization/)和其他元素也应适应不同的屏幕大小。

## 7. 元字符集（Meta Charset）

meta charset meta 标记是一个 HTML 元素，用于指定 HTML do. 的[字符编码](https://www.w3schools.com/html/html_charset.asp)，它支持来自不同语言的各种字符。

```html
<meta charset="UTF-8">
```

它几乎支持所有语言的所有字符和符号，确保您的内容在不同平台和语言上正确显示。

## 8. 元刷新标签（Meta Refresh Tag）

关于这个标签，你唯一应该知道的是你永远不应该用它来实施重定向。相反，请设置[服务器端重定向](https://www.searchenginejournal.com/technical-seo/redirects/)，以便 Google 正确地获取它。

## 9. Keywords 元标签（Keywords Meta Tag）

keywords meta 标记是一个 HTML 元素，用于指定与网页内容相关的关键字列表。

但是，早在 2009 年，[Google 就宣布](https://developers.google.com/search/blog/2009/09/google-does-not-use-keywords-meta-tag)它不使用这个元标记，因为它被网站所有者滥用。

第二大搜索引擎 Bing 也在 [2014](https://blogs.bing.com/webmaster/October-2014/Blame-The-Meta-Keyword-Tag/) 年宣布不再使用它。

但是，最受欢迎的 WordPress 插件 Yoast SEO 有一个有点令人困惑的焦点关键字设置。

该设置与关键词 meta 标签无关，但用于分析你的内容并就如何改进它提出建议，以更好地定位你想要的关键词。

## 10. 架构标记（Schema Markup）

[架构标记](https://www.searchenginejournal.com/technical-seo/schema/)是一种特定技术，用于以搜索引擎识别的方式组织每个网页上的数据。

这是一个很棒的功能，因为它是真正的双赢。

具有结构化架构标记：

- 这对您的 UX 有很大的提升。
- 具有巨大的 SEO 价值。
- 提高内容理解能力。
- 帮助进入 SERP 功能。
- 增加赢得丰富网页摘要的机会。

SEO 已经远远超出了关键字和反向链接。在许多情况下，如果您想吸引流量并排名靠前，则必须在您的页面上拥有相关且正确实施的结构化数据。

例如，如果您的网站来自电子商务利基市场，您将别无选择，只能在您的产品页面上添加产品架构标记。否则，您的代码段将丢失。

关于烹饪的网站也是如此——搜索任何食谱，你只会看到 Recipes SERP 功能。

[![A screenshot of search results for "beef wellington recipe" displaying images of various styles of beef wellington dishes](https://www.searchenginejournal.com/wp-content/uploads/2024/04/beef_recipes-377.png)](https://www.searchenginejournal.com/wp-content/uploads/2024/04/beef_recipes-377.png)
搜索 `[beef wellington recipe]` 的屏幕截图，谷歌，2024 年 4 月

当然，您希望您的网站在那里。

**注意**：当今[大多数流行的内容管理系统](https://w3techs.com/technologies/history_overview/content_management/all/y)，尤其是那些与电子商务相关的系统，如 Shopify，默认内置了相关的结构化数据。

“语义网 ”是一个 “有意义的网络”，其中的重点从单独的关键词实例和外链转移到它们背后的概念以及这些概念之间的关系。

结构化数据标记正是帮助搜索引擎不仅阅读内容，而且理解某些单词相关内容的原因。

[SERP 已经发展](https://www.searchenginejournal.com/serp-search-engine-results-page-features-guide/377094/)得如此之快，以至于您甚至可能不需要点击结果即可获得查询的答案。

但是，如果一个人即将点击，[一个丰富的摘要](https://www.searchenginejournal.com/structured-data-errors/246267/) - 具有漂亮的图像、5 星评级、指定的价格范围、库存状态、营业时间或任何有用的信息 - 很可能比纯文本结果吸引眼球并吸引更多的点击。

将架构标签分配给某些页面元素可以使您的 SERP 代码段包含对用户有用和有吸引力的信息。

而且，回到原点，点击率和跳出率等用户行为因素会影响搜索引擎对你的网站的排名。

### 最佳 SEO 实践

- 在 [schema.org](http://schema.org/) 上研究可用的架构。
- 创建您最重要的页面的地图，并确定与每个页面相关的概念。
- 仔细实施标记（如果需要，请使用 [Structured Data Markup Helper](https://www.google.com/webmasters/markup-helper/?hl=en) ）。
- 彻底[测试标记](https://search.google.com/structured-data/testing-tool/u/0/)，以确保它不会产生误导或添加不当。

# HTML 元素

## 11. 标题标签 （H1-H6）

[标题标签](https://www.searchenginejournal.com/on-page-seo/header-tags/)（Heading）是 HTML 标签，用于标识页面内容的不同部分，并充当不同部分的迷你标题。

如今，标题标签的使用引起了一些争论。

虽然 H2-H6 标签被认为不如搜索引擎重要，但许多[行业研究](https://www.searchenginejournal.com/ranking-factors/top-ranking-factors/)都强调了 H1 标签的正确使用。

尽管 H2-H6 标签最初用于 UX 目的，但 [2021 年引入段落索引](https://blog.google/products/search/search-on/)使它们非常有价值。比如，如果查询与 H3 标题和与之相关的段落匹配，Google 可以对你的页面的一部分进行索引和排名。

相反，我们应该考虑到标题对于文本和内容组织至关重要，应该认真对待。

使用标题标签肯定会增加[内容的架构](https://www.searchenginejournal.com/google-headings-with-hierarchical-structure-an-awesome-idea/478491/)。

- **对于搜索引擎来说**，阅读和理解组织良好的内容比爬行结构问题更容易。
- **对于用户来说**，标题就像文本墙中的锚点，在页面中导航并使其更易于消化。

这些因素提高了仔细优化的重要性，其中小细节加起来就是对 SEO 和用户友好的大图景，并可能导致排名上升。

### 最佳实践

- 保持您的标题与他们描述的文本块相关。仅仅因为它们不是排名因素并不意味着搜索引擎不考虑它们。
- 始终让您的标题反映它们所覆盖的文本的情绪。避免使用“`第 1 章......` `第 2 章...` `第 3 章...`”。
- 不要过度使用标签和其中的关键词。保持用户可读。

### 你的标题标签和H1应该匹配吗？

根据 [Google 的建议](https://support.google.com/news/publisher-center/answer/9607104?hl=en&ref_topic=9606945)，我们鼓励您将页面的标题和 H1 匹配，稍微改变顺序并在这里和那里更改它。

因此，如果您正在努力想出完美的 H1，只需再次使用您的标题即可。

## 12. HTML5 语义标签（Semantic Tags）

[HTML5 语义标签](https://www.searchenginejournal.com/why-you-should-consider-semantic-html-for-seo/506384/)属于最新的 HTML 标准，对于帮助 Google 和其他搜索引擎更好地理解页面内容是必要的。

以下是 HTML5 标签在页面源代码中的外观：

```html
<article>

<h1>10 Most Important Meta Tags You Need to Know for SEO</h1>

<p>Title tags are placed in the 'head' of your webpage and are meant to provide a clear and comprehensive idea of what the page is all about.</p>

</article>
```

### HTML5 标记示例

今天有很多 HTML5 标签被 SEO 专业人士广泛使用。如果你仔细观察这些标签，你会发现它们的名称重复了任何页面上最常见的元素，比如视频、菜单等。

所以他们是这样的（他们中的大多数）：

- `<article>` — 定义作为独立单元的大型且有意义的内容（文章、论坛帖子等）。
- `<audio>` — 显示嵌入的声音或音频流。
- `<details>` — 描述一个小组件，用户可以从中按需获取其他信息或控件。
- `<dialog>` — 定义用户在必要时可以与之交互的对话框或子窗口。
- `<embed>` — 嵌入一段多媒体内容，如视频、声音或任何外部应用程序。
- `<footer>` — 定义页面、文档或节的页脚内容。
- `<header>` — 定义页面、文档或节的页眉部分的内容。
- `<main>` -定义页面内容或 `<article>` 中最重要和最有意义的部分（`<main>` 可以放在 `<article>` 部分中）。 
- `<nav>` — 定义带有导航链接的页面部分。
- `<picture>` — 定义多个图像源的容器。
- **<source>** `<source>` — 显示嵌入媒体元素（如 或 ）的替代源
- `<summary>` — 与`<details>` 一起，该元素提供了对用户可见的摘要。
- `<svg>` — 在 HTML 文档中嵌入 SVG 文件。
- `<time>` — 以机器可读的格式对日期和时间（生日、事件、会议等）进行编码。
- `<video>` — 将视频内容嵌入到 HTML 文档中，而无需任何其他插件即可播放视频。

###  最佳 SEO 实践

事实是，HTML5 标签取代了我们大家都知道的永无止境的 `<div>`，并且这些天一直在使用。

尽管如此，HTML5 属性可以帮助您的内容更快地索引和获得更好的排名，因为 Google 清楚地看到并理解什么是 `<article>`，什么是 `<video>`，以及在哪里可以找到一组导航链接 `<nav>`。

这就是为什么与 HTML5 标签相关的唯一最佳实践实际上是在你的页面上使用它们并正确地应用它们 — 一个特定的标签到内容的特定部分。

不要试图欺骗和标记带有 `<video>` 标签的文本内容 — Google 不会喜欢这样的。

# 重要的 HTML 属性

## 13. 图像 Alt 属性

图像 `alt` 属性是您添加到图像中以提供书面描述的标记。在实践中，它可能看起来像这样：

![coffee](https://www.searchenginejournal.com/wp-content/uploads/2024/04/coffee_beans-648.png)

图片来自 mtpak.coffee，2024 年 5 月

```html
<img src="https://mtpak.coffee/wp-content/uploads/2021/02/image2.jpg" alt="Roasting coffee beans">
```

Alt 属性在页面优化方面很重要，原因有两个：

- 如果无法加载任何特定图像（或图像被禁用），则会向访客显示替换文本。
- `Alt` 属性提供上下文，因为搜索引擎无法 “看到” 图像。

对于[电子商务网站](https://www.shopify.com/blog/7412852-10-must-know-image-optimization-tips)，图像通常对访问者与页面的交互方式产生至关重要的影响。
 
[谷歌也直言](https://www.searchenginejournal.com/google-image-publishing-guidelines/252149/)不讳地表示：帮助搜索引擎了解图像的内容以及它们与其他内容的关系可能有助于它们为合适的搜索查询提供页面。

根据 Mueller 的说法，[如果您想在 Google 图片中排名](https://www.searchenginejournal.com/google-alt-text-only-a-factor-for-image-search/442865/)，经过深思熟虑的图像 `alt` 描述也至关重要。

但请记住相关性的重要性：不仅 `alt` 文本、标题和说明需要与图像相关，而且图像本身也应该放置在适当的相关上下文中。

### 最佳实践

- 尽最大努力[优化最突出的图片](https://www.searchenginejournal.com/on-page-seo/image-optimization/)（产品图片、信息图表或培训图片），这些图片可能会在 Google 图片搜索中查找。
- 在除图像之外没有太多内容的页面上添加 alt 文本。
- 保持替代文本足够清晰和描述性，合理使用你的关键词，并确保它们自然地融入页面内容的整个画布。

## 14. `Nofollow` 属性

[外部/出站链接](https://www.searchenginejournal.com/seo/why-links-important-seo/)是您网站上指向其他网站的链接。

自然，这些被用来指代经过验证的来源，将人们引向其他有用的资源，或出于其他原因提及相关网站。

这些链接对 SEO 非常重要：它们可以使你的内容看起来像一个由可靠来源支持的手工制作的综合作品，或者像一个没有太多有价值内容的链接转储。

谷歌以其对操纵性链接策略的强烈反感而闻名，坚持这些策略可能会导致处罚，而且它在检测它们方面并没有变得不那么聪明。

除此之外，在语义搜索时代，Google 可能会将您引用的来源视为上下文，以更好地理解您页面上的内容。

由于这两个原因，值得关注您的链接位置和方式。

默认情况下，所有超链接都会被跟踪，当你在你的网站上放置一个链接时，你基本上是对链接页面的 “投下信任票”。

当你向链接添加 [nofollow 属性](https://www.searchenginejournal.com/when-to-use-nofollow-on-links/383468/)时，它会指示搜索引擎的机器人不要跟踪该链接（并且不要传递任何链接资产）。

在 HTML 中，nofollow link 属性如下所示：

```html
<a rel=“nofollow” href=“https://www.apple.com”>Apple</a>
```

除了传统的 nofollow 之外，Google 还引入了[另外两个选项来指定 nofollow 链接](https://developers.google.com/search/docs/crawling-indexing/qualify-outbound-links)，**_rel=“sponsored”_** 用于付费链接，**_rel=“UGC”_** 用于用户生成的内容，如论坛评论：
```html
<a rel=“sponsored” href=“https://www.apple.com”>buy Apple</a>
<a rel=“UGC” href=“https://www.apple.com”>what users say about Apple</a>
```

保持你的 SEO 整洁，你会在你的页面上保持 follow 和 nofollow 链接之间的[健康平衡](https://www.searchenginejournal.com/ranking-factors/nofollow-links/)，但通常会将以下类型的链接设置为 nofollow：

- 指向任何可被视为 “untrusted content” 的资源的链接。
- 任何付费或赞助链接（您不希望 Google 发现您出售您的“投票”）。
- 来自评论的链接或其他类型的用户生成内容，这些内容可能会成为您无法控制的垃圾内容。
- 内部的 “Sign in” 和 “Register” 链接紧随其后，这只是浪费了[抓取预算](https://www.searchenginejournal.com/technical-seo/crawl-budget/)。

# 结论

HTML 元标记是一种常青的 SEO 技术，因为 HTML 是 Web 上每个页面的基础。这些是您的[页面 SEO](https://www.searchenginejournal.com/on-page-seo/essential-factors/) 中不应忽视的基础知识。

有时，这些 “基础知识 ”是阻止你排名靠前的问题，因为 Google 无法识别你的内容。

嗯，你明白了。此外，当今的 AI 炒作使得正确的 HTML 标签使用变得更加重要——它们帮助 Google 理解内容、建立联系，从而训练 AI。

SEO 不断发展，HTML 也在不断发展，并且出现了新的标签。观看新闻、保持警觉并使用标签。

# 更多资源

- [标题标签优化：完整的操作指南](https://www.searchenginejournal.com/on-page-seo/title-tag-optimization/)
- [Meta Keywords 标签是排名因素吗？](https://www.searchenginejournal.com/ranking-factors/meta-keywords/)
- [页面 SEO 完整指南](https://www.searchenginejournal.com/on-page-seo/?itm_source=website&itm_medium=ebooks-landing-page&itm_campaign=ebooks-landing-page "Download Now")