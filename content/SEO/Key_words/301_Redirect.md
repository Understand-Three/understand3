---
title: 301 重定向
original: https://ahrefs.com/zh/seo/glossary/301-redirect
---
# 301 Redirect 301 重定向
# 301 Redirect 301 重定向

## What is a 301 redirect?  
什么是 301 重定向？

A **301 redirect** indicates that the web page or resource was moved from one location to another permanently.  
**301 重定向**表示网页或资源已从一个位置永久移动到另一个位置。

It works by sending the 301 “Moved Permanently” HTTP status response code to the browser or web crawler along with the new destination URL.  
它的工作原理是将 301 “Moved Permanently” HTTP 状态响应代码与新的目标 URL 一起发送到浏览器或 Web 爬虫。

image 图像

The 301 redirect is the most common redirection method.  
301 重定向是最常见的重定向方法。

Unlike the [302 redirect](https://ahrefs.com/seo/glossary/302-redirect) (temporary redirect), the 301 redirect signals to search engines that they should update the URL of the resource in their index to a new one. For website visitors, there’s no difference between the 301 and 302 redirects.  
与 [302 重定向](https://ahrefs.com/seo/glossary/302-redirect)（临时重定向）不同，301 重定向向搜索引擎发出信号，表明它们应该将其索引中的资源 URL 更新为新 URL。对于网站访问者，301 和 302 重定向之间没有区别。

## Why are 301 redirects important?  
为什么 301 重定向很重要？

If you move a piece of content from a certain URL and someone tries to visit it, they’ll get a “404 Page Not Found” error. A 301 redirect prevents that and forwards website visitors and search engine crawlers to the new URL.   
如果你从某个 URL 移动了一段内容，并且有人试图访问它，他们会收到 “404 Page Not Found” 错误。301 重定向可以防止这种情况，并将网站访问者和搜索引擎爬虫转发到新的 URL。

Besides, the 301 redirection method transfers the [link equity](https://ahrefs.com/seo/glossary/link-equity) from the old URL to the new one, meaning that the [PageRank](https://ahrefs.com/seo/glossary/pagerank) will be preserved.   
此外，301 重定向方法将[链接资产](https://ahrefs.com/seo/glossary/link-equity)从旧 URL 转移到新 URL，这意味着 [PageRank](https://ahrefs.com/seo/glossary/pagerank) 将被保留。

As Google’s John Mueller put it:   
正如 Google 的 John Mueller 所说：

> “For the most part that is not a problem. We can forward PageRank through 301 and 302 redirects. Essentially what happens there is we use these redirects to pick a canonical. By picking a canonical we’re concentrating all the signals that go to those URLs to the canonical URL.”  
> “在大多数情况下，这不是问题。我们可以通过 301 和 302 重定向转发 PageRank。从本质上讲，我们使用这些重定向来选择一个规范的。通过选择规范 URL，我们将所有发送到这些 URL 的信号集中到规范 URL。

With that said, here are examples of when to use a 301 redirect:  
话虽如此，以下是何时使用 301 重定向的示例：

- When you want content that was moved to a new location to be accessible with the old URL  
    当您希望可以使用旧 URL 访问已移动到新位置的内容时
- When you want to permanently migrate a website to a new domain  
    当您想要将网站永久迁移到新域时
- When you want to ensure that all pages are accessible via the preferred URL standard, such as HTTPS  
    当您希望确保所有页面都可以通过首选 URL 标准（如 HTTPS）访问时
- When you want to merge multiple pages or websites  
    当您想要合并多个页面或网站时

## How to implement 301 redirects?  
如何实施 301 重定向？

There are several different ways to implement 301 redirects; your choice depends on the server and CMS your website uses.   
有几种不同的方法可以实现 301 重定向;您的选择取决于您的网站使用的服务器和 CMS。

The most common method, however, is the one that involves editing the website’s .htaccess file, which can be found in your website’s root directory.   
然而，最常见的方法是涉及编辑网站的 .htaccess 文件的方法，该文件可以在您网站的根目录中找到。

If you’re looking to create a redirect for an individual page, for example, simply add the following line of code:   
例如，如果您希望为单个页面创建重定向，只需添加以下代码行：

_Redirect 301 /old-page.html /new-page.html  
重定向 301 /old-page.html /new-page.html_

One thing to keep in mind before you proceed is that there are different types of web servers, so it is possible that your website doesn’t run on an Apache server - which is the only one that uses .htaccess.   
在继续之前要记住的一件事是，有不同类型的 Web 服务器，因此您的网站可能不在 Apache 服务器上运行 - 这是唯一使用 .htaccess 的服务器。

In that case, these instructions wouldn’t work for you. Instead, you can check [this guide](https://www.bowlerhat.co.uk/301-redirects-for-seo-from-windows-server-iis) if your site runs on Windows/IIS - and [this](https://www.bjornjohansen.com/nginx-redirect) if it runs on Nginx.   
在这种情况下，这些说明对您不起作用。相反，如果您的网站在 Windows/IIS 上运行，您可以查看本指南 [- 如果它在](https://www.bjornjohansen.com/nginx-redirect) Nginx 上运行，则可以查看[本指南](https://www.bowlerhat.co.uk/301-redirects-for-seo-from-windows-server-iis)。

If you are using WordPress, you can simplify the process of implementing 301 redirects by using an SEO plugin:   
如果您使用的是 WordPress，您可以使用 SEO 插件简化实施 301 重定向的过程：

[RankMath](https://wordpress.org/plugins/seo-by-rank-math/), for example, is free and has this feature built-in. Another option for WordPress users is the free [Redirection plugin](https://wordpress.org/plugins/redirection/), which allows you to create and manage redirects with ease.  
例如，[RankMath](https://wordpress.org/plugins/seo-by-rank-math/) 是免费的，并且内置了此功能。WordPress 用户的另一个选择是免费的[重定向插件](https://wordpress.org/plugins/redirection/)，它允许您轻松创建和管理重定向。

## How to find and fix 301 redirect issues on your site  
如何查找并解决您网站上的 301 重定向问题

When trying to identify technical SEO issues - including problems with 301 redirects - the best approach is using website crawlers designed for that purpose.   
当尝试识别技术 SEO 问题（包括 301 重定向问题）时，最好的方法是使用为此目的设计的网站爬虫。

Ahrefs’ [Site Audit](https://ahrefs.com/site-audit) and [Webmaster Tools](https://ahrefs.com/webmaster-tools) will simplify this process - and make it easier to find any 301 redirect errors.   
Ahrefs [Site Audit（网站诊断](https://ahrefs.com/site-audit)）和 [Webmaster Tools（网站管理员工具](https://ahrefs.com/webmaster-tools)）将简化此过程 - 并更容易找到任何 301 重定向错误。

Here’s how you can identify any 301-redirect-related issues - and what you can do to fix them:   
以下是识别任何与 301 重定向相关的问题的方法 - 以及您可以采取哪些措施来修复它们：

Here are the most common 301-redirect-related issues - and what you can do to fix them:   
以下是最常见的 301 重定向相关问题 - 以及您可以采取哪些措施来修复它们：

### 1. HTTP pages 1. HTTP 页面

Considering the security-related benefits and the fact that Google recognized HTTPS (Hypertext Transfer Protocol Secure) as a [ranking signal](https://developers.google.com/search/blog/2014/08/https-as-ranking-signal) in 2014, it makes sense to have an [SSL](https://ahrefs.com/seo/glossary/secure-sockets-layer) certificate and migrate from HTTP to HTTPS.   
考虑到与安全相关的好处以及 Google 在 2014 年将 HTTPS（安全超文本传输协议）视为[排名信号](https://developers.google.com/search/blog/2014/08/https-as-ranking-signal)的事实，拥有 [SSL](https://ahrefs.com/seo/glossary/secure-sockets-layer) 证书并从 HTTP 迁移到 HTTPS 是有意义的。

When migrating to HTTPS, it’s typically recommended to do so by using 301 redirects. However, you could face some issues, such as failing to implement the HTTP to HTTPS redirect across all pages.   
迁移到 HTTPS 时，通常建议使用 301 重定向来实现。但是，您可能会遇到一些问题，例如无法在所有页面上实施 HTTP 到 HTTPS 重定向。

So, to ensure that your website’s visitors are actually seeing the HTTPS version of your website, use Ahrefs’ Site Audit to crawl your site and check the Internal pages report for any issues.   
因此，为了确保你网站的访问者真的看到你网站的 HTTPS 版本，请使用 Ahrefs Site Audit（网站诊断）来抓取你的网站并检查 Internal pages（内部页面）报告是否有任何问题。

### 2. Redirect chains 2. 重定向链

When there is more than one redirect between the original URL and the destination page, that is called a “redirect chain.”   
当原始 URL 和目标页面之间存在多个重定向时，这称为 “重定向链”。

While [Googlebot](https://ahrefs.com/seo/glossary/googlebot) doesn’t have an issue with following this chain of redirects, it might slow things down and affect the user experience negatively. It’s not a critical issue, but it is recommended to redirect directly to the destination page.   
虽然 [Googlebot](https://ahrefs.com/seo/glossary/googlebot) 在遵循此重定向链方面没有问题，但它可能会减慢速度并对用户体验产生负面影响。这不是一个关键问题，但建议直接重定向到目标页面。

If that’s not possible, keep the number of redirects in your “chain” low - no more than three or at least fewer than five.  
如果无法做到这一点，请将 “链” 中的重定向数量保持在较低水平 - 不超过 3 个或至少少于 5 个。

### 3. Broken redirects 3. 重定向损坏

Broken redirects are links that redirect the user (and search engine) to a dead page - or, more specifically, one that returns an HTTP 404 Not Found response status code.   
损坏的重定向是将用户（和搜索引擎）重定向到无效页面的链接 - 或者更具体地说，返回 HTTP 404 Not Found 响应状态代码的链接。

The issue with these so-called “dead” or broken links is that there is no way for Google’s bots or users to access the destination page, meaning they will likely leave the website.   
这些所谓的 “死 ”或断开的链接的问题在于，谷歌的机器人或用户无法访问目标页面，这意味着他们很可能会离开网站。

Once you’ve identified broken redirects in the Internal pages report, you can fix the errors by:   
在 Internal pages （内部页面） 报告中发现损坏的重定向后，您可以通过以下方式修复错误：

- Removing links that point to a redirected URL  
    删除指向重定向 URL 的链接
- Restoring the dead page (in case it has been removed by accident)  
    恢复失效页面（如果它被意外删除）

### 4. 301 redirects in a sitemap  
4. 站点地图中的 301 重定向

The [sitemap](https://ahrefs.com/seo/glossary/sitemap) is a list of all the pages on a site that you want Google - or any other search engine - to find and index. As such, it should only include canonical and indexable pages that you want to be featured in search results.   
[站点地图](https://ahrefs.com/seo/glossary/sitemap)是您希望 Google 或任何其他搜索引擎查找和索引的网站上所有页面的列表。因此，它应该只包含您希望在搜索结果中出现的规范和可索引页面。

And since a 301 redirect is permanent and implies that the initial URL is no longer in use, there’s no point in keeping such pages in your sitemap because Google will continue to crawl them.   
由于 301 重定向是永久性的，这意味着初始 URL 不再使用，因此在您的站点地图中保留此类页面是没有意义的，因为 Google 将继续抓取它们。

To find and remove 301 redirects from your sitemap, you can either:   
要从站点地图中查找并删除 301 重定向，您可以：

- Go to the sitemap URL (“domain.com/sitemap_index.xml” or “domain.com/sitemap.xml”), download all the URLs, and then use a free HTTP status code checker.  
    转到站点地图 URL（“domain.com/sitemap_index.xml”或“domain.com/sitemap.xml”），下载所有 URL，然后使用免费的 HTTP 状态代码检查器。
- Use Ahrefs’ Site Audit to crawl your site, check for “3XX redirect in sitemap” errors in the report overview, and replace these with the redirect URL.  
    使用 Ahrefs Site Audit（网站诊断）来抓取你的网站，检查报告概述中的 “3XX redirect in sitemap”（站点地图中的 3XX 重定向）错误，并将这些错误替换为重定向 URL。

### 5. External redirecting links  
5. 外部重定向链接

If your site contains links to relevant third-party websites, it would be wise to check for any “bad” external redirecting links from time to time.   
如果您的网站包含指向相关第三方网站的链接，那么不时检查任何“不良”的外部重定向链接是明智的。

Sometimes the resource you’re linking to gets redirected elsewhere, meaning that the URL now points to a different page - one that might be irrelevant or potentially harmful.   
有时，您链接到的资源会被重定向到其他位置，这意味着 URL 现在指向不同的页面 - 一个可能不相关或可能有害的页面。

Unless you have checked for issues related to external redirecting links, you will have no way of knowing that it happened - and you’ll continue linking to it unintentionally.   
除非你已经检查了与外部重定向链接相关的问题，否则你将无法知道它是否发生 - 并且你会继续无意中链接到它。

You can use the Ahrefs Site Audit or Webmaster Tools to discover any links that lead to external 301 URLs and remove them manually.   
你可以使用 Ahrefs Site Audit（网站诊断）或 Webmaster Tools（站长工具）来发现任何指向外部 301 URL 的链接并手动删除它们。