---
title: 元数据
original: https://nextjs.org/docs/app/api-reference/functions/generate-metadata
---

This page covers all **Config-based Metadata** options with `generateMetadata` and the static metadata object.  
本页介绍了所有**基于配置的元数据**选项以及`generateMetadata`和静态元数据对象。

layout.tsx | page.tsx

TypeScript

JavaScriptTypeScript

```js
import type { Metadata } from 'next' // either Static metadataexport const metadata: Metadata = {  title: '...',} // or Dynamic metadataexport async function generateMetadata({ params }) {  return {    title: '...',  }}
```

> **Good to know**:  
> **很高兴知道**：
> 
> - The `metadata` object and `generateMetadata` function exports are **only supported in Server Components**.  
>     `元数据`对象和`generateMetadata`函数导出**仅在服务器组件中受支持**。
> - You cannot export both the `metadata` object and `generateMetadata` function from the same route segment.  
>     不能从同一个管段同时导出`元数据`对象和`generateMetadata`函数。
> - On the initial load, streaming is blocked until `generateMetadata` has fully resolved, including any content from `loading.js`.  
>     在初始加载时，流被阻止，直到`generateMetadata`完全解析，包括来自`loading.js的`任何内容。

## [The `metadata` object  
`元数据`对象](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#the-metadata-object)

To define static metadata, export a [`Metadata` object](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#metadata-fields) from a `layout.js` or `page.js` file.  
要定义静态元数据，请从`layout.js`或`page.js`文件导出[`Metadata`对象](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#metadata-fields)。

layout.tsx | page.tsx

TypeScript

JavaScriptTypeScript

```
import type { Metadata } from 'next' export const metadata: Metadata = {  title: '...',  description: '...',} export default function Page() {}
```

See the [Metadata Fields](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#metadata-fields) for a complete list of supported options.  
有关支持选项的完整列表，请参见[元数据字段](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#metadata-fields)。

## [`generateMetadata` function  
`generateMetadata`函数](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#generatemetadata-function)

Dynamic metadata depends on **dynamic information**, such as the current route parameters, external data, or `metadata` in parent segments, can be set by exporting a `generateMetadata` function that returns a [`Metadata` object](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#metadata-fields).  
动态元数据取决于**动态信息**，例如当前路径参数、外部数据或父段中`的元数据`，可以通过导出返回[`Metadata`对象](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#metadata-fields)的`generateMetadata`函数进行设置。

app/products/[id]/page.tsx

TypeScript

JavaScriptTypeScript

```
import type { Metadata, ResolvingMetadata } from 'next' type Props = {  params: Promise<{ id: string }>  searchParams: Promise<{ [key: string]: string | string[] | undefined }>} export async function generateMetadata(  { params, searchParams }: Props,  parent: ResolvingMetadata): Promise<Metadata> {  // read route params  const id = (await params).id   // fetch data  const product = await fetch(`https://.../${id}`).then((res) => res.json())   // optionally access and extend (rather than replace) parent metadata  const previousImages = (await parent).openGraph?.images || []   return {    title: product.title,    openGraph: {      images: ['/some-specific-page-image.jpg', ...previousImages],    },  }} export default function Page({ params, searchParams }: Props) {}
```

### [Parameters 参数](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#parameters)

`generateMetadata` function accepts the following parameters:  
`generateMetadata`函数接受以下参数：

- `props` - An object containing the parameters of the current route:  
    `props`-包含当前路由参数的对象：
    
    - `params` - An object containing the [dynamic route parameters](https://nextjs.org/docs/app/building-your-application/routing/dynamic-routes) object from the root segment down to the segment `generateMetadata` is called from. Examples:  
        `params`- 从中调用包含从根段到段`generateMetadata`的[动态路由参数](https://nextjs.org/docs/app/building-your-application/routing/dynamic-routes)对象的对象。举例说明：
        
        |Route 路线|URL|`params`|
        |---|---|---|
        |`app/shop/[slug]/page.js`|`/shop/1`|`{ slug: '1' } { slug：'1' }`|
        |`app/shop/[tag]/[item]/page.js`|`/shop/1/2`|`{ tag: '1', item: '2' }   {标签：'1'，项目：'2' }`|
        |`app/shop/[...slug]/page.js   app/shop/[. slug]/page.js`|`/shop/1/2`|`{ slug: ['1', '2'] }   { slug：'1'，'2'] }`|
        
    - `searchParams` - An object containing the current URL's [search params](https://developer.mozilla.org/docs/Learn/Common_questions/What_is_a_URL#parameters). Examples:  
        `searchParams`-包含当前URL的[搜索参数](https://developer.mozilla.org/docs/Learn/Common_questions/What_is_a_URL#parameters)的对象。举例说明：
        
        |URL|`searchParams`|
        |---|---|
        |`/shop?a=1 /商店？a=1`|`{ a: '1' } { a：'1' }`|
        |`/shop?a=1&b=2 /商店？a=1&b=2`|`{ a: '1', b: '2' }   { a：“1”，B：“2”}`|
        |`/shop?a=1&a=2 /商店？a=1&a=2`|`{ a: ['1', '2'] }   { a：'1'，'2'] }`|
        
- `parent` - A promise of the resolved metadata from parent route segments.  
    `parent`-来自父路由段的已解析元数据的承诺。
    

### [Returns 返回](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#returns)

`generateMetadata` should return a [`Metadata` object](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#metadata-fields) containing one or more metadata fields.  
`generateMetadata`应该返回一个包含一个或多个元数据字段[`的Metadata`对象](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#metadata-fields)。

> **Good to know**:  
> **很高兴知道**：
> 
> - If metadata doesn't depend on runtime information, it should be defined using the static [`metadata` object](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#the-metadata-object) rather than `generateMetadata`.  
>     如果元数据不依赖于运行时信息，则应该使用静态[`元数据`对象](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#the-metadata-object)而不是`generateMetadata来`定义它。
> - `fetch` requests are automatically [memoized](https://nextjs.org/docs/app/building-your-application/caching#request-memoization) for the same data across `generateMetadata`, `generateStaticParams`, Layouts, Pages, and Server Components. React [`cache` can be used](https://nextjs.org/docs/app/building-your-application/caching#react-cache-function)if `fetch` is unavailable.  
>     对于同一数据`，获取`请求会自动`在generateMetadata`、`generateStaticParams`、Layouts、Pages和Server Components之间[进行存储](https://nextjs.org/docs/app/building-your-application/caching#request-memoization)。如果`fetch`不可用[`，`可以使用](https://nextjs.org/docs/app/building-your-application/caching#react-cache-function)React缓存。
> - `searchParams` are only available in `page.js` segments.  
>     `searchParams`仅在`page.js`段中可用。
> - The [`redirect()`](https://nextjs.org/docs/app/api-reference/functions/redirect) and [`notFound()`](https://nextjs.org/docs/app/api-reference/functions/not-found) Next.js methods can also be used inside `generateMetadata`.  
>     redirect[`（）`](https://nextjs.org/docs/app/api-reference/functions/redirect)和[`notFound（）`](https://nextjs.org/docs/app/api-reference/functions/not-found)Next.js方法也可以在`generateMetadata`中使用。

## [Metadata Fields 元数据字段](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#metadata-fields)

### [`title 标题`](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#title)

The `title` attribute is used to set the title of the document. It can be defined as a simple [string](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#string) or an optional [template object](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#template-object).  
`title`属性用于设置文档的标题。它可以被定义为一个简单[的字符串](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#string)或一个可选[的模板对象](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#template-object)。

#### [String 字符串](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#string)

layout.js | page.js

```
export const metadata = {  title: 'Next.js',}
```

<head> output <head>输出

```
<title>Next.js</title>
```

#### [Template object 模板对象](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#template-object)

app/layout.tsx

TypeScript

JavaScriptTypeScript

```
import type { Metadata } from 'next' export const metadata: Metadata = {  title: {    template: '...',    default: '...',    absolute: '...',  },}
```

##### [Default 默认](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#default)

`title.default` can be used to provide a **fallback title** to child route segments that don't define a `title`.  
`title.default`可用于为未定义`标题`的子路由段提供**备用标题**。

app/layout.tsx

```
import type { Metadata } from 'next' export const metadata: Metadata = {  title: {    default: 'Acme',  },}
```

app/about/page.tsx

```
import type { Metadata } from 'next' export const metadata: Metadata = {} // Output: <title>Acme</title>
```

##### [Template 模板](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#template)

`title.template` can be used to add a prefix or a suffix to `titles` defined in **child**route segments.  
`title.template`可用于为**子**管段中定义`的标题`添加前缀或后缀。

app/layout.tsx

TypeScript

JavaScriptTypeScript

```
import type { Metadata } from 'next' export const metadata: Metadata = {  title: {    template: '%s | Acme',    default: 'Acme', // a default is required when creating a template  },}
```

app/about/page.tsx

TypeScript

JavaScriptTypeScript

```
import type { Metadata } from 'next' export const metadata: Metadata = {  title: 'About',} // Output: <title>About | Acme</title>
```

> **Good to know**:  
> **很高兴知道**：
> 
> - `title.template` applies to **child** route segments and **not** the segment it's defined in. This means:  
>     `template`应用于**子**管段，而**不是**定义它的管段。这意味着：
>     
>     - `title.default` is **required** when you add a `title.template`.  
>         当你添加一个`title.template`时`，title.default`是**必需**的。
>     - `title.template` defined in `layout.js` will not apply to a `title` defined in a `page.js`of the same route segment.  
>         `layout.js`中定义的`title.template`将不适用于同一路线段的`page.js`中定义的`title`。
>     - `title.template` defined in `page.js` has no effect because a page is always the terminating segment (it doesn't have any children route segments).  
>         在`page.js`中定义`的title.template`没有效果，因为页面总是终止段（它没有任何子路由段）。
> - `title.template` has **no effect** if a route has not defined a `title` or `title.default`.  
>     如果路由没有定义`title`或`title.default`，则`title.template`**无效**。
>     

##### [Absolute 绝对](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#absolute)

`title.absolute` can be used to provide a title that **ignores** `title.template` set in parent segments.  
`title.absolute`可用于提供**忽略**父段中设置`的title.template`的标题。

app/layout.tsx

TypeScript

JavaScriptTypeScript

```
import type { Metadata } from 'next' export const metadata: Metadata = {  title: {    template: '%s | Acme',  },}
```

app/about/page.tsx

TypeScript

JavaScriptTypeScript

```
import type { Metadata } from 'next' export const metadata: Metadata = {  title: {    absolute: 'About',  },} // Output: <title>About</title>
```

> **Good to know**:  
> **很高兴知道**：
> 
> - `layout.js`
>     
>     - `title` (string) and `title.default` define the default title for child segments (that do not define their own `title`). It will augment `title.template` from the closest parent segment if it exists.  
>         `title`（string）和`title.default`定义子段的默认标题（不定义自己`的标题`）。它将从最近的父段（如果存在的话）中增加`title.template`。
>     - `title.absolute` defines the default title for child segments. It ignores `title.template`from parent segments.  
>         `title.absolute`定义子段的默认标题。它忽略父段中`的title.template`。
>     - `title.template` defines a new title template for child segments.  
>         `template`为子段定义了一个新的标题模板。
> - `page.js`
>     
>     - If a page does not define its own title the closest parents resolved title will be used.  
>         如果页面没有定义自己的标题，则将使用最接近的父项解析标题。
>     - `title` (string) defines the routes title. It will augment `title.template` from the closest parent segment if it exists.  
>         `title`（string）定义路由标题。它将从最近的父段（如果存在的话）中增加`title.template`。
>     - `title.absolute` defines the route title. It ignores `title.template` from parent segments.  
>         `title.absolute`定义路由标题。它忽略父段中`的title.template`。
>     - `title.template` has no effect in `page.js` because a page is always the terminating segment of a route.  
>         `title.template`在`page.js`中没有作用，因为页面总是路由的终止段。

### [`description 描述`](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#description)

layout.js | page.js

```
export const metadata = {  description: 'The React Framework for the Web',}
```

<head> output <head>输出

```
<meta name="description" content="The React Framework for the Web" />
```

### [Basic Fields 基础领域](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#basic-fields)

layout.js | page.js

```
export const metadata = {  generator: 'Next.js',  applicationName: 'Next.js',  referrer: 'origin-when-cross-origin',  keywords: ['Next.js', 'React', 'JavaScript'],  authors: [{ name: 'Seb' }, { name: 'Josh', url: 'https://nextjs.org' }],  creator: 'Jiachi Liu',  publisher: 'Sebastian Markbåge',  formatDetection: {    email: false,    address: false,    telephone: false,  },}
```

<head> output <head>输出

```
<meta name="application-name" content="Next.js" /><meta name="author" content="Seb" /><link rel="author" href="https://nextjs.org" /><meta name="author" content="Josh" /><meta name="generator" content="Next.js" /><meta name="keywords" content="Next.js,React,JavaScript" /><meta name="referrer" content="origin-when-cross-origin" /><meta name="color-scheme" content="dark" /><meta name="creator" content="Jiachi Liu" /><meta name="publisher" content="Sebastian Markbåge" /><meta name="format-detection" content="telephone=no, address=no, email=no" />
```

### [`metadataBase 元数据库`](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#metadatabase)

`metadataBase` is a convenience option to set a base URL prefix for `metadata` fields that require a fully qualified URL.  
`metadataBase`是一个方便的选项，用于为需要完全限定URL的`元数据`字段设置基本URL前缀。

- `metadataBase` allows URL-based `metadata` fields defined in the **current route segment and below** to use a **relative path** instead of an otherwise required absolute URL.  
    `metadataBase`允许在**当前路由段和以下路由段**中定义的基于URL的`元数据`字段使用**相对路径，**而不是其他所需的绝对URL。
- The field's relative path will be composed with `metadataBase` to form a fully qualified URL.  
    该字段的相对路径将与`metadataBase`一起组成一个完全限定的URL。
- If not configured, `metadataBase` is **automatically populated** with a [default value](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#default-value).  
    如果未配置，则`metadataBase`将**自动**填充[默认值](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#default-value)。

layout.js | page.js

```
export const metadata = {  metadataBase: new URL('https://acme.com'),  alternates: {    canonical: '/',    languages: {      'en-US': '/en-US',      'de-DE': '/de-DE',    },  },  openGraph: {    images: '/og-image.png',  },}
```

<head> output <head>输出

```
<link rel="canonical" href="https://acme.com" /><link rel="alternate" hreflang="en-US" href="https://acme.com/en-US" /><link rel="alternate" hreflang="de-DE" href="https://acme.com/de-DE" /><meta property="og:image" content="https://acme.com/og-image.png" />
```

> **Good to know**:  
> **很高兴知道**：
> 
> - `metadataBase` is typically set in root `app/layout.js` to apply to URL-based `metadata`fields across all routes.  
>     `metadataBase`通常在根`app/layout.js`中设置，以应用于所有路由中基于URL的`元数据`字段。
> - All URL-based `metadata` fields that require absolute URLs can be configured with a `metadataBase` option.  
>     所有需要绝对URL的基于URL`的元数据`字段都可以使用`metadataBase`选项进行配置。
> - `metadataBase` can contain a subdomain e.g. `https://app.acme.com` or base path e.g. `https://acme.com/start/from/here`  
>     `metadataBase`可以包含一个子域，例如`https://app.acme.com`或基本路径，例如`https://acme.com/start/from/here`
> - If a `metadata` field provides an absolute URL, `metadataBase` will be ignored.  
>     如果`元数据`字段提供绝对URL，则将忽略`metadataBase`。
> - Using a relative path in a URL-based `metadata` field without configuring a `metadataBase`will cause a build error.  
>     在基于URL的`元数据`字段中使用相对路径而不配置`metadataBase`将导致生成错误。
> - Next.js will normalize duplicate slashes between `metadataBase` (e.g. `https://acme.com/`) and a relative field (e.g. `/path`) to a single slash (e.g. `https://acme.com/path`)  
>     Next.js会将`metadataBase`（例如`https://acme.com/`）和相对字段（例如`/path`）之间的重复斜杠规范化为单个斜杠（例如`https://acme.com/path`）

#### [Default value 默认值](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#default-value)

If not configured, `metadataBase` has a **default value**.  
如果未配置，则`metadataBase`具有**默认值**。

> On Vercel: 关于Vercel：
> 
> - For production deployments, `VERCEL_PROJECT_PRODUCTION_URL` will be used.  
>     对于生产部署，将使用`VERCEL_PROJECT_PRODUCTION_URL`。
> - For preview deployments, `VERCEL_BRANCH_URL` will take priority, and fallback to `VERCEL_URL`if it's not present.  
>     对于预览部署，`VERCEL_分支_URL`将优先，如果不存在，则回退到`VERCEL_URL`。
> 
> If these values are present they will be used as the **default value** of `metadataBase`, otherwise it falls back to `http://localhost:${process.env.PORT || 3000}`. This allows Open Graph images to work on both local build and Vercel preview and production deployments. When overriding the default, we recommend using environment variables to compute the URL. This allows configuring a URL for local development, staging, and production environments.  
> 如果这些值存在，它们将被用作metadataBase的**默认值**，否则福尔斯`http：//localhost：${process.env.PORT|| 3000}`。这允许Open Graph映像在本地构建和Vercel预览以及生产部署上工作。当覆盖默认值时，我们建议使用环境变量来计算URL。这允许为本地开发、登台和生产环境配置URL。
> 
> See more details about these environment variables in the [System Environment Variables](https://vercel.com/docs/concepts/projects/environment-variables/system-environment-variables)docs.  
> 有关这些环境变量的更多详细信息，请参阅[System Environment Variables](https://vercel.com/docs/concepts/projects/environment-variables/system-environment-variables)文档。

#### [URL Composition URL组合](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#url-composition)

URL composition favors developer intent over default directory traversal semantics.  
URL组合比默认目录遍历语义更有利于开发人员的意图。

- Trailing slashes between `metadataBase` and `metadata` fields are normalized.  
    `metadataBase`和`元数据`字段之间的尾随斜线是规范化的。
- An "absolute" path in a `metadata` field (that typically would replace the whole URL path) is treated as a "relative" path (starting from the end of `metadataBase`).  
    `元数据`字段中的“绝对”路径（通常会替换整个URL路径）被视为“相对”路径（从`metadataBase`的末尾开始）。

For example, given the following `metadataBase`:  
例如，给定以下`metadataBase`：

app/layout.tsx

TypeScript

JavaScriptTypeScript

```
import type { Metadata } from 'next' export const metadata: Metadata = {  metadataBase: new URL('https://acme.com'),}
```

Any `metadata` fields that inherit the above `metadataBase` and set their own value will be resolved as follows:  
继承上述`metadataBase`并设置自己值的任何`元数据`字段将按如下方式解析：

|`metadata` field  <br>`元数据`字段|Resolved URL 已解析URL|
|---|---|
|`/`|`https://acme.com`|
|`./`|`https://acme.com`|
|`payments 付款`|`https://acme.com/payments`|
|`/payments`|`https://acme.com/payments`|
|`./payments ./付款`|`https://acme.com/payments`|
|`../payments ../付款`|`https://acme.com/payments`|
|`https://beta.acme.com/payments`|`https://beta.acme.com/payments`|

### [`openGraph`](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#opengraph)

layout.js | page.js

```
export const metadata = {  openGraph: {    title: 'Next.js',    description: 'The React Framework for the Web',    url: 'https://nextjs.org',    siteName: 'Next.js',    images: [      {        url: 'https://nextjs.org/og.png', // Must be an absolute URL        width: 800,        height: 600,      },      {        url: 'https://nextjs.org/og-alt.png', // Must be an absolute URL        width: 1800,        height: 1600,        alt: 'My custom alt',      },    ],    videos: [      {        url: 'https://nextjs.org/video.mp4', // Must be an absolute URL        width: 800,        height: 600,      },    ],    audio: [      {        url: 'https://nextjs.org/audio.mp3', // Must be an absolute URL      },    ],    locale: 'en_US',    type: 'website',  },}
```

<head> output <head>输出

```
<meta property="og:title" content="Next.js" /><meta property="og:description" content="The React Framework for the Web" /><meta property="og:url" content="https://nextjs.org/" /><meta property="og:site_name" content="Next.js" /><meta property="og:locale" content="en_US" /><meta property="og:image" content="https://nextjs.org/og.png" /><meta property="og:image:width" content="800" /><meta property="og:image:height" content="600" /><meta property="og:image" content="https://nextjs.org/og-alt.png" /><meta property="og:image:width" content="1800" /><meta property="og:image:height" content="1600" /><meta property="og:image:alt" content="My custom alt" /><meta property="og:video" content="https://nextjs.org/video.mp4" /><meta property="og:video:width" content="800" /><meta property="og:video:height" content="600" /><meta property="og:audio" content="https://nextjs.org/audio.mp3" /><meta property="og:type" content="website" />
```

layout.js | page.js

```
export const metadata = {  openGraph: {    title: 'Next.js',    description: 'The React Framework for the Web',    type: 'article',    publishedTime: '2023-01-01T00:00:00.000Z',    authors: ['Seb', 'Josh'],  },}
```

<head> output <head>输出

```
<meta property="og:title" content="Next.js" /><meta property="og:description" content="The React Framework for the Web" /><meta property="og:type" content="article" /><meta property="article:published_time" content="2023-01-01T00:00:00.000Z" /><meta property="article:author" content="Seb" /><meta property="article:author" content="Josh" />
```

> **Good to know**:  
> **很高兴知道**：
> 
> - It may be more convenient to use the [file-based Metadata API](https://nextjs.org/docs/app/api-reference/file-conventions/metadata/opengraph-image#image-files-jpg-png-gif) for Open Graph images. Rather than having to sync the config export with actual files, the file-based API will automatically generate the correct metadata for you.  
>     对于Open Graph图像，使用[基于文件的元数据API](https://nextjs.org/docs/app/api-reference/file-conventions/metadata/opengraph-image#image-files-jpg-png-gif)可能更方便。基于文件的API将自动为您生成正确的元数据，而不必将配置导出与实际文件同步。

### [`robots 机器人`](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#robots)

layout.tsx | page.tsx

```
import type { Metadata } from 'next' export const metadata: Metadata = {  robots: {    index: false,    follow: true,    nocache: true,    googleBot: {      index: true,      follow: false,      noimageindex: true,      'max-video-preview': -1,      'max-image-preview': 'large',      'max-snippet': -1,    },  },}
```

<head> output <head>输出

```
<meta name="robots" content="noindex, follow, nocache" /><meta  name="googlebot"  content="index, nofollow, noimageindex, max-video-preview:-1, max-image-preview:large, max-snippet:-1"/>
```

### [`icons 图标`](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#icons)

> **Good to know**: We recommend using the [file-based Metadata API](https://nextjs.org/docs/app/api-reference/file-conventions/metadata/app-icons#image-files-ico-jpg-png) for icons where possible. Rather than having to sync the config export with actual files, the file-based API will automatically generate the correct metadata for you.  
> **好消息**：我们建议尽可能使用[基于文件的元数据API](https://nextjs.org/docs/app/api-reference/file-conventions/metadata/app-icons#image-files-ico-jpg-png)。基于文件的API将自动为您生成正确的元数据，而不必将配置导出与实际文件同步。

layout.js | page.js

```
export const metadata = {  icons: {    icon: '/icon.png',    shortcut: '/shortcut-icon.png',    apple: '/apple-icon.png',    other: {      rel: 'apple-touch-icon-precomposed',      url: '/apple-touch-icon-precomposed.png',    },  },}
```

<head> output <head>输出

```
<link rel="shortcut icon" href="/shortcut-icon.png" /><link rel="icon" href="/icon.png" /><link rel="apple-touch-icon" href="/apple-icon.png" /><link  rel="apple-touch-icon-precomposed"  href="/apple-touch-icon-precomposed.png"/>
```

layout.js | page.js

```
export const metadata = {  icons: {    icon: [      { url: '/icon.png' },      new URL('/icon.png', 'https://example.com'),      { url: '/icon-dark.png', media: '(prefers-color-scheme: dark)' },    ],    shortcut: ['/shortcut-icon.png'],    apple: [      { url: '/apple-icon.png' },      { url: '/apple-icon-x3.png', sizes: '180x180', type: 'image/png' },    ],    other: [      {        rel: 'apple-touch-icon-precomposed',        url: '/apple-touch-icon-precomposed.png',      },    ],  },}
```

<head> output <head>输出

```
<link rel="shortcut icon" href="/shortcut-icon.png" /><link rel="icon" href="/icon.png" /><link rel="icon" href="https://example.com/icon.png" /><link rel="icon" href="/icon-dark.png" media="(prefers-color-scheme: dark)" /><link rel="apple-touch-icon" href="/apple-icon.png" /><link  rel="apple-touch-icon-precomposed"  href="/apple-touch-icon-precomposed.png"/><link  rel="apple-touch-icon"  href="/apple-icon-x3.png"  sizes="180x180"  type="image/png"/>
```

> **Good to know**: The `msapplication-*` meta tags are no longer supported in Chromium builds of Microsoft Edge, and thus no longer needed.  
> **很高兴知道**：微软Edge的Chromium版本不再支持`msapplication-*`Meta标记，因此不再需要。

### [`themeColor 主题颜色`](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#themecolor)

> **Deprecated**: The `themeColor` option in `metadata` is deprecated as of Next.js 14. Please use the [`viewport` configuration](https://nextjs.org/docs/app/api-reference/functions/generate-viewport) instead.  
> **废弃**：`元数据`中的`themeColor`选项从Next.js 14起废弃。请改用[`视口`配置](https://nextjs.org/docs/app/api-reference/functions/generate-viewport)。

### [`manifest 清单`](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#manifest)

A web application manifest, as defined in the [Web Application Manifest specification](https://developer.mozilla.org/docs/Web/Manifest).  
Web应用程序清单，如[Web应用程序清单规范](https://developer.mozilla.org/docs/Web/Manifest)中定义的。

layout.js | page.js

```
export const metadata = {  manifest: 'https://nextjs.org/manifest.json',}
```

<head> output <head>输出

```
<link rel="manifest" href="https://nextjs.org/manifest.json" />
```

### [`twitter`](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#twitter)

The Twitter specification is (surprisingly) used for more than just X (formerly known as Twitter).  
Twitter规范（令人惊讶地）不仅仅用于X（以前称为Twitter）。

Learn more about the [Twitter Card markup reference](https://developer.x.com/en/docs/twitter-for-websites/cards/overview/markup).  
了解有关[Twitter Card标记参考的](https://developer.x.com/en/docs/twitter-for-websites/cards/overview/markup)更多信息。

layout.js | page.js

```
export const metadata = {  twitter: {    card: 'summary_large_image',    title: 'Next.js',    description: 'The React Framework for the Web',    siteId: '1467726470533754880',    creator: '@nextjs',    creatorId: '1467726470533754880',    images: ['https://nextjs.org/og.png'], // Must be an absolute URL  },}
```

<head> output <head>输出

```
<meta name="twitter:card" content="summary_large_image" /><meta name="twitter:site:id" content="1467726470533754880" /><meta name="twitter:creator" content="@nextjs" /><meta name="twitter:creator:id" content="1467726470533754880" /><meta name="twitter:title" content="Next.js" /><meta name="twitter:description" content="The React Framework for the Web" /><meta name="twitter:image" content="https://nextjs.org/og.png" />
```

layout.js | page.js

```
export const metadata = {  twitter: {    card: 'app',    title: 'Next.js',    description: 'The React Framework for the Web',    siteId: '1467726470533754880',    creator: '@nextjs',    creatorId: '1467726470533754880',    images: {      url: 'https://nextjs.org/og.png',      alt: 'Next.js Logo',    },    app: {      name: 'twitter_app',      id: {        iphone: 'twitter_app://iphone',        ipad: 'twitter_app://ipad',        googleplay: 'twitter_app://googleplay',      },      url: {        iphone: 'https://iphone_url',        ipad: 'https://ipad_url',      },    },  },}
```

<head> output <head>输出

```
<meta name="twitter:site:id" content="1467726470533754880" /><meta name="twitter:creator" content="@nextjs" /><meta name="twitter:creator:id" content="1467726470533754880" /><meta name="twitter:title" content="Next.js" /><meta name="twitter:description" content="The React Framework for the Web" /><meta name="twitter:card" content="app" /><meta name="twitter:image" content="https://nextjs.org/og.png" /><meta name="twitter:image:alt" content="Next.js Logo" /><meta name="twitter:app:name:iphone" content="twitter_app" /><meta name="twitter:app:id:iphone" content="twitter_app://iphone" /><meta name="twitter:app:id:ipad" content="twitter_app://ipad" /><meta name="twitter:app:id:googleplay" content="twitter_app://googleplay" /><meta name="twitter:app:url:iphone" content="https://iphone_url" /><meta name="twitter:app:url:ipad" content="https://ipad_url" /><meta name="twitter:app:name:ipad" content="twitter_app" /><meta name="twitter:app:name:googleplay" content="twitter_app" />
```

### [`viewport 视口`](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#viewport)

> **Deprecated**: The `viewport` option in `metadata` is deprecated as of Next.js 14. Please use the [`viewport` configuration](https://nextjs.org/docs/app/api-reference/functions/generate-viewport) instead.  
> **废弃**：`元数据`中的`viewport`选项从Next.js 14起废弃。请改用[`视口`配置](https://nextjs.org/docs/app/api-reference/functions/generate-viewport)。

### [`verification 验证`](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#verification)

layout.js | page.js

```
export const metadata = {  verification: {    google: 'google',    yandex: 'yandex',    yahoo: 'yahoo',    other: {      me: ['my-email', 'my-link'],    },  },}
```

<head> output <head>输出

```
<meta name="google-site-verification" content="google" /><meta name="y_key" content="yahoo" /><meta name="yandex-verification" content="yandex" /><meta name="me" content="my-email" /><meta name="me" content="my-link" />
```

### [`appleWebApp`](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#applewebapp)

layout.js | page.js

```
export const metadata = {  itunes: {    appId: 'myAppStoreID',    appArgument: 'myAppArgument',  },  appleWebApp: {    title: 'Apple Web App',    statusBarStyle: 'black-translucent',    startupImage: [      '/assets/startup/apple-touch-startup-image-768x1004.png',      {        url: '/assets/startup/apple-touch-startup-image-1536x2008.png',        media: '(device-width: 768px) and (device-height: 1024px)',      },    ],  },}
```

<head> output <head>输出

```
<meta  name="apple-itunes-app"  content="app-id=myAppStoreID, app-argument=myAppArgument"/><meta name="mobile-web-app-capable" content="yes" /><meta name="apple-mobile-web-app-title" content="Apple Web App" /><link  href="/assets/startup/apple-touch-startup-image-768x1004.png"  rel="apple-touch-startup-image"/><link  href="/assets/startup/apple-touch-startup-image-1536x2008.png"  media="(device-width: 768px) and (device-height: 1024px)"  rel="apple-touch-startup-image"/><meta  name="apple-mobile-web-app-status-bar-style"  content="black-translucent"/>
```

### [`alternates 交替`](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#alternates)

layout.js | page.js

```
export const metadata = {  alternates: {    canonical: 'https://nextjs.org',    languages: {      'en-US': 'https://nextjs.org/en-US',      'de-DE': 'https://nextjs.org/de-DE',    },    media: {      'only screen and (max-width: 600px)': 'https://nextjs.org/mobile',    },    types: {      'application/rss+xml': 'https://nextjs.org/rss',    },  },}
```

<head> output <head>输出

```
<link rel="canonical" href="https://nextjs.org" /><link rel="alternate" hreflang="en-US" href="https://nextjs.org/en-US" /><link rel="alternate" hreflang="de-DE" href="https://nextjs.org/de-DE" /><link  rel="alternate"  media="only screen and (max-width: 600px)"  href="https://nextjs.org/mobile"/><link  rel="alternate"  type="application/rss+xml"  href="https://nextjs.org/rss"/>
```

### [`appLinks 应用链接`](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#applinks)

layout.js | page.js

```
export const metadata = {  appLinks: {    ios: {      url: 'https://nextjs.org/ios',      app_store_id: 'app_store_id',    },    android: {      package: 'com.example.android/package',      app_name: 'app_name_android',    },    web: {      url: 'https://nextjs.org/web',      should_fallback: true,    },  },}
```

<head> output <head>输出

```
<meta property="al:ios:url" content="https://nextjs.org/ios" /><meta property="al:ios:app_store_id" content="app_store_id" /><meta property="al:android:package" content="com.example.android/package" /><meta property="al:android:app_name" content="app_name_android" /><meta property="al:web:url" content="https://nextjs.org/web" /><meta property="al:web:should_fallback" content="true" />
```

### [`archives 档案`](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#archives)

Describes a collection of records, documents, or other materials of historical interest ([source](https://www.w3.org/TR/2011/WD-html5-20110113/links.html#rel-archives)).  
描述一系列记录、文件或其他具有历史意义的材料（[来源](https://www.w3.org/TR/2011/WD-html5-20110113/links.html#rel-archives)）。

layout.js | page.js

```
export const metadata = {  archives: ['https://nextjs.org/13'],}
```

<head> output <head>输出

```
<link rel="archives" href="https://nextjs.org/13" />
```

### [`assets 资产`](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#assets)

layout.js | page.js

```
export const metadata = {  assets: ['https://nextjs.org/assets'],}
```

<head> output <head>输出

```
<link rel="assets" href="https://nextjs.org/assets" />
```

### [`bookmarks 书签`](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#bookmarks)

layout.js | page.js

```
export const metadata = {  bookmarks: ['https://nextjs.org/13'],}
```

<head> output <head>输出

```
<link rel="bookmarks" href="https://nextjs.org/13" />
```

### [`category 类别`](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#category)

layout.js | page.js

```
export const metadata = {  category: 'technology',}
```

<head> output <head>输出

```
<meta name="category" content="technology" />
```

### [`facebook`](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#facebook)

You can connect a Facebook app or Facebook account to you webpage for certain Facebook Social Plugins [Facebook Documentation](https://developers.facebook.com/docs/plugins/comments/#moderation-setup-instructions)  
您可以将Facebook应用程序或Facebook帐户连接到您的网页，以获得某些Facebook社交插件[Facebook文档](https://developers.facebook.com/docs/plugins/comments/#moderation-setup-instructions)

> **Good to know**: You can specify either appId or admins, but not both.  
> **好消息**：你可以指定appId或admins，但不能同时指定两者。

layout.js | page.js

```
export const metadata = {  facebook: {    appId: '12345678',  },}
```

<head> output <head>输出

```
<meta property="fb:app_id" content="12345678" />
```

layout.js | page.js

```
export const metadata = {  facebook: {    admins: '12345678',  },}
```

<head> output <head>输出

```
<meta property="fb:admins" content="12345678" />
```

If you want to generate multiple fb:admins meta tags you can use array value.  
如果你想生成多个fb：admins Meta标签，你可以使用数组值。

layout.js | page.js

```
export const metadata = {  facebook: {    admins: ['12345678', '87654321'],  },}
```

<head> output <head>输出

```
<meta property="fb:admins" content="12345678" /><meta property="fb:admins" content="87654321" />
```

### [`other 其他`](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#other)

All metadata options should be covered using the built-in support. However, there may be custom metadata tags specific to your site, or brand new metadata tags just released. You can use the `other` option to render any custom metadata tag.  
所有的元数据选项都应该使用内置的支持。但是，可能会有特定于您的站点的自定义元数据标记，或者刚刚发布的全新元数据标记。您可以使用`其他`选项来呈现任何自定义元数据标记。

layout.js | page.js

```
export const metadata = {  other: {    custom: 'meta',  },}
```

<head> output <head>输出

```
<meta name="custom" content="meta" />
```

If you want to generate multiple same key meta tags you can use array value.  
如果您想生成多个相同的关键Meta标签，您可以使用数组值。

layout.js | page.js

```
export const metadata = {  other: {    custom: ['meta1', 'meta2'],  },}
```

<head> output <head>输出

```
<meta name="custom" content="meta1" /> <meta name="custom" content="meta2" />
```

## [Unsupported Metadata 不支持的元数据](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#unsupported-metadata)

The following metadata types do not currently have built-in support. However, they can still be rendered in the layout or page itself.  
以下元数据类型当前没有内置支持。但是，它们仍然可以在布局或页面本身中呈现。

|Metadata 元数据|Recommendation 建议|
|---|---|
|`<meta http-equiv="...">   <meta http-equiv="...“>`|Use appropriate HTTP Headers via [`redirect()`](https://nextjs.org/docs/app/api-reference/functions/redirect), [Middleware](https://nextjs.org/docs/app/building-your-application/routing/middleware#nextresponse), [Security Headers](https://nextjs.org/docs/app/api-reference/next-config-js/headers)  <br>通过[`redirect（）`](https://nextjs.org/docs/app/api-reference/functions/redirect)、[中间件](https://nextjs.org/docs/app/building-your-application/routing/middleware#nextresponse)、[安全头](https://nextjs.org/docs/app/api-reference/next-config-js/headers)使用适当的HTTP头|
|`<base>`|Render the tag in the layout or page itself.  <br>在布局或页面本身中呈现标记。|
|`<noscript>`|Render the tag in the layout or page itself.  <br>在布局或页面本身中呈现标记。|
|`<style> <样式>`|Learn more about [styling in Next.js](https://nextjs.org/docs/app/building-your-application/styling/css).  <br>了解有关[Next.js中样式的](https://nextjs.org/docs/app/building-your-application/styling/css)更多信息。|
|`<script> <脚本>`|Learn more about [using scripts](https://nextjs.org/docs/app/building-your-application/optimizing/scripts).  <br>了解有关[使用脚本的](https://nextjs.org/docs/app/building-your-application/optimizing/scripts)详细信息。|
|`<link rel="stylesheet" />   <link rel=“样式表”/>`|`import` stylesheets directly in the layout or page itself.  <br>直接在布局或页面本身中`导入`样式表。|
|`<link rel="preload />   <link rel=“预加载/>`|Use [ReactDOM preload method](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#link-relpreload)  <br>使用[ReactDOM预加载方法](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#link-relpreload)|
|`<link rel="preconnect" />   <link rel=“预连接”/>`|Use [ReactDOM preconnect method](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#link-relpreconnect)  <br>使用[ReactDOM预连接方法](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#link-relpreconnect)|
|`<link rel="dns-prefetch" />   <link rel=“dns-prefetch”/>`|Use [ReactDOM prefetchDNS method](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#link-reldns-prefetch)  <br>使用[ReactDOM预取DNS方法](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#link-reldns-prefetch)|

### [Resource hints 资源提示](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#resource-hints)

The `<link>` element has a number of `rel` keywords that can be used to hint to the browser that an external resource is likely to be needed. The browser uses this information to apply preloading optimizations depending on the keyword.  
`<link>`元素有许多`rel`关键字，可用于提示浏览器可能需要外部资源。浏览器使用此信息根据关键字应用预加载优化。

While the Metadata API doesn't directly support these hints, you can use new [`ReactDOM`methods](https://github.com/facebook/react/pull/26237) to safely insert them into the `<head>` of the document.  
虽然Metadata API不直接支持这些提示，但您可以使用新[`的ReactDOM`方法](https://github.com/facebook/react/pull/26237)将它们安全地插入到文档的`<head>`中。

app/preload-resources.tsx

TypeScript

JavaScriptTypeScript

```
'use client' import ReactDOM from 'react-dom' export function PreloadResources() {  ReactDOM.preload('...', { as: '...' })  ReactDOM.preconnect('...', { crossOrigin: '...' })  ReactDOM.prefetchDNS('...')   return '...'}
```

##### [`<link rel="preload"> <link rel=“preload”>`](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#link-relpreload)

Start loading a resource early in the page rendering (browser) lifecycle. [MDN Docs](https://developer.mozilla.org/docs/Web/HTML/Attributes/rel/preload).  
在页面呈现（浏览器）生命周期的早期开始加载资源。[](https://developer.mozilla.org/docs/Web/HTML/Attributes/rel/preload)MDN

```
ReactDOM.preload(href: string, options: { as: string })
```

<head> output <head>输出

```
<link rel="preload" href="..." as="..." />
```

##### [`<link rel="preconnect">   <link rel=“预连接”>`](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#link-relpreconnect)

Preemptively initiate a connection to an origin. [MDN Docs](https://developer.mozilla.org/docs/Web/HTML/Attributes/rel/preconnect).  
抢先启动到源的连接。[MDN文档](https://developer.mozilla.org/docs/Web/HTML/Attributes/rel/preconnect)。

```
ReactDOM.preconnect(href: string, options?: { crossOrigin?: string })
```

<head> output <head>输出

```
<link rel="preconnect" href="..." crossorigin />
```

##### [`<link rel="dns-prefetch">   <link rel=“dns-prefetch”>`](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#link-reldns-prefetch)

Attempt to resolve a domain name before resources get requested. [MDN Docs](https://developer.mozilla.org/docs/Web/HTML/Attributes/rel/dns-prefetch).  
在请求资源之前尝试解析域名。[MDN文档](https://developer.mozilla.org/docs/Web/HTML/Attributes/rel/dns-prefetch)。

```
ReactDOM.prefetchDNS(href: string)
```

<head> output <head>输出

```
<link rel="dns-prefetch" href="..." />
```

> **Good to know**:  
> **很高兴知道**：
> 
> - These methods are currently only supported in Client Components, which are still Server Side Rendered on initial page load.  
>     这些方法目前仅在客户端组件中受支持，客户端组件在初始页面加载时仍然是服务器端呈现的。
> - Next.js in-built features such as `next/font`, `next/image` and `next/script` automatically handle relevant resource hints.  
>     Next.js的内置功能，如`next/font`，`next/image`和`next/script，会`自动处理相关的资源提示。

## [Types 类型](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#types)

You can add type safety to your metadata by using the `Metadata` type. If you are using the [built-in TypeScript plugin](https://nextjs.org/docs/app/api-reference/config/typescript) in your IDE, you do not need to manually add the type, but you can still explicitly add it if you want.  
可以使用`Metadata`类型向元数据添加类型安全。如果您在IDE中使用[内置的TypeScript插件](https://nextjs.org/docs/app/api-reference/config/typescript)，则不需要手动添加类型，但如果需要，您仍然可以显式添加它。

### [`metadata` object  
`元数据`对象](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#metadata-object)

layout.tsx | page.tsx

```
import type { Metadata } from 'next' export const metadata: Metadata = {  title: 'Next.js',}
```

### [`generateMetadata` function  
`generateMetadata`函数](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#generatemetadata-function-1)

#### [Regular function 正则函数](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#regular-function)

layout.tsx | page.tsx

```
import type { Metadata } from 'next' export function generateMetadata(): Metadata {  return {    title: 'Next.js',  }}
```

#### [Async function Async函数](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#async-function)

layout.tsx | page.tsx

```
import type { Metadata } from 'next' export async function generateMetadata(): Promise<Metadata> {  return {    title: 'Next.js',  }}
```

#### [With segment props 带分段道具](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#with-segment-props)

layout.tsx | page.tsx

```
import type { Metadata } from 'next' type Props = {  params: Promise<{ id: string }>  searchParams: Promise<{ [key: string]: string | string[] | undefined }>} export function generateMetadata({ params, searchParams }: Props): Metadata {  return {    title: 'Next.js',  }} export default function Page({ params, searchParams }: Props) {}
```

#### [With parent metadata 使用父元数据](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#with-parent-metadata)

layout.tsx | page.tsx

```
import type { Metadata, ResolvingMetadata } from 'next' export async function generateMetadata(  { params, searchParams }: Props,  parent: ResolvingMetadata): Promise<Metadata> {  return {    title: 'Next.js',  }}
```

#### [JavaScript Projects JavaScript项目](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#javascript-projects)

For JavaScript projects, you can use JSDoc to add type safety.  
对于JavaScript项目，可以使用JSDoc添加类型安全。

layout.js | page.js

```
/** @type {import("next").Metadata} */export const metadata = {  title: 'Next.js',}
```

## [Version History 版本历史](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#version-history)

|Version Version版本|Changes|
|---|---|
|`v13.2.0`|`viewport`, `themeColor`, and `colorScheme` deprecated in favor of the [`viewport` configuration](https://nextjs.org/docs/app/api-reference/functions/generate-viewport).  <br>`viewport`、`themeColor`和`colorScheme已`弃用，转而支持[`viewport`配置](https://nextjs.org/docs/app/api-reference/functions/generate-viewport)。|
|`v13.2.0`|`metadata` and `generateMetadata` introduced.  <br>`metadata`和`generateMetadata`。|

## Next Steps 后续步骤

View all the Metadata API options.  
查看所有元数据API选项。

[

### Metadata Files 元数据文件

API documentation for the metadata file conventions.  
元数据文件约定的API文档。

](https://nextjs.org/docs/app/api-reference/file-conventions/metadata)[

### generateViewport

API Reference for the generateViewport function.  
generateViewport函数的API参考。

](https://nextjs.org/docs/app/api-reference/functions/generate-viewport)[

### Metadata 元数据

Use the Metadata API to define metadata in any layout or page.  
使用元数据API在任何布局或页面中定义元数据。

](https://nextjs.org/docs/app/building-your-application/optimizing/metadata)

[Previous 先前

generateImageMetadata

](https://nextjs.org/docs/app/api-reference/functions/generate-image-metadata)

[Next 下

generateSitemaps generate网站地图

](https://nextjs.org/docs/app/api-reference/functions/generate-sitemaps)

Was this helpful? 这有帮助吗？

supported.

[](https://vercel.com/home?utm_source=next-site&utm_medium=footer&utm_campaign=next-website "Go to the Vercel website")

#### Resources

[Docs](https://nextjs.org/docs)[Learn](https://nextjs.org/learn)[Showcase](https://nextjs.org/showcase)[Blog](https://nextjs.org/blog)[Analytics](https://vercel.com/analytics?utm_source=next-site&utm_medium=footer&utm_campaign=docs_app_api-reference_functions_generate-metadata)[Next.js Conf](https://nextjs.org/conf)[Previews](https://vercel.com/products/previews?utm_source=next-site&utm_medium=footer&utm_campaign=docs_app_api-reference_functions_generate-metadata)

#### More

[Next.js Commerce](https://vercel.com/templates/next.js/nextjs-commerce?utm_source=next-site&utm_medium=footer&utm_campaign=docs_app_api-reference_functions_generate-metadata)[Contact Sales](https://vercel.com/contact/sales?utm_source=next-site&utm_medium=footer&utm_campaign=docs_app_api-reference_functions_generate-metadata)[GitHub](https://github.com/vercel/next.js)[Releases](https://github.com/vercel/next.js/releases)[Telemetry](https://nextjs.org/telemetry)[Governance](https://nextjs.org/governance)

#### About Vercel