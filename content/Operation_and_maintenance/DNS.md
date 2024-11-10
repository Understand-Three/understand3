---
title: Vercel 更改 DNS
draft: true
---

# 【多图预警】vercel部署及国内访问

少年，想要给网站整个好看的域名吗

Aling

2024-05-09

6 min

为什么想起来写这个呢，今天看nextjs中文官网时在[部署](https://www.nextjs.cn/docs/deployment)页面看到这么一句话。![image.png](https://www.zhongfw.online/img/memorys/cf8e8dff9c67b81ddf0afb571a292c7a.png)

不适合国内哈哈，想起了被科学上网支配的恐惧。这个问题我通过couldflare解决了，仔细一想还是有点东西的，所以就水这个吧。

## [#](https://www.zhongfw.online/posts/%E3%80%90%E5%A4%9A%E5%9B%BE%E9%A2%84%E8%AD%A6%E3%80%91vercel%E9%83%A8%E7%BD%B2%E5%8F%8A%E5%9B%BD%E5%86%85%E8%AE%BF%E9%97%AE.html#%E9%83%A8%E7%BD%B2%E7%BD%91%E7%AB%99%E5%88%B0vercel)部署网站到Vercel

目前网上对于在[vercel](https://vercel.com/)上部署静态页面都有比较详细的教程，其中大多都是通过github直接导入项目的方法，这也是官方比较推荐的方法，好处是当git提交时vercel可以检测并自动重新构建项目更新网站。

### [#](https://www.zhongfw.online/posts/%E3%80%90%E5%A4%9A%E5%9B%BE%E9%A2%84%E8%AD%A6%E3%80%91vercel%E9%83%A8%E7%BD%B2%E5%8F%8A%E5%9B%BD%E5%86%85%E8%AE%BF%E9%97%AE.html#%E5%AF%BC%E5%85%A5%E9%A1%B9%E7%9B%AE)导入项目

#### [#](https://www.zhongfw.online/posts/%E3%80%90%E5%A4%9A%E5%9B%BE%E9%A2%84%E8%AD%A6%E3%80%91vercel%E9%83%A8%E7%BD%B2%E5%8F%8A%E5%9B%BD%E5%86%85%E8%AE%BF%E9%97%AE.html#%E4%BB%8Egithub%E5%AF%BC%E5%85%A5)从github导入

通过邮箱注册一个vercel账号，类型我们选择个人即可:

![image.png](https://www.zhongfw.online/img/memorys/03860e4df46ae28a2cc3785a7db7596d.png)

在控制台我们直接新建个项目：

![image.png](https://www.zhongfw.online/img/memorys/69d7c39c5c2d36a8996879a3511ca9c2.png)

登录 github 账号，选择需要导入的项目:

![image.png](https://www.zhongfw.online/img/memorys/1dd0f4b160f9c8ae845f7463c15d4800.png)

随后我们就需要根据配置项目构建的配置:

![image.png](https://www.zhongfw.online/img/memorys/263fb255dd6fb9f32ec23c796a17f7b7.png)

其中比较重要的是构建和输入的配置，一般使用了框架的话构建和输入都是默认配置不需要二次修改，这也就是为什么上面会让你选择Framework Preset。我的建议是没有前端基础的小白直接默认 Deploy（啥，报错？那只能看看项目文档或者问问开发者了），作为前端开发者则需要根据自己的项目来修改相关配置。

最后点击Deploy即可构建项目，vercel会自动安装依赖，打包最后读取打包文件。顺利的话再构建成功后你就成功部署了自己的网站。

![image.png](https://www.zhongfw.online/img/memorys/28362b098c01481cfd1ed96357029393.png)

返回到工作台即可看到构建成功的网站及vercel生成的网站域名，并且当你提交新的git记录到github时，vercel将会自动触发构建。当然想要访问你还需要挂上梯子，这也就是为什么文章最开始提到的vercel部署不适合国内。

#### 本地构架打包

除了通过再网站上通过github导入项目，vercel也提供了一个[脚手架](https://vercel.com/docs/getting-started-with-vercel)让你能再本地直接打包构建到vercel。

我们直接安装:

```bash
npm i -g vercel
```

安装成功后我们即可进入项目根目录，切换终端到项目根，让我们登录vercel:

```bash
vercel login
```


![image.png](https://www.zhongfw.online/img/memorys/ac0b510fec60697ec84fe4ffcfe56f1d.png)

登录成功后我们就可以打包我们的项目了，执行`vercel`：

```bash
vercel 

# vercel --prod
```

![image.png](https://www.zhongfw.online/img/memorys/db0faf9ff0be0173883740fbd96e422e.png)

这里可以选择是否链接到已经存在的项目，如果想要覆盖一个已有的项目可以选是，否则选否来新建一个项目。

![image.png](https://www.zhongfw.online/img/memorys/90e027f8fd0ab7be40671444e1ffdfa8.png)

与在网页上配置的相似，配置项目构建的根目录

随后vercel会在目录下生成.vercel文件，并提示是否需要修改相关打包和安装命令，这些配置和在网页上的配置项一致:

![image.png](https://www.zhongfw.online/img/memorys/e4740adf80747cb40f714fce264e39a2.png)

随后vercel会自动构建并上传构建资源到对应项目，你可以在网站上看到生成的项目。

这种构建方法相较于前者失去了自动化构建的优势，优点嘛，我想是能避免掉本地构建成功但是在网站上Deploy构建失败却束手无策的情况吧😕。


# 在 Vercel 中添加自定义的域名

![[Pasted image 20241107002606.png]]

# 使用 cloudflare 代理访问

在vercel上构建的网站在国内是无法正常访问的，而且自动生成的域名会有 `.vercel` 的后缀。下面我们来解决掉这两个问题。

## 购买域名

腾讯云，阿里云，华为云等等够可以购买域名。这里以腾讯云为例：


### 注册腾讯云账号

点击域名注册：

![image.png](https://www.zhongfw.online/img/memorys/74a32461b274a89080870009bd4d5504.png)

选个自己喜欢的然后购买即可：

![image.png](https://www.zhongfw.online/img/memorys/e06e77b666e2fd0b649e4e3760d295a8.png)

### 修改dns服务器

这里有必要提一下为什么要修改dns服务器，我们绕过墙的方式是当我们请求自己购买的域名时，能重定向到我们实际的网站地址。国内云服务厂商没有提供相关免费服务，我们需要使用cloudflare完成重定向。为了能让cloudflare有能力重定向所以我们要修改域名的dns服务器，改成 cloudflare 的 dns 服务器地址。

前往控制台，管理域名:

![image.png](https://www.zhongfw.online/img/memorys/18893ffa8df8f18c2ea7b496b041f413.png)

![image.png](https://www.zhongfw.online/img/memorys/f9034e0f70aafb6c9eda319da8670fe1.png)

修改dns服务为如下:

![image.png](https://www.zhongfw.online/img/memorys/303d671b432002d1a09638bef851a368.png)

```bash
aliza.ns.cloudflare.com  
ezra.ns.cloudflare.com
```


好嘞！这下等待修改生效即可，虽然提示要48小时但是我貌似一会就好了。

如此我们的域名操作告一段落。

### 配置 cloudflare 重定向

前往 [cloudfare](https://www.cloudflare-cn.com/) 注册账号，新增一个站点:

![image.png](https://www.zhongfw.online/img/memorys/f55bf22bbd096f15d7b15afa32a56c0f.png)

输入你买的域名，使用免费的服务:

![image.png](https://www.zhongfw.online/img/memorys/abf56cb7e82e0ae6c7467d86b6f27fe5.png)

![image.png](https://www.zhongfw.online/img/memorys/d8c0b98966180d79f7428488c8dfdbaa.png)

一路继续，这里可以看到我们刚刚使用的 dns 服务器地址:

![image.png](https://www.zhongfw.online/img/memorys/1d7dd00e33c871364d2d47304dc8910b.png)

完成后点击进入我们的域名，让我们配置dns解析规则:

![image.png](https://www.zhongfw.online/img/memorys/2865f3b67511bbe0934cb0c85e3c9d28.png)

因为我们是代理重定向域名所以类型我们是CNAME，随后填入你的域名和实际vercel服务域名即可。

就像下面这样:

![image.png](https://www.zhongfw.online/img/memorys/0783785d3ce76ce661c451146f2b4ad2.png)

最后还要设置加密模式为完全严格，然后就完事了：

![image.png](https://www.zhongfw.online/img/memorys/bcf3c77801577eb614af623bde9334bc.png)

现在就可以愉快的用域名访问自己的项目了。


## 使用阿里云
### 注册阿里云账号

### 购买域名

### 修改记录
![[Pasted image 20241107003019.png]]
## 修改 DNS

域名列表，在域名的后方点击管理

![[Pasted image 20241107002749.png]]

修改为 cloudflare 的 DNS

harleigh.ns.cloudflare.com
armando.ns.cloudflare.com

![[Pasted image 20241107002732.png]]

修改 cloudflare

![[Pasted image 20241107003108.png]]

![[Pasted image 20241107003149.png]]