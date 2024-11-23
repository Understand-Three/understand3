---
title: 304 未修改
aliases:
  - 304 未修改
tags:
  - SEO
original: https://ahrefs.com/zh/seo/glossary/304-not-modified
draft: true
---
# 304 Not Modified 304 未修改

## What is 304 Not Modified Response?  
什么是 304 未修改响应？

The 304 Not Modified HTTP server response code indicates that the requested resource has not been modified since the last time it was loaded, and there’s no need to transfer it again.   
304 Not Modified HTTP 服务器响应代码表示请求的资源自上次加载以来未被修改，无需再次传输。

For browsers, this means that the cached version of the resource can be shown to the user. For crawlers, such as [Googlebot](https://ahrefs.com/seo/glossary/googlebot), it means that there’s no need to recrawl the page because nothing has changed on it.  
对于浏览器，这意味着可以向用户显示资源的缓存版本。对于抓取工具（例如 [Googlebot](https://ahrefs.com/seo/glossary/googlebot)），这意味着无需重新抓取该网页，因为该网页没有任何变化。

Here’s how it works (in simple terms):  
以下是它的工作原理（简单来说）：

1. When the client (browser or crawler) requests a resource from the web server for the first time, the server sends the requested resource (with the 200 OK HTTP code) along with its hash code, called `ETag`. The client also records the time when it requested the page/resource.  
    当客户端（浏览器或爬网程序）首次从 Web 服务器请求资源时，服务器会发送请求的资源（带有 200 OK HTTP 代码）及其哈希代码（称为 `ETag`）。客户端还会记录请求页面/资源的时间。
2. When the client requests the resource again, the server checks the `If-None-Match` and/or `If-Modified-Since` request readers from the client. This is a so-called _conditional HTTP request_.  
    当客户端再次请求资源时，服务器会检查来自客户端的 `If-None-Match`和/或 `If-Modified-Since` 请求读取器。这就是所谓的_条件 HTTP 请求_。
    
    `If-None-Match` contains the `ETag` (content hash code). If it matches the value on the server, this indicates that the content has not been changed, and there’s no need to load it again (when the content changes, so does its hash code).  
    `If-None-Match` 包含 `ETag`（内容哈希代码）。如果它与服务器上的值匹配，则表示内容尚未更改，无需再次加载它（当内容更改时，其哈希代码也会更改）。
    
    `If-Modified-Since` contains the date and time when the client last requested the content. If the server sees that content was not changed since this date, there’s no need to send the resource to the client.  
    `If-Modified-Since` 包含客户端上次请求内容的日期和时间。如果服务器发现内容自此日期以来未更改，则无需将资源发送到客户端。
    
    In both cases, the server will respond with the 304 HTTP code.  
    在这两种情况下，服务器都将使用 304 HTTP 代码进行响应。
    
    When both `If-None-Match` and `If-Modified-Since` are used, `If-None-Match` takes precedence over `If-Modified-Since`.  
    当同时使用 `If-None-Match` 和 `If-Modified-Since` 时，`If-None-Match` 优先于 `If-Modified-Since`。
    
3. When the browser receives the 304 Not Modified HTTP code from the server, it will show the cached version to the user. That is why 304 is one of the client-side redirection codes.  
    当浏览器从服务器收到 304 Not Modified HTTP 代码时，它将向用户显示缓存的版本。这就是为什么 304 是客户端重定向代码之一的原因。

## Why Is the 304 response code important?  
为什么 304 响应代码很重要？

For small websites, the caching opportunities that the 304 HTTP code provides are not that crucial.  
对于小型网站，304 HTTP 代码提供的缓存机会并不那么重要。

However, for large websites, the 304 response code is a great opportunity to save the [crawl budget](https://ahrefs.com/seo/glossary/crawl-budget). Google’s crawler won’t recrawl the pages that were not changed and will be able to crawl more new and updated pages instead.  
但是，对于大型网站，304 响应代码是节省[抓取预算](https://ahrefs.com/seo/glossary/crawl-budget)的绝佳机会。Google 的爬虫不会重新抓取未更改的页面，而是能够抓取更多新页面和更新的页面。