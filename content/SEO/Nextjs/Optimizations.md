---
title: 优化
original: https://nextjs.org/docs/app/building-your-application/optimizing/metadata#usage
---
# 元数据

Next.js 有一个 Metadata API，可用于定义应用程序元数据（例如 HTML `head` 元素中的 `Meta` 和 `link` 标签），以改善 SEO 和 Web 共享性。

有两种方法可以将元数据添加到应用程序中：

- **基于配置的元数据**：在`layout.js`或`page.js`文件中导出[静态`元数据`对象](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#metadata-object)或动态[`generateMetadata`函数](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#generatemetadata-function)。
- **基于文件的元数据**：将静态或动态生成的特殊文件添加到路由段。

使用这两个选项，Next.js 将自动为您的页面生成相关的 `<head>` 元素。您还可以使用[`ImageResponse`](https://nextjs.org/docs/app/api-reference/functions/image-response)构造函数创建动态OG图像。

## 静态元数据

若要定义静态元数据，请从`layout.js`或静态`page.js`文件导出[`Metadata`对象](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#metadata-object)。

```ts
import type { Metadata } from 'next'
 
export const metadata: Metadata = {
  title: '...',
  description: '...',
}
 
export default function Page() {}
```

有关所有可用选项，请参阅[API参考](https://nextjs.org/docs/app/api-reference/functions/generate-metadata)。

## 动态元数据

您可以使用`generateMetadata`函数来`获取`需要动态值的元数据。

```ts
import type { Metadata, ResolvingMetadata } from 'next'
 
type Props = {
  params: Promise<{ id: string }>
  searchParams: Promise<{ [key: string]: string | string[] | undefined }>
}
 
export async function generateMetadata(
  { params, searchParams }: Props,
  parent: ResolvingMetadata
): Promise<Metadata> {
  // read route params
  const id = (await params).id
 
  // fetch data
  const product = await fetch(`https://.../${id}`).then((res) => res.json())
 
  // optionally access and extend (rather than replace) parent metadata
  const previousImages = (await parent).openGraph?.images || []
 
  return {
    title: product.title,
    openGraph: {
      images: ['/some-specific-page-image.jpg', ...previousImages],
    },
  }
}
 
export default function Page({ params, searchParams }: Props) {}
```

有关所有可用参数，请参阅[API参考](https://nextjs.org/docs/app/api-reference/functions/generate-metadata)。

> **很高兴知道**：
> 
> - 通过`generateMetadata生成`的静态和动态元数据**仅在服务器组件中**受支持。
> - 对于同一数据`，fetch`请求会自动`在generateMetadata`、`generateStaticParams`、Layouts、Pages和Server Components之间[进行存储](https://nextjs.org/docs/app/building-your-application/caching#request-memoization)。如果`fetch`不可用[`，`可以使用](https://nextjs.org/docs/app/building-your-application/caching#react-cache-function)React缓存。
> - Next.js 将等待 `generateMetadata` 中的数据获取完成，然后将 UI 流传输到客户端。这可保证[流式响应](https://nextjs.org/docs/app/building-your-application/routing/loading-ui-and-streaming)的第一部分包含`<head>`标记。

## 文件元数据

这些特殊文件可用于元数据：

- [favicon.ico、apple-icon.jpg和icon.jpg](https://nextjs.org/docs/app/api-reference/file-conventions/metadata/app-icons)
- [opengraph-image.jpg和twitter-image.jpg](https://nextjs.org/docs/app/api-reference/file-conventions/metadata/opengraph-image)
- [robots.txt](https://nextjs.org/docs/app/api-reference/file-conventions/metadata/robots)
- [sitemap.xml](https://nextjs.org/docs/app/api-reference/file-conventions/metadata/sitemap)

您可以将这些文件用于静态元数据，也可以使用代码以编程方式生成这些文件。

有关实现和示例，请参见[元数据文件](https://nextjs.org/docs/app/api-reference/file-conventions/metadata)API参考和[动态图像生成](https://nextjs.org/docs/app/building-your-application/optimizing/metadata#dynamic-image-generation)。

## 行为

基于文件的元数据具有更高的优先级，并将覆盖任何基于XML的元数据。

### 默认字段

有两个默认`的Meta`标记，即使路由没有定义元数据，也会始终添加：

- [Meta charset标记](https://developer.mozilla.org/docs/Web/HTML/Element/meta#attr-charset)设置网站的字符编码。
- [Meta viewport标签](https://developer.mozilla.org/docs/Web/HTML/Viewport_meta_tag)设置网站的viewport宽度和比例，以适应不同的设备。

```html
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
```

> **好消息**：你可以覆盖默认的[`viewport`](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#viewport)Meta标签。

### 订购

元数据按顺序进行评估，从根段开始，向下到最接近最后一`个page.js`段的段。举例来说：

1. `app/layout.tsx`（根布局）
2. `app/blog/layout.tsx`（嵌套博客布局）
3. `app/blog/[slug]/page.tsx`（博客页面）

### 合并

按照[评估顺序](https://nextjs.org/docs/app/building-your-application/optimizing/metadata#ordering)，从同一路线中的多个路段导出的元数据对象将**浅**合并在一起，以形成路线的最终元数据输出。重复的键将根据它们的顺序进行**替换**。

这意味着具有嵌套字段的元数据，例如在前面的段中定义的[`openGraph`](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#opengraph)和[`robots，`](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#robots)将被最后一个段**覆盖**以定义它们。

#### 覆盖字段

`app/layout.js`

```js
export const metadata = {
  title: 'Acme',
  openGraph: {
    title: 'Acme',
    description: 'Acme is a...',
  },
}
```

`app/blog/page.js`

```js
export const metadata = {
  title: 'Blog',
  openGraph: {
    title: 'Blog',
  },
}
 
// Output:
// <title>Blog</title>
// <meta property="og:title" content="Blog" />
```


In the example above: 在上面的例子中：

- `app/layout.js`中的`title`被`app/blog/page.js`中的`title`**替换**。
- `app/layout.js`中的所有`openGraph`字段在`app/blog/page.js`中被**替换**，因为`app/blog/page.js`设置`了openGraph`元数据。注意`openGraph.description`的缺失。

如果你想在段之间共享一些嵌套字段，同时隐藏其他字段，你可以将它们拉到一个单独的变量中：

`app/shared-metadata.js`

```js
export const openGraphImage = { images: ['http://...'] }
```

`app/page.js`

```js
import { openGraphImage } from './shared-metadata'
 
export const metadata = {
  openGraph: {
    ...openGraphImage,
    title: 'Home',
  },
}
```

`app/about/page.js`

```js
import { openGraphImage } from '../shared-metadata'
 
export const metadata = {
  openGraph: {
    ...openGraphImage,
    title: 'About',
  },
}
```

在上面的示例中，OG镜像在`app/layout.js`和`app/about/page.js`之间共享，但标题不同。
#### 继承字段

`app/layout.js`

```js
export const metadata = {
  title: 'Acme',
  openGraph: {
    title: 'Acme',
    description: 'Acme is a...',
  },
}
```

`app/about/page.js`

```js
export const metadata = {
  title: 'About',
}
 
// Output:
// <title>About</title>
// <meta property="og:title" content="Acme" />
// <meta property="og:description" content="Acme is a..." />
```

**注意**

- `app/layout.js`中的`title`被`app/about/page.js`中的`title`**替换**。
- `app/layout.js`中的所有`openGraph`字段都在`app/about/page.js`中**继承**，因为`app/about/page.js`不设置`openGraph`元数据。

## 动态图像生成

`ImageResponse`构造函数允许您使用JSX和CSS生成动态图像。这对于创建社交媒体图像（如Open Graph图像、Twitter卡片等）非常有用。

要使用它，您可以从`next/og`导入`ImageResponse`：

`app/about/route.js`

```js
import { ImageResponse } from 'next/og'
 
export async function GET() {
  return new ImageResponse(
    (
      <div
        style={{
          fontSize: 128,
          background: 'white',
          width: '100%',
          height: '100%',
          display: 'flex',
          textAlign: 'center',
          alignItems: 'center',
          justifyContent: 'center',
        }}
      >
        Hello world!
      </div>
    ),
    {
      width: 1200,
      height: 600,
    }
  )
}
```

`ImageResponse`与其他Next.js API集成良好，包括[路由处理程序](https://nextjs.org/docs/app/building-your-application/routing/route-handlers)和基于文件的元数据。例如，您可以在`opengraph-image.tsx`文件中使用`ImageResponse`在构建时或在请求时动态生成Open Graph图像。

`ImageResponse`支持常见的CSS属性，包括flexbox和绝对定位，自定义字体，文本换行，居中和嵌套图像。[查看支持的CSS属性的完整列表](https://nextjs.org/docs/app/api-reference/functions/image-response)。

> **很高兴知道**：
> 
>     在[Vercel OG Playground](https://og-playground.vercel.app/)提供示例。
> - `ImageResponse` uses [@vercel/og](https://vercel.com/docs/concepts/functions/edge-functions/og-image-generation), [Satori](https://github.com/vercel/satori), and Resvg to convert HTML and CSS into PNG.  
>     `ImageResponse`使用[@vercel/og](https://vercel.com/docs/concepts/functions/edge-functions/og-image-generation)、[Satori](https://github.com/vercel/satori)和Resvg将HTML和CSS转换为PNG。
> - 仅支持Edge浏览器。默认的Node.js运行时将无法工作。
> - 仅支持flexbox和CSS属性的子集。高级布局（例如`显示：网格`）将不起作用。
> - 最大捆绑包大小为`500 KB`。捆绑包大小包括您的JSX、CSS、字体、图像和任何其他资产。如果超过了限制，请考虑减少任何资产的大小或在运行时进行抓取。
> - 仅支持`ttf`、`otf`和`woff`字体格式。为了最大化字体解析速度，`ttf` 或`otf` 比 `woff` 更受欢迎。

## JSON-LD

[JSON-LD](https://json-ld.org/)是一种结构化数据格式，搜索引擎可以使用它来理解您的内容。例如，您可以使用它来描述一个人、一个事件、一个组织、一部电影、一本书、一个食谱和许多其他类型的实体。

我们目前对JSON-LD的建议是将结构化数据呈现为`layout.js`或`page.js`组件中的`<script>`标记。举例来说：

`app/products/[id]/page.tsx`

```ts
export default async function Page({ params }) {
  const product = await getProduct(params.id)
 
  const jsonLd = {
    '@context': 'https://schema.org',
    '@type': 'Product',
    name: product.name,
    image: product.image,
    description: product.description,
  }
 
  return (
    <section>
      {/* Add JSON-LD to your page */}
      <script
        type="application/ld+json"
        dangerouslySetInnerHTML={{ __html: JSON.stringify(jsonLd) }}
      />
      {/* ... */}
    </section>
  )
}
```

您可以使用[Rich Results Test](https://search.google.com/test/rich-results)for Google 或通用的 [Schema Markup Validator](https://validator.schema.org/) 验证和测试结构化数据。

您可以使用社区包（如[`schema-dts）`](https://www.npmjs.com/package/schema-dts)使用TypeScript键入JSON-LD：

```js
import { Product, WithContext } from 'schema-dts'
 
const jsonLd: WithContext<Product> = {
  '@context': 'https://schema.org',
  '@type': 'Product',
  name: 'Next.js Sticker',
  image: 'https://nextjs.org/imgs/sticker.png',
  description: 'Dynamic at the speed of static.',
}
```
