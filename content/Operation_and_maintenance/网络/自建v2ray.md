---
title: 自建 v2ray
draft: true
---
# 方法一
## [自 建 v2ray](https://www.triadprogram.com/v2ray-build-by-yourself)


[10条评论](https://www.triadprogram.com/v2ray-build-by-yourself/#comments) / [vpn](https://www.triadprogram.com/vpn/) / 作者： [superddk](https://www.triadprogram.com/author/admin/)

现在科学上网工具中最好用的就是 `V2Ray` 机场，不过，一到晚上高峰期、或者敏感时期，不管你买便宜、还是贵的机场，统统都慢，便宜的机场直接就是没法翻墙。这都是好的了，有的机场直接捐款跑路，我们也只能干瞪眼。

所以，既然机场都是通过V2Ray 来实现，原理也简单，所以我们干脆就 自 建 v2ray，网上一堆教程，包括官网也有，博主自己也试过，只要选对了vps服务商，效果一流。 另外，文章中提到的几个网站，基本都需要翻墙才能访问，为此可以先注册[威伯斯云](https://www.triadprogram.com/vps000_sign_up)，它提供2小时的免费试用，注册好后，就可以翻墙出去，具体注册方法可以参考[威伯斯云的测评](https://www.triadprogram.com/vpn-cisco-anyconnect-hongkong-vpn-services/)。这篇文章主要将具体步骤列出来，供大家参考。

文章目录

[注册域名](https://www.triadprogram.com/v2ray-build-by-yourself/#%E6%B3%A8%E5%86%8C%E5%9F%9F%E5%90%8D)[注册账号](https://www.triadprogram.com/v2ray-build-by-yourself/#%E6%B3%A8%E5%86%8C%E8%B4%A6%E5%8F%B7)[购买域名](https://www.triadprogram.com/v2ray-build-by-yourself/#%E8%B4%AD%E4%B9%B0%E5%9F%9F%E5%90%8D)[域名注册后的一些设置](https://www.triadprogram.com/v2ray-build-by-yourself/#%E5%9F%9F%E5%90%8D%E6%B3%A8%E5%86%8C%E5%90%8E%E7%9A%84%E4%B8%80%E4%BA%9B%E8%AE%BE%E7%BD%AE)[cloudflare中进行dns设置](https://www.triadprogram.com/v2ray-build-by-yourself/#cloudflare%E4%B8%AD%E8%BF%9B%E8%A1%8Cdns%E8%AE%BE%E7%BD%AE)[vps推荐Vultr](https://www.triadprogram.com/v2ray-build-by-yourself/#vps%E6%8E%A8%E8%8D%90Vultr)[概述](https://www.triadprogram.com/v2ray-build-by-yourself/#%E6%A6%82%E8%BF%B0)[价格](https://www.triadprogram.com/v2ray-build-by-yourself/#%E4%BB%B7%E6%A0%BC)[自 建 v2ray–xray设置](https://www.triadprogram.com/v2ray-build-by-yourself/#%E8%87%AA_%E5%BB%BA_v2ray%E2%80%93xray%E8%AE%BE%E7%BD%AE)[服务器端的设置](https://www.triadprogram.com/v2ray-build-by-yourself/#%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%AB%AF%E7%9A%84%E8%AE%BE%E7%BD%AE)[服务器端面板设置](https://www.triadprogram.com/v2ray-build-by-yourself/#%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%AB%AF%E9%9D%A2%E6%9D%BF%E8%AE%BE%E7%BD%AE)[客户端–Qv2ray设置](https://www.triadprogram.com/v2ray-build-by-yourself/#%E5%AE%A2%E6%88%B7%E7%AB%AF%E2%80%93Qv2ray%E8%AE%BE%E7%BD%AE)[小结](https://www.triadprogram.com/v2ray-build-by-yourself/#%E5%B0%8F%E7%BB%93)

## 注册域名

---

域名服务商很多很多，我们的目的是建设机场，成本要控制好，我推荐在[namesilo](https://www.triadprogram.com/namesilo)购买–6元人民币/年。这是个不错的地方，域名便宜的–适合做翻墙的“掩护网站”。另外，还提供隐私保护–其他域名服务网站大多收费，这功能还是有必要的。

### 注册账号

![在namesilo购买](https://www.triadprogram.com/wp-content/uploads/2021/08/namesilo%E7%94%A8%E6%88%B7%E6%B3%A8%E5%86%8C-1024x403.png)

在[NameSoli](https://www.namesilo.com/?rid=3853d48oc&gad_source=1)注册账号

### 购买域名

![在namesilo选择域名](https://www.triadprogram.com/wp-content/uploads/2021/08/namesilo%E5%9F%9F%E5%90%8D%E9%80%89%E6%8B%A9-1024x571.png)

在[namesilo](https://www.triadprogram.com/namesilo)购买注册，可以使用支付宝，最便宜的0.99美元，用1年。

选择好域名后，就可以继续下一步设置：

![在namesilo进行域名设置](https://www.triadprogram.com/wp-content/uploads/2021/08/namesilo%E5%9F%9F%E5%90%8D%E9%80%89%E9%A1%B9-998x1024.png)

- 注意这里先选择：WHOIS Privacy（保护隐私）
    
- 其他选项不需要更改，继续
    

之后就简单了：选择支付宝–先填入支付宝账号，然后扫描付款就搞定了。

### 域名注册后的一些设置

买了域名之后，我们还要进行一些简单设置，主要是把namesilo中的dns域名解释服务去掉，我们用cloudflare来干这些。另外，第一次使用 namesilo，多少人（包括我自己）不知道购买的域名在那里找，所以，写个说明给大家参考。

第一步：在网站的右上部分选择 `My Account`

![第一步：在网站的右上部分选择--My Account](https://www.triadprogram.com/wp-content/uploads/2021/08/%E5%9C%A8%E7%BD%91%E7%AB%99%E7%9A%84%E5%8F%B3%E4%B8%8A%E9%83%A8%E5%88%86%E9%80%89%E6%8B%A9%EF%BC%9AMy-Account-1024x264.png)

第二步：在你的账号中选择刚才购买的域名

![第二步：在你的账号中选择刚才购买的域名](https://www.triadprogram.com/wp-content/uploads/2021/08/%E7%AC%AC%E4%BA%8C%E6%AD%A5%EF%BC%9A%E5%9C%A8%E4%BD%A0%E7%9A%84%E8%B4%A6%E5%8F%B7%E4%B8%AD%E9%80%89%E6%8B%A9%E5%88%9A%E6%89%8D%E8%B4%AD%E4%B9%B0%E7%9A%84%E5%9F%9F%E5%90%8D-1024x871.png)

第三步：按上面👆那个 `1`（表示我刚才买了1个域名），进去后就看到下面👇的东东，按下那个浅蓝色的图标

![第三步：按上面👆那个‘1’（表示我刚才买了1个域名），进去后就看到下面👇的东东，按下那个浅蓝色的图标](https://www.triadprogram.com/wp-content/uploads/2021/08/%E6%8C%89%E4%B8%8B%E9%82%A3%E4%B8%AA%E6%B5%85%E8%93%9D%E8%89%B2%E7%9A%84%E5%9B%BE%E6%A0%87.png)

第四部：删除里面所以的DNS设置，剩下我截图这个样子😄

![第四部：删除里面所以的DNS设置，剩下我截图这个样子😄](https://www.triadprogram.com/wp-content/uploads/2021/08/%E5%88%A0%E9%99%A4%E9%87%8C%E9%9D%A2%E6%89%80%E4%BB%A5%E7%9A%84DNS%E8%AE%BE%E7%BD%AE-1024x215.png)

到此为止，购买域名的部分就解释了，**保留namesilo页面，下面还要用到**。

## cloudflare 中进行dns设置

第一步，去cloudflare网站注册一个免费的账号，cloudflare 有中文，在右上角可以选择。至于为什么用cloudflare进行dns解释，大家有兴趣可以谷歌一下。反正就是好用，好用到当你开网店流量越来越大的时候，一定会付费买他们的服务。

第二步，把购买的域名输入，然后按下“添加站点”

![第二步，把购买的域名输入，然后按下“添加站点”](https://www.triadprogram.com/wp-content/uploads/2021/08/%E6%8A%8A%E8%B4%AD%E4%B9%B0%E7%9A%84%E5%9F%9F%E5%90%8D%E8%BE%93%E5%85%A5-1024x375.png)

第三步，跟着一直按3步，直到我们的目标–“更改名称服务器”

![更改名称服务器](https://www.triadprogram.com/wp-content/uploads/2021/08/%E6%9B%B4%E6%94%B9%E5%90%8D%E7%A7%B0%E6%9C%8D%E5%8A%A1%E5%99%A8-1024x286.png)

第四步，将这个网页拉下一些，可以看到”添加 cloudflare 名称服务器“

![添加cloudflare名称服务器](https://www.triadprogram.com/wp-content/uploads/2021/08/%E6%B7%BB%E5%8A%A0cloudflare%E5%90%8D%E7%A7%B0%E6%9C%8D%E5%8A%A1%E5%99%A8.png)

第五步之1，将上面这两个东西 copy 到 namesilo 中。这个就是 cloudflare 提供给我们的免费 dns 服务。把这两个贴到 namesilo 的相应位置，如下图：

- 首先，按下 “Click here to select our **Premium**…..”
    
- 接着就可以拷贝这两个 dns了，将多余的dns删除掉。
    

![namesilo的相应位置](https://www.triadprogram.com/wp-content/uploads/2021/08/namesilo%E7%9A%84%E7%9B%B8%E5%BA%94%E4%BD%8D%E7%BD%AE-1024x487.png)

第五步之2，上面这个东东，在namesilo中–你的账号–选择购买的域名–最后选下面这个图标。回头看看上面的章节就知道在哪了。

![namesilo dns设置](https://www.triadprogram.com/wp-content/uploads/2021/08/namesilo%E4%B8%AD%E7%9A%84%E4%BD%8D%E7%BD%AE.png)

第五步之3，在 namesilo中不要忘记提交，很快就有结果。

![namesilo提交](https://www.triadprogram.com/wp-content/uploads/2021/08/namesilo%E6%8F%90%E4%BA%A4.png)

第五步之4，在namesilo中核对一下返回的结果（刷新一下网页），如果是Cloudflare提供的dns就搞定了。

![核对结果](https://www.triadprogram.com/wp-content/uploads/2021/08/%E6%A0%B8%E5%AF%B9%E7%BB%93%E6%9E%9C-1024x252.png)

第六步，返回到Cloudflare页面中，选择“完成，检查名称服务器“

![检查名称服务器](https://www.triadprogram.com/wp-content/uploads/2021/08/%E5%AE%8C%E6%88%90%EF%BC%8C%E6%A3%80%E6%9F%A5%E5%90%8D%E7%A7%B0%E6%9C%8D%E5%8A%A1%E5%99%A8.png)

第七步，接着这部直接按完成就行，并会进入下面这个页面。我们选择Cloudflare图标–返回首页。

![选择Cloudflare图标](https://www.triadprogram.com/wp-content/uploads/2021/08/%E5%9B%9E%E5%88%B0%E9%A6%96%E9%A1%B5-1024x651.png)

第八步，选择“电子邮箱验证”，加快进程。不这样做，可能要等Cloudflare干很久😭。验证成功，会在域名前面出现一个绿色的✅

![电子邮箱验证](https://www.triadprogram.com/wp-content/uploads/2021/08/%E8%BF%9B%E8%A1%8C%E7%94%B5%E5%AD%90%E9%82%AE%E7%AE%B1%E9%AA%8C%E8%AF%81-1024x346.png)

第九步，修改SSL/TLS mode。

![修改SSL/TLS mode](https://www.triadprogram.com/wp-content/uploads/2021/08/%E4%BF%AE%E6%94%B9SSLTLS-mode-1024x713.png)

第十步，添加一条“解析”记录。

![添加一条记录](https://www.triadprogram.com/wp-content/uploads/2021/08/%E6%B7%BB%E5%8A%A0A%E8%AE%B0%E5%BD%95-1-1024x637.png)

终于搞定，这里的每一步都不要出错。后面安装vps的时候，如果出现错误提示，一定是以上步骤出了问题。不要怀疑命令行的问题，很多安装说明并没有提到上面的所有步骤。

## vps推荐[Vultr](https://www.triadprogram.com/vultr)

![Vultr主页](https://www.triadprogram.com/wp-content/uploads/2022/11/VULTR-1024x357.png)

[Vultr](https://www.triadprogram.com/vultr)是目前公认服务器性能最好的VPS服务商，而且套餐价格非常灵活，可否丰俭由人，选择最便宜的套餐也不会比垃圾vps贵多少，而且可以免费更换vps的IP地址。使用之前，ping一下速度如何，不行换一个就是了。

另外，[Vultr](https://www.triadprogram.com/vultr)在国内被墙了的话，推荐大家去[威伯斯云](https://www.triadprogram.com/vps000_sign_up)注册一个账号，可以得到2小时免费上网时间。相信2小时足够各位搞定，实在不行，买一个月，威伯斯云支持退款。

### 概述

目前支持17个国家/地区的服务器，在使用过程中，可以随时停用或删除，然后切换到任何一个你想要的服务器位置。其计费方式是**按照小时计费**，意味着您如果遇到IP被封的情况，可以随时删除当前的服务器，新建一个服务器获取新的IP地址，即可正常使用，十分方便。

国内用户选择**洛杉矶**或**硅谷**的服务器，根据我的测试，这两个地方的延迟最低，可能是国内使用的用户数量较少的原因。

### 价格

![VULTR 价格](https://www.triadprogram.com/wp-content/uploads/2022/11/VULTR-%E4%BB%B7%E6%A0%BC.png)

对于只用于翻墙使用的VPS，我们使用最低配置即可，每月只需$6美金。支付方式支持信用卡、Paypal、**支付宝**。

通过本站链接注册：**首充20美金，即可赠送100美金**。

[Vultr 优惠链接](https://www.triadprogram.com/vultr)

## 自 建 v2ray–xray设置

自建机场，大概分成两个部分：vps 服务器端的设置，客户端的设置。

- 客户端安装一个软件就搞定；
    
- vps服务器端有点麻烦，最好是安装一个图形界面，方便设置，而通常的“一键安装脚本”就是干这个的。


下面用的是 `X-ui` 面板，[GitHub有安装说明](https://github.com/vaxilu/x-ui)。有空大家可以去看看，我自己按照他们的说明安装了一下，代码本身没问题。不过，如果你是第一次折腾这些，最好还是按照我上面介绍的关于：vps、Cloudflare的相关步骤进行设置。还有，代码报错，不用怀疑代码有问题😄

### 服务器端的设置

#### 安装 X-ui 面板

第一步，申请 SSL 证书

下面环境的安装方式，大家根据自己的系统选择命令安装就好了。
```bash
#debain / ubuntu
apt update -y # Debian/Ubuntu 命令
apt install -y curl #Debian/Ubuntu 命令
apt install -y socat #Debian/Ubuntu 命令

# centos
yum update -y #CentOS 命令
yum install -y curl #CentOS 命令
yum install -y socat #CentOS 命令
```


第二步，安装 Acme 脚本
```bash
curl https://get.acme.sh | sh
```


第三步，80 端口空闲的证书申请方式

自行更换代码中的域名、邮箱为你解析的域名及邮箱
```bash
~/.acme.sh/acme.sh --register-account -m xxxx@xxxx.com

~/.acme.sh/acme.sh --issue -d de.申请的域名.xyz --standalone
```


注意：第2段命令，如果出错，就是因为Cloudfare设置的第十步出了问题–记得将它改成：**de.申请的域名.xyz**

第四部，安装证书到指定文件夹。注意：更换代码中的域名为你解析的域名。
```bash
~/.acme.sh/acme.sh --installcert -d mydomain.com --key-file /root/private.key --fullchain-file /root/cert.crt
```


第五步，安装 & 升级 X-ui 面板
```bash
bash <(curl -Ls https://raw.githubusercontent.com/sprov065/x-ui/master/install.sh)
```


最后这行完成，在你的命令行中，应该可以看到下面安装成功的画面 🎉🎉

![安装成功](https://www.triadprogram.com/wp-content/uploads/2021/08/%E9%9D%A2%E6%9D%BF%E5%AE%89%E8%A3%85%E5%AE%8C%E6%88%90-1024x634.png)

### 服务器端面板设置

![服务器端面板设置](https://www.triadprogram.com/wp-content/uploads/2021/08/xray%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%AB%AF-1024x404.png)

在浏览器中输入：购买的 vps的IP地址，加上端口号54321，记得中间加个“分号”，这样就可以进入面板管理xray服务器端了。

进入正题，建立一个入站协议，方便我们的客户端进行连接。这里其实包括了10个小步骤，改改就行。

![入站协议](https://www.triadprogram.com/wp-content/uploads/2021/08/%E5%85%A5%E7%AB%99%E5%8D%8F%E8%AE%AE-1024x701.png)

上面步骤中，需要注意的：

- `id` –是一串数字，要拷贝到后面将的客户端的相应位置；
    
- 第8、9两步中，域名：是之前在 `Cloudflare` 设置中第十步中“解释”过的域名，比如：`de.购买的域名`；
    
- 证书文件路径：`/root/cert.crt`
    
- 密钥文件路径：`/root/private.key`
    

这两个文件存放的位置—如果你按照了ftp软件，进去就可以看到他们位于root根目录下面

![文件存放的位置](https://www.triadprogram.com/wp-content/uploads/2021/08/%E8%AF%81%E4%B9%A6%E8%B7%AF%E5%BE%84.png)

我在macOS下面，比较喜欢用Transmit–好用，ssh可以建立持久连接。当然，也可以通过命令进行持久连接的设置。

### 客户端–Qv2ray设置

[Qv2ray](https://www.triadprogram.com/v2ray-client/)最新版支持xray的vless协议，这个链接是我的博客中的，大家也可以直接去[Qv2ray GitHub官方下载](https://github.com/Qv2ray/Qv2ray/releases)。Qv2ray是全平台的包括：windows、macos、linux，我觉得是最好用的。当然手机版还是推荐[v2rayNG](https://www.triadprogram.com/v2ray-client/)。

`Qv2ray` 已经停止更新了，大家可以 `clash`、`clashx`、`v2rayN`，设置大同小异。

Qv2ray 的相应设置我截图如下：

![Qv2ray的相应设置1](https://www.triadprogram.com/wp-content/uploads/2021/08/Qv2ray%E7%9A%84%E7%9B%B8%E5%BA%94%E8%AE%BE%E7%BD%AE1-1024x412.png)

![Qv2ray的相应设置2](https://www.triadprogram.com/wp-content/uploads/2021/08/Qv2ray%E7%9A%84%E7%9B%B8%E5%BA%94%E8%AE%BE%E7%BD%AE2-1024x383.png)

设置好，连接就OK了！Qv2ray已经停止更新了，我推荐用[v2rayNG](https://github.com/2dust/v2rayNG)，设置大同小异。

## 小结

这套方案，比起传统的v2ray方案，复杂了很多。主要是两点：增加了“掩护网站”，增加了Cloudflare解释DNS。实际上，速度下降了一点，毕竟多了解析证书、解析网站的过程；安全性提高了多少，只有电信局知道。实际上，原来的v2ray方案就已经很难识别，除非是机场这种大流量的活动。

话说回来，折腾了这个东西出来自己用，不要干违法的事情，不要拿出去卖钱经营就没事。自己用是没啥大问题的，包括使用各种翻墙软件。

萝莉啰嗦了一大堆，希望各位玩的开心！另外，我也不能保证以上方法能够一直管用，所以，还是推荐两个比较保险的机场给大家备用：

[极客云优惠链接](https://www.triadprogram.com/jike)

[速云梯优惠链接](https://www.triadprogram.com/suyunti)

**极客云**机场架设了多年（5年是以上），就算最紧张的时刻，他们的网站也都可以登陆。[速云梯](https://www.triadprogram.com/suyunti)也是他们最近搞出了的新机场，速度更快、延时更少。极客云由于人多，普通套餐经常卡，所以，他们搞多一个机场，分流我这样的老客户，我建议新客户也分流进去吧。




---
# 方法二

## [【小白福利】2024 最新 V2Ray 搭建图文教程，V2Ray 一键搭建脚本！](https://www.itblogcn.com/article/406.html)

2024-06-16

**此教程 2024/05/22 日更新并测试通过!!!**

一键搭建 V2Ray，小白福利一条命令搞定 V2Ray 搭建，最详细的 V2Ray 图文教程！

## 前言

此教程面向小白萌新，从创建 VPS 到使用 SSH 登录并安装和配置 V2Ray，尽量详细一些，老鸟可以直接跳到 [第四部分](https://www.itblogcn.com/article/406.html#title-7)。

## 第一部分：环境信息

- 服务器系统：Centos7 ×64+、Ubuntu、Debian 等系统兼容本教程
    
- VPS：我使用的是 [Vultr](https://www.itblogcn.com/vultr)
    
- 手机和电脑都支持搭建
    

## 第二部分：创建服务器

已有服务器的同学可以跳过这部分，没有服务器的同学可以先创建服务器，我使用的是 [Vultr](https://www.itblogcn.com/vultr)。

[Vultr VPS](https://www.itblogcn.com/vultr/t) 推出了 **2024 年最新的限时促销活动**，「新用户」，充多少送多少活动力度相当巨大！！用于建站、学习、自建网盘或各种网络服务等等都很实用，优势是价格低，按时计费，随时更换 IP。有购买海外 [VPS](https://www.itblogcn.com/vultr) 需求的同学就得抓紧机会了。

> **Vultr 目前活动：**
> 
> 1. 【**推荐**】新用户，**优惠码：**`VULTRMATCH` **，赠金：**充多少送多少，最高100美元；**赠金有效期：**365天，**付款方式：**PayPal、支付宝、信用卡
>     
> 2. 新用户，**优惠码：**`FLYTWOHUNDRED` ，**赠金：**200美元；**赠金有效期：**30天，**付款方式：**信用卡、PayPal (此活动不支持支付宝)。
>     

**Vultr 活动地址：**[https://www.itblogcn.com/vultr/t](https://www.itblogcn.com/vultr/t)

**Vultr 注册教程：**[注册 Vultr 教程和创建 VPS 服务器教程](https://www.itblogcn.com/article/registervultr.html)

预算充足的朋友也可以选择搬瓦工的 VPS 服务器，其 **CN2 GIA** 专线网速极快。

**搬瓦工注册教程(内附优惠券)：**[https://www.itblogcn.com/article/bwg-register.html](https://www.itblogcn.com/article/bwg-register.html)

**搬瓦工 VPS 在售列表一览：**[https://www.itblogcn.com/bwg/index.html](https://www.itblogcn.com/bwg/index.html)

**Tips：**以上 2 家都支持支付宝支付。

## 第三部分：JuiceSSH 或 Xshell 或 Windows自带工具连接服务器

准备好你的服务器，确认账号（一般是 root）和密码，系统建议 Centos7 ×64+、Ubuntu、Debian

### ★ 手机 JuiceSSH 连接服务器教程

**官网：**[https://juicessh.com/](https://juicessh.com/)

**下载地址：**[https://juicessh-builds.s3.amazonaws.com/juicessh-v3.2.2_200.apk](https://juicessh-builds.s3.amazonaws.com/juicessh-v3.2.2_200.apk)

安装好后，连接 VPS 服务器步骤如下：

(1）进入JuiceSSH

(2）点上侧连接

(3）点右下角+

(4）昵称随意，类型SSH，地址你的服务器ip（外网IP），端口默认22不变（映射端口和自设端口除外）

(5）认证选新建

(6）昵称随意，用户名一般为root，密码填你的服务器密码

(7）点右上角√

(8）再点右上角√

(9）点你设置的配置，如无昵称就是以服务器ip命名

(10）如无意外，这时就自动登陆服务器了，如果提示你输入密码，再输一遍就行了，输入后记得点保存

(11）进入服务器后，就可以运行代码了，本机键盘手打或者复制粘帖均可

### ★ 电脑端 Windows 系统自带方式连接服务器教程(201809之后的系统自带)

[[CMD] Windows SSH 连接服务器教程(系统自带方式)](https://www.itblogcn.com/article/2266.html)

### ★ 电脑端 XShell 连接服务器教程

**官网下载地址：**[https://www.xshell.com/zh/free-for-home-school/](https://www.xshell.com/zh/free-for-home-school/)

电脑用 **XShell** 连接 VPS 服务器，步骤如下：

(1）进入XShell

(2）点左上角文件

(3）点新建

(4）名称随意，协议SSH，主机你的服务器IP（外网IP），端口默认22不变（映射端口和自设端口除外）

(5）确定

(6）在左侧会话管理器，选中设置的配置双击打开

(7）提示输入账号和密码，输入后记得点保存(没有提示可能IP被墙)

(8）进入服务器后，就可以运行代码了，本机键盘手打或者复制粘帖均可

Copy

> **注意：假如连不上服务器，可能是 IP 被墙，或者是 TCP 阻断了，建议重新创建服务器，并且删除原有的。**

![20181231151835.png](https://www.itblogcn.com/wp-content/uploads/2020/04/img_5ea111dd73c13.png) ![img](https://www.itblogcn.com/wp-content/uploads/2020/04/img_5ea111fdeb54d.png)

## 第四部分：V2Ray 搭建

新的一键 V2Ray 脚本，经过笔者的测试，安装简单方便，自动关闭防火墙，自动安装 BBR 加速，因此推荐大家使用！

**安装命令：**

输入以下命令一键安装，回车执行（`shift+insert`可粘贴）

```bash
bash <(curl -s -L https://git.io/v2ray-setup.sh)
```

老鸟可以用这个自定义安装：
```bash
bash <(curl -s -L https://git.io/v2rayinstall.sh)
```

**如果要解锁 ChatGPT 可以执行以下命令（利用 `CloudFlare WARP` 解锁）**：

> 先不解锁直接用代里访问ChatGPT, 如果可以正常访问就不需要解锁了.

```bash
bash <(curl -s -L https://raw.githubusercontent.com/xyz690/v2ray/master/unlock_chatgpt.sh)
```

显示一下信息代表安装成功（可直接用以下配置进行连接）(以下配置在链接时使用)：

```bash
---------- V2Ray 配置信息 -------------
 地址 (Address) = 207.148.27.37
 端口 (Port) = 8080
 用户ID (User ID / UUID) = 20be1f8e-2169-4aa1-843e-5ead4250a9f7
 额外ID (Alter Id) = 0
 传输协议 (Network) = kcp
 伪装类型 (header type) = dtls
---------- END -------------
V2Ray 客户端使用教程: https://git.io/v2ray-client
提示: 输入 v2ray url 可生成 vmess URL 链接 / 输入 v2ray qr 可生成二维码链接
---------- V2Ray vmess URL / V2RayNG v0.4.1+ / V2RayN v2.1+ / 仅适合部分客户端 -------------
vmess://ewoidiI6I*****g==
```

**配置文件要注意(建议直接复制安装结果中 `vmess://****`地址，直接导入，避免自己填配置出错)：**

> Network(传输协议)： kcp 
> type(伪装类型)：dtls 
> 不对的话连不上！！！

好了到这里我们就搭建成功了(_▽_)

**相关命令：**

> `v2ray info` 查看 V2Ray 配置信息
> `v2ray config` 修改 V2Ray 配置 
> `v2ray link` 生成 V2Ray 配置文件链接 
> `v2ray infolink` 生成 V2Ray 配置信息链接 
> `v2ray qr` 生成 V2Ray 配置二维码链接 
> `v2ray ss` 修改 Shadowsocks 配置 
> `v2ray ssinfo` 查看 Shadowsocks 配置信息 
> `v2ray ssqr` 生成 Shadowsocks 配置二维码链接 
> `v2ray status` 查看 V2Ray 运行状态 
> `v2ray start` 启动 V2Ray 
> `v2ray stop` 停止 V2Ray 
> `v2ray restart` 重启 V2Ray 
> `v2ray log` 查看 V2Ray 运行日志 
> `v2ray update` 更新 V2Ray 
> `v2ray update.sh` 更新 V2Ray 管理脚本 
> `v2ray uninstall` 卸载 V2Ray

**vmess 协议配置**

查看配置文件(**该配置在后面链接时使用**)：

```bash
cat /etc/v2ray/config.json
```

![14.png](https://www.itblogcn.com/wp-content/uploads/2020/04/img_5ea11229bca76.png)

## 第五部分：客户端链接 V2Ray

> 最近 GitHub 被 `部分` 运营商 DNS 污染，cmd `ping github.com` 看是不是解析到本机地址 `127.0.0.1`

**解决方案：**

> 网络设置里面设置 DNS 为 `114.114.114.114` 或者 `8.8.8.8`，不会的搜一下。 cmd 执行命令 `ipconfig /flushdns` 清除本地 DNS 缓存

### Windows v2ray 客户端（v2rayN）：

**下载方式一：网盘**

【完整版 v2rayN 带核心，网盘下载地址】：[https://cloud.degoo.com/share/o5JfAH-dE8UepSF3tR4QVg](https://cloud.degoo.com/share/o5JfAH-dE8UepSF3tR4QVg)

> 解压后【点击 v2rayN.exe 启动】

**下载方式二：GitHub 官方**

【完整版 v2rayN 带核心 Github 下载地址】： [https://github.com/2dust/v2rayN/releases/download/5.39/v2rayN-Core.zip](https://github.com/2dust/v2rayN/releases/download/5.39/v2rayN-Core.zip)

> 解压后【点击 v2rayN.exe 启动】

---

其他版本发布列表：[v2rayN.exe Github Releases](https://github.com/2dust/v2rayN/releases)

---

注意电脑右下角 V 图标，双击图标，点右上角 **服务器** ，添加 [VMess] 服务器。

**进行配置:**

客户端的配置需要根据你的服务端进行相应的配置，因为你的服务端协议可能是 vmess 等。

如果你的服务端配置是协议 vmess ，则配置如下：

**注意本教程：**

> Network(传输协议)： kcp
> 
> type(伪装类型)：dtls

不对的话连不上！！！

![v2rayng](https://www.itblogcn.com/wp-content/uploads/2020/04/590ce3a23a8a884.png)

保存后，右键电脑右下角 V 图标：

- **系统代理 ==> 自动配置系统代理**
    
- **路由 ==> 绕开大陆**
    
- **服务器 ==> 选择你添加的节点**
    

### Android v2ray 客户端（v2rayNG）：

**下载方式一：网盘 （APK 直接安装）**

【APK 网盘下载地址】：[https://cloud.degoo.com/share/yDOFoOBbgLmp8sNa6oEX9g](https://cloud.degoo.com/share/yDOFoOBbgLmp8sNa6oEX9g)

**下载方式二：GitHub 官方 APK 直接安装**

> 一般手机是 arm 架构，我就直接给出对应客户端了，其他架构需要你去网上找设备相应的 CPU 架构并进行选择下载：

【安卓版 v2rayNG 带核心 Github 下载地址】[[https://github.com/2dust/v2rayNG/releases/download/1.7.38/v2rayNG_1.7.38_arm64-v8a.apk](https://github.com/2dust/v2rayNG/releases/download/1.7.38/v2rayNG_1.7.38_arm64-v8a.apk)

---

其他版本发布列表：[v2rayNG Github Releases](https://github.com/2dust/v2rayNG/releases)

---

**使用方法:**

(1）打开 v2rayNG APP

(2）点击右上角 + 号

(3）选择 手动输入[Vmess]

(4）别名随意，地址(填服务器外网IP地址)，端口(你设置的V2Ray端口)，用户ID，额外ID:0，加密方式:auto，其他设置默认

(5）右上角 √ 保存

(6）右下角 V图标 点击启动.

(7）打开浏览器试试吧

Copy

### MacOS v2ray 客户端:

[https://github.com/Cenmrev/V2RayX/releases](https://github.com/Cenmrev/V2RayX/releases)

### Linux 内核 v2ray 客户端：

Debian、Ubantu、CentOS 等电脑桌面发行版（不能完全通用，可以尝试一下） [https://github.com/jiangxufeng/v2rayL/releases](https://github.com/jiangxufeng/v2rayL/releases)

### IOS v2ray 客户端：

需要国外账号，推荐 shadow（小火箭）rocket，quantumult（圈），kitsunebi

---

## 测试

打开浏览器，访问`www.google.com`，如下：

![16.png](https://www.itblogcn.com/wp-content/uploads/2020/04/img_5ea10e5244462-300x154.png)

v2ray 搭建教程到此结束，祝大家春风得意！

## 第六部分：v2ray 提速之 BBR

本文脚本对支持 BBR 加速的系统，自动安装 BBR 加速！

CentOS 查看 BBR 是否运行，输入以下命令，回车执行（`shift+insert`可粘贴）：
```bash
lsmod | grep bbr
```

---

  
Q: 楼主你好，我安装了解锁ChatGpt的一键脚本，可是我想卸载，不知道怎么卸载

A: 配置文件 `/etc/v2ray/config.json` 删除这个路由规则就行, 然后重启 v2ray  
```bash
{  
“type”: “field”,  
“outboundTag”: “warp-IPv4”,  
“domain”: [  
“geosite:openai”,  
“ip.gs”  
]  
}
```
  
  Q: 楼主，有一点不明白： “准备好你的服务器，确认账号（一般是 root）和密码，系统建议 Centos7 ×64+、Ubuntu、Debian”是指自己要准备一台安装了上述系统的电脑做服务器还是指购买的远程服务器？
  A: 国外的远程服务器

M: 自定义安装用这个脚本:`bash <(curl -s -L https://git.io/v2rayinstall.sh)`

M: PAC模式：国内网站依旧走本地网络，速度快，绝大部分国外网站都走dai理，速度也快。。

M: 全局模式：所有网站都走dai理，访问国内网站速度变慢。

Q: 推荐的两个服务器哪个便宜快
A: vultr更灵活，随时删除或换IP。  
A: 搬瓦工cn2 gia线路速度非常快。  
A: 想省事就直接用搬瓦工官方梯子：https://www.itblogcn.com/article/1012.html



# 方法三

## 背景

亲爱的小伙伴大家好，今天教大家如何在云服务器上自建机场进行科学上网。

### 为什么自建机场？

Chatgpt的爆火带动了一批科学上网的需求剧增，很多人都是订阅机场来满足科学上网的需求，订阅的机场第一是非常不安全容易暴露个人隐私，第二是使用同一IP的人数太多，像使用来访问chatgpt，非常容易被识别出来然后被封号。所以这种场景下还是自己搭建科学上网梯子最安全，独立的IP地址，同时个人隐私也有保障。

### 为什么不选择国内的云服务器供应商？

自己搭建机场需要一台VPS或者云服务器，拥有一台VPS不仅可以搭建机场，还可以用来部署服务把chatgpt接入各种平台，比如微信，公众号，网站，电报等等。

国内的云服务器供应商，如果搭建科学上网或者部署Chatgpt服务，都面临被封的风险，所以建议有此需求的小伙伴去国外的服务器供应商购买。

## VPS/云服务器

如果你还没有VPS或者云服务器，我给大家推荐一家国外的云服务器供应商[raksmart.com](https://www.raksmart.com/)

它们的`VPS`非常便宜，最便宜的VPS只需要3美刀一个月，你可以在上面自建机场搭建`科学上网`，搭建`个人网站`，也可以用来`接入ChatGPT`。如果你的预算充足，也可以直接购买`云服务器`，也非常便宜，每个月只需要7美刀左右。

![raksmart](https://www.techxiaofei.com/img/vpn/v2ray/raksmart.png)

你购买一个靠谱的机场的价格也差不多这个价，但是自己购买VPS可以在上面自建机场代理，同时还可以接入ChatGPT。有需求的小伙伴可以点此 [http://bit.ly/3GlfucW](http://bit.ly/3GlfucW) 链接注册购买。

## 协议选择

科学上网的技术一直在发展。从最开始的VPN到SS到SSR再到v2ray，像VPN或者SSR这些前些年比较火，但是由于流量特征比较明显，非常容易被识别并被封。所以现在已经很少使用了。

V2Ray使用了新的自行研发的VMess协议，改正了SSR一些已有的缺点，更难被墙检测到。所以V2ray就成了最近非常火的科学上网工具。v2ray要说缺点，那就是配置比较复杂，不过现在越来越多的大牛写了很多一键部署脚本，让小白少走很多弯路，可以轻松一键部署v2ray进行科学上网。

## 快速搭建 v2ray

我们使用Ubuntu服务器来快速搭建v2ray，首先你需要有一台在境外的ubuntu云服务器，

如果没有可以点此地址购买，它们的VPS服务器非常便宜：[http://bit.ly/3GlfucW](http://bit.ly/3GlfucW)

### v2ray 一键脚本安装

我们直接使用大神一键安装脚本。

1. 切换root权限
    
2. 执行v2ray一键安装脚本
    
```bash
sudo su 
bash <(curl -s -L https://git.io/v2ray.sh)
```

如果提示`bash: curl: command not found`，执行如下命令安装curl：
```bash
sudo apt install curl -y
```

### 安装

执行上述命令然后点击Enter

![install](https://www.techxiaofei.com/img/vpn/v2ray/install.png)

输入`1`选择安装

### TCP协议

如果选择TCP协议，之后所有的都选默认（点击Enter即可，不需要输入），点击继续。

## 安装成功

如果提示需要重启服务，选择Yes即可。

![restart](https://www.techxiaofei.com/img/vpn/vpn/restart.png)

### 1.TCP成功

如果你选择的1：TCP。

有几个信息比较重要，是需要配置在你连接v2ray的客户端上的。

![info](https://www.techxiaofei.com/img/vpn/vpn/info.png)

地址（Address）  
端口（Port）  
用户ID（UUID）   
额外ID（Alter ID）

可以保存下来，也可以之后进入到 `/etc/v2ray/config.json` 文件查看。

## 查看

执行完成之后，v2ray已经默认启动了，你可以执行指令查看是否真的启动

### v2ary命令

输入`v2ray`命令查看运行状态： ![run](https://www.techxiaofei.com/img/vpn/vpn/run.png)

显示正在运行代表运行成功。

### Linux命令

linux命令，可以查看v2ray的进程是否存在
```bash
ps -ef | grep -v grep | grep v2ray
```

![grep](https://www.techxiaofei.com/img/vpn/vpn/grep.png)

## 配置信息

如果你刚才保存了地址，端口等配置信息，就不需要查看了，如果忘了保存。

cat /etc/v2ray/config.json

可以查看配置信息

里面的inbounds信息比较重要，也就是入口流量
```bash
"inbounds": [
		{
			"port": 24649,
			"protocol": "vmess",
			"settings": {
				"clients": [
					{
						"id": "16b44a2c-106d-44f2-b4e9-e756b2294044",
						"level": 1,
						"alterId": 0
					}
				]
			},
			"streamSettings": {
				"network": "tcp"
			},
			"sniffing": {
				"enabled": true,
				"destOverride": [
					"http",
					"tls"
				]
			}
		}
]

```

## 防火墙

一般的云服务器都会有防火墙来阻挡非法流量，你需要把刚才的端口加到安全组策略里面。

你可以在个人电脑尝试telent你的IP和端口
```bash
# 例子 telnet IP port，使用你的真实IP和端口代替 
telnet 123.123.123.123 12345
```

如果能联通，说明可以使用，如果不行，那么就需要设置安全组策略。 ![wall](https://www.techxiaofei.com/img/vpn/vpn/wall.png)

- 规则方向选择入口流量
    
- 协议选择自定义TCP
    
- 端口选择你部署的v2ray端口
    
- 授权IP填写 `0.0.0.0/0` 表示所有 IP
    

添加成功之后使用 `telnet IP port`就可以成功了。（使用你的真实IP端口代替）

## 不同平台客户端

每个平台都有多种客户端可以连接v2ray进行科学上网。

客户端连接一般来说只需要填写

地址（Address）  
端口（Port）  
用户ID（UUID）   
额外ID（Alter ID）

我这里每个平台推荐一个软件来进行科学上网。

### 1. Windows

Windows推荐使用Clash For Window客户端，教程可以参考：

[https://www.techxiaofei.com/post/vpn/clash_for_windows/](https://www.techxiaofei.com/post/vpn/clash_for_windows/)

### 2. Android

安卓系统推荐使用 [V2rayNG](https://github.com/2dust/v2rayNG)

点击右边的Release选择最新版下载。

### 3. MacOS

MacOS系统推荐使用ClashX客户端，教程可以参考：

[https://www.techxiaofei.com/post/vpn/clashx/](https://www.techxiaofei.com/post/vpn/clashx/)

### 4. iOS

如果你是`iPhone/iPad`用户，那么最好的选择就是去海外的`App Store`下载 `Shadowrocket`，这是一个付费软件，但是是iOS系统上最好用的代理软件，，支持多种协议。（需海外App Sotre账号）

![iphone_app](https://www.techxiaofei.com/img/vpn/v2ray/iphone_app.png)

只需要配置下面信息即可：

- 协议类型选择你的代理的协议类型，我使用的是v2ary的VMESS协议。
    
- IP/端口/UUID/额外ID 选择你的代理配置即可。 ![ss](https://www.techxiaofei.com/img/vpn/vpn/ss.png)
    

## 结语

我只是推荐了几款我觉得比较好用的客户端，v2ray整体来说配置有一定的难度，如果你需要某个系统的客户端安装配置教程，可以评论区留言，我会单独制作一篇教程。

<全文完>

## 视频教程

本篇博客的视频教程首发于 [**Youtube：科技小飞哥**](https://www.youtube.com/@techxiaofei)，加入 [**电报粉丝群**](https://t.me/+5OzmrG-iyJE2YzM9) 获得最新视频更新和问题解答。

​