---
title: Nextjs 中使用 SEO
---
![Manage Seo Next Js Next Seo](https://blog.logrocket.com/wp-content/uploads/2023/01/manage-seo-next-js-next-seo.png)

[SEO](https://blog.logrocket.com/how-next-js-can-help-improve-seo/) 是营销的一个关键方面，可帮助网站在搜索引擎结果页面 （SERP） 中更有效地排名。在 SERP 中排名越高，自然流量就越大，商机也就越大，所以你就会明白为什么牢记它很重要！

因此，作为开发人员，确保我们项目的网站 SEO 得到正确管理而不错过任何属性至关重要。

在本文中，我们将使用 Next SEO 来管理我们 Next.js 应用程序中的搜索引擎优化。

# 下一页 SEO 和 Next.js

[Next.js](https://blog.logrocket.com/tag/nextjs/) 具有静态站点生成 （SSG） 支持，可提供比客户端渲染更好的 SEO 功能。它还具有一个内置的 head 组件来管理 SEO 元信息，如标题、描述、规范和 Open Graph 标签。

当网站上的页面更多时，也有更多的元标记需要考虑。随着网站的发展，管理这些可能会成为一个令人生畏的过程。

为了简化这一点，我们可以使用一个名为 [next-seo](https://github.com/garmeeh/next-seo) 的包。接下来，SEO 使在您的 Next.js 项目中管理 SEO 变得更加容易。
 
通过使用 Next SEO，我们可以将 SEO 属性作为对象传递，并且包会自动将属性添加到页面头中。

您可以单独将其添加到每个页面，也可以使用 `DefaultSeo` 组件将其覆盖到其他页面上。

让我们开始吧，看看它的实际效果。

# 快速设置

首先，使用以下命令将 next-seo 包安装到 Next.js 项目中：

```bash
yarn add next-seo
```
# 将 Next SEO 添加到页面

让我们将 next-seo 包导入到具有 SEO 属性的`page`组件中。为此，请将以下代码添加到 `home` 组件中：
```html
//home.js
import { NextSeo } from 'next-seo';

const Home = () => (
    <>
        <NextSeo
            title="Home Page Title"
            description="Home page description of the page"
        />
        <p>Simple Usage</p>
    </>
);
export default Home;
```

这将呈现一个 `<head>` 标签，其中包含页面的标题和描述。您可以通过检查来验证它，如下所示：

![Inspecting Head Tag](https://blog.logrocket.com/wp-content/uploads/2023/01/inspecting-head-tag.png)


您可以看到，默认情况下，该标签包括 `og：title` 和 `og：description`，使用 title 和 description 属性。

这是一个简单的配置;让我们探索 Next SEO 中可用的其他选项。

# 默认 SEO

要将默认属性添加到我们的所有页面，我们可以使用 `DefaultSeo` 组件，而不是手动将属性单独添加到每个页面。如果需要，我们还可以覆盖页面上的任何属性。

将 `DefaultSeo` 组件添加到 `_app.js`并添加以下代码：

```html
//_app.js
import '../styles/globals.css'
import {DefaultSeo} from 'next-seo';

function MyApp({Component, pageProps}) {
    return (
        <>
            <DefaultSeo
                title="Next SEO Example"
                description="Next SEO is a plug in that makes managing your SEO easier in Next.js projects."
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
        </>
    )
}

export default MyApp
```

现在，添加到默认组件的 SEO 属性将呈现在所有页面上。您可以通过再次检查页面来验证这一点，如下所示：

![Verify Seo Properties Default Component](https://blog.logrocket.com/wp-content/uploads/2023/01/verify-seo-properties-default-component.png)

## 覆盖默认属性

现在，让我们覆盖**博客**页面上的默认 SEO 属性，因为每个博客都有一个单独的标题和描述。将以下代码添加到页面中：

```html
//blog.js
import {NextSeo} from 'next-seo';

const Blog = () => (
    <>
        <NextSeo
            title="Manage SEO in NextJS with Next SEO"
            description="Next SEO packages simplifies the SEO management in Next Apps with less configurations"
            canonical="www.example.com/next-seo-blog"
            openGraph={{
                type: 'article',
                article: {
                    publishedTime: '2022-06-21T23:04:13Z',
                    modifiedTime: '2022-01-21T18:04:43Z',
                    authors: [
                        'https://www.example.com/authors/@firstnameA-lastnameA',
                        'https://www.example.com/authors/@firstnameB-lastnameB',
                    ],
                    tags: ['Tag A', 'Tag B', 'Tag C'],
                },
                url: 'www.example.com/next-seo-blog',
                images: {
                    url: 'https://www.test.ie/images/cover.jpg',
                    width: 850,
                    height: 650,
                    alt: 'Photo of text',
                },
                site_name: 'Next Blog'
            }}
        />
        <p>Manage SEO in NextJS with Next SEO - Blog</p>
    </>
);

export default Blog;
```

在这里，我们覆盖了 `title`、`description` 和其他属性。您还可以看到一些与我们的博客文章特别相关的新属性：

- `publishedTime`：博客发布日期
- `modifiedTime`：博客更新日期
- `tags`：与博客文章关联的标签
- `authors` ： 博客的作者

您可以通过检查页面来验证这些内容：

![Verify Default Properties Override](https://blog.logrocket.com/wp-content/uploads/2023/01/verify-default-properties-override.png)

如您所见，有一些与 Twitter 卡片相关的元信息，但我们没有在博客页面中包含这些信息——它是由 Next SEO 添加的，我们之前使用 `DefaultSeo` 组件添加了这些信息。

---

[

![](https://blog.logrocket.com/wp-content/uploads/2022/11/Screen-Shot-2022-09-22-at-12.50.47-PM.png)


通过此示例，您可以看到它如何开箱即用地支持与博客相关的 SEO 属性以方便使用。

# Open Graph support Open Graph 支持

Open Graph 协议控制在社交媒体上分享链接时应显示的内容。在网页中使用 Open Graph 标签可以使它们成为社交图谱中的丰富对象。

例如，OG 协议允许您控制在社交媒体平台上分享链接时显示的标题、图像和描述。如果您在没有 OG 标签的情况下分享，社交媒体平台将随机选择标题、图像和描述。

Twitter、LinkedIn 和 Facebook 等平台可以识别 Open Graph 标签——但是，Twitter 也有称为 Twitter 卡片的元标签，但在不需要使用 Twitter 卡片标签时将使用 OG 标签。

Next SEO 支持以下 OG 属性：

1. Audio 音频
2. Video 视频
3. Article 品
4. Profile 轮廓
5. Book 书

# Audio 音频示例

以下配置启用具有多个音频文件的音频 Open Graph 支持：

```html
//Podcast.js

import { NextSeo } from 'next-seo';
const Podcast = () => (
  <>
    <NextSeo
      title="Podcast Page Title"
      description="Next SEO PodCast"
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
export default Podcast;
```

您可以查看其他 OG 类型的其他[示例](https://github.com/garmeeh/next-seo#open-graph-examples)以了解更多信息。

# 结构化数据支持

结构化数据是一种标准化格式，用于提供有关网页的信息并对网页内容进行分类。这有助于搜索引擎了解网页并向最终用户显示最相关的标题、描述、图像和其他信息。

Next SEO 还支持结构化数据，只需进行有限的配置，支持多种 JSON-LD 类型，如`文章`、`博客`、`常见问题解答`和`课程`。

让我们通过一个例子来了解一下它的实际效果。

`ArticleJsonLd` 组件用于将结构化数据添加到页面。添加以下代码以将结构化数据添加到我们的博客中：

```html
//blog.js
import {ArticleJsonLd, NextSeo} from 'next-seo';

const Blog = () => (
    <>
        <NextSeo
            title="Manage SEO in NextJS with Next SEO"
            description="Next SEO packages simplifies the SEO management in Next Apps with less configurations"
            canonical="www.example.com/next-seo-blog"
            openGraph={{
                type: 'article',
                article: {
                    publishedTime: '2022-06-21T23:04:13Z',
                    modifiedTime: '2022-01-21T18:04:43Z',
                    authors: [
                        'https://www.example.com/authors/@firstnameA-lastnameA',
                        'https://www.example.com/authors/@firstnameB-lastnameB',
                    ],
                    tags: ['Tag A', 'Tag B', 'Tag C'],
                },
                url: 'www.example.com/next-seo-blog',
                images: {
                    url: 'https://www.test.ie/images/cover.jpg',
                    width: 850,
                    height: 650,
                    alt: 'Photo of text',
                },
                site_name: 'Next Blog'
            }}
        />
        <ArticleJsonLd
            type="BlogPosting"
            url="https://example.com/blog"
            title="Manage SEO in NextJS with Next SEO"
            images={[
                'https://example.com/photos/1x1/photo.jpg',
                'https://example.com/photos/4x3/photo.jpg',
                'https://example.com/photos/16x9/photo.jpg',
            ]}
            datePublished="2022-06-21T23:04:13Z"
            dateModified="2022-06-21T23:04:13Z"
            authorName="Author Name"
            description="Next SEO packages simplifies the SEO management in Next Apps with less configurations"
        />
        <p>Manage SEO in NextJS with Next SEO - Blog</p>
    </>
);

export default Blog;
```

我们现在已向 `JsonLd` 添加了一些 SEO 属性，它们将如下所示：

![Add Seo Properties To Json](https://blog.logrocket.com/wp-content/uploads/2023/01/add-seo-properties-to-json.png)

JSON 数据在 `<script>` 标记中呈现。您可以检查所有可用的 [JSON-LD 类型](https://github.com/garmeeh/next-seo#json-ld)以了解更多信息。

# Next SEO 选项

以下是 `NextSeo` 组件的属性，我们可以使用它来处理不同的 meta 标记属性。一些最常用的属性是：

- `defaultTitle`：如果页面上没有设置标题，则将使用此字符串而不是空标题
- `noindex`：设置是否应将页面编入索引的选项
- `nofollow`：用于设置是否应关注页面的选项
- `canonical`：设置页面的规范 URL
- `facebook.appId`：将 Facebook 应用 ID 添加到您的页面以接收 Facebook Insights 数据
- `additionalMetaTags`：其他元标记，如 `title` 和 `content`
- `additionalLinkTags`：其他元链接，如 favicons

# Next.js 13 应用程序目录支持
  
Next.js 13 为 `app` 目录引入了一个 beta 功能，用于与 `pages` 目录一起路由。

由于此更改，next-seo 的用法和配置也发生了变化，因为新的 `app` 目录为现有流程带来了以下更改：

1. Next.js 不再删除 head 中的重复标签，因此我们不能使用 `DefaultSeo` 组件进行全局 SEO
2. `app` 目录包括 `head.JS`文件以包含 `<head>` 标签，但它不支持同步内联脚本。因此，无法在 head 中添加 JSON-LD 组件`。js`，所以需要把它添加到 `page 中。js`，它添加到文档的 `<body/>` 中
3. Next.js 默认不会添加以下 meta 标记，因此我们需要在根布局中手动添加它

# 常见 meta 标记

根据新的`应用程序`目录，`DefaultSeo` 元标记不能在其他页面上覆盖。

因此，我们需要识别常用标记并将它们放置在根布局 （`/app/layout.js`），如下所示：

```html
// app/layout.js
import { NextSeo } from 'next-seo';

export default function RootLayout({ children }) {
  return (
    <html>
      <head>
        {/* Used to be added by default, now we need to add manually */}
        <meta charSet="utf-8" />
        <meta name="viewport" content="width=device-width" />
        {/* 
          Anything we add in layout will appear on EVERY PAGE. At present it can not be overridden lower down the tree.
          This can be useful for things like favicons, or other meta tags that are the same on every page.
        */}
        <NextSeo
          useAppDir={true}
          facebook={{ appId: '1234567890' }}
          themeColor="#73fa97"
          titleTemplate="%s | Next SEO"
        />
      </head>
      <body>{children}</body>
    </html>
  );
}
```

> **注意**，新属性 `useAppDir` 强制 next-seo 使用兼容版本的 `app` 目录。

以下是上述示例中渲染的 meta 标记：

![Rendered Meta Tags](https://blog.logrocket.com/wp-content/uploads/2023/01/rendered-meta-tags.png)

## 默认 meta 配置

要使用常见的元标记，如 `og`、`image`、`title` 和 `description`，请先添加 `next-seo-config。JS`文件并将其导入到所需的页面中。下面是我意思的一个例子：


```js
// next-seo-config.js
export const NEXT_SEO_DEFAULT = {
  title: 'Page Title',
  description: 'Page Description',
  openGraph: {
    type: 'website',
    locale: 'en_IE',
    url: 'https://www.url.ie/a',
    title: 'OG Title',
    description: 'OG Decription',
    siteName: 'Example',
  },
};
```

现在，导入 `next-seo-config。JS`文件放入 `head 中。js`，如下所示：
```js
// app/head.js
import { NextSeo } from 'next-seo';

import { NEXT_SEO_DEFAULT } from './next-seo-config'; // your path will vary

export default async function Head() {
  return <NextSeo {...NEXT_SEO_DEFAULT} useAppDir={true} />;
}
```

这是我们对上述示例的输出：

![Output Of Example Properties](https://blog.logrocket.com/wp-content/uploads/2023/01/output-of-example-properties.png)

## 覆盖默认 SEO

如有必要，您可以覆盖其他页面上的默认 `next-seo-config` 元标记 — 请查看以下示例以了解它是如何完成的：

```js
// app/profile/head.js
import { NextSeo } from 'next-seo';

import { NEXT_SEO_DEFAULT } from '../next-seo-config'; // your path may vary

export default async function Head() {
  const updateMeta = {
    ...NEXT_SEO_DEFAULT,
    title: 'Profile',
    description: 'User Profile',
  };
  return <NextSeo {...updateMeta} useAppDir={true} />;
}
```

在这里，我们将默认 SEO 元标记的标题和描述更新为我们自己的规范。

下面是上述示例的输出：

![Output Default Seo Updated Title And Description](https://blog.logrocket.com/wp-content/uploads/2023/01/output-default-seo-updated-title-and-description.png)

# 添加 JSON-LD 组件

正如我们之前看到的，新的 `app` directory `head.JS`不支持内联 `<script>`。我们可以将 JSON-LD 添加到`页面。JS`文件，它将 JSON-LD 结构化数据添加到文档正文中。

查看以下示例：

```js
// app/blog/page.js
import { ArticleJsonLd } from 'next-seo';

const Article = () => (
  <>
    <h1>Article</h1>
    <p>Inspect page for output.</p>
    <ArticleJsonLd
      useAppDir={true}
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

export default Article;
```

下面是上述示例的输出：

![Final Output For Default Seo Export](https://blog.logrocket.com/wp-content/uploads/2023/01/final-output-for-default-seo-export.png)

## 结论

SEO 对于需要有机发现的网页至关重要。要获得较高的页面排名，需要对网站进行组织，以便搜索引擎可以轻松抓取它们。

Next SEO 使 Next.js 项目中的搜索引擎优化管理非常简单且易于实施——它帮助开发人员有效地添加 SEO 属性，而不会错过任何重要的元标记，同时避免重复的发生。

你可以在官方[文档](https://github.com/garmeeh/next-seo)中找到其他属性和示例。

在下面的评论中让我知道您自己使用 Next SEO 的经验，感谢您的阅读！