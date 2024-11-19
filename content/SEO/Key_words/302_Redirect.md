---
title: 302 临时重定向
original: https://ahrefs.com/zh/seo/glossary/302-redirect
---
# 302 Redirect 
302 临时重定向

## What is a 302 Redirect?  
什么是 302 重定向？

A 302 redirect indicates that the requested resource has been moved to another URL **temporarily**.  
302 重定向表示请求的资源已**临时**移动到另一个 URL。

The 302 Found HTTP response code sends the browser users to a new URL and informs the search engine crawlers that the redirection is temporary.   
302 Found HTTP 响应代码将浏览器用户发送到新 URL，并通知搜索引擎爬网程序重定向是临时的。

There are several ways to redirect users and search engines to a different URL, the two main ones being the [301](https://ahrefs.com/seo/glossary/301-redirect) and 302 redirects. While from the user’s standpoint, there’s virtually no difference between the two, search engines interpret these redirects differently.   
有几种方法可以将用户和搜索引擎重定向到不同的 URL，其中两种主要方法是 [301](https://ahrefs.com/seo/glossary/301-redirect) 和 302 重定向。虽然从用户的角度来看，两者之间几乎没有区别，但搜索引擎对这些重定向的解释不同。

Since the type of redirect you use can severely impact your SEO, you must choose the appropriate one based on whether the move to a new URL is permanent or temporary.   
由于您使用的重定向类型会严重影响您的 SEO，因此您必须根据移动到新 URL 是永久的还是临时的来选择合适的重定向。

You can add a 302 redirect and define the new URL by including the following bit of code in your .htaccess file (found in your website’s root directory):   
您可以通过在 .htaccess 文件（位于您网站的根目录中）中包含以下代码来添加 302 重定向并定义新 URL：

`Redirect 302 /old-page.html /new-page.html   重定向 302 /old-page.html /new-page.html`

In WordPress, you can use the [Redirections](https://wordpress.org/plugins/redirection/) plugin.  
在 WordPress 中，您可以使用 [Redirections](https://wordpress.org/plugins/redirection/) 插件。

## How is 302 redirect different from 301?   
302 重定向与 301 有何不同？

Given that the 301 and 302 redirects both take the user to a different URL, the user’s experience is no different. In other words, on the website visitor’s end, there will be no difference between these two types of redirects.   
鉴于 301 和 302 重定向都将用户带到不同的 URL，因此用户体验没有什么不同。换句话说，在网站访问者方面，这两种类型的重定向之间不会有什么区别。

However, from the search engines’ standpoint, there is a major difference between the two since it interprets and handles the URL redirects differently.   
但是，从搜索引擎的角度来看，两者之间存在重大差异，因为它解释和处理 URL 重定向的方式不同。

Here’s an example:  下面是一个示例：

If you use a [301 redirect](https://ahrefs.com/seo/glossary/301-redirect), you’re implying that a page has been moved permanently - and that you do not intend to bring it back at any point. This permanent redirect tells the browser that the desired webpage no longer exists at that URL.   
如果您使用 [301 重定向](https://ahrefs.com/seo/glossary/301-redirect)，则意味着页面已被永久移动 - 并且您不打算在任何时候将其恢复。此永久重定向告诉浏览器该 URL 中不再存在所需的网页。

In other words, it is no longer relevant to Google; the search engine will update its database and index the new URL instead, transferring [link equity](https://ahrefs.com/seo/glossary/link-equity) onto the new page.  
换句话说，它不再与 Google 相关;搜索引擎将更新其数据库并索引新 URL，将[链接资产](https://ahrefs.com/seo/glossary/link-equity)转移到新页面上。

But when you use a 302 redirect, you signal to Google that the move is temporary and that the initial URL will be used again at some point. So, there’s no need for Google to index the new URL, meaning you get to keep your traffic, rankings, and authority.   
但是，当您使用 302 重定向时，您向 Google 发出信号，表明移动是临时的，并且初始 URL 将在某个时候再次使用。因此，Google 无需为新 URL 编制索引，这意味着您可以保留流量、排名和权限。

However, you should note that Google will treat any **long-term** 302 redirects as 301 redirects.  
但是，您应该注意，Google 会将任何**长期的** 302 重定向视为 301 重定向。

## When to use the 302 redirects?   
何时使用 302 重定向？

Considering that the 302 redirect implies that the redirection is temporary, it should only be used in cases where you intend to return the original URL soon.   
考虑到 302 重定向意味着重定向是临时的，它只应在您打算很快返回原始 URL 的情况下使用。

For example, a 302 redirect should be used when:  
例如，在以下情况下应使用 302 重定向：

- You are doing A/B testing of a page to assess its functionality and design   
    您正在对页面进行 A/B 测试以评估其功能和设计
- You want to gather client feedback on a new page but don’t want to impact the website’s current ranking   
    您想在新页面上收集客户反馈，但又不想影响网站的当前排名
- You are updating a particular webpage but want to keep the user experience consistent  
    您正在更新特定网页，但希望保持用户体验一致
- You are dealing with a broken webpage but still want to provide a good user experience while you work on resolving the issues  
    您正在处理损坏的网页，但仍希望在解决问题时提供良好的用户体验
- You are running a promotion and want to redirect users to a temporary sales page  
    您正在开展促销活动，并希望将用户重定向到临时销售页面

The main point is that the 302 redirect is a temporary one. It should not be used for permanent redirection.  
重点是 302 重定向是临时的。它不应用于永久重定向。