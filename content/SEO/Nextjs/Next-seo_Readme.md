---
title: Next SEO
aliases:
  - Next SEO
original: 
description: 使用 app 目录时可以不用这个插件
---
# Next SEO

Next SEO 是一个插件，可让您更轻松地在 Next.js 项目中管理您的 SEO。

非常欢迎 Pull Request。如果您正在寻找有关要添加的内容的灵感，请务必查看功能请求的问题。


**关于应用目录的注意事项**

此说明仅在使用 `app` 目录时才有意义。

对于标准元数据（例如，`<title>`），强烈建议您使用内置的 `generateMetaData` 方法。您可以[在此处](https://beta.nextjs.org/docs/guides/seo#usage)查看文档

对于 JSON-LD，唯一需要的更改是将 `useAppDir={true}` 添加到正在使用的 JSON-LD 组件中。您应该在 `page.js`中添加 use this 组件，而不是在 `head.js` 中添加。

```html
<ArticleJsonLd
  useAppDir={true}
  url="https://example.com/article"
  title="Article headline" <- required for app directory
  />
```

如果您使用的是 **`pages`** 目录，那么 `NextSeo` **正是您满足** SEO 需求所需要的！


## 用法

`NextSeo` 的工作原理是将其包含在您希望添加 SEO 属性的页面上。一旦包含在页面中，您就向其传递一个包含页面 SEO 属性的配置对象。这可以在页面级别动态生成，或者在某些情况下，您的 API 可能会返回 SEO 对象。

### 设置

首先，安装它：

```shell
npm install next-seo
```

或

```shell
yarn add next-seo
```

### Add SEO to Page 将 SEO 添加到页面

使用 Next.js 13 中引入Next.js应用程序目录？

如果您使用的是 Next.js 的 app 目录，则强烈建议您使用内置的 `generateMetaData` 方法。您可以[在此处](https://beta.nextjs.org/docs/guides/seo#usage)查看文档

如果您使用的是 `pages` 目录，那么 `NextSeo` 正是您的 SEO 需求所需要的！

然后，您需要导入 `NextSeo` 并添加所需的属性。这将呈现 `<head>` 中用于 SEO 的标签。至少应添加标题和描述。

**仅包含 title 和 description 的示例：**

```js
import { NextSeo } from 'next-seo';

const Page = () => (
  <>
    <NextSeo
      title="Simple Usage Example"
      description="A short description goes here."
    />
    <p>Simple Usage</p>
  </>
);

export default Page;
```

但是 `NextSeo` 为您提供了更多可以添加的选项。请参阅下面的页面典型示例。

**Typical page example: 典型页面示例：**

```js
import { NextSeo } from 'next-seo';

const Page = () => (
  <>
    <NextSeo
      title="Using More of Config"
      description="This example uses more of the available config options."
      canonical="https://www.canonical.ie/"
      openGraph={{
        url: 'https://www.url.ie/a',
        title: 'Open Graph Title',
        description: 'Open Graph Description',
        images: [
          {
            url: 'https://www.example.ie/og-image-01.jpg',
            width: 800,
            height: 600,
            alt: 'Og Image Alt',
            type: 'image/jpeg',
          },
          {
            url: 'https://www.example.ie/og-image-02.jpg',
            width: 900,
            height: 800,
            alt: 'Og Image Alt Second',
            type: 'image/jpeg',
          },
          { url: 'https://www.example.ie/og-image-03.jpg' },
          { url: 'https://www.example.ie/og-image-04.jpg' },
        ],
        siteName: 'SiteName',
      }}
      twitter={{
        handle: '@handle',
        site: '@site',
        cardType: 'summary_large_image',
      }}
    />
    <p>SEO Added to Page</p>
  </>
);

export default Page;
```

**关于 Twitter 标签的说明**

props `cardType`， `site`， `handle` 等同于 `twitter：card`， `twitter：site`， `twitter：creator`。可[在此处](https://developer.twitter.com/en/docs/twitter-for-websites/cards/overview/summary)找到文档。

Twitter 将读取其卡片的 `og：title`、`og：image` 和 `og：description` 标签。`next-seo` 省略了 `twitter：title`、`twitter：image` 和 `twitter：description` 以避免重复。

某些工具可能会将此报告为错误。查看 [Issue #14](https://github.com/garmeeh/next-seo/issues/14)

### 默认 SEO 配置

`NextSeo` 使您能够设置一些默认的 SEO 属性，这些属性将出现在所有页面上，而无需在其上包含任何内容。如果需要，您还可以逐页覆盖这些内容。

要实现此目的，您需要创建自定义 `<App>`。在 pages 目录中，创建一个新文件 `_app.js`。有关自定义 `<App>` 的更多信息，请参阅[此处](https://nextjs.org/docs/advanced-features/custom-app)的 Next.js 文档。

在此文件中，您需要从 `next-seo` 导入 `DefaultSeo` 并为其传递 props。

下面是一个典型的示例：

```js
import App, { Container } from 'next/app';
import { DefaultSeo } from 'next-seo';

// import your default seo configuration
import SEO from '../next-seo.config';

export default class MyApp extends App {
  render() {
    const { Component, pageProps } = this.props;
    return (
      <Container>
        <DefaultSeo
          openGraph={{
            type: 'website',
            locale: 'en_IE',
            url: 'https://www.url.ie/',
            siteName: 'SiteName',
          }}
          twitter={{
            handle: '@handle',
            site: '@site',
            cardType: 'summary_large_image',
          }}
        />
        <Component {...pageProps} />
      </Container>
    );
  }
}
```

为了正常工作，由于 Next.js 内部的行为，`DefaultSeo` 应该放在 `Component` 的上方（之前）。

或者，您也可以创建一个配置文件来存储默认值，例如 `next-seo.config.js`

```js
export default {
  openGraph: {
    type: 'website',
    locale: 'en_IE',
    url: 'https://www.url.ie/',
    siteName: 'SiteName',
  },
  twitter: {
    handle: '@handle',
    site: '@site',
    cardType: 'summary_large_image',
  },
};
```

或者像这样，如果你使用的是 TypeScript

```ts
import { DefaultSeoProps } from 'next-seo';

const config: DefaultSeoProps = {
  openGraph: {
    type: 'website',
    locale: 'en_IE',
    url: 'https://www.url.ie/',
    siteName: 'SiteName',
  },
  twitter: {
    handle: '@handle',
    site: '@site',
    cardType: 'summary_large_image',
  },
};

export default config;
```

Import 在 `_app.js` 的顶部

```js
import SEO from '../next-seo.config';
```

`DefaultSeo` 组件可以像这样使用

```js
<DefaultSeo {...SEO} />
```

从现在开始，您的所有页面都将应用上述默认值。

**请注意，`Container` 在 Next.js v9.0.4 中已弃用，因此在此版本及更高版本中，您应该将该组件替换为 `React.Fragment` - 请参阅[此处](https://github.com/zeit/next.js/blob/master/errors/app-container-deprecated.md)**

### NextSeo 选项

| Property                                                         | Name         | Type                                        | Description                                                                                                                                                                                                                                                                                                                                                                         |
| ---------------------------------------------------------------- | ------------ | ------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `titleTemplate`                                                  | 标题模板         | string 字符串                                  | 允许您设置将添加到标题的默认标题模板 [更多信息](https://github.com/garmeeh/next-seo?tab=readme-ov-file#title-template)                                                                                                                                                                                                                                                                                    |
| `title`                                                          | 标题           | string 字符串                                  | 设置页面的元标题                                                                                                                                                                                                                                                                                                                                                                            |
| `defaultTitle`                                                   | 默认标题         | string 字符串                                  | 如果未在页面上设置标题，则将使用此字符串而不是空的 `titleTemplate`[更多信息](https://github.com/garmeeh/next-seo?tab=readme-ov-file#default-title)                                                                                                                                                                                                                                                               |
| `noindex`                                                        | 无索引          | boolean (default false) boolean （默认为 false） | Sets whether page should be indexed or not [More Info](https://github.com/garmeeh/next-seo?tab=readme-ov-file#no-index)  <br>设置是否应将页面编入索引 [更多信息](https://github.com/garmeeh/next-seo?tab=readme-ov-file#no-index)                                                                                                                                                                   |
| `nofollow`                                                       | 不跟随          | boolean (default false) boolean （默认为 false） | Sets whether page should be followed or not [More Info](https://github.com/garmeeh/next-seo?tab=readme-ov-file#no-follow)  <br>设置是否应关注页面 [更多信息](https://github.com/garmeeh/next-seo?tab=readme-ov-file#no-follow)                                                                                                                                                                   |
| `robotsProps`                                                    | 机器人属性        | Object 对象                                   | Set the more meta information for the `X-Robots-Tag` [More Info](https://github.com/garmeeh/next-seo?tab=readme-ov-file#robotsprops)  <br>为 `X-Robots-Tag`[更多信息](https://github.com/garmeeh/next-seo?tab=readme-ov-file#robotsprops)设置更多元信息                                                                                                                                         |
| `description`                                                    | 描述           | string 字符串                                  | Set the page meta description  <br>设置页面元描述                                                                                                                                                                                                                                                                                                                                          |
| `canonical`                                                      | 规范           | string 字符串                                  | Set the page canonical url  <br>设置页面规范 URL                                                                                                                                                                                                                                                                                                                                          |
| `mobileAlternate.media`                                          | 移动替代媒体       | string 字符串                                  | Set what screen size the mobile website should be served from  <br>设置应从中提供移动网站的屏幕大小                                                                                                                                                                                                                                                                                                 |
| `mobileAlternate.href mobileAlternate.href 中`                    |              | string 字符串                                  | Set the mobile page alternate url  <br>设置移动页面备用 URL                                                                                                                                                                                                                                                                                                                                 |
| `languageAlternates`                                             | language替代   | array 数组                                    | 设置备用 URL 的语言。期望对象数组的形状为：`{ hrefLang： string， href： string }`                                                                                                                                                                                                                                                                                                                        |
| `themeColor`                                                     | 主题颜色         | string 字符串                                  | 指示用户代理应该使用的建议颜色来自定义页面或周围用户界面的显示。必须包含有效的 CSS 颜色                                                                                                                                                                                                                                                                                                                                      |
| `additionalMetaTags`                                             |              | array 数组                                    | 允许您添加此处未记录的 meta 标记。[更多信息](https://github.com/garmeeh/next-seo?tab=readme-ov-file#additional-meta-tags)                                                                                                                                                                                                                                                                             |
| `additionalLinkTags`                                             |              | array 数组                                    | 允许您添加此处未记录的 link 标签。[更多信息](https://github.com/garmeeh/next-seo?tab=readme-ov-file#additional-link-tags)                                                                                                                                                                                                                                                                             |
| `twitter.cardType `                                              | twitter 卡片类型 | string 字符串                                  | The card type, which will be one of `summary`, `summary_large_image`, `app`, or `player`  <br>卡片类型，可以是 `summary`、`summary_large_image`、`app` 或 `player` 之一                                                                                                                                                                                                                          |
| `twitter.site`                                                   |              | string 字符串                                  | @username 卡片页脚中使用的网站                                                                                                                                                                                                                                                                                                                                                                |
| `twitter.handle twitter.句柄`                                      |              | string 字符串                                  | 内容创建者/作者的@username（输出为 `twitter：creator`）                                                                                                                                                                                                                                                                                                                                           |
| `facebook.appId`                                                 |              | string 字符串                                  | 用于 Facebook Insights，您必须将 Facebook 应用程序 ID 添加到您的页面[才能了解更多信息](https://github.com/garmeeh/next-seo?tab=readme-ov-file#facebook)                                                                                                                                                                                                                                                       |
| `openGraph.url openGraph.url 中`                                  |              | string 字符串                                  | The canonical URL of your object that will be used as its permanent ID in the graph  <br>对象的规范 URL，该 URL 将用作其在图形中的永久 ID                                                                                                                                                                                                                                                             |
| `openGraph.type`                                                 |              | string 字符串                                  | The type of your object. Depending on the type you specify, other properties may also be required [More Info](https://github.com/garmeeh/next-seo?tab=readme-ov-file#open-graph)  <br>对象的类型。根据您指定的类型，可能还需要其他属性 [更多信息](https://github.com/garmeeh/next-seo?tab=readme-ov-file#open-graph)                                                                                            |
| `openGraph.title`                                                |              | string 字符串                                  | The open graph title, this can be different than your meta title.  <br>打开的图形标题，这可能与您的元标题不同。                                                                                                                                                                                                                                                                                         |
| `openGraph.description`                                          |              | string 字符串                                  | The open graph description, this can be different than your meta description.  <br>打开的图形描述，这可能与您的元描述不同。                                                                                                                                                                                                                                                                             |
| `openGraph.images`                                               |              | array 数组                                    | An array of images (object) to be used by social media platforms, slack etc as a preview. If multiple supplied you can choose one when sharing. [See Examples](https://github.com/garmeeh/next-seo?tab=readme-ov-file#open-graph-examples)  <br>供社交媒体平台、Slack 等用作预览的图像（对象）数组。如果提供了多个，您可以在共享时选择一个。[查看示例](https://github.com/garmeeh/next-seo?tab=readme-ov-file#open-graph-examples) |
| `openGraph.videos openGraph.videos 视频`                           |              | array 数组                                    | 视频数组 （对象）                                                                                                                                                                                                                                                                                                                                                                           |
| `openGraph.locale openGraph.locale 中`                            |              | string 字符串                                  | 标记打开的图形标记的区域设置。的格式 language_TERRITORY。默认值为 en_US。                                                                                                                                                                                                                                                                                                                                   |
| `openGraph.siteName`                                             |              | string 字符串                                  | 如果对象是较大 Web 站点的一部分，则为整个 Web 站点显示的名称。                                                                                                                                                                                                                                                                                                                                                |
| `openGraph.profile.firstName`                                    |              | string 字符串                                  | 人员的名字。                                                                                                                                                                                                                                                                                                                                                                              |
| `openGraph.profile.lastName`                                     |              | string 字符串                                  | 人员的姓氏。                                                                                                                                                                                                                                                                                                                                                                              |
| `openGraph.profile.username`                                     |              | string 字符串                                  | 人员的用户名。                                                                                                                                                                                                                                                                                                                                                                             |
| `openGraph.profile.gender`                                       |              | string 字符串                                  | 人员的性别。                                                                                                                                                                                                                                                                                                                                                                              |
| `openGraph.book.authors`                                         |              | string[] 字符串[]                              | 文章的作者。[查看示例](https://github.com/garmeeh/next-seo?tab=readme-ov-file#open-graph-examples)                                                                                                                                                                                                                                                                                            |
| `openGraph.book.isbn 打开Graph.book.isbn`                          |              | string 字符串                                  | [国际标准书号](https://en.wikipedia.org/wiki/International_Standard_Book_Number)                                                                                                                                                                                                                                                                                                          |
| `openGraph.book.releaseDate`                                     |              | datetime 日期时间                               | The date the book was released.  <br>图书的发行日期。                                                                                                                                                                                                                                                                                                                                       |
| `openGraph.book.tags`                                            |              | string[] 字符串[]                              | Tag words associated with this book.  <br>标记与此图书关联的单词。                                                                                                                                                                                                                                                                                                                              |
| `openGraph.article.publishedTime`                                |              | datetime 日期时间                               | When the article was first published. [See Examples](https://github.com/garmeeh/next-seo?tab=readme-ov-file#open-graph-examples)  <br>文章首次发布时。[查看示例](https://github.com/garmeeh/next-seo?tab=readme-ov-file#open-graph-examples)                                                                                                                                                    |
| `openGraph.article.modifiedTime`                                 |              | datetime 日期时间                               | When the article was last changed.  <br>文章上次更改的时间。                                                                                                                                                                                                                                                                                                                                  |
| `openGraph.article.expirationTimeopenGraph.article.expiration时间` |              | datetime 日期时间                               | When the article is out of date after.  <br>当文章过期时。                                                                                                                                                                                                                                                                                                                                 |
| `openGraph.article.authors`                                      |              | string[] 字符串[]                              | Writers of the article. 文章的作者。                                                                                                                                                                                                                                                                                                                                                      |
| `openGraph.article.section`                                      |              | string 字符串                                  | A high-level section name. E.g. Technology  <br>高级部分名称。例如技术                                                                                                                                                                                                                                                                                                                         |
| `openGraph.article.tags`                                         |              | string[] 字符串[]                              | Tag words associated with this article.  <br>标记与本文关联的单词。                                                                                                                                                                                                                                                                                                                            |

#### Title Template 标题模板

[](https://github.com/garmeeh/next-seo?tab=readme-ov-file#title-template)

Replaces `%s` with your title string  
将 `%s` 替换为您的标题字符串

```js
title = 'This is my title';
titleTemplate = 'Next SEO | %s';
// outputs: Next SEO | This is my title
```

```js
title = 'This is my title';
titleTemplate = '%s | Next SEO';
// outputs: This is my title | Next SEO
```

#### 默认标题（Title）

```js
title = undefined;
titleTemplate = 'Next SEO | %s';
defaultTitle = 'Next SEO';
// outputs: Next SEO
```

#### 无索引（No Index ）

将此项设置为 `true` 将设置 `noindex，follow` （要设置 `nofollow`，请参考 [`nofollow`](https://github.com/garmeeh/next-seo?tab=readme-ov-file#no-follow)）。这是逐页进行的。此属性与 `nofollow` 属性协同工作，它们一起填充 `robots` 元标记。

**注意：**`noindex` 和 [`nofollow`](https://github.com/garmeeh/next-seo?tab=readme-ov-file#no-follow) 属性与所有其他属性略有不同，因为它们设置为默认值不会按预期工作。这是因为 Next SEO 已经默认了 `index，follow` 因为 `next-seo` 毕竟是一个 SEO 插件。因此，如果您想全局地使用这些属性，请参阅 [dangerouslySetAllPagesToNoIndex](https://github.com/garmeeh/next-seo?tab=readme-ov-file#dangerouslySetAllPagesToNoIndex) 和 [dangerouslySetAllPagesToNoFollow](https://github.com/garmeeh/next-seo?tab=readme-ov-file#dangerouslySetAllPagesToNoFollow)。

**单个页面上无索引的示例：**

如果您有一个不想编入索引的页面，您可以通过以下方式实现此目的：

```js
import { NextSeo } from 'next-seo';

const Page = () => (
  <>
    <NextSeo noindex={true} />
    <p>This page is no indexed</p>
  </>
);

export default Page;

/*
<meta name="robots" content="noindex,follow">
*/
```

#### dangerouslySetAllPagesToNoIndex

它有 `Dangerous` 的前缀，因为它会对所有页面`进行 noindex`。由于这是一个 SEO 插件，这是一个有点危险的行为。使用这个**还不错**。只是请确保您要对**每个**页面`都进行 noindex`。如果您有`为页面编制索引`的用例，您仍然可以在页面级别覆盖此 URL。这可以通过设置 `noindex： false` 来完成。

取消设置它的唯一方法是从自定义 `<App>` 中的 `DefaultSeo` 中删除 prop。

#### 不跟随（No Follow ）

将此设置为 `true` 将设置 `index，nofollow`（要设置 `noindex`，请参考 [`noindex`](https://github.com/garmeeh/next-seo?tab=readme-ov-file#no-index)）。这是逐页进行的。此属性与 `noindex` 属性协同工作，它们一起填充 `robots` 元标记。

**注意**：与其他属性不同，默认情况下设置 `noindex` 和 `nofollow` 不会按预期工作。这是因为 Next SEO 默认为 `index，follow`，因为 `next-seo` 毕竟是一个 SEO 插件。如果要全局允许这些属性，请参阅 [dangerouslySetAllPagesToNoIndex](https://github.com/garmeeh/next-seo?tab=readme-ov-file#dangerouslySetAllPagesToNoIndex) 和 [dangerouslySetAllPagesToNoFollow](https://github.com/garmeeh/next-seo?tab=readme-ov-file#dangerouslySetAllPagesToNoFollow)。

**单个页面上的 No Follow 示例：**

如果您有一个不想编入索引的页面，您可以通过以下方式实现此目的：

```js
import { NextSeo } from 'next-seo';

const Page = () => (
  <>
    <NextSeo nofollow={true} />
    <p>This page is not followed</p>
  </>
);

export default Page;

/*
<meta name="robots" content="index,nofollow">
*/
```

#### dangerouslySetAllPagesToNoFollow

它的前缀是 `dangerous`，因为它不会 `nofollow` 所有页面。由于这是一个 SEO 插件，这是一个有点危险的行为。使用这个**还不错**。只是请确保您想要 `nofollow`**每个**页面。如果您有`关注`页面的用例，您仍然可以在页面级别覆盖此权限。这可以通过设置 `nofollow： false` 来完成。

取消设置它的唯一方法是从自定义 `<App>` 中的 `DefaultSeo` 中删除 prop。

| `noindex 无索引` | `nofollow 不跟随` | `meta` content of `robots`  <br>`机器人`的`元`内容       |
| ------------- | -------------- | ------------------------------------------------- |
| --            | --             | `index,follow` (default)  <br>`index，follow` （默认） |
| false 假       | false 假        | `index,follow 索引，关注`                              |
| true 真        | --             | `noindex,follow noindex，关注`                       |
| true 真        | false 假        | `noindex,follow noindex，关注`                       |
| --            | true 真         | `index,nofollow 索引，nofollow`                      |
| false 假       | true 真         | `index,nofollow 索引，nofollow`                      |
| true 真        | true 真         | `noindex,nofollow noindex，nofollow`               |

#### robotsProps 机器人属性

除了索引之外`，follow` `robots` meta tag 接受更多属性以存档更准确的抓取，并为抓取您的页面的 SEO 机器人提供更好的片段。

例子：

```js
import { NextSeo } from 'next-seo';

const Page = () => (
  <>
    <NextSeo
      robotsProps={{
        nosnippet: true,
        notranslate: true,
        noimageindex: true,
        noarchive: true,
        maxSnippet: -1,
        maxImagePreview: 'none',
        maxVideoPreview: -1,
      }}
    />
    <p>Additional robots props in Next-SEO!!</p>
  </>
);

export default Page;

/*
<meta name="robots" content="index,follow,nosnippet,max-snippet:-1,max-image-preview:none,noarchive,noimageindex,max-video-preview:-1,notranslate">
*/
```

**Available properties 可用属性**

|Property 财产|Type 类型|Description 描述|
|---|---|---|
|`noarchive 无存档`|boolean 布尔|Do not show a [cached link](https://support.google.com/websearch/answer/1687222) in search results.  <br>不要在搜索结果中显示[缓存的链接](https://support.google.com/websearch/answer/1687222)。|
|`nosnippet nosnippet （无摘要）`|boolean 布尔|Do not show a text snippet or video preview in the search results for this page.  <br>请勿在此网页的搜索结果中显示文本片段或视频预览。|
|`max-snippet`|number 数|Use a maximum of [number] characters as a textual snippet for this search result. [Read more](https://developers.google.com/search/reference/robots_meta_tag?hl=en-GB#directives)  <br>最多使用 [number] 个字符作为此搜索结果的文本片段。[阅读更多](https://developers.google.com/search/reference/robots_meta_tag?hl=en-GB#directives)|
|`max-image-preview 最大图像预览`|'none','standard','large'  <br>'无'，'标准'，'大'|Set the maximum size of an image preview for this page in a search results.  <br>设置搜索结果中此页面的图像预览的最大大小。|
|`max-video-preview 最大视频预览`|number 数|Use a maximum of [number] seconds as a video snippet for videos on this page in search results. [Read more](https://developers.google.com/search/reference/robots_meta_tag?hl=en-GB#directives)  <br>对于搜索结果中此页面上的视频，使用最多 [number] 秒作为视频片段。[阅读更多](https://developers.google.com/search/reference/robots_meta_tag?hl=en-GB#directives)|
|`notranslate 无翻译`|boolean 布尔|Do not offer translation of this page in search results.  <br>请勿在搜索结果中提供此页面的翻译。|
|`noimageindex noimage索引`|boolean 布尔|Do not index images on this page.  <br>请勿在此页面上为图像编制索引。|
|`unavailable_after`|string 字符串|Do not show this page in search results after the specified date/time. The date/time must be specified in a widely adopted format including, but not limited to RFC 822, RFC 850, and ISO 8601.  <br>在指定的日期/时间之后，不要在搜索结果中显示此页面。日期/时间必须以广泛采用的格式指定，包括但不限于 RFC 822、RFC 850 和 ISO 8601。|

For more reference about the `X-Robots-Tag` visit [Google Search Central - Control Crawling and Indexing](https://developers.google.com/search/reference/robots_meta_tag?hl=en-GB#directives)  
有关 `X-Robots-Tag` 的更多参考资料，请访问 [Google 搜索中心 - 控制抓取和索引](https://developers.google.com/search/reference/robots_meta_tag?hl=en-GB#directives)

#### Twitter 

Twitter 会读取他们卡片的 `og：title`、`og：image` 和 `og：description` 标签，这就是为什么 `next-seo` 省略`了 twitter：title`、`twitter：image` 和 `twitter：description` 以免重复。

某些工具可能会将此报告为错误。查看 [Issue #14](https://github.com/garmeeh/next-seo/issues/14)

#### Facebook

```js
facebook={{
  appId: '1234567890',
}}
```

如果您需要为您的网站启用 Facebook Insights，请将其添加到您的 SEO 配置中以包含 fb：app_id 元。有关这方面的信息可以在 Facebook [的文档](https://developers.facebook.com/docs/sharing/webmasters/)中找到

#### Canonical URL 规范 URL

当您要合并重复的 URL 时，请逐页添加此项。

```js
canonical = 'https://www.canonical.ie/';
```

#### Alternate 互生

此链接关系用于指示桌面网站和移动网站与搜索引擎之间的关系。

例子：

```js
mobileAlternate={{
  media: 'only screen and (max-width: 640px)',
  href: 'https://m.canonical.ie',
}}
```

```js
languageAlternates={[{
  hrefLang: 'de-AT',
  href: 'https://www.canonical.ie/de',
}]}
```

#### Additional Meta Tags 其他 Meta 标记

这允许你添加`配置`中未涵盖的任何其他 meta 标签，这些标签应该使用 children prop 来代替 `children` prop。

`content` 是必需的。然后是 `name`、`property` 或 `httpEquiv`。（每个只有一个）

Example: 例：

```js
additionalMetaTags={[{
  property: 'dc:creator',
  content: 'Jane Doe'
}, {
  name: 'application-name',
  content: 'NextSeo'
}, {
  httpEquiv: 'x-ua-compatible',
  content: 'IE=edge; chrome=1'
}]}
```

无效示例：

这些是无效的，因为它们在同一条目上包含多个 `name`、`property` 和 `httpEquiv`。

```js
additionalMetaTags={[{
  property: 'dc:creator',
  name: 'dc:creator',
  content: 'Jane Doe'
}, {
  property: 'application-name',
  httpEquiv: 'application-name',
  content: 'NextSeo'
}]}
```

需要注意的一点是，它目前仅支持唯一标签，除非你使用 `keyOverride` 属性为每个额外的 meta 标签提供唯一的[键](https://reactjs.org/docs/lists-and-keys.html#keys)。

默认行为（没有 `keyOverride` 属性）是为每个唯一`名称` / `属性` / `httpEquiv` 渲染一个标签。将呈现定义的最后一个。

例如，如果您传递 2 个具有相同`property`的标记：

```js
additionalMetaTags={[{
  property: 'dc:creator',
  content: 'Joe Bloggs'
}, {
  property: 'dc:creator',
  content: 'Jane Doe'
}]}
```

it will result in this being rendered:  
它将导致 this 被渲染：

```html
<meta property="dc:creator" content="Jane Doe" />
```

提供一个额外的 `keyOverride` 属性，如下所示：

```js
additionalMetaTags={[{
  property: 'dc:creator',
  content: 'Joe Bloggs',
  keyOverride: 'creator1',
}, {
  property: 'dc:creator',
  content: 'Jane Doe',
  keyOverride: 'creator2',
}]}
```

导致呈现正确的 HTML：

```html
<meta property="dc:creator" content="Joe Bloggs" />
<meta property="dc:creator" content="Jane Doe" />
```

#### 其他链接标签

这允许您添加`config`中未涵盖的任何其他链接标签。

`rel` 和 `href` 是必需的。

例子：

```js
additionalLinkTags={[
  {
    rel: 'icon',
    href: 'https://www.test.ie/favicon.ico',
  },
  {
    rel: 'apple-touch-icon',
    href: 'https://www.test.ie/touch-icon-ipad.jpg',
    sizes: '76x76'
  },
  {
    rel: 'manifest',
    href: '/manifest.json'
  },
  {
    rel: 'preload',
    href: 'https://www.test.ie/font/sample-font.woof2',
    as: 'font',
    type: 'font/woff2',
    crossOrigin: 'anonymous'
  }
]}
```

it will result in this being rendered:  
它将导致 this 被渲染：

```html
<link rel="icon" href="https://www.test.ie/favicon.ico" />
<link
  rel="apple-touch-icon"
  href="https://www.test.ie/touch-icon-ipad.jpg"
  sizes="76x76"
/>
<link rel="manifest" href="/manifest.json" />
<link
  rel="preload"
  href="https://www.test.ie/font/sample-font.woof2"
  as="font"
  type="font/woff2"
  crossorigin="anonymous"
/>
```

## Open Graph

有关完整规格，请查看 [http://ogp.me/](http://ogp.me/)

Next SEO 目前支持：

- [basic 基本](https://github.com/garmeeh/next-seo?tab=readme-ov-file#basic)
- [video 视频](https://github.com/garmeeh/next-seo?tab=readme-ov-file#video)
- [article 品](https://github.com/garmeeh/next-seo?tab=readme-ov-file#article)
- [book 书](https://github.com/garmeeh/next-seo?tab=readme-ov-file#book)
- [profile 轮廓](https://github.com/garmeeh/next-seo?tab=readme-ov-file#profile)

### Open Graph 示例
#### Basic 基本

```js
import { NextSeo } from 'next-seo';

const Page = () => (
  <>
    <NextSeo
      openGraph={{
        type: 'website',
        url: 'https://www.example.com/page',
        title: 'Open Graph Title',
        description: 'Open Graph Description',
        images: [
          {
            url: 'https://www.example.ie/og-image.jpg',
            width: 800,
            height: 600,
            alt: 'Og Image Alt',
          },
          {
            url: 'https://www.example.ie/og-image-2.jpg',
            width: 800,
            height: 600,
            alt: 'Og Image Alt 2',
          },
        ],
      }}
    />
    <p>Basic</p>
  </>
);

export default Page;
```

**注意**

next.js版本 `7.0.0-canary.0` 中提供了多个映像

对于版本 `6.0.0` - `7.0.0-canary.0`，您只需提供一个项目数组：

```js
images: [
  {
    url: 'https://www.example.ie/og-image-01.jpg',
    width: 800,
    height: 600,
    alt: 'Og Image Alt',
  },
],
```

提供多张图片不会破坏任何东西，但只会将一张图片添加到头部。

#### Video 视频

[http://ogp.me/](http://ogp.me/#type_video) 的完整信息

```js
import { NextSeo } from 'next-seo';

const Page = () => (
  <>
    <NextSeo
      title="Video Page Title"
      description="Description of video page"
      openGraph={{
        title: 'Open Graph Video Title',
        description: 'Description of open graph video',
        url: 'https://www.example.com/videos/video-title',
        type: 'video.movie',
        video: {
          // Multiple Open Graph actors is only available in version `7.0.2-canary.35`+ of next
          actors: [
            {
              profile: 'https://www.example.com/actors/@firstnameA-lastnameA',
              role: 'Protagonist',
            },
            {
              profile: 'https://www.example.com/actors/@firstnameB-lastnameB',
              role: 'Antagonist',
            },
          ],
          // Multiple Open Graph directors is only available in version `7.0.2-canary.35`+ of next
          directors: [
            'https://www.example.com/directors/@firstnameA-lastnameA',
            'https://www.example.com/directors/@firstnameB-lastnameB',
          ],
          // Multiple Open Graph writers is only available in version `7.0.2-canary.35`+ of next
          writers: [
            'https://www.example.com/writers/@firstnameA-lastnameA',
            'https://www.example.com/writers/@firstnameB-lastnameB',
          ],
          duration: 680000,
          releaseDate: '2022-12-21T22:04:11Z',
          // Multiple Open Graph tags is only available in version `7.0.2-canary.35`+ of next
          tags: ['Tag A', 'Tag B', 'Tag C'],
        },
        siteName: 'SiteName',
      }}
    />
    <h1>Video Page SEO</h1>
  </>
);

export default Page;
```

**注意**

next.js版本 `7.0.0-canary.0` 中提供了多个映像

对于版本 `6.0.0` - `7.0.0-canary.0`，您只需提供一个项目数组：

```js
images: [
  {
    url: 'https://www.example.ie/og-image-01.jpg',
    width: 800,
    height: 600,
    alt: 'Og Image Alt',
  },
],
```

提供多张图片不会破坏任何东西，但只会将一张图片添加到头部。

#### Audio 音频

[http://ogp.me/](https://ogp.me/#structured) 的完整信息

```js
import { NextSeo } from 'next-seo';
const Page = () => (
  <>
    <NextSeo
      title="Audio Page Title"
      description="Description of audio page"
      openGraph={{
        title: 'Open Graph Audio',
        description: 'Description of open graph audio',
        url: 'https://www.example.com/audio/audio',
        audio: [
          {
            url: 'http://examples.opengraphprotocol.us/media/audio/1khz.mp3',
            secureUrl: 'https://d72cgtgi6hvvl.cloudfront.net/media/audio/1khz.mp3',
            type: "audio/mpeg"
          },
          {
            url: 'http://examples.opengraphprotocol.us/media/audio/250hz.mp3',
            secureUrl: 'https://d72cgtgi6hvvl.cloudfront.net/media/audio/250hz.mp3',
            type: "audio/mpeg"
          },
        ]
        site_name: 'SiteName',
      }}
    />
    <h1>Audio Page SEO</h1>
  </>
);
export default Page;
```

#### Article 文章

```js
import { NextSeo } from 'next-seo';

const Page = () => (
  <>
    <NextSeo
      openGraph={{
        title: 'Open Graph Article Title',
        description: 'Description of open graph article',
        url: 'https://www.example.com/articles/article-title',
        type: 'article',
        article: {
          publishedTime: '2017-06-21T23:04:13Z',
          modifiedTime: '2018-01-21T18:04:43Z',
          expirationTime: '2022-12-21T22:04:11Z',
          section: 'Section II',
          authors: [
            'https://www.example.com/authors/@firstnameA-lastnameA',
            'https://www.example.com/authors/@firstnameB-lastnameB',
          ],
          tags: ['Tag A', 'Tag B', 'Tag C'],
        },
        images: [
          {
            url: 'https://www.test.ie/images/cover.jpg',
            width: 850,
            height: 650,
            alt: 'Photo of text',
          },
        ],
      }}
    />
    <p>Article</p>
  </>
);

export default Page;
```

**注意**

版本 `7.0.0-canary.0` next.js提供了多个图像、作者和标签

对于版本 `6.0.0` - `7.0.0-canary.0`，您只需提供一个项目数组：

`images:`

```js
images: [
  {
    url: 'https://www.example.ie/og-image-01.jpg',
    width: 800,
    height: 600,
    alt: 'Og Image Alt',
  },
],
```

`authors:`

```js
authors: [
  'https://www.example.com/authors/@firstnameA-lastnameA',
],
```

`tags:`

```js
tags: ['Tag A'],
```

提供上述任何一项的倍数都不会破坏任何东西，但只会向头部添加一个。

#### Book

```js
import { NextSeo } from 'next-seo';

const Page = () => (
  <>
    <NextSeo
      openGraph={{
        title: 'Open Graph Book Title',
        description: 'Description of open graph book',
        url: 'https://www.example.com/books/book-title',
        type: 'book',
        book: {
          releaseDate: '2018-09-17T11:08:13Z',
          isbn: '978-3-16-148410-0',
          authors: [
            'https://www.example.com/authors/@firstnameA-lastnameA',
            'https://www.example.com/authors/@firstnameB-lastnameB',
          ],
          tags: ['Tag A', 'Tag B', 'Tag C'],
        },
        images: [
          {
            url: 'https://www.test.ie/images/book.jpg',
            width: 850,
            height: 650,
            alt: 'Cover of the book',
          },
        ],
      }}
    />
    <p>Book</p>
  </>
);

export default Page;
```

**注意**

版本 `7.0.0-canary.0` next.js提供了多个图像、作者和标签

对于版本 `6.0.0` - `7.0.0-canary.0`，您只需提供一个项目数组：

`images:`

```js
images: [
  {
    url: 'https://www.example.ie/og-image-01.jpg',
    width: 800,
    height: 600,
    alt: 'Og Image Alt',
  },
],
```

`authors:`

```js
authors: [
  'https://www.example.com/authors/@firstnameA-lastnameA',
],
```

`tags:`

```js
tags: ['Tag A'],
```

提供上述任何一项的倍数都不会破坏任何东西，但只会向头部添加一个。

#### Profile

```js
import { NextSeo } from 'next-seo';

const Page = () => (
  <>
    <NextSeo
      openGraph={{
        title: 'Open Graph Profile Title',
        description: 'Description of open graph profile',
        url: 'https://www.example.com/@firstlast123',
        type: 'profile',
        profile: {
          firstName: 'First',
          lastName: 'Last',
          username: 'firstlast123',
          gender: 'female',
        },
        images: [
          {
            url: 'https://www.test.ie/images/profile.jpg',
            width: 850,
            height: 650,
            alt: 'Profile Photo',
          },
        ],
      }}
    />
    <p>Profile</p>
  </>
);

export default Page;
```

**注意**

next.js版本 `7.0.0-canary.0` 中提供了多个映像

对于版本 `6.0.0` - `7.0.0-canary.0`，您只需提供一个项目数组：

```js
images: [
  {
    url: 'https://www.example.ie/og-image-01.jpg',
    width: 800,
    height: 600,
    alt: 'Og Image Alt',
  },
],
```

Supplying multiple images will not break anything, but only one will be added to the head.  
提供多张图片不会破坏任何东西，但只会将一张图片添加到头部。

## JSON-LD JSON-LD 格式
\
Next SEO 现在能够将 JSON-LD 设置为一种结构化数据形式。结构化数据是一种标准化格式，用于提供有关页面的信息并对页面内容进行分类。

Google 在 [JSON-LD](https://developers.google.com/search/docs/data-types/article) -> 有很好的内容

如果使用 app 目录，请确保添加 `useAppDir={true}` prop，并且您正在使用 `page.js` 中的组件**

您将在下面找到一个非常基本的页面，实现了每种可用的 JSON-LD 类型：

- [Article 品](https://github.com/garmeeh/next-seo?tab=readme-ov-file#article-1)
- [Breadcrumb 面包屑](https://github.com/garmeeh/next-seo?tab=readme-ov-file#breadcrumb)
- [Blog 博客](https://github.com/garmeeh/next-seo?tab=readme-ov-file#blog)
- [Campground 野营地](https://github.com/garmeeh/next-seo?tab=readme-ov-file#campground)
- [Recipe 食谱](https://github.com/garmeeh/next-seo?tab=readme-ov-file#recipe)
- [Sitelinks Search Box 附加链接搜索框](https://github.com/garmeeh/next-seo?tab=readme-ov-file#sitelinks-search-box)
- [Course 课程](https://github.com/garmeeh/next-seo?tab=readme-ov-file#course)
- [Dataset 数据](https://github.com/garmeeh/next-seo?tab=readme-ov-file#dataset)
- [Corporate Contact 公司联系方式](https://github.com/garmeeh/next-seo?tab=readme-ov-file#corporate-contact)
- [FAQ Page FAQ 页面](https://github.com/garmeeh/next-seo?tab=readme-ov-file#faq-page)
- [How-to 操作方法](https://github.com/garmeeh/next-seo?tab=readme-ov-file#how-to)
- [Job Posting 招聘启事](https://github.com/garmeeh/next-seo?tab=readme-ov-file#job-posting)
- [Local Business 本地业务](https://github.com/garmeeh/next-seo?tab=readme-ov-file#local-business)
- [Product 产品](https://github.com/garmeeh/next-seo?tab=readme-ov-file#product)
- [Social Profile 社交资料](https://github.com/garmeeh/next-seo?tab=readme-ov-file#social-profile)
- [News Article 新闻报道](https://github.com/garmeeh/next-seo?tab=readme-ov-file#news-article)
- [Park 公园](https://github.com/garmeeh/next-seo?tab=readme-ov-file#park)

非常欢迎拉取请求从[此处的](https://developers.google.com/search/docs/data-types/article)列表中添加任何内容

#### JSON-LD Security JSON-LD 安全性

关于安全性的快速说明。要将 JSON-LD 放到页面上，它需要位于 script 标签中。`next-seo` 通过使用带有 `dangerouslySetInnerHTML` 的 script 标签来实现这一点。

因此，如果直接从 URL 向下面的组件之一传递任何内容，请确保在需要时先对其进行清理。

查看 `toJson.tsx` 了解实现详细信息。

#### Handling multiple instances  
处理多个实例

如果您的页面需要给定 JSON-LD 组件的多个实例，您可以指定唯一的 `keyOverride` 属性，`next-seo` 将处理其余部分。

这对于博客滚动、搜索结果和概述页面非常方便。

请充分研究何时应该和不应该添加多个 JSON-LD 实例。

```js
<ExampleJsonLd keyOverride="my-new-key" />
```

### Article 文章

```js
import { ArticleJsonLd } from 'next-seo';

const Page = () => (
  <>
    <h1>Article JSON-LD</h1>
    <ArticleJsonLd
      useAppDir={false}
      url="https://example.com/article"
      title="Article headline"
      images={[
        'https://example.com/photos/1x1/photo.jpg',
        'https://example.com/photos/4x3/photo.jpg',
        'https://example.com/photos/16x9/photo.jpg',
      ]}
      datePublished="2015-02-05T08:00:00+08:00"
      dateModified="2015-02-05T09:00:00+08:00"
      authorName={[
        {
          name: 'Jane Blogs',
          url: 'https://example.com',
        },
        {
          name: 'Mary Stone',
          url: 'https://example.com',
        },
      ]}
      publisherName="Gary Meehan"
      publisherLogo="https://www.example.com/photos/logo.jpg"
      description="This is a mighty good description of this article."
      isAccessibleForFree={true}
    />
  </>
);

export default Page;
```

### Breadcrumb 面包屑

```js
import { BreadcrumbJsonLd } from 'next-seo';

const Page = () => (
  <>
    <h1>Breadcrumb JSON-LD</h1>
    <BreadcrumbJsonLd
      itemListElements={[
        {
          position: 1,
          name: 'Books',
          item: 'https://example.com/books',
        },
        {
          position: 2,
          name: 'Authors',
          item: 'https://example.com/books/authors',
        },
        {
          position: 3,
          name: 'Ann Leckie',
          item: 'https://example.com/books/authors/annleckie',
        },
        {
          position: 4,
          name: 'Ancillary Justice',
          item: 'https://example.com/books/authors/ancillaryjustice',
        },
      ]}
    />
  </>
);

export default Page;
```

**Required properties 必需属性**

| Property 财产                                      | Info 信息                                                                                                                                       |
| ------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------- |
| `itemListElements itemListElements （项目列表元素）`     |                                                                                                                                               |
| `itemListElements.position`                      | The position of the breadcrumb in the breadcrumb trail. Position 1 signifies the beginning of the trail.  <br>痕迹导航在 痕迹导航 轨迹中的位置。位置 1 表示轨迹的开始。 |
| `itemListElements.name`                          | The title of the breadcrumb displayed for the user.  <br>为用户显示的痕迹导航的标题。                                                                       |
| `itemListElements.item itemListElements.item 项目` | The URL to the webpage that represents the breadcrumb.  <br>表示痕迹导航的网页的 URL。                                                                   |

**Other** | `useAppDir` | This should be set to true if using the new app directory. Not required if outside of the app directory. |  
**其他** |`useAppDir` |如果使用新的 app 目录，则应将其设置为 true。如果位于 app 目录之外，则不需要。|

### Blog 博客

```js
import { ArticleJsonLd } from 'next-seo';

const Page = () => (
  <>
    <h1>Blog JSON-LD</h1>
    <ArticleJsonLd
      type="BlogPosting"
      url="https://example.com/blog"
      title="Blog headline"
      images={[
        'https://example.com/photos/1x1/photo.jpg',
        'https://example.com/photos/4x3/photo.jpg',
        'https://example.com/photos/16x9/photo.jpg',
      ]}
      datePublished="2015-02-05T08:00:00+08:00"
      dateModified="2015-02-05T09:00:00+08:00"
      authorName="Jane Blogs"
      description="This is a mighty good description of this blog."
    />
  </>
);

export default Page;
```

### Campground 野营地

```js
import { CampgroundJsonLd } from 'next-seo';

const Page = () => (
  <>
    <h1>Campground JSON-LD</h1>
    <CampgroundJsonLd
      id="https://www.example.com/campground/rip-van-winkle-campground"
      name="Rip Van Winkle Campgrounds"
      url="https://www.example.com/campground"
      telephone="+18452468114"
      images={['https://example.com/photos/1x1/photo.jpg']}
      address={{
        streetAddress: '149 Blue Mountain Rd',
        addressLocality: 'Saugerties',
        addressRegion: 'NY',
        postalCode: '12477',
        addressCountry: 'US',
      }}
      description="Description about Rip Van Winkle Campgrounds"
      geo={{
        latitude: '42.092599',
        longitude: '-74.018580',
      }}
      openingHours={[
        {
          opens: '09:00',
          closes: '17:00',
          dayOfWeek: [
            'Monday',
            'Tuesday',
            'Wednesday',
            'Thursday',
            'Friday',
            'Saturday',
            'Sunday',
          ],
          validFrom: '2019-12-23',
          validThrough: '2020-04-02',
        },
      ]}
      petsAllowed
      rating={{
        ratingValue: '5',
        ratingCount: '18',
      }}
      amenityFeature={{
        name: 'Showers',
        value: true,
      }}
      priceRange="$$"
    />
  </>
);

export default Page;
```

**Required properties 必需属性**

|Property 财产|Info 信息|
|---|---|
|`@id`|Globally unique ID of the specific campground in the form of a URL.  <br>特定露营地的全局唯一 ID，采用 URL 形式。|
|`address 地址`|Address of the specific campground location  <br>具体露营地位置的地址|
|`address.addressCountry address.addressCountry 地址`|The 2-letter ISO 3166-1 alpha-2 country code  <br>由 2 个字母组成的 ISO 3166-1 alpha-2 国家/地区代码|
|`address.addressLocality address.addressLocality 地址`|City 城市|
|`address.addressRegion address.addressRegion 地址区域`|State or province, if applicable.  <br>州或省（如果适用）。|
|`address.postalCode 地址.postalCode`|Postal or zip code. 邮政编码。|
|`address.streetAddress address.street地址`|Street number, street name, and unit number.  <br>街道号码、街道名称和单元号。|
|`name 名字`|Campground name. 露营地名称。|
|`description 描述`|Campground description. 露营地描述。|

**Supported properties 支持的属性**

|Property 财产|Info 信息|
|---|---|
|`geo 地理`|Geographic coordinates of the campground.  <br>露营地的地理坐标。|
|`geo.latitude geo.latitude 的`|The latitude of the campground location  <br>露营地位置的纬度|
|`geo.longitude geo.longitude （地理经度）`|The longitude of the campground location  <br>露营地位置的经度|
|`images 图像`|An image or images of the campground. Required for valid markup depending on the type  <br>露营地的一张或多张图片。有效标记是必需的，具体取决于类型|
|`telephone 电话`|A campground phone number meant to be the primary contact method for customers.  <br>露营地电话号码，旨在作为客户的主要联系方式。|
|`url 网址`|The fully-qualified URL of the specific campground.  <br>特定露营地的完全限定 URL。|
|`openingHours 营业时间`|Opening hour specification of the campground. You can provide this as a single object, or an array of objects with the properties below.  <br>露营地的开放时间说明。您可以将其作为单个对象或具有以下属性的对象数组提供。|
|`openingHours.opens openingHours.打开`|The opening hour of the place or service on the given day(s) of the week.  <br>地点或服务在一周中指定日期的营业时间。|
|`openingHours.closes`|The closing hour of the place or service on the given day(s) of the week.  <br>地点或服务在一周中指定日期的关闭时间。|
|`openingHours.dayOfWeek`|The day of the week for which these opening hours are valid. Can be a string or array of strings. Refer to [DayOfWeek](https://schema.org/DayOfWeek)  <br>这些营业时间在一周中的哪一天有效。可以是字符串或字符串数组。请参阅 [DayOfWeek](https://schema.org/DayOfWeek)|
|`openingHours.validFrom openingHours.valid发件人`|The date when the item becomes valid.  <br>项生效的日期。|
|`openingHours.validThrough`|The date after when the item is not valid.  <br>项无效的日期。|
|`isAccessibleForFree isAccessibleForFree 免费`|Whether or not the campground is accessible for free.  <br>露营地是否免费进入。|
|`petsAllowed 允许携带宠物`|Whether or not the campgroud allows pets.  <br>campgroud 是否允许携带宠物。|
|`amenityFeature 便利设施特色`|An amenity feature (e.g. a characteristic or service) of the campground.  <br>露营地的便利设施特征（例如特色或服务）。|
|`amenityFeature.name`|The name of the amenity.  <br>便利设施的名称。|
|`amenityFeature.value`|The value of the amenity.  <br>便利设施的价值。|
|`priceRange 价格范围`|The price range of the campground, for example $$$.  <br>露营地的价格范围，例如 $$$。|
|`rating 额定值`|The average rating of the campground based on multiple ratings or reviews.  <br>基于多个评分或评论的露营地的平均评分。|
|`rating.ratingValue rating.rating值`|The rating for the content.  <br>内容的评级。|
|`rating.ratingCount`|The count of total number of ratings.  <br>评分总数的计数。|

**其他** |`useAppDir` |如果使用新的 app 目录，则应将其设置为 true。如果位于 app 目录之外，则不需要。|

### Recipe 食谱

[](https://github.com/garmeeh/next-seo?tab=readme-ov-file#recipe)

```js
import { RecipeJsonLd } from 'next-seo';

const Page = () => (
  <>
    <h1>Recipe JSON-LD</h1>
    <RecipeJsonLd
      name="Party Coffee Cake"
      description="This coffee cake is awesome and perfect for parties."
      datePublished="2018-03-10"
      authorName={['Jane Blogs', 'Mary Stone']}
      prepTime="PT20M"
      cookTime="PT30M"
      totalTime="PT50M"
      keywords="cake for a party, coffee"
      yields="10"
      category="Dessert"
      cuisine="American"
      calories={270}
      images={[
        'https://example.com/photos/1x1/photo.jpg',
        'https://example.com/photos/4x3/photo.jpg',
        'https://example.com/photos/16x9/photo.jpg',
      ]}
      ingredients={[
        '2 cups of flour',
        '3/4 cup white sugar',
        '2 teaspoons baking powder',
        '1/2 teaspoon salt',
        '1/2 cup butter',
        '2 eggs',
        '3/4 cup milk',
      ]}
      instructions={[
        {
          name: 'Preheat',
          text: 'Preheat the oven to 350 degrees F. Grease and flour a 9x9 inch pan.',
          url: 'https://example.com/party-coffee-cake#step1',
          image: 'https://example.com/photos/party-coffee-cake/step1.jpg',
        },
      ]}
      aggregateRating={{
        ratingValue: '5',
        ratingCount: '18',
      }}
      video={{
        name: 'How to make a Party Coffee Cake',
        description: 'This is how you make a Party Coffee Cake.',
        contentUrl: 'http://www.example.com/video123.mp4',
        embedUrl: 'http://www.example.com/videoplayer?video=123',
        uploadDate: '2018-02-05T08:00:00+08:00',
        duration: 'PT1M33S',
        thumbnailUrls: [
          'https://example.com/photos/1x1/photo.jpg',
          'https://example.com/photos/4x3/photo.jpg',
          'https://example.com/photos/16x9/photo.jpg',
        ],
        expires: '2019-02-05T08:00:00+08:00',
        hasPart: {
          '@type': 'Clip',
          name: 'Preheat oven',
          startOffset: 30,
          url: 'http://www.example.com/example?t=30',
        },
        watchCount: 2347,
        publication: {
          '@type': 'BroadcastEvent',
          isLiveBroadcast: true,
          startDate: '2020-10-24T14:00:00+00:00',
          endDate: '2020-10-24T14:37:14+00:00',
        },
        regionsAllowed: ['IT', 'NL'],
      }}
    />
  </>
);

export default Page;
```

**Required properties 必需属性**

|Property 财产|Info 信息|
|---|---|
|`name 名字`|The name of the recipe  <br>配方的名称|
|`description 描述`|A description of the recipe  <br>配方描述|
|`authorName authorName （作者姓名）`|The name of the recipe author. Can be a string or array of strings.  <br>配方作者的姓名。可以是字符串或字符串数组。|
|`ingredients 成分`|A list of ingredient strings  <br>成分字符串列表|
|`instructions 指示`|-|
|`instructions.name`|The name of the instruction step.  <br>指令步骤的名称。|
|`instructions.text instructions.text （说明文本）`|The directions of the instruction step.  <br>指令步骤的方向。|

**其他** |`useAppDir` |如果使用新的 app 目录，则应将其设置为 true。如果位于 app 目录之外，则不需要。|

### Sitelinks Search Box 附加链接搜索框

[](https://github.com/garmeeh/next-seo?tab=readme-ov-file#sitelinks-search-box)

```js
import { SiteLinksSearchBoxJsonLd } from 'next-seo';

const Page = () => (
  <>
    <h1>Sitelinks Search Box JSON-LD</h1>
    <SiteLinksSearchBoxJsonLd
      url="https://www.example.com"
      potentialActions={[
        {
          target: 'https://query.example.com/search?q',
          queryInput: 'search_term_string',
        },
        {
          target: 'android-app://com.example/https/query.example.com/search/?q',
          queryInput: 'search_term_string',
        },
      ]}
    />
  </>
);

export default Page;
```

**Required properties 必需属性**

|Property 财产|Info 信息|
|---|---|
|`url 网址`|URL of the website associated with the sitelinks searchbox  <br>与站点链接搜索框关联的网站的 URL|
|`potentialActions`|Array of one or two SearchAction objects. Describes the URI to send the query to, and the syntax of the request that is sent  <br>一个或两个 SearchAction 对象的数组。描述要将查询发送到的 URI 以及发送的请求的语法|
|`potentialActions.target`|For websites, the URL of the handler that should receive and handle the search query; for apps, the URI of the intent handler for your search engine that should handle queries  <br>对于网站，应接收和处理搜索查询的处理程序的 URL;对于应用，应处理查询的搜索引擎的 intent 处理程序的 URI|
|`potentialActions.queryInput`|Placeholder used in target, gets substituted for user given query  <br>在 target 中使用的占位符，被替换为用户给定的查询|

**Other** | `useAppDir` | This should be set to true if using the new app directory. Not required if outside of the app directory. |  
**其他** |`useAppDir` |如果使用新的 app 目录，则应将其设置为 true。如果位于 app 目录之外，则不需要。|

Read the [documentation](https://developers.google.com/search/docs/appearance/structured-data/sitelinks-searchbox)  
阅读[文档](https://developers.google.com/search/docs/appearance/structured-data/sitelinks-searchbox)

### Course 课程

```js
import { CourseJsonLd } from 'next-seo';

const Page = () => (
  <>
    <h1>Course JSON-LD</h1>
    <CourseJsonLd
      courseName="Course Name"
      description="Introductory CS course laying out the basics."
      provider={{
        name: 'Course Provider',
        url: 'https//www.example.com/provider',
      }}
    />
  </>
);

export default Page;
```

**Required properties 必需属性**

|Property 财产|Info 信息|
|---|---|
|`courseName 课程名称`|The title of the course.  <br>课程的标题。|
|`description 描述`|A description of the course. Display limit of 60 characters.  <br>课程的描述。显示限制为 60 个字符。|
|`provider.name`|The course provider name.  <br>课程提供者名称。|
|`provider.url provider.url 的`|The course provider name url.  <br>课程提供者名称 URL。|

**Recommended properties 推荐属性**

|Property 财产|Info 信息|
|---|---|
|`providerUrl providerUrl 的`|The url to the course provider.  <br>课程提供商的 URL。|

**其他** |`useAppDir` |如果使用新的 app 目录，则应将其设置为 true。如果位于 app 目录之外，则不需要。|

### Dataset 数据

```js
import { DatasetJsonLd } from 'next-seo';

const Page = () => (
  <>
    <h1>Dataset JSON-LD</h1>
    <DatasetJsonLd
      description="The description needs to be at least 50 characters long"
      name="name of the dataset"
      license="https//www.example.com"
    />
  </>
);

export default Page;
```

**Required properties 必需属性**

|Property 财产|Info 信息|
|---|---|
|`description 描述`|A short summary describing a dataset. Needs to be between 50 and 5000 characters.  <br>描述数据集的简短摘要。需要介于 50 到 5000 个字符之间。|
|`name 名字`|A license under which the dataset is distributed.  <br>分发数据集所依据的许可证。|

**Recommended properties 推荐属性**

|Property 财产|Info 信息|
|---|---|
|`license 许可证`|The url to the course provider.  <br>课程提供商的 URL。|

**其他** |`useAppDir` |如果使用新的 app 目录，则应将其设置为 true。如果位于 app 目录之外，则不需要。|

### Corporate Contact 公司联系方式

```js
import { CorporateContactJsonLd } from 'next-seo';

const Page = () => (
  <>
    <h1>Corporate Contact JSON-LD</h1>
    <CorporateContactJsonLd
      url="http://www.your-company-site.com"
      logo="http://www.example.com/logo.png"
      contactPoint={[
        {
          telephone: '+1-401-555-1212',
          contactType: 'customer service',
          email: 'customerservice@email.com',
          areaServed: 'US',
          availableLanguage: ['English', 'Spanish', 'French'],
        },
        {
          telephone: '+1-877-746-0909',
          contactType: 'customer service',
          email: 'servicecustomer@email.com',
          contactOption: 'TollFree',
          availableLanguage: 'English',
        },
        {
          telephone: '+1-877-453-1304',
          contactType: 'technical support',
          contactOption: 'TollFree',
          areaServed: ['US', 'CA'],
          availableLanguage: ['English', 'French'],
        },
      ]}
    />
  </>
);

export default Page;
```

**Required properties 必需属性**

|Property 财产|Info 信息|
|---|---|
|`url 网址`|Url to the home page of the company's official site.  <br>指向公司官方网站主页的 URL。|
|`contactPoint 联系点`||
|`contactPoint.telephone contactPoint.电话`|An internationalized version of the phone number, starting with the "+" symbol and country code  <br>电话号码的国际化版本，以“+”符号和国家/地区代码开头|
|`contactPoint.contactType`|Description of the purpose of the phone number i.e. `Technical Support`.  <br>电话号码的用途说明，即`技术支持`。|

**Recommended ContactPoint properties  
建议的 ContactPoint 属性**

|Property 财产|Info 信息|
|---|---|
|`contactPoint.areaServed contactPoint.area服务`|`String` or `Array` of geographical regions served by the business. Example `"US"` or `["US", "CA", "MX"]`  <br>企业服务的地理区域的`字符串`或`数组`。示例 `“US”` 或 `[“US”， “CA”， “MX”]`|
|`contactPoint.availableLanguage`|Details about the language spoken. Example `"English"` or `["English", "French"]`  <br>有关所说语言的详细信息。示例 `“English”` 或 `[“English”， “French”]`|
|`contactPoint.email`|Email asscosiated with the business`  <br>与企业关联的电子邮件|
|`gecontactPointo.contactOption`|Details about the phone number. Example `"TollFree"`  <br>有关电话号码的详细信息。示例 `“TollFree”`|

**其他** |`useAppDir` |如果使用新的 app 目录，则应将其设置为 true。如果位于 app 目录之外，则不需要。|

### FAQ Page FAQ 页面

```js
import { FAQPageJsonLd } from 'next-seo';

const Page = () => (
  <>
    <h1>FAQ Page JSON-LD</h1>
    <FAQPageJsonLd
      mainEntity={[
        {
          questionName: 'How long is the delivery time?',
          acceptedAnswerText: '3-5 business days.',
        },
        {
          questionName: 'Where can I find information about product recalls?',
          acceptedAnswerText: 'Read more on under information.',
        },
      ]}
    />
  </>
);

export default Page;
```

**Required properties 必需属性**

|Property 财产|Info 信息|
|---|---|
|`mainEntity mainEntity （主实体）`||
|`mainEntity.questionName`|The full text of the question. For example, "How long is the delivery time?".  <br>问题的全文。例如，“How long is the delivery time？”。|
|`mainEntity.acceptedAnswerText`|The full answer to the question.  <br>问题的完整答案。|

**Other** | `useAppDir` | This should be set to true if using the new app directory. Not required if outside of the app directory. |  
**其他** |`useAppDir` |如果使用新的 app 目录，则应将其设置为 true。如果位于 app 目录之外，则不需要。|

### How-to 操作方法

```js
import { HowToJsonLd } from 'next-seo';

const Page = () => (
  <>
    <h1>How-to JSON-LD</h1>
    <HowToJsonLd
      name="How to tile a kitchen backsplash"
      image="https://example.com/photos/1x1/photo.jpg"
      estimatedCost={{ currency: 'USD', value: '100' }}
      supply={['tiles', 'thin-set', 'mortar', 'tile grout', 'grout sealer']}
      tool={['notched trowel', 'bucket', 'large sponge']}
      step={[
        {
          url: 'https://example.com/kitchen#step1',
          name: 'Prepare the surfaces',
          itemListElement: [
            {
              type: 'HowToTip',
              text: 'Turn off the power to the kitchen and then remove everything that is on the wall, such as outlet covers, switchplates, and any other item in the area that is to be tiled.',
            },
            {
              type: 'HowToDirection',
              text: 'Then clean the surface thoroughly to remove any grease or other debris and tape off the area.',
            },
          ],
          image: 'https://example.com/photos/1x1/photo-step1.jpg',
        },
      ]}
      totalTime="P2D"
    />
  </>
);

export default Page;
```

**Required properties 必需属性**

|Property 财产|Info 信息|
|---|---|
|`name 名字`|Name of the HowTo HowTo 名称|
|`step 步`|An array of HowToStep elements which comprise the full instructions of the how-to.  <br>一组 HowToStep 元素，它们构成了 how-to 的完整说明。|

**Supported properties 支持的属性**

|Property 财产|Info 信息|
|---|---|
|`estimatedCost estimatedCost （估计成本）`|The estimated cost of the supplies consumed when performing instructions.  <br>执行指令时消耗的耗材的估计成本。|
|`image 图像`|Image of the completed how-to.  <br>已完成的操作方法的图像。|
|`supply 供应`|A supply consumed when performing instructions or a direction.  <br>执行指令或指示时消耗的供应。|
|`tool 工具`|An object used (but not consumed) when performing instructions or a direction.  <br>执行指令或指示时使用 （但未使用） 的对象。|
|`totalTime 总计时间`|The total time required to perform all instructions or directions (including time to prepare the supplies), in ISO 8601 duration format.  <br>执行所有说明或指示所需的总时间（包括准备耗材的时间），采用 ISO 8601 持续时间格式。|

**其他** |`useAppDir` |如果使用新的 app 目录，则应将其设置为 true。如果位于 app 目录之外，则不需要。|

### Job Posting 招聘启事

```js
import { JobPostingJsonLd } from 'next-seo';

const Page = () => (
  <>
    <h1>Job Posting JSON-LD</h1>
    <JobPostingJsonLd
      datePosted="2020-01-06T03:37:40Z"
      description="Company is looking for a software developer...."
      hiringOrganization={{
        name: 'company name',
        sameAs: 'www.company-website-url.dev',
      }}
      jobLocation={{
        streetAddress: '17 street address',
        addressLocality: 'Paris',
        addressRegion: 'Ile-de-France',
        postalCode: '75001',
        addressCountry: 'France',
      }}
      title="Job Title"
      baseSalary={{
        currency: 'EUR',
        value: 40, // Can also be a salary range, like [40, 50]
        unitText: 'HOUR',
      }}
      employmentType="FULL_TIME"
      jobLocationType="TELECOMMUTE"
      validThrough="2020-01-06"
      applicantLocationRequirements="FR"
      experienceRequirements={{
        occupational: {
          minimumMonthsOfExperience: 12,
        },
        educational: {
          credentialCategory: 'high school',
        },
        experienceInPlaceOfEducation: true,
      }}
    />
  </>
);

export default Page;
```

**Required properties 必需属性**

|Property 财产|Info 信息|
|---|---|
|`datePosted 发布日期`|The original date that employer posted the job in ISO 8601 format  <br>雇主以 ISO 8601 格式发布职位的原始日期|
|`description 描述`|The full description of the job in HTML format  <br>HTML 格式的工作完整描述|
|`hiringOrganization 招聘组织`|An object containing information about the company hiring with the following fields or the string `'confidential'` when hiring anonymously  <br>一个对象，其中包含有关公司招聘的信息，其中包含以下字段或匿名招聘时字符串 `'confidential'`|
|`hiringOrganization.name`|Name of the company offering the job position  <br>提供招聘职位的公司名称|
|`hiringOrganization.sameAs`|URL of a reference Web page  <br>引用网页的 URL|
|`title 标题`|The title of the job (not the title of the posting)  <br>职位名称（不是发布内容的标题）|
|`validThrough 有效通过`|The date when the job posting will expire in [ISO 8601 format](https://en.wikipedia.org/wiki/ISO_8601)  <br>职位发布以 [ISO 8601 格式](https://en.wikipedia.org/wiki/ISO_8601)发布的到期日期|

**Supported properties 支持的属性**

|Property 财产|Info 信息|
|---|---|
|`applicantLocationRequirementsapplicantLocation要求`|The geographic location(s) in which employees may be located for to be eligible for the remote job  <br>员工可能位于的地理位置，以便有资格进行远程工作|
|`baseSalary baseSalary 基本工资`||
|`baseSalary.currency`|The currency in which the monetary amount is expressed  <br>用于表示货币金额的货币|
|`baseSalary.value`|The value of the quantitative value. You can also provide an array of minimum and maximum salaries. .  <br>定量值的值。您还可以提供一系列最低和最高工资。.|
|`baseSalary.unitText baseSalary.unit文本`|A string indicating the unit of measurement [Base salary guideline](https://developers.google.com/search/docs/data-types/job-posting#basesalary)  <br>指示计量单位[的字符串 Base salary guidelines](https://developers.google.com/search/docs/data-types/job-posting#basesalary)|
|`employmentType employmentType （就业类型）`|Type of employment [Employement type guideline](https://developers.google.com/search/docs/data-types/job-posting#basesalary)  <br>就业类型 [就业类型 指南](https://developers.google.com/search/docs/data-types/job-posting#basesalary)|
|`jobLocation`|The physical location(s) of the business where the employee will report to work (such as an office or worksite), not the location where the job was posted.  <br>员工上班的公司的实际位置（例如办公室或工作场所），而不是发布职位的地点。|
|`jobLocation.streetAddressjobLocation.street地址`|The street address. For example, 1600 Amphitheatre Pkwy  <br>街道地址。例如，1600 Amphitheatre Pkwy|
|`jobLocation.addressLocality`|The locality. For example, Mountain View.  <br>地方。例如，Mountain View。|
|`jobLocation.addressRegion`|The region. For example, CA.  <br>区域。例如，CA。|
|`jobLocation.postalCode jobLocation.postal代码`|The postal code. For example, 94043  <br>邮政编码。例如，94043|
|`jobLocation.addressCountry`|The country. For example, USA. You can also provide the two-letter ISO 3166-1 alpha-2 country code.  <br>这个国家。例如，USA。您还可以提供两个字母的 ISO 3166-1 alpha-2 国家/地区代码。|
|`jobLocationType jobLocation类型`|A description of the job location [Job Location type guideline](https://developers.google.com/search/docs/data-types/job-posting#job-location-type)  <br>工作地点的说明 [工作地点类型准则](https://developers.google.com/search/docs/data-types/job-posting#job-location-type)|
|`hiringOrganization.logo 招聘组织.logo`|Logos on third-party job sites [Hiring Organization guideline](https://developers.google.com/search/docs/data-types/job-posting#hiring)  <br>第三方招聘网站上的徽标[招聘组织指南](https://developers.google.com/search/docs/data-types/job-posting#hiring)|
|`experienceRequirements.occupational.minimumMonthsOfExperience`|The minimum number of months of experience that are required for the job posting. [Experience and Education Requirements](https://developers.google.com/search/docs/appearance/structured-data/job-posting#education-and-experience-properties-beta)  <br>发布职位所需的最低经验月数。[经验和教育要求](https://developers.google.com/search/docs/appearance/structured-data/job-posting#education-and-experience-properties-beta)|
|`experienceRequirements.educational.credentialCategoryexperienceRequirements.educational.credential类别`|The level of education that's required for the job posting. Use one of the following: `high school`, `associate degree`, `bachelor degree`, `professional certificate`, `postgraduate degree`  <br>招聘启事所需的教育水平。使用以下选项之一：`高中`、`副学士学位`、`学士学位`、`专业证书`、`研究生学位`|
|`experienceRequirements.experienceInPlaceOfEducation`|Boolean: If set to true, this property indicates whether a job posting will accept experience in place of its formal educational qualifications. If set to true, you must include both the experienceRequirements and educationRequirements properties.  <br>布尔值：如果设置为 true，则此属性指示职位发布是否接受经验而不是其正式的教育资格。如果设置为 true，则必须同时包含 experienceRequirements 和 educationRequirements 属性。|

**其他** |`useAppDir` |如果使用新的 app 目录，则应将其设置为 true。如果位于 app 目录之外，则不需要。|

### Local Business 本地业务

本地业务由一组属性支持。

```js
<LocalBusinessJsonLd
  type="Store"
  id="http://davesdeptstore.example.com"
  name="Dave's Department Store"
  description="Dave's latest department store in San Jose, now open"
  url="http://www.example.com/store-locator/sl/San-Jose-Westgate-Store/1427"
  telephone="+14088717984"
  address={{
    streetAddress: '1600 Saratoga Ave',
    addressLocality: 'San Jose',
    addressRegion: 'CA',
    postalCode: '95129',
    addressCountry: 'US',
  }}
  geo={{
    latitude: '37.293058',
    longitude: '-121.988331',
  }}
  images={[
    'https://example.com/photos/1x1/photo.jpg',
    'https://example.com/photos/4x3/photo.jpg',
    'https://example.com/photos/16x9/photo.jpg',
  ]}
  sameAs={[
    'www.company-website-url1.dev',
    'www.company-website-url2.dev',
    'www.company-website-url3.dev',
  ]}
  openingHours={[
    {
      opens: '08:00',
      closes: '23:59',
      dayOfWeek: [
        'Monday',
        'Tuesday',
        'Wednesday',
        'Thursday',
        'Friday',
        'Saturday',
      ],
      validFrom: '2019-12-23',
      validThrough: '2020-04-02',
    },
    {
      opens: '14:00',
      closes: '20:00',
      dayOfWeek: 'Sunday',
      validFrom: '2019-12-23',
      validThrough: '2020-04-02',
    },
  ]}
  rating={{
    ratingValue: '4.5',
    ratingCount: '2',
  }}
  review={[
    {
      author: 'John Doe',
      datePublished: '2006-05-04',
      name: 'A masterpiece of literature',
      reviewBody:
        'I really enjoyed this book. It captures the essential challenge people face as they try make sense of their lives and grow to adulthood.',
      reviewRating: {
        bestRating: '5',
        worstRating: '1',
        reviewAspect: 'Ambiance',
        ratingValue: '4',
      },
    },
    {
      author: 'Bob Smith',
      datePublished: '2006-06-15',
      name: 'A good read.',
      reviewBody: "Catcher in the Rye is a fun book. It's a good book to read.",
      reviewRating: {
        ratingValue: '4',
      },
    },
  ]}
  makesOffer={[
    {
      priceSpecification: {
        type: 'UnitPriceSpecification',
        priceCurrency: 'EUR',
        price: '1000-10000',
      },
      itemOffered: {
        name: 'Motion Design Services',
        description:
          'We are the expert of animation and motion design productions.',
      },
    },
    {
      priceSpecification: {
        type: 'UnitPriceSpecification',
        priceCurrency: 'EUR',
        price: '2000-10000',
      },
      itemOffered: {
        name: 'Branding Services',
        description:
          'Real footage is a powerful tool when it comes to show what the business is about. Can be used to present your company, show your factory, promote a product packshot, or just tell any story. It can help create emotional links with your audience by showing punchy images.',
      },
    },
  ]}
  areaServed={[
    {
      geoMidpoint: {
        latitude: '41.108237',
        longitude: '-80.642982',
      },
      geoRadius: '1000',
    },
    {
      geoMidpoint: {
        latitude: '51.108237',
        longitude: '-80.642982',
      },
      geoRadius: '1000',
    },
  ]}
  action={{
    actionName: 'potentialAction',
    actionType: 'ReviewAction',
    target: 'https://www.example.com/review/this/business',
  }}
/>
```

**Required properties 必需属性**

|Property 财产|Info 信息|
|---|---|
|`@id`|Globally unique ID of the specific business location in the form of a URL.  <br>特定营业地点的全局唯一 ID，采用 URL 形式。|
|`type 类型`|LocalBusiness or any sub-type  <br>LocalBusiness 或任何子类型|
|`address 地址`|Address of the specific business location  <br>具体营业地点的地址|
|`address.addressCountry address.addressCountry 地址`|The 2-letter ISO 3166-1 alpha-2 country code  <br>由 2 个字母组成的 ISO 3166-1 alpha-2 国家/地区代码|
|`address.addressLocality address.addressLocality 地址`|City 城市|
|`address.addressRegion address.addressRegion 地址区域`|State or province, if applicable.  <br>州或省（如果适用）。|
|`address.postalCode 地址.postalCode`|Postal or zip code. 邮政编码。|
|`address.streetAddress address.street地址`|Street number, street name, and unit number.  <br>街道号码、街道名称和单元号。|
|`name 名字`|Business name. 公司名称。|

**Supported properties 支持的属性**

|Property 财产|Info 信息|
|---|---|
|`description 描述`|Description of the business location  <br>营业地点描述|
|`geo 地理`|Geographic coordinates of the business.  <br>企业的地理坐标。|
|`geo.latitude geo.latitude 的`|The latitude of the business location  <br>营业地点的纬度|
|`geo.longitude geo.longitude （地理经度）`|The longitude of the business location  <br>营业地点的经度|
|`rating 额定值`|The average rating of business based on multiple ratings or reviews.  <br>基于多个评分或评价的企业平均评分。|
|`rating.ratingValue rating.rating值`|The rating for the content.  <br>内容的评级。|
|`rating.ratingCount`|The count of total number of ratings.  <br>评分总数的计数。|
|`priceRange 价格范围`|The relative price range of the business.  <br>商家的相对价格范围。|
|`servesCuisine serves美食`|The type of cuisine the restaurant serves.  <br>餐厅供应的美食类型。|
|`images 图像`|An image or images of the business. Required for valid markup depending on the type  <br>企业的一张或多张图片。有效标记是必需的，具体取决于类型|
|`telephone 电话`|A business phone number meant to be the primary contact method for customers.  <br>旨在作为客户主要联系方式的业务电话号码。|
|`url 网址`|The fully-qualified URL of the specific business location.  <br>特定营业地点的完全限定 URL。|
|`sameAs`|An array of URLs that represent this business  <br>代表此业务的 URL 数组|
|`openingHours 营业时间`|Opening hour specification of business. You can provide this as a single object, or an array of objects with the properties below.  <br>营业时间 指定业务。您可以将其作为单个对象或具有以下属性的对象数组提供。|
|`openingHours.opens openingHours.打开`|The opening hour of the place or service on the given day(s) of the week.  <br>地点或服务在一周中指定日期的营业时间。|
|`openingHours.closes`|The closing hour of the place or service on the given day(s) of the week.  <br>地点或服务在一周中指定日期的关闭时间。|
|`openingHours.dayOfWeek`|The day of the week for which these opening hours are valid. Can be a string or array of strings. Refer to [DayOfWeek](https://schema.org/DayOfWeek)  <br>这些营业时间在一周中的哪一天有效。可以是字符串或字符串数组。请参阅 [DayOfWeek](https://schema.org/DayOfWeek)|
|`openingHours.validFrom openingHours.valid发件人`|The date when the item becomes valid.  <br>项生效的日期。|
|`openingHours.validThrough`|The date after when the item is not valid.  <br>项无效的日期。|
|`review 回顾`|A review of the local business.  <br>对当地企业的评论。|
|`review.author 评论.author`|The author of this content or rating.  <br>此内容或评级的作者。|
|`review.reviewBody review.review正文`|The actual body of the review.  <br>评价的实际正文。|
|`review.datePublished review.date已发布`|Date of first broadcast/publication.  <br>首次广播/出版的日期。|
|`review.name`|The name of the item.  <br>项目的名称。|
|`review.rating 评论评分`|The rating given in this review  <br>本评论中给出的评级|
|`review.rating.ratingValuereview.rating.rating值`|The rating for the content.  <br>内容的评级。|
|`review.rating.reviewAspectreview.rating.review方面`|This Review or Rating is relevant to this part or facet of the itemReviewed.  <br>此评论或评级与 itemReviewed 的此部分或方面相关。|
|`review.rating.worstRatingreview.rating.worst 评分`|The lowest value allowed in this rating system. If worstRating is omitted, 1 is assumed.  <br>此评级系统中允许的最低值。如果省略 worstRating，则假定为 1。|
|`review.rating.bestRating review.rating.best评分`|The highest value allowed in this rating system. If bestRating is omitted, 5 is assumed  <br>此评级系统中允许的最高值。如果省略 bestRating，则假定为 5|
|`areasServed 服务区域`|The geographic area where a service or offered item is provided.  <br>提供服务或提供项目的地理区域。|
|`areasServed.GeoCircle 区域服务.GeoCircle`|A GeoCircle is a GeoShape representing a circular geographic area.  <br>GeoCircle 是表示圆形地理区域的 GeoShape。|
|`areasServed.GeoCircle.geoMidpoint区域服务.GeoCircle.geoMidpoint`|Indicates the GeoCoordinates at the centre of a GeoShape e.g. GeoCircle.  <br>指示 GeoShape 中心的 GeoCoordinates，例如 GeoCircle。|
|`areasServed.GeoCircle.geoMidpoint.latitude`|The latitude of a location. For example 37.42242  <br>位置的纬度。例如 37.42242|
|`areasServed.GeoCircle.geoMidpoint.longitude`|The name of the item.  <br>项目的名称。|
|`areasServed.GeoCircle.geoRadius区域服务.GeoCircle.geoRadius`|Indicates the approximate radius of a GeoCircle (metres unless indicated otherwise via Distance notation).  <br>指示 GeoCircle 的近似半径（米，除非通过距离表示法另有说明）。|
|`makesOffer`|A pointer to products or services offered by the organization or person.  <br>指向组织或个人提供的产品或服务的指针。|
|`makesOffer.offer`|An offer to transfer some rights to an item or to provide a service  <br>转让商品部分权利或提供服务的要约|
|`makesOffer.offer.priceSpecificationmakesOffer.offer.price规范`|One or more detailed price specifications, indicating the unit price and delivery or payment charges.  <br>一个或多个详细的价格规格，指示单价和运费或付款费用。|
|`makesOffer.offer.priceSpecification.priceCurrency`|The currency of the price, or a price component when attached to PriceSpecification and its subtypes.  <br>价格的货币，或附加到 PriceSpecification 及其子类型时的价格组成部分。|
|`makesOffer.offer.priceSpecification.price`|The offer price of a product, or of a price component when attached to PriceSpecification and its subtypes.  <br>产品的报价，或附加到 PriceSpecification 及其子类型时的价格组成部分的报价。|
|`makesOffer.offer.itemOffered`|An item being offered (or demanded)  <br>提供 （或要求） 的项目|
|`makesOffer.offer.itemOffered.name`|The name of the item  <br>项目的名称|
|`makesOffer.offer.itemOffered.description`|The description of the item.  <br>项目的描述。|
|`action 行动`|An action performed by a direct agent and indirect participants upon a direct object.  <br>由直接代理和间接参与者对直接对象执行的操作。|
|`action.target`|Indicates a target EntryPoint for an Action.  <br>指示 Action 的目标 EntryPoint。|

**其他** |`useAppDir` |如果使用新的 app 目录，则应将其设置为 true。如果位于 app 目录之外，则不需要。|

**NOTE: 注意：**

对于可用于 `LocalBusiness` 的大多数类型，建议使用图像;如有疑问，您应该添加一张图片。您可以在 Google 的[结构化数据测试工具](https://search.google.com/structured-data/testing-tool)中检查生成的 JSON

### Logo 商标

```js
import { LogoJsonLd } from 'next-seo';

const Page = () => (
  <>
    <h1>Logo JSON-LD</h1>
    <LogoJsonLd
      logo="http://www.your-site.com/images/logo.jpg"
      url="http://www.your-site.com"
    />
  </>
);

export default Page;
```

|Property 财产|Info 信息|
|---|---|
|`url 网址`|The URL of the website associated with the logo. [Logo guidelines](https://developers.google.com/search/docs/data-types/logo#definitions)  <br>与徽标关联的网站的 URL。[徽标准则](https://developers.google.com/search/docs/data-types/logo#definitions)|
|`logo 商标`|URL of a logo that is representative of the organization.  <br>代表组织的徽标的 URL。|

**Other** | `useAppDir` | This should be set to true if using the new app directory. Not required if outside of the app directory. |  
**其他** |`useAppDir` |如果使用新的 app 目录，则应将其设置为 true。如果位于 app 目录之外，则不需要。|

### Product 产品

[](https://github.com/garmeeh/next-seo?tab=readme-ov-file#product)

```js
import { ProductJsonLd } from 'next-seo';

const Page = () => (
  <>
    <h1>Product JSON-LD</h1>
    <ProductJsonLd
      productName="Executive Anvil"
      images={[
        'https://example.com/photos/1x1/photo.jpg',
        'https://example.com/photos/4x3/photo.jpg',
        'https://example.com/photos/16x9/photo.jpg',
      ]}
      description="Sleeker than ACME's Classic Anvil, the Executive Anvil is perfect for the business traveler looking for something to drop from a height."
      brand="ACME"
      color="blue"
      manufacturerName="Gary Meehan"
      manufacturerLogo="https://www.example.com/photos/logo.jpg"
      material="steel"
      slogan="For the business traveller looking for something to drop from a height."
      disambiguatingDescription="Executive Anvil, perfect for the business traveller."
      releaseDate="2014-02-05T08:00:00+08:00"
      productionDate="2015-02-05T08:00:00+08:00"
      purchaseDate="2015-02-06T08:00:00+08:00"
      award="Best Executive Anvil Award."
      reviews={[
        {
          author: 'Jim',
          datePublished: '2017-01-06T03:37:40Z',
          reviewBody:
            'This is my favorite product yet! Thanks Nate for the example products and reviews.',
          name: 'So awesome!!!',
          reviewRating: {
            bestRating: '5',
            ratingValue: '5',
            worstRating: '1',
          },
          publisher: {
            type: 'Organization',
            name: 'TwoVit',
          },
        },
      ]}
      aggregateRating={{
        ratingValue: '4.4',
        reviewCount: '89',
      }}
      offers={[
        {
          price: '119.99',
          priceCurrency: 'USD',
          priceValidUntil: '2020-11-05',
          itemCondition: 'https://schema.org/UsedCondition',
          availability: 'https://schema.org/InStock',
          url: 'https://www.example.com/executive-anvil',
          seller: {
            name: 'Executive Objects',
          },
        },
        {
          price: '139.99',
          priceCurrency: 'CAD',
          priceValidUntil: '2020-09-05',
          itemCondition: 'https://schema.org/UsedCondition',
          availability: 'https://schema.org/InStock',
          url: 'https://www.example.ca/executive-anvil',
          seller: {
            name: 'Executive Objects',
          },
        },
      ]}
      mpn="925872"
    />
  </>
);

export default Page;
```

Also available: `sku`, `gtin8`, `gtin13`, `gtin14`.  
还提供：`sku`、`gtin8`、`gtin13`、`gtin14`。

Valid values for `offers.itemCondition`:  
`offers.itemCondition` 的有效值：

- [https://schema.org/DamagedCondition](https://schema.org/DamagedCondition)
- [https://schema.org/NewCondition](https://schema.org/NewCondition)
- [https://schema.org/RefurbishedCondition](https://schema.org/RefurbishedCondition)
- [https://schema.org/UsedCondition](https://schema.org/UsedCondition)

Valid values for `offers.availability`:  
`offers.availability` 的有效值：

- [https://schema.org/Discontinued](https://schema.org/Discontinued)
- [https://schema.org/InStock](https://schema.org/InStock)
- [https://schema.org/InStoreOnly](https://schema.org/InStoreOnly)
- [https://schema.org/LimitedAvailability](https://schema.org/LimitedAvailability)
- [https://schema.org/OnlineOnly](https://schema.org/OnlineOnly)
- [https://schema.org/OutOfStock](https://schema.org/OutOfStock)
- [https://schema.org/PreOrder](https://schema.org/PreOrder)
- [https://schema.org/PreSale](https://schema.org/PreSale)
- [https://schema.org/SoldOut](https://schema.org/SoldOut)

The property `aggregateOffer` is also available: (It is ignored if `offers` is set)  
属性 `aggregateOffer` 也可用：（如果设置`了选件`，则会忽略它）

**Required properties 必需属性**

|Property 财产|Info 信息|
|---|---|
|`lowPrice 低价`|The lowest price of all offers available. Use a floating point number.  <br>所有可用优惠中最低的价格。使用浮点数。|
|`priceCurrency price货币`|The currency used to describe the product price, in three-letter ISO 4217 format.  <br>用于描述商品价格的货币，采用三个字母的 ISO 4217 格式。|

**Recommended properties 推荐属性**

|Property 财产|Info 信息|
|---|---|
|`highPrice 高价`|The highest price of all offers available. Use a floating point number.  <br>所有可用报价中最高的价格。使用浮点数。|
|`offerCount`|The number of offers for the product.  <br>商品的报价数量。|
|`offers 提供`|An offer to transfer some rights to an item or to provide a service. You can provide this as a single object, or an array of objects with the properties below.  <br>转让商品部分权利或提供服务的要约。您可以将其作为单个对象或具有以下属性的对象数组提供。|

**Other** | `useAppDir` | This should be set to true if using the new app directory. Not required if outside of the app directory. |  
**其他** |`useAppDir` |如果使用新的 app 目录，则应将其设置为 true。如果位于 app 目录之外，则不需要。|

More info on the product data type can be found [here](https://developers.google.com/search/docs/data-types/product).  
有关商品数据类型的更多信息，[请点击此处](https://developers.google.com/search/docs/data-types/product)。

### Social Profile 社交资料

[](https://github.com/garmeeh/next-seo?tab=readme-ov-file#social-profile)

```js
import { SocialProfileJsonLd } from 'next-seo';

const Page = () => (
  <>
    <h1>Social Profile JSON-LD</h1>
    <SocialProfileJsonLd
      type="Person"
      name="your name"
      url="http://www.your-site.com"
      sameAs={[
        'http://www.facebook.com/your-profile',
        'http://instagram.com/yourProfile',
        'http://www.linkedin.com/in/yourprofile',
        'http://plus.google.com/your_profile',
      ]}
    />
  </>
);

export default Page;
```

**Required properties 必需属性**

|Property 财产|Info 信息|
|---|---|
|`type 类型`|Person or Organization 个人或组织|
|`name 名字`|The name of the person or organization  <br>人员或组织的名称|
|`url 网址`|The URL for the person's or organization's official website.  <br>个人或组织的官方网站的 URL。|
|`sameAs`|An array of URLs for the person's or organization's official social media profile page(s)  <br>个人或组织的官方社交媒体个人资料页面的 URL 数组|

**Other** | `useAppDir` | This should be set to true if using the new app directory. Not required if outside of the app directory. |  
**其他** |`useAppDir` |如果使用新的 app 目录，则应将其设置为 true。如果位于 app 目录之外，则不需要。|

**Google Supported Social Profiles  
Google 支持的社交资料**

- Facebook 脸书
- Twitter 唽
- Google+ 谷歌+
- Instagram Instagram的
- YouTube 优酷
- LinkedIn 唽
- Myspace 我的空间
- Pinterest Pinterest 公司
- SoundCloud SoundCloud 的
- Tumblr

### News Article 新闻报道

[](https://github.com/garmeeh/next-seo?tab=readme-ov-file#news-article)

```js
import { NewsArticleJsonLd } from 'next-seo';

const Page = () => (
  <>
    <h1>News Article JSON-LD</h1>
    <NewsArticleJsonLd
      url="https://example.com/article"
      title="Article headline"
      images={[
        'https://example.com/photos/1x1/photo.jpg',
        'https://example.com/photos/4x3/photo.jpg',
        'https://example.com/photos/16x9/photo.jpg',
      ]}
      section="politic"
      keywords="prayuth,taksin"
      datePublished="2015-02-05T08:00:00+08:00"
      dateModified="2015-02-05T09:00:00+08:00"
      authorName="Jane Blogs"
      publisherName="Gary Meehan"
      publisherLogo="https://www.example.com/photos/logo.jpg"
      description="This is a mighty good description of this article."
      body="This is all text for this news article"
      isAccessibleForFree={true}
    />
  </>
);

export default Page;
```

### Park 公园

[](https://github.com/garmeeh/next-seo?tab=readme-ov-file#park)

```js
import { ParkJsonLd } from 'next-seo';

const Page = () => (
  <>
    <h1>Park JSON-LD</h1>
    <ParkJsonLd
      id="https://www.example.com/park/minnewaska-state-park"
      name="Minnewaska State Park"
      url="https://www.example.com/park"
      telephone="+18452550752"
      images={['https://example.com/photos/1x1/photo.jpg']}
      address={{
        streetAddress: '5281 Route 44-55',
        addressLocality: 'Kerhonkson',
        addressRegion: 'NY',
        postalCode: '12446',
        addressCountry: 'US',
      }}
      description="A wonderful description about Minnewaska State Park"
      geo={{
        latitude: '41.735149',
        longitude: '-74.239037',
      }}
      openingHours={[
        {
          opens: '09:00',
          closes: '18:00',
          dayOfWeek: [
            'Monday',
            'Tuesday',
            'Wednesday',
            'Thursday',
            'Friday',
            'Saturday',
            'Sunday',
          ],
          validFrom: '2019-12-23',
          validThrough: '2020-04-02',
        },
      ]}
    />
  </>
);

export default Page;
```

**Required properties 必需属性**

|Property 财产|Info 信息|
|---|---|
|`@id`|Globally unique ID of the specific park in the form of a URL.  <br>特定公园的全局唯一 ID，以 URL 的形式显示。|
|`address 地址`|Address of the specific park location  <br>特定公园位置的地址|
|`address.addressCountry address.addressCountry 地址`|The 2-letter ISO 3166-1 alpha-2 country code  <br>由 2 个字母组成的 ISO 3166-1 alpha-2 国家/地区代码|
|`address.addressLocality address.addressLocality 地址`|City 城市|
|`address.addressRegion address.addressRegion 地址区域`|State or province, if applicable.  <br>州或省（如果适用）。|
|`address.postalCode 地址.postalCode`|Postal or zip code. 邮政编码。|
|`address.streetAddress address.street地址`|Street number, street name, and unit number.  <br>街道号码、街道名称和单元号。|
|`name 名字`|Park name. 公园名称。|
|`description 描述`|Park description. 公园描述。|

**Supported properties 支持的属性**

|Property 财产|Info 信息|
|---|---|
|`geo 地理`|Geographic coordinates of the park.  <br>公园的地理坐标。|
|`geo.latitude geo.latitude 的`|The latitude of the park location  <br>公园位置的纬度|
|`geo.longitude geo.longitude （地理经度）`|The longitude of the park location  <br>园区位置的经度|
|`images 图像`|An image or images of the park. Required for valid markup depending on the type  <br>公园的一张或多张图片。有效标记是必需的，具体取决于类型|
|`telephone 电话`|A business phone number meant to be the primary contact method for customers.  <br>旨在作为客户主要联系方式的业务电话号码。|
|`url 网址`|The fully-qualified URL of the specific park.  <br>特定公园的完全限定 URL。|
|`openingHours 营业时间`|Opening hour specification of the park. You can provide this as a single object, or an array of objects with the properties below.  <br>公园的开放时间规格。您可以将其作为单个对象或具有以下属性的对象数组提供。|
|`openingHours.opens openingHours.打开`|The opening hour of the place or service on the given day(s) of the week.  <br>地点或服务在一周中指定日期的营业时间。|
|`openingHours.closes`|The closing hour of the place or service on the given day(s) of the week.  <br>地点或服务在一周中指定日期的关闭时间。|
|`openingHours.dayOfWeek`|The day of the week for which these opening hours are valid. Can be a string or array of strings. Refer to [DayOfWeek](https://schema.org/DayOfWeek)  <br>这些营业时间在一周中的哪一天有效。可以是字符串或字符串数组。请参阅 [DayOfWeek](https://schema.org/DayOfWeek)|
|`openingHours.validFrom openingHours.valid发件人`|The date when the item becomes valid.  <br>项生效的日期。|
|`openingHours.validThrough`|The date after when the item is not valid.  <br>项无效的日期。|
|`isAccessibleForFree isAccessibleForFree 免费`|Whether or not the park is accessible for free.  <br>公园是否免费进入。|

**Other** | `useAppDir` | This should be set to true if using the new app directory. Not required if outside oft the app directory. |  
**其他** |`useAppDir` |如果使用新的 app 目录，则应将其设置为 true。如果位于 app 目录之外，则不需要。|

[Google Docs for Social Profile](https://developers.google.com/search/docs/data-types/social-profile)

### Video 视频

[](https://github.com/garmeeh/next-seo?tab=readme-ov-file#video-1)

```js
import { VideoJsonLd } from 'next-seo';

const Page = () => (
  <>
    <h1>Video JSON-LD</h1>
    <VideoJsonLd
      name="How to make a Party Coffee Cake"
      description="This is how you make a Party Coffee Cake."
      contentUrl="http://www.example.com/video123.mp4"
      embedUrl="http://www.example.com/videoplayer?video=123"
      uploadDate="2018-02-05T08:00:00+08:00"
      duration="PT1M33S"
      thumbnailUrls={[
        'https://example.com/photos/1x1/photo.jpg',
        'https://example.com/photos/4x3/photo.jpg',
        'https://example.com/photos/16x9/photo.jpg',
      ]}
      expires="2019-02-05T08:00:00+08:00"
      hasPart={{
        name: 'Preheat oven',
        startOffset: 30,
        url: 'http://www.example.com/example?t=30',
      }}
      watchCount={2347}
      publication={{
        isLiveBroadcast: true,
        startDate: '2020-10-24T14:00:00+00:00',
        endDate: '2020-10-24T14:37:14+00:00',
      }}
      regionsAllowed={['IT', 'NL']}
    />
  </>
);

export default Page;
```

**Required properties 必需属性**

|Property 财产|Info 信息|
|---|---|
|`name 名字`|The title of the video.  <br>视频的标题。|
|`description 描述`|The description of the video. HTML tags are ignored.  <br>视频的描述。HTML 标记将被忽略。|
|`thumbnailUrl thumbnailUrl 的`|A URL pointing to the video thumbnail image file.  <br>指向视频缩略图文件的 URL。|
|`uploadDate 上传日期`|The date the video was first published, in ISO 8601 format.  <br>视频首次发布日期，采用 ISO 8601 格式。|

**Recommended properties 推荐属性**

|Property 财产|Info 信息|
|---|---|
|`contentUrl 内容网址`|A URL pointing to the actual video media file, in one of the supported encoding formats.  <br>指向实际视频媒体文件的 URL，采用支持的编码格式之一。|
|`duration 期间`|The duration of the video in ISO 8601 format  <br>ISO 8601 格式的视频时长|
|`embedUrl 嵌入 Url`|A URL pointing to a player for the specific video.  <br>指向特定视频的播放器的 URL。|
|`expires 到期`|If applicable, the date after which the video will no longer be available.  <br>视频将不再可用的日期（如果适用）。|
|`interactionStatistic`|The number of times the video has been watched.  <br>视频被观看的次数。|
|`publication 出版`|If your video is happening live and you want to be eligible for the LIVE badge.  <br>如果您的视频正在直播，并且您希望有资格获得 LIVE 徽章。|
|`regionsAllowed 区域允许`|The regions where the video is allowed.  <br>允许播放视频的地区。|

**Other** | `useAppDir` | This should be set to true if using the new app directory. Not required if outside of the app directory. |  
**其他** |`useAppDir` |如果使用新的 app 目录，则应将其设置为 true。如果位于 app 目录之外，则不需要。|

### VideoGame 电子游戏

[](https://github.com/garmeeh/next-seo?tab=readme-ov-file#videogame)

```js
import { VideoGameJsonLd } from 'next-seo';

const Page = () => (
  <>
    <h1>VideoGame JSON-LD</h1>
    <VideoGameJsonLd
      name="Red Dead Redemption 2"
      translatorName={['Translator 1', 'Translator 2']}
      languageName={['English', 'Kurdish']}
      description="Arthur Morgan and the Van der Linde gang are outlaws on the run. With federal agents and the best bounty hunters in the nation massing on their heels, the gang must rob, steal and fight their way across the rugged heartland of America in order to survive."
      processorRequirements="4 GHz"
      memoryRequirements="16 Gb"
      playMode="SinglePlayer"
      applicationCategory="Game"
      url="https://example.com/rdr2-game"
      platformName={['PC game', 'PlayStation 4']}
      operatingSystemName="windows"
      keywords="outlaw, gang, federal agents"
      datePublished="2019-02-05T08:00:00+08:00"
      image="https://example.com/photos/1x1/photo.jpg"
      publisherName="Vertical Games"
      producerName="Rockstar Games"
      producerUrl="https//www.example.com/producer"
      offers={[
        {
          price: '119.99',
          priceCurrency: 'USD',
          priceValidUntil: '2020-11-05',
          availability: 'https://schema.org/InStock',
          url: 'https://example.net/rdr2-game',
          seller: {
            name: 'Executive Gaming',
          },
        },
        {
          price: '139.99',
          priceCurrency: 'CAD',
          priceValidUntil: '2020-09-05',
          availability: 'https://schema.org/InStock',
          url: 'https://example.org/rdr2-game',
          seller: {
            name: 'Executive Gaming',
          },
        },
      ]}
      aggregateRating={{
        ratingValue: '44',
        reviewCount: '89',
        ratingCount: '684',
        bestRating: '100',
        worstRating: '1',
      }}
      reviews={[
        {
          author: {
            type: 'Person',
            name: 'AhmetKaya',
          },
          publisher: {
            type: 'Organization',
            name: 'Gam Production',
          },
          datePublished: '2017-01-06T03:37:40Z',
          reviewBody: 'Iki gozum.',
          name: 'Rica ederim.',
          reviewRating: {
            bestRating: '5',
            ratingValue: '5',
            worstRating: '1',
          },
        },
      ]}
    />
  </>
);

export default Page;
```

**Required properties 必需属性**

|Property 财产|Info 信息|
|---|---|
|`name 名字`|The title of the video game.  <br>视频游戏的标题。|

**Other** | `useAppDir` | This should be set to true if using the new app directory. Not required if outside of the app directory. |  
**其他** |`useAppDir` |如果使用新的 app 目录，则应将其设置为 true。如果位于 app 目录之外，则不需要。|

[More information about the schema  
有关 Schema 的更多信息](https://schema.org/VideoGame)

### Event 事件

[](https://github.com/garmeeh/next-seo?tab=readme-ov-file#event)

```js
import { EventJsonLd } from 'next-seo';

const Page = () => (
  <>
    <h1>Event JSON-LD</h1>
    <EventJsonLd
      name="My Event"
      startDate="2020-01-23T00:00:00.000Z"
      endDate="2020-01-24T00:00:00.000Z"
      location={{
        name: 'My Place',
        sameAs: 'https://example.com/my-place',
        address: {
          streetAddress: '1600 Saratoga Ave',
          addressLocality: 'San Jose',
          addressRegion: 'CA',
          postalCode: '95129',
          addressCountry: 'US',
        },
      }}
      url="https://example.com/my-event"
      images={['https://example.com/photos/photo.jpg']}
      description="My event @ my place"
      offers={[
        {
          price: '119.99',
          priceCurrency: 'USD',
          priceValidUntil: '2020-11-05',
          itemCondition: 'https://schema.org/UsedCondition',
          availability: 'https://schema.org/InStock',
          url: 'https://www.example.com/executive-anvil',
          seller: {
            name: 'John Doe',
          },
          validFrom: '2020-11-01T00:00:00.000Z',
        },
        {
          price: '139.99',
          priceCurrency: 'CAD',
          priceValidUntil: '2020-09-05',
          itemCondition: 'https://schema.org/UsedCondition',
          availability: 'https://schema.org/InStock',
          url: 'https://www.example.ca/executive-anvil',
          seller: {
            name: 'John Doe Sr.',
          },
          validFrom: '2020-08-05T00:00:00.000Z',
        },
      ]}
      performers={[
        {
          name: 'Adele',
        },
        {
          name: 'Kira and Morrison',
        },
      ]}
      organizer={{
        type: 'Organization',
        name: 'Unnamed organization',
        url: 'https://www.unnamed.com',
      }}
      eventStatus="EventScheduled"
      eventAttendanceMode="OfflineEventAttendanceMode"
    />
  </>
);

export default Page;
```

**Required properties 必需属性**

|Property 财产|Info 信息|
|---|---|
|`name 名字`|The name of the event  <br>事件的名称|
|`startDate 开始日期`|The start date time of the event in iso8601 format  <br>事件的开始日期时间（iso8601 格式）|
|`endDate 结束日期`|The end date time of the event in iso8601 format  <br>事件的结束日期时间（以 iso8601 格式表示）|
|`location 位置`|Location of the event, can be `Place` or `VirtualLocation`  <br>事件的位置，可以是 `Place` 或 `VirtualLocation`|

**Other** | `useAppDir` | This should be set to true if using the new app directory. Not required if outside of the app directory. |  
**其他** |`useAppDir` |如果使用新的 app 目录，则应将其设置为 true。如果位于 app 目录之外，则不需要。|

**`Place` type** Requires `address` property and `name`.  
**`地点`类型**需要 `address` 属性和 `name`。

**`VirtualLocation` type** Requires `url` property, doesn't require `name`.  
**`VirtualLocation` 类型**需要 `url` 属性，不需要 `name`。

**Supported properties 支持的属性**

|Property 财产|Info 信息|
|---|---|
|`description 描述`|Description of the event 活动描述|
|`location.name`|Name of the location 位置名称|
|`location.sameAs`|URL of a reference web page that identifies location  <br>标识位置的参考网页的 URL|
|`images 图像`|An image or images of the event.  <br>活动的一张或多张图片。|
|`url 网址`|The fully-qualified URL of the event.  <br>事件的完全限定 URL。|
|`offers 提供`|An offer to transfer some rights to an item or to provide a service. You can provide this as a single object, or an array of objects with the properties below.  <br>转让商品部分权利或提供服务的要约。您可以将其作为单个对象或具有以下属性的对象数组提供。|
|`performers 演员`|All artists that perform at this event. You can provide this as a single object, or an array of objects with the properties below.  <br>在本次活动中表演的所有艺术家。您可以将其作为单个对象或具有以下属性的对象数组提供。|
|`performers.name`|The name of the performer  <br>执行者的姓名|
|`performers.type`|Either `Person` or `PerformingGroup`  <br>`Person` 或 `PerformingGroup`|
|`organizer 组织者`|The organizer of the event  <br>活动组织者|
|`organizer.type organizer.type （组织者类型）`|Either `Organization` or `Person`  <br>`组织`或`个人`|
|`organizer.name`|Name of the organizer of the event  <br>活动组织者的名称|
|`organizer.url`|URL of the organizer of the event  <br>活动组织者的 URL|
|`eventStatus 事件状态`|Status of the event, type `EventStatus`  <br>事件的状态，键入 `EventStatus`|
|`eventAttendanceMode eventAttendanceMode 事件`|Attendance mode of the event, type `EventAttendanceMode`  <br>活动的 Attendance mode，键入 `EventAttendanceMode`|

**`EventStatus` type  
`EventStatus` 类型**

- 'EventCancelled' '事件已取消'
- 'EventMovedOnline'
- 'EventPostponed' “EventPostponed”
- 'EventRescheduled' 'EventRescheduled' （事件重新安排）
- 'EventScheduled'

**`EventAttendanceMode` type  
`EventAttendanceMode` 类型**

- 'MixedEventAttendanceMode'
- 'OfflineEventAttendanceMode'
- 'OnlineEventAttendanceMode'

**`offers` Required properties  
`提供`必需属性**

|Property 财产|Info 信息|
|---|---|
|`offers.price offers.price 优惠价`|The cost of the offer  <br>产品/服务的成本|
|`offers.priceCurrency offers.priceCurrency 的`|The currency of the offer  <br>选件的货币|

**`offers` Recommended properties  
`提供`推荐属性**

|Property 财产|Info 信息|
|---|---|
|`offers.priceValidUntil`|Until when the price of the offer expires  <br>直到优惠价格到期|
|`offers.itemCondition`|The condition of the product or service  <br>产品或服务的状况|
|`offers.availability offers.availability （优惠可用性）`|The availability of this item — for example In stock, Out of stock, Pre-order, etc.  <br>此商品的库存情况 — 例如：有货、缺货、预购等。|
|`offers.url offers.url 的`|URL of the item 项目的 URL|
|`offers.seller offers.seller 卖家`|The person who is selling this item  <br>销售此商品的人|
|`offers.seller.name`|The name of the person  <br>人员的姓名|
|`offers.validFrom offers.valid发件人`|Since when the price of the offer is valid  <br>优惠价格有效时起|

The property `aggregateOffer` is also available: (It is ignored if `offers` is set)  
属性 `aggregateOffer` 也可用：（如果设置`了选件`，则会忽略它）

**Required properties 必需属性**

|Property 财产|Info 信息|
|---|---|
|`lowPrice 低价`|The lowest price of all offers available. Use a floating point number.  <br>所有可用优惠中最低的价格。使用浮点数。|
|`priceCurrency price货币`|The currency used to describe the product price, in three-letter ISO 4217 format.  <br>用于描述商品价格的货币，采用三个字母的 ISO 4217 格式。|

**Recommended properties 推荐属性**

|Property 财产|Info 信息|
|---|---|
|`highPrice 高价`|The highest price of all offers available. Use a floating point number.  <br>所有可用报价中最高的价格。使用浮点数。|
|`offerCount`|The number of offers for the product.  <br>商品的报价数量。|

For reference and more info check [Google's Search Event DataType](https://developers.google.com/search/docs/data-types/event)  
有关参考和更多信息，请查看 [Google 的 Search Event DataType](https://developers.google.com/search/docs/data-types/event)

### Q&A Q&A （问答）

[](https://github.com/garmeeh/next-seo?tab=readme-ov-file#qa)

Q&A pages are web pages that contain data in a question-and-answer format, which is one question followed by its answers.  
Q&A 页面是包含问答格式数据的网页，即一个问题后跟其答案。

```js
import { QAPageJsonLd } from 'next-seo';

const Page = () => (
  <>
    <h1>Q&A Page JSON-LD</h1>
    <QAPageJsonLd
      mainEntity={{
        name: 'How many ounces are there in a pound?',
        text: 'I have taken up a new interest in baking and keep running across directions in ounces and pounds. I have to translate between them and was wondering how many ounces are in a pound?',
        answerCount: 3,
        upvoteCount: 26,
        dateCreated: '2016-07-23T21:11Z',
        author: {
          name: 'New Baking User',
          url: 'https://example.com/bakinguser',
        },
        acceptedAnswer: {
          text: '1 pound (lb) is equal to 16 ounces (oz).',
          dateCreated: '2016-11-02T21:11Z',
          upvoteCount: 1337,
          url: 'https://example.com/question1#acceptedAnswer',
          author: {
            name: 'SomeUser',
            url: 'https://example.com/someuser',
          },
        },
        suggestedAnswer: [
          {
            text: 'Are you looking for ounces or fluid ounces? If you are looking for fluid ounces there are 15.34 fluid ounces in a pound of water.',
            dateCreated: '2016-11-02T21:11Z',
            upvoteCount: 42,
            url: 'https://example.com/question1#suggestedAnswer1',
            author: {
              name: 'AnotherUser',
              url: 'https://example.com/anotheruser',
            },
          },
          {
            text: `I can't remember exactly, but I think 18 ounces in a lb. You might want to double check that.`,
            dateCreated: '2016-11-06T21:11Z',
            upvoteCount: 0,
            url: 'https://example.com/question1#suggestedAnswer2',
            author: {
              name: 'ConfusedUser',
              url: 'https://example.com/confuseduser',
            },
          },
        ],
      }}
    />
  </>
);

export default Page;
```

**Required properties 必需属性**

|Property 财产|Info 信息|
|---|---|
|`mainEntity mainEntity （主实体）`|The Question for this page must be nested under the mainEntity property of the QAPageJsonld component.  <br>此页面的问题必须嵌套在 QAPageJsonld 组件的 mainEntity 属性下。|

**Other** | `useAppDir` | This should be set to true if using the new app directory. Not required if outside of the app directory. |  
**其他** |`useAppDir` |如果使用新的 app 目录，则应将其设置为 true。如果位于 app 目录之外，则不需要。|

**`mainEntity` Required properties  
`mainEntity （主实体）`必需属性**

|Property 财产|Info 信息|
|---|---|
|`answerCount`|The total number of answers to the question.  <br>问题的答案总数。|
|`acceptedAnswer` or `suggestedAnswer`  <br>`acceptedAnswer` 或 `suggestedAnswer`|To be eligible for the rich result, a question must have at least one answer – either an acceptedAnswer or a suggestedAnswer.  <br>要符合显示富媒体搜索结果的条件，问题必须至少包含一个答案，即 acceptedAnswer 或 suggestedAnswer。|
|`name 名字`|The full text of the short form of the question.  <br>问题的简短形式的完整文本。|

**`mainEntity` Supported properties  
`mainEntity （主实体）`支持的属性**

|Property 财产|Info 信息|
|---|---|
|`author 作者`|The author of the question.  <br>问题的作者。|
|`dateCreated 创建日期`|The date at which the question was added to the page, in ISO-8601 format.  <br>问题添加到页面的日期，采用 ISO-8601 格式。|
|`text 发短信`|The full text of the long form of the question.  <br>问题的长格式的全文。|
|`upvoteCount`|The total number of votes that this question has received.  <br>此问题已获得的总票数。|

**`acceptedAnswer`/`suggestedAnswer` Required properties  
`acceptedAnswer`/`suggestedAnswer` 必需属性**

|Property 财产|Info 信息|
|---|---|
|`text 发短信`|The full text of the answer.  <br>答案的全文。|

**`acceptedAnswer`/`suggestedAnswer` Supported properties  
`acceptedAnswer`/`suggestedAnswer` 支持的属性**

|Property 财产|Info 信息|
|---|---|
|`author 作者`|The author of the question.  <br>问题的作者。|
|`dateCreated 创建日期`|The date at which the question was added to the page, in ISO-8601 format.  <br>问题添加到页面的日期，采用 ISO-8601 格式。|
|`upvoteCount`|The total number of votes that this question has received.  <br>此问题已获得的总票数。|
|`url 网址`|A URL that links directly to this answer.  <br>直接链接到此答案的 URL。|

For reference and more info check [Google's Search Q&A DataType](https://developers.google.com/search/docs/data-types/qapage)  
有关参考和更多信息，请查看 [Google 的搜索 Q&A 数据类型](https://developers.google.com/search/docs/data-types/qapage)

### Collection Page 集合页面

[](https://github.com/garmeeh/next-seo?tab=readme-ov-file#collection-page)

Collection pages are web pages. Every web page is implicitly assumed to be declared to be of type WebPage, so the various properties about that webpage, such as breadcrumb may be used. We recommend explicit declaration if these properties are specified, but if they are found outside of an item scope, they will be assumed to be about the page.  
集合页是网页。每个网页都被隐式假定为类型 WebPage，因此可以使用该网页的各种属性，例如痕迹导航。如果指定了这些属性，我们建议使用显式声明，但如果在项目范围之外找到它们，则假定它们与页面有关。

```js
import { CollectionPageJsonLd } from 'next-seo';

const Page = () => (
  <>
    <h1>Collection Page JSON-LD</h1>
    <CollectionPageJsonLd
      name="Resistance 3: Fall of Man"
      hasPart={[
        {
          about:
            'Britten Four Sea Interludes and Passacaglia from Peter Grimes',
          author: 'John Doe',
          name: 'Schema.org Ontology',
          datePublished: '2021-03-09',
          audience: 'Internet',
          keywords: 'schema',
          thumbnailUrl: 'https://i.ytimg.com/vi/eXSJ3PO9Tas/hqdefault.jpg',
          image: 'hqdefault.jpg',
        },
        {
          about: 'Shostakovich Symphony No. 7 (Leningrad)',
          author: 'John Smith',
          name: 'Creative work name',
          datePublished: '2014-10-01T19:30',
        },
      ]}
    />
  </>
);

export default Page;
```

**Required properties 必需属性**

|Property 财产|Info 信息|
|---|---|
|`name 名字`|The name of the item.  <br>项目的名称。|
|`hasPart`|Indicates an item or CreativeWork that is part of this item, or CreativeWork (in some sense).  <br>指示属于此项的项或 CreativeWork，或某种意义上的 CreativeWork。|

**Supported properties 支持的属性**

|Property 财产|Info 信息|
|---|---|
|`hasPart.creativeWork`|The most generic kind of [creative work](https://schema.org/CreativeWork), including books, movies, photographs, software programs, etc  <br>最通用的[创意作品](https://schema.org/CreativeWork)，包括书籍、电影、照片、软件程序等|

**Other** | `useAppDir` | This should be set to true if using the new app directory. Not required if outside of the app directory. |  
**其他** |`useAppDir` |如果使用新的 app 目录，则应将其设置为 true。如果位于 app 目录之外，则不需要。|

**`creativeWork` Required properties  
`创意工作`必需属性**

|Property 财产|Info 信息|
|---|---|
|`hasPart.creativeWork.author`|The author of this content or rating. Please note that author is special in that HTML 5 provides a special mechanism for indicating authorship via the rel tag. That is equivalent to this and may be used interchangeably.  <br>此内容或评级的作者。请注意，author 很特殊，因为 HTML 5 提供了一种特殊的机制，用于通过 rel 标签来指示作者身份。这与此等效，可以互换使用。|
|`hasPart.creativeWork.abouthasPart.creativeWork.关于`|The subject matter of the content.  <br>内容的主题。|
|`hasPart.creativeWork.datePublishedhasPart.creativeWork.date已发布`|Date of first broadcast/publication.  <br>首次广播/出版的日期。|
|`hasPart.creativeWork.name`|The name of the item.  <br>项目的名称。|

**`creativeWork` Supported properties  
`创意工作`支持的属性**

|Property 财产|Info 信息|
|---|---|
|`hasPart.creativeWork.audiencehasPart.creativeWork.观众`|An intended audience, i.e. a group for whom something was created.  <br>目标受众，即为其创建某物的组。|
|`hasPart.creativeWork.keywordshasPart.creativeWork.关键字`|Keywords or tags used to describe this content. Multiple entries in a keywords list are typically delimited by commas.  <br>用于描述此内容的关键字或标签。关键字列表中的多个条目通常用逗号分隔。|
|`hasPart.creativeWork.thumbnailUrl`|A thumbnail image relevant to the Thing.  <br>与事物相关的缩略图图像。|
|`hasPart.creativeWork.image`|An image of the item. This can be a URL or a fully described ImageObject.  <br>项目的图像。这可以是 URL 或完整描述的 ImageObject。|

For reference and more info check [Collection Page DataType](https://schema.org/CollectionPage)  
有关参考和更多信息，请查看 [Collection Page DataType](https://schema.org/CollectionPage)

### Profile page “个人资料”页面

[](https://github.com/garmeeh/next-seo?tab=readme-ov-file#profile-page)

Profile pages are web pages. Every web page is implicitly assumed to be declared to be of type WebPage, so the various properties about that webpage, such as breadcrumb may be used. We recommend explicit declaration if these properties are specified, but if they are found outside of an item scope, they will be assumed to be about the page.  
个人资料页面是网页。每个网页都被隐式假定为类型 WebPage，因此可以使用该网页的各种属性，例如痕迹导航。如果指定了这些属性，我们建议使用显式声明，但如果在项目范围之外找到它们，则假定它们与页面有关。

```js
import { ProfilePageJsonLd } from 'next-seo';

const Page = () => (
  <>
    <h1>Profile page JSON-LD</h1>
    <ProfilePageJsonLd
      lastReviewed="2014-10-01T19:30"
      breadcrumb={[
        {
          position: 1,
          name: 'Books',
          item: 'https://example.com/books',
        },
        {
          position: 2,
          name: 'Authors',
          item: 'https://example.com/books/authors',
        },
      ]}
    />
  </>
);

export default Page;
```

**Required properties 必需属性**

|Property 财产|Info 信息|
|---|---|
|`breadcrumb 面包屑`|A set of links that can help a user understand and navigate a website hierarchy represented as string or [BreadcrumbList](https://github.com/garmeeh/next-seo?tab=readme-ov-file#breadcrumb).  <br>一组链接，可帮助用户了解和导航以 string 或 [BreadcrumbList](https://github.com/garmeeh/next-seo?tab=readme-ov-file#breadcrumb) 表示的网站层次结构。|

**Supported properties 支持的属性**

|Property 财产|Info 信息|
|---|---|
|`lastReviewed 上次评论`|Date on which the content on this web page was last reviewed for accuracy and/or completeness.  <br>上次审核本网页上内容的准确性和/或完整性的日期。|

**Other** | `useAppDir` | This should be set to true if using new app directory. Not required if outside of app directory. |  
**其他** |`useAppDir` |如果使用 new app directory，则应将其设置为 true。如果位于 app 目录之外，则不需要。|

For reference and more info check [Profile Page DataType](https://schema.org/ProfilePage)  
有关参考和更多信息，请查看 [Profile Page DataType](https://schema.org/ProfilePage)

### Carousel 旋转 木马

[](https://github.com/garmeeh/next-seo?tab=readme-ov-file#carousel)

**Required properties of Carousel Component  
Carousel Component 的必需属性**

|Property 财产|Info 信息|
|---|---|
|`type 类型`|The type of carousel 轮播的类型|
|`data 数据`|The data in the form of an array for the item list in the carousel  <br>轮播中商品列表的数组形式的数据|

**Other** | `useAppDir` | This should be set to true if using the new app directory. Not required if outside of the app directory. |  
**其他** |`useAppDir` |如果使用新的 app 目录，则应将其设置为 true。如果位于 app 目录之外，则不需要。|

#### Default (Summary List) 默认 （摘要列表）

[](https://github.com/garmeeh/next-seo?tab=readme-ov-file#default-summary-list)

```js
import React from 'react';
import { CarouselJsonLd } from 'next-seo';

export default () => (
  <>
    <h1>Carousel Default JSON-LD</h1>
    <CarouselJsonLd
      ofType="default"
      data={[
        { url: 'http://example.com/peanut-butter-cookies.html' },
        {
          url: 'http://example.com/triple-chocolate-chunk.html',
        },
      ]}
    />
  </>
);
```

**Data required properties 数据必需属性**

|Property 财产|Info 信息|
|---|---|
|`url 网址`|URL of the item's detailed page.  <br>项目详细信息页面的 URL。|

#### Course 课程

[](https://github.com/garmeeh/next-seo?tab=readme-ov-file#course-1)

```js
import React from 'react';
import { CarouselJsonLd } from 'next-seo';

export default () => (
  <>
    <h1>Carousel Course JSON-LD</h1>
    <CarouselJsonLd
      ofType="course"
      data={[
        {
          courseName: 'Course 1',
          description: 'Course 1 Description',
          providerName: 'Course Provider',
          url: 'http://example.com/course-1.html',
        },
        {
          courseName: 'Course 2',
          description: 'Course 2 Description',
          providerName: 'Course Provider',
          url: 'http://example.com/course-2.html',
        },
      ]}
    />
  </>
);
```

**Data required properties 数据必需属性**

|Property 财产|Info 信息|
|---|---|
|`courseName 课程名称`|The title of the course.  <br>课程的标题。|
|`description 描述`|A description of the course. Display limit of 60 characters.  <br>课程的描述。显示限制为 60 个字符。|
|`providerName providerName （提供商名称）`|The course provider name.  <br>课程提供者名称。|
|`url 网址`|URL of the item's detailed page .  <br>项目详情页面的 URL 。|

**Data Recommended properties  
数据 Recommended properties**

|Property 财产|Info 信息|
|---|---|
|`providerUrl providerUrl 的`|The url to the course provider.  <br>课程提供商的 URL。|

#### Movie 电影

[](https://github.com/garmeeh/next-seo?tab=readme-ov-file#movie)

```js
import React from 'react';
import { CarouselJsonLd } from 'next-seo';

export default () => (
  <>
    <h1>Carousel Movie JSON-LD</h1>
    <CarouselJsonLd
      ofType="movie"
      data={[
        {
          name: 'Movie 1',
          url: 'http://example.com/movie-1.html',
          image:
            'https://i.pinimg.com/originals/96/a0/0d/96a00d42b0ff8f80b7cdf2926a211e47.jpg',
          director: {
            name: 'John Doe',
          },
          review: {
            author: { type: 'Person', name: 'Ronan Farrow' },
            reviewBody:
              'Heartbreaking, inpsiring, moving. Bradley Cooper is a triple threat.',
            reviewRating: { ratingValue: '5' },
          },
        },
        {
          name: 'Movie 2',
          url: 'http://example.com/movie-1.html',
          image:
            'https://i.pinimg.com/originals/96/a0/0d/96a00d42b0ff8f80b7cdf2926a211e47.jpg',
          director: [
            {
              name: 'Mary Doe',
            },
            {
              name: 'John Doe',
            },
          ],
          review: {
            author: { type: 'Person', name: 'Ronan Farrow' },
            reviewBody:
              'Heartbreaking, inpsiring, moving. Rowan Atkinson is a triple threat.',
            reviewRating: { ratingValue: '5' },
          },
        },
      ]}
    />
  </>
);
```

**Data required properties 数据必需属性**

|Property 财产|Info 信息|
|---|---|
|`name 名字`|Name of the movie. 影片名称。|
|`image 图像`|An image that represents the movie.  <br>表示影片的图像。|
|`url 网址`|URL of the item's detailed page.  <br>项目详细信息页面的 URL。|

**Data Recommended properties  
数据 Recommended properties**

|Property 财产|Info 信息|
|---|---|
|`director 导演`|The directors of the movie.  <br>电影的导演。|
|`dateCreated 创建日期`|The date the movie was released.  <br>影片的上映日期。|
|`aggregateRating aggregateRating （聚合评分）`|Aggregate Rating object for the movie.  <br>影片的 Aggregate Rating 对象。|
|`review 回顾`|Review for the movie. 电影评论。|

#### Recipe 食谱

[](https://github.com/garmeeh/next-seo?tab=readme-ov-file#recipe-1)

```js
import React from 'react';
import { CarouselJsonLd } from 'next-seo';

export default () => (
  <>
    <h1>Carousel Recipe JSON-LD</h1>
    <CarouselJsonLd
      ofType="recipe"
      data={[
        {
          name: 'Party Coffee Cake',
          url: 'http://example.com/recipe-1.html',
          images: [
            'https://example.com/photos/1x1/photo.jpg',
            'https://example.com/photos/4x3/photo.jpg',
            'https://example.com/photos/16x9/photo.jpg',
          ],
          authorName: 'Mary Stone',
          datePublished: '2018-03-10',
          description: 'This coffee cake is awesome and perfect for parties.',
          prepTime: 'PT20M',
          cookTime: 'PT30M',
          totalTime: 'PT50M',
          keywords: 'cake for a party, coffee',
          yields: '10',
          category: 'Dessert',
          calories: 270,
          cuisine: 'American',
          ingredients: [
            '2 cups of flour',
            '3/4 cup white sugar',
            '2 teaspoons baking powder',
            '1/2 teaspoon salt',
            '1/2 cup butter',
            '2 eggs',
            '3/4 cup milk',
          ],
          instructions: [
            {
              name: 'Preheat',
              text: 'Preheat the oven to 350 degrees F. Grease and flour a 9x9 inch pan.',
              url: 'https://example.com/party-coffee-cake#step1',
              image: 'https://example.com/photos/party-coffee-cake/step1.jpg',
            },
            {
              name: 'Mix dry ingredients',
              text: 'In a large bowl, combine flour, sugar, baking powder, and salt.',
              url: 'https://example.com/party-coffee-cake#step2',
              image: 'https://example.com/photos/party-coffee-cake/step2.jpg',
            },
            {
              name: 'Spread into pan',
              text: 'Spread into the prepared pan.',
              url: 'https://example.com/party-coffee-cake#step4',
              image: 'https://example.com/photos/party-coffee-cake/step4.jpg',
            },
            {
              name: 'Bake',
              text: 'Bake for 30 to 35 minutes, or until firm.',
              url: 'https://example.com/party-coffee-cake#step5',
              image: 'https://example.com/photos/party-coffee-cake/step5.jpg',
            },
          ],
          aggregateRating: {
            ratingValue: '5',
            ratingCount: '18',
          },
          video: {
            name: 'How to make a Party Coffee Cake',
            description: 'This is how you make a Party Coffee Cake.',
            thumbnailUrls: [
              'https://example.com/photos/1x1/photo.jpg',
              'https://example.com/photos/4x3/photo.jpg',
              'https://example.com/photos/16x9/photo.jpg',
            ],
            contentUrl: 'http://www.example.com/video123.mp4',
            embedUrl: 'http://www.example.com/videoplayer?video=123',
            uploadDate: '2018-02-05T08:00:00+08:00',
            duration: 'PT1M33S',
            expires: '2019-02-05T08:00:00+08:00',
          },
        },
        {
          name: 'Party Coffee Cake 2',
          url: 'http://example.com/recipe-2.html',
          images: [
            'https://example.com/photos/1x1/photo.jpg',
            'https://example.com/photos/4x3/photo.jpg',
            'https://example.com/photos/16x9/photo.jpg',
          ],
          authorName: 'Mary Stone 2',
          datePublished: '2018-03-10',
          description: 'This coffee cake is awesome and perfect for parties.',
          prepTime: 'PT20M',
          cookTime: 'PT30M',
          totalTime: 'PT50M',
          keywords: 'cake for a party, coffee',
          yields: '10',
          category: 'Dessert',
          calories: 270,
          cuisine: 'American',
          ingredients: [
            '2 cups of flour',
            '3/4 cup white sugar',
            '2 teaspoons baking powder',
            '1/2 teaspoon salt',
            '1/2 cup butter',
            '2 eggs',
            '3/4 cup milk',
          ],
          instructions: [
            {
              name: 'Preheat',
              text: 'Preheat the oven to 350 degrees F. Grease and flour a 9x9 inch pan.',
              url: 'https://example.com/party-coffee-cake#step1',
              image: 'https://example.com/photos/party-coffee-cake/step1.jpg',
            },
            {
              name: 'Mix dry ingredients',
              text: 'In a large bowl, combine flour, sugar, baking powder, and salt.',
              url: 'https://example.com/party-coffee-cake#step2',
              image: 'https://example.com/photos/party-coffee-cake/step2.jpg',
            },
            {
              name: 'Spread into pan',
              text: 'Spread into the prepared pan.',
              url: 'https://example.com/party-coffee-cake#step4',
              image: 'https://example.com/photos/party-coffee-cake/step4.jpg',
            },
            {
              name: 'Bake',
              text: 'Bake for 30 to 35 minutes, or until firm.',
              url: 'https://example.com/party-coffee-cake#step5',
              image: 'https://example.com/photos/party-coffee-cake/step5.jpg',
            },
          ],
          aggregateRating: {
            ratingValue: '5',
            ratingCount: '18',
          },
          video: {
            name: 'How to make a Party Coffee Cake',
            description: 'This is how you make a Party Coffee Cake.',
            thumbnailUrls: [
              'https://example.com/photos/1x1/photo.jpg',
              'https://example.com/photos/4x3/photo.jpg',
              'https://example.com/photos/16x9/photo.jpg',
            ],
            contentUrl: 'http://www.example.com/video123.mp4',
            embedUrl: 'http://www.example.com/videoplayer?video=123',
            uploadDate: '2018-02-05T08:00:00+08:00',
            duration: 'PT1M33S',
            expires: '2019-02-05T08:00:00+08:00',
          },
        },
      ]}
    />
  </>
);
```

**Data required properties 数据必需属性**

|Property 财产|Info 信息|
|---|---|
|`name 名字`|The name of the dish.  <br>菜品的名称。|
|`description 描述`|A description of the recipe  <br>配方描述|
|`authorName authorName （作者姓名）`|The name of the recipe author  <br>配方作者的姓名|
|`ingredients 成分`|A list of ingredient strings  <br>成分字符串列表|
|`instructions 指示`|-|
|`instructions.name`|The name of the instruction step.  <br>指令步骤的名称。|
|`instructions.text instructions.text （说明文本）`|The directions of the instruction step.  <br>指令步骤的方向。|
|`url 网址`|URL of the item's detailed page.  <br>项目详细信息页面的 URL。|

#### Custom 习惯

[](https://github.com/garmeeh/next-seo?tab=readme-ov-file#custom)

```js
import React from 'react';
import { CarouselJsonLd } from 'next-seo';

export default () => (
  <>
    <h1>Carousel Custom JSON-LD</h1>
    <CarouselJsonLd
      ofType="custom"
      url="http://example.com/custom-carousel.html"
      name="Carousel Custom"
      description="Custom Carousel Description"
      data={[
        {
          position: 1,
          type: 'CustomList',
          name: 'Custom 1',
        },
        {
          position: 2,
          type: 'CustomList',
          name: 'Custom 2',
        },
      ]}
    />
  </>
);
```

**Data Required Properties 数据必需属性**

|Property 财产|Info 信息|
|---|---|
|`type 类型`|Type of the item. 项目的类型。|
|`name 名字`|Name of the item. 项目的名称。|

**Data Recommended properties  
数据 Recommended properties**

|Property 财产|Info 信息|
|---|---|
|`position 位置`|Position of the item. If not pass property, it will increase regularly.  <br>项目的位置。如果不传递属性，它将定期增加。|

### Software App 软件应用

[](https://github.com/garmeeh/next-seo?tab=readme-ov-file#software-app)

```js
import React from 'react';
import { SoftwareAppJsonLd } from 'next-seo';

export default () => (
  <>
    <h1>Software App JSON-LD</h1>
    <SoftwareAppJsonLd
      name="Angry Birds"
      price="1.00"
      priceCurrency="USD"
      aggregateRating={{ ratingValue: '4.6', reviewCount: '8864' }}
      operatingSystem="ANDROID"
      applicationCategory="GameApplication"
      keywords="angrybirds, arcade, slingshot"
    />
  </>
);
```

**Data required properties 数据必需属性**

|Property 财产|Info 信息|
|---|---|
|`name 名字`|The name of the app.  <br>应用程序的名称。|
|`price 价格`|Price of the app. If the app is free of charge, set offers.price to 0  <br>应用程序的价格。如果应用程序是免费的，请将 offers.price 设置为 0|
|`priceCurrency price货币`|If the app has a price greater than 0, you must include offers.currency.  <br>如果应用的价格大于 0，则必须包含 offers.currency。|
|`aggregateRating aggregateRating （聚合评分）`|The average review score of the app. (Not required if review is present.)  <br>应用的平均评分。（如果存在评论，则不需要。|
|`review 回顾`|A single review of the app. (Not required if aggregateRating is present.)  <br>应用程序的单个评论。（如果存在 aggregateRating，则不需要。|

**Other** | `useAppDir` | This should be set to true if using the new app directory. Not required if outside of the app directory. |  
**其他** |`useAppDir` |如果使用新的 app 目录，则应将其设置为 true。如果位于 app 目录之外，则不需要。|

**Data Recommended properties  
数据 Recommended properties**

|Property 财产|Info 信息|
|---|---|
|`operatingSystem 操作系统`|The operating System supported by the game it self.  <br>游戏本身支持的操作系统。|
|`applicationCategory 应用类别`|Desktop Software or Video Game...  <br>桌面软件或视频游戏...|

**Data other properties data 其他属性**

|Property 财产|Info 信息|
|---|---|
|`keywords 关键字`|Keywords or tags used to describe this content. Multiple entries in a keywords list are typically delimited by commas.  <br>用于描述此内容的关键字或标签。关键字列表中的多个条目通常用逗号分隔。|

For reference and more info check [Google docs for Software App](https://developers.google.com/search/docs/data-types/software-app) and [Schema.org docs](https://schema.org/SoftwareApplication)  
有关参考和更多信息，请查看 [Google 文档 软件应用](https://developers.google.com/search/docs/data-types/software-app) 和 [Schema.org 文档](https://schema.org/SoftwareApplication)

### Organization 组织

[](https://github.com/garmeeh/next-seo?tab=readme-ov-file#organization)

```js
import React from 'react';
import { OrganizationJsonLd } from 'next-seo';

export default () => (
  <>
    <h1>Organization JSON-LD</h1>
    <OrganizationJsonLd
      type="Corporation"
      id="https://www.purpule-fox.io/#corporation"
      logo="https://www.example.com/photos/logo.jpg"
      legalName="Purple Fox LLC"
      name="Purple Fox"
      address={{
        streetAddress: '1600 Saratoga Ave',
        addressLocality: 'San Jose',
        addressRegion: 'CA',
        postalCode: '95129',
        addressCountry: 'US',
      }}
      contactPoint={[
        {
          telephone: '+1-401-555-1212',
          contactType: 'customer service',
          email: 'customerservice@email.com',
          areaServed: 'US',
          availableLanguage: ['English', 'Spanish', 'French'],
        },
        {
          telephone: '+1-877-746-0909',
          contactType: 'customer service',
          email: 'servicecustomer@email.com',
          contactOption: 'TollFree',
          availableLanguage: 'English',
        },
        {
          telephone: '+1-877-453-1304',
          contactType: 'technical support',
          contactOption: 'TollFree',
          areaServed: ['US', 'CA'],
          availableLanguage: ['English', 'French'],
        },
      ]}
      sameAs={['https://www.orange-fox.com']}
      url="https://www.purpule-fox.io/"
    />
  </>
);
```

**Data required properties 数据必需属性**

|Property 财产|Info 信息|
|---|---|
|`name 名字`|The name of the Organization.  <br>组织的名称。|
|`url 网址`|Url of the organization 组织的 URL|
|`contactPoint 联系点`||
|`contactPoint.telephone contactPoint.电话`|An internationalized version of the phone number, starting with the "+" symbol and country code  <br>电话号码的国际化版本，以“+”符号和国家/地区代码开头|
|`contactPoint.contactType`|Description of the purpose of the phone number i.e. `Technical Support`.  <br>电话号码的用途说明，即`技术支持`。|

**Data Recommended properties  
数据 Recommended properties**

|Property 财产|Info 信息|
|---|---|
|`logo 商标`|ImageObject or URL an associated logo to the Organization.  <br>ImageObject 或 URL 与组织的关联徽标。|
|`type 类型`|Organization type, check [here](https://schema.org/Organization#subtypes)  <br>组织类型，[请在此处](https://schema.org/Organization#subtypes)查看|
|`legalName 法律名称`|The official name of the organization, e.g. the registered company name.  <br>组织的正式名称，例如注册公司名称。|
|`sameAs`|URL of a reference Web page that unambiguously indicates the item's identity.  <br>明确指示项目标识的引用网页的 URL。|
|`address 地址`|Address of the specific business location  <br>具体营业地点的地址|
|`address.addressCountry address.addressCountry 地址`|The 2-letter ISO 3166-1 alpha-2 country code  <br>由 2 个字母组成的 ISO 3166-1 alpha-2 国家/地区代码|
|`address.addressLocality address.addressLocality 地址`|City 城市|
|`address.addressRegion address.addressRegion 地址区域`|State or province, if applicable.  <br>州或省（如果适用）。|
|`address.postalCode 地址.postalCode`|Postal or zip code. 邮政编码。|
|`address.streetAddress address.street地址`|Street number, street name, and unit number.  <br>街道号码、街道名称和单元号。|
|`contactPoint.areaServed contactPoint.area服务`|`String` or `Array` of geographical regions served by the business. Example `"US"` or `["US", "CA", "MX"]`  <br>企业服务的地理区域的`字符串`或`数组`。示例 `“US”` 或 `[“US”， “CA”， “MX”]`|
|`contactPoint.availableLanguage`|Details about the language spoken. Example `"English"` or `["English", "French"]`  <br>有关所说语言的详细信息。示例 `“English”` 或 `[“English”， “French”]`|
|`contactPoint.email`|Email asscosiated with the business`  <br>与企业关联的电子邮件|

**Other** | `useAppDir` | This should be set to true if using the new app directory. Not required if outside of the app directory. |  
**其他** |`useAppDir` |如果使用新的 app 目录，则应将其设置为 true。如果位于 app 目录之外，则不需要。|

For reference and more info check [Docs](https://schema.org/Organization)  
有关参考和更多信息，请查看 [文档](https://schema.org/Organization)

### Brand 品牌

[](https://github.com/garmeeh/next-seo?tab=readme-ov-file#brand)

```js
import React from 'react';
import { BrandJsonLd } from 'next-seo';

export default () => (
  <>
    <h1>Brand JSON-LD</h1>
    <BrandJsonLd
      slogan="What does the fox say?"
      id="https://www.purpule-fox.io/#corporation"
      logo="https://www.example.com/photos/logo.jpg"
      aggregateRating={{
        ratingValue: '5',
        ratingCount: '18',
      }}
    />
  </>
);
```

**Data required properties 数据必需属性**

|Property 财产|Info 信息|
|---|---|
|`id 身份证`|'URL to main entity of page'  <br>“指向页面主实体的 URL”|

**Data Recommended properties  
数据 Recommended properties**

|Property 财产|Info 信息|
|---|---|
|`logo 商标`|ImageObject or URL an associated logo to the Organization.  <br>ImageObject 或 URL 与组织的关联徽标。|
|`slogan 口号`|A slogan or motto associated with the item.  <br>与项目关联的标语或座右铭。|
|`aggregateRating.ratingValue`|The rating for the content.(Check the [reference](https://schema.org/ratingValue)  <br>内容的评级。（查看[参考资料](https://schema.org/ratingValue)|
|`aggregateRating.ratingCount`|The count of total number of ratings.  <br>评分总数的计数。|
|`aggregateRating.reviewCount`|The count of total number of reviews.  <br>评论总数的计数。|
|`aggregateRating.bestRatingaggregateRating.bestRating（聚合评分.最佳评分）`|The highest value allowed in this rating system. If bestRating is omitted, 5 is assumed.  <br>此评级系统中允许的最高值。如果省略 bestRating，则假定为 5。|
|`aggregateRating.worstRatingaggregateRating.worstRating的评级`|The lowest value allowed in this rating system. If worstRating is omitted, 1 is assumed.  <br>此评级系统中允许的最低值。如果省略 worstRating，则假定为 1。|

**Other** | `useAppDir` | This should be set to true if using the new app directory. Not required if outside of the app directory. |  
**其他** |`useAppDir` |如果使用新的 app 目录，则应将其设置为 true。如果位于 app 目录之外，则不需要。|

For reference and more info check [Docs](https://schema.org/Brand)  
有关参考和更多信息，请查看 [文档](https://schema.org/Brand)

### WebPage 网页

[](https://github.com/garmeeh/next-seo?tab=readme-ov-file#webpage)

```js
import React from 'react';
import { WebPageJsonLd } from 'next-seo';

export default () => (
  <>
    <h1>WebPage JSON-LD</h1>
    <WebPageJsonLd
      description="What does the fox say?"
      id="https://www.purpule-fox.io/#corporation"
      lastReviewed="2021-05-26T05:59:02.085Z"
      reviewedBy={{
        type: 'Person',
        name: 'Garmeeh',
      }}
    />
  </>
);
```

**Data required properties 数据必需属性**

|Property 财产|Info 信息|
|---|---|
|`id 身份证`|'URL to main entity of page'  <br>“指向页面主实体的 URL”|

**Data Recommended properties  
数据 Recommended properties**

|Property 财产|Info 信息|
|---|---|
|`description 描述`|ImageObject or URL an associated logo to the Organization.  <br>ImageObject 或 URL 与组织的关联徽标。|
|`lastReviewed 上次评论`|Date on which the content on this web page was last reviewed for accuracy and/or completeness.  <br>上次审核本网页上内容的准确性和/或完整性的日期。|
|`reviewedBy.type`|People or organizations that will review the content of the web page.  <br>将审阅网页内容的人员或组织。|
|`reviewedBy.name`|Name of the entity that have reviewed the content on this web page for accuracy and/or completeness.  <br>审查此网页上内容的准确性和/或完整性的实体的名称。|

**Other** | `useAppDir` | This should be set to true if using the new app directory. Not required if outside of the app directory. |  
**其他** |`useAppDir` |如果使用新的 app 目录，则应将其设置为 true。如果位于 app 目录之外，则不需要。|

For reference and more info check [Docs](https://schema.org/WebPage)  
有关参考和更多信息，请查看 [文档](https://schema.org/WebPage)

### Image Metadata 图像元数据

[](https://github.com/garmeeh/next-seo?tab=readme-ov-file#image-metadata)

```js
import React from 'react';
import { ImageJsonLd } from 'next-seo';

function Image() {
  return (
    <>
      <h1>Image</h1>
      <ImageJsonLd
        images={[
          {
            contentUrl: 'http://www.example.com/images/image.png',
            creator: {
              '@type': 'Person',
              name: 'Jane Doe',
            },
            creditText: 'Jane Doe',
            copyrightNotice: '© Jane Doe',
            license: 'http://www.example.com/license',
            acquireLicensePage: 'http://www.example.com/acquire-license',
          },
        ]}
      />
    </>
  );
}

export default Image;
```

**Data Recommended properties  
数据 Recommended properties**

|Property 财产|Info 信息|
|---|---|
|`contentUrl 内容网址`|A URL to the actual image content. Google uses contentUrl to determine which image the photo metadata applies to.  <br>指向实际图像内容的 URL。Google 使用 contentUrl 来确定照片元数据适用于哪张图片。|
|`creator.name`|The name of the creator.  <br>创建者的名称。|
|`creditText 信用文本`|The name of person and/or organization that is credited for the image when it's published.  <br>发布图像时为图像提供信用的人员和/或组织的名称。|
|`copyrightNotice 版权声明`|The copyright notice for claiming the intellectual property for this photograph. This identifies the current owner of the copyright for the photograph.  <br>声明此照片的知识产权的版权声明。这将标识照片版权的当前所有者。|
|`license 许可证`|A URL to a page that describes the license governing an image's use. For example, it could be the terms and conditions that you have on your website.  <br>指向描述管理映像使用的许可证的页面的 URL。例如，它可能是您网站上的条款和条件。|
|`acquireLicensePage`|A URL to a page where the user can find information on how to license that image.  <br>指向某个页面的 URL，用户可以在其中找到有关如何许可该图像的信息。|

**Other** | `useAppDir` | This should be set to true if using the new app directory. Not required if outside of the app directory. |  
**其他** |`useAppDir` |如果使用新的 app 目录，则应将其设置为 true。如果位于 app 目录之外，则不需要。|

For reference and more info check [Google Docs](https://developers.google.com/search/docs/appearance/structured-data/image-license-metadata)  
有关参考和更多信息，请查看 [Google 文档](https://developers.google.com/search/docs/appearance/structured-data/image-license-metadata)

## Contributors 贡献

[](https://github.com/garmeeh/next-seo?tab=readme-ov-file#contributors)

[Contributing Guide 贡献指南](https://github.com/garmeeh/next-seo/blob/master/CONTRIBUTING.md)

A massive thank you to [everyone who contributes](https://github.com/garmeeh/next-seo/graphs/contributors) to this project 👏  
衷心感谢所有为本项目👏[做出贡献的人](https://github.com/garmeeh/next-seo/graphs/contributors)

## About

Next SEO is a plug in that makes managing your SEO easier in Next.js projects.  
Next SEO 是一个插件，可让您更轻松地在 Next.js 项目中管理您的 SEO。

### Topics

[react](https://github.com/topics/react "Topic: react") [typescript](https://github.com/topics/typescript "Topic: typescript") [nextjs](https://github.com/topics/nextjs "Topic: nextjs") [seo](https://github.com/topics/seo "Topic: seo")[json-ld](https://github.com/topics/json-ld "Topic: json-ld") [hacktoberfest](https://github.com/topics/hacktoberfest "Topic: hacktoberfest")[hacktoberfest-accepted](https://github.com/topics/hacktoberfest-accepted "Topic: hacktoberfest-accepted")

### Resources

 [Readme](https://github.com/garmeeh/next-seo?tab=readme-ov-file#readme-ov-file)

### License

 [MIT license](https://github.com/garmeeh/next-seo?tab=readme-ov-file#MIT-1-ov-file)

 [Activity](https://github.com/garmeeh/next-seo/activity)

### Stars

 [**7.7k** stars](https://github.com/garmeeh/next-seo/stargazers)

### Watchers

 [**30** watching](https://github.com/garmeeh/next-seo/watchers)

### Forks

 [**400** forks](https://github.com/garmeeh/next-seo/forks)

[Report repository](https://github.com/contact/report-content?content_url=https%3A%2F%2Fgithub.com%2Fgarmeeh%2Fnext-seo&report=garmeeh+%28user%29)

## [Releases 83](https://github.com/garmeeh/next-seo/releases)

[

v6.6.0Latest

on Sep 2



](https://github.com/garmeeh/next-seo/releases/tag/v6.6.0)

[+ 82 releases](https://github.com/garmeeh/next-seo/releases)

## Sponsor this project

- ![patreon](https://github.githubassets.com/assets/patreon-96b15b9db4b9.svg)[patreon.com/**garmeeh**](https://patreon.com/garmeeh)

## [Packages](https://github.com/users/garmeeh/packages?repo_name=next-seo)

No packages published   

## [Used by 66.4k](https://github.com/garmeeh/next-seo/network/dependents)

[

- ![@DopamineDriven](https://avatars.githubusercontent.com/u/46355797?s=64&v=4)
- ![@ryanhij](https://avatars.githubusercontent.com/u/16454210?s=64&v=4)
- ![@arberiii](https://avatars.githubusercontent.com/u/8199285?s=64&v=4)
- ![@ChenHaoTech](https://avatars.githubusercontent.com/u/32390273?s=64&v=4)
- ![@CHNsPart](https://avatars.githubusercontent.com/u/58574102?s=64&v=4)
- ![@xdevx32](https://avatars.githubusercontent.com/u/8018765?s=64&v=4)
- ![@xdevx32](https://avatars.githubusercontent.com/u/8018765?s=64&v=4)
- ![@ytang07](https://avatars.githubusercontent.com/u/17556662?s=64&v=4)

+ 66,416](https://github.com/garmeeh/next-seo/network/dependents)

## [Contributors113](https://github.com/garmeeh/next-seo/graphs/contributors)

- [![@dependabot-preview[bot]](https://avatars.githubusercontent.com/in/2141?s=64&v=4)](https://github.com/apps/dependabot-preview)
- [![@garmeeh](https://avatars.githubusercontent.com/u/13333582?s=64&v=4)](https://github.com/garmeeh)
- [![@allcontributors[bot]](https://avatars.githubusercontent.com/in/23186?s=64&v=4)](https://github.com/apps/allcontributors)
- [![@dependabot[bot]](https://avatars.githubusercontent.com/in/29110?s=64&v=4)](https://github.com/apps/dependabot)
- [![@Myoxocephalus](https://avatars.githubusercontent.com/u/2316544?s=64&v=4)](https://github.com/Myoxocephalus)
- [![@econdie](https://avatars.githubusercontent.com/u/15269328?s=64&v=4)](https://github.com/econdie)
- [![@erickeno](https://avatars.githubusercontent.com/u/3820632?s=64&v=4)](https://github.com/erickeno)
- [![@edoardolincetto](https://avatars.githubusercontent.com/u/19685709?s=64&v=4)](https://github.com/edoardolincetto)
- [![@ykzts](https://avatars.githubusercontent.com/u/12539?s=64&v=4)](https://github.com/ykzts)
- [![@nyedidikeke](https://avatars.githubusercontent.com/u/19228770?s=64&v=4)](https://github.com/nyedidikeke)
- [![@timReynolds](https://avatars.githubusercontent.com/u/168870?s=64&v=4)](https://github.com/timReynolds)
- [![@valse](https://avatars.githubusercontent.com/u/1492995?s=64&v=4)](https://github.com/valse)
- [![@hsynlms](https://avatars.githubusercontent.com/u/1780171?s=64&v=4)](https://github.com/hsynlms)
- [![@nandenjin](https://avatars.githubusercontent.com/u/7803255?s=64&v=4)](https://github.com/nandenjin)

[+ 99 contributors](https://github.com/garmeeh/next-seo/graphs/contributors)

## Languages

- [JavaScript52.3%](https://github.com/garmeeh/next-seo/search?l=javascript) 
- [TypeScript47.7%](https://github.com/garmeeh/next-seo/search?l=typescript)

## Footer

[](https://github.com/ "GitHub")© 2024 GitHub, Inc.

### Footer navigation

- [Terms](https://docs.github.com/site-policy/github-terms/github-terms-of-service)
- [Privacy](https://docs.github.com/site-policy/privacy-policies/github-privacy-statement)
- [Security](https://github.com/security)
- [Status](https://www.githubstatus.com/)
- [Docs](https://docs.github.com/)
- [Contact](https://support.github.com/?tags=dotcom-footer)
- Manage cookies
- Do not share my personal information

Copied!