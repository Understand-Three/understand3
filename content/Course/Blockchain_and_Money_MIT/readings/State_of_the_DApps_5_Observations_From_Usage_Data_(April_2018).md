---
title: DApp 的状态：使用数据中的 5 个观察结果（2018 年 4 月）
draft: true
---
Naval Ravikant recently shared this thought:  
Naval Ravikant 最近分享了这个想法：

> “The dirty secrets of blockchains: they don’t scale (yet), aren’t really decentralized, distribute wealth poorly, lack killer apps, and run on a controlled Internet.”  
> “区块链的肮脏秘密：它们（还）没有扩展，还没有真正去中心化，财富分配不善，缺乏杀手级应用程序，并且在受控的互联网上运行。”  
> [_https://twitter.com/naval/status/983016288195829770_](https://twitter.com/naval/status/983016288195829770)

In this post, I want to dive into his fourth observation that blockchains “lack killer apps” and understand just how far away we are to real applications (not tokens, not store of value, etc.) being built on top of blockchains.  
在这篇文章中，我想深入探讨他的第四个观察，即区块链“缺乏杀手级应用程序”，并了解我们距离构建在区块链之上的真实应用程序（不是代币、不是价值储存等）有多远。

Thanks to [Dappradar](https://dappradar.com/), I was able to analyze the top decentralized applications (DApps) built on top of Ethereum, the largest decentralized application platform. My research is focused on live public DApp’s which are deployed and usable today. This does not include any future or potential applications not deployed yet.  
多亏了 [Dappradar](https://dappradar.com/)，我能够分析构建在最大的去中心化应用程序平台 Ethereum 之上的顶级去中心化应用程序 （DApp）。我的研究重点是目前已部署和可用的实时公共 DApp。这不包括任何尚未部署的未来或潜在应用程序。

If you look at a broad overview of the 312 DApps created, the main broad categories are:  
如果您查看创建的 312 个 DApp 的广泛概述，主要的宽泛类别是：

I. Decentralized Exchanges  
I. 去中心化交易所  
II. Games (Largely collectible type games, excluding casino/games of chance)  
II. 游戏（主要是收藏类型的游戏，不包括赌场/机会游戏）  
III. Casino Applications III. 赌场应用  
IV. Other (we’ll revisit this category later)  
IV. 其他（我们稍后会再次讨论此类别）

![](https://miro.medium.com/v2/resize:fit:764/0*WdbahASGhnCwiFbw.)

On closer examination, it becomes clear only a few individual DApps make up the majority of transactions within their respective category:  
仔细研究会发现，只有少数单独的 DApp 构成了各自类别中的大部分交易：

![](https://miro.medium.com/v2/resize:fit:2000/0*X6PFWJ5bonpGaMi2.)

Diving into the “Other” category, the largest individual DApps in this category are primarily pyramid schemes: [PoWH 3D](https://powh.io/index.html), [PoWM](https://powm.io/), [PoWL](https://powl.io/), [LockedIn](https://lockedin.io/), etc. (*Please exercise caution, all of these projects are actual pyramid schemes.)  
深入到“其他”类别，该类别中最大的单个 DApp 主要是金字塔计划：[PoWH 3D](https://powh.io/index.html)、[PoWM](https://powm.io/)、[PoWL](https://powl.io/)、[LockedIn](https://lockedin.io/) 等（*请谨慎使用，所有这些项目都是真正的金字塔计划。

These top DApps are all still very small relative to traditional consumer web and mobile applications.  
相对于传统的消费者 Web 和移动应用程序，这些顶级 DApp 仍然非常小。

![](https://miro.medium.com/v2/resize:fit:1400/1*nPFYDhAPdTZG2Hb36xbcpg.png)

*Even “Peak DApp” isn’t that large: by our rough estimates, CryptoKitties only had ~14,000 unique users and 130,000 transactions daily.  
*即使是“Peak DApp”也没有那么大：根据我们的粗略估计，CryptoKitties 每天只有 ~14,000 个独立用户和 130,000 笔交易。

Compared to: 与以下比较：

![](https://miro.medium.com/v2/resize:fit:1400/1*fp4lwnsH7LdTEbNiKOthQw.png)

*As another comparison point, even the top 50 apps in the Google Play Store alone get on average 25,000+ downloads per day. (This is just downloads, not even counting “transactions”).  
*作为另一个比较点，即使是 Google Play 商店中排名前 50 的应用，平均每天的下载量也达到 25,000+ 次。（这只是下载量，甚至不算“交易”）。

Further trends emerge on closer inspection of the transactions of DApps tracked here:  
仔细检查此处跟踪的 DApp 交易后，会出现进一步的趋势：

- More than half of all DApps have zero transactions in the last week.  
    超过一半的 DApp 在上周没有交易。
- Of the DApps with any usage, the majority of usage is skewed to a small few (see graph).  
    在有任何使用情况的 DApp 中，大部分使用量偏向于少数（见图表）。
- Only 25% of DApps have more than 100 transactions in a week.  
    只有 25% 的 DApp 在一周内有超过 100 笔交易。

![](https://miro.medium.com/v2/resize:fit:1400/0*PkY_axf1bbTVvkUW.)

# **Takeaways 要点**

**Where we are and what it means for protocols and the ecosystem:  
我们在哪里，这对协议和生态系统意味着什么：**

After looking through the data, my personal takeaways are:  
在浏览了数据之后，我个人的收获是：

1. ==We are orders of magnitudes away from consumer adoption of DApps. No killer app (outside of tokens and trading) have been created yet.== Any seemingly “large” DApp (ex. IDEX, CryptoKitties, etc) has low usage overall.  
    ==我们距离消费者采用 DApp 还有几个数量级的距离。尚未创建杀手级应用程序（除了代币和交易）。==任何看似“大型”的 DApp（例如 IDEX、CryptoKitties 等）总体使用率较低。
2. All of the top DApps are still very much about speculation of value. Decentralized exchanges, casino games, pyramid schemes, and even the current collectible games (I would argue) are all around speculation.  
    所有顶级 DApp 仍然非常注重价值投机。去中心化交易所、赌场游戏、传销，甚至当前的收藏游戏（我认为）都是围绕着投机的。
3. What applications (aside from value transfer and speculation) really take advantage of the true unique properties of a blockchain (censorship resistance, immutability of data, etc) and unlock real adoption?  
    哪些应用程序（除了价值转移和投机）真正利用了区块链真正独特的属性（抗审查性、数据不变性等）并解锁了真正的采用？
4. For new protocol developers, instead of trying to convince existing DApp developers to build on your new platform — think hard about what DApps actually make sense on your protocol and how to help them have a chance at real adoption.  
    对于新的协议开发者来说，与其试图说服现有的 DApp 开发者在你的新平台上构建，不如认真思考哪些 DApp 在你的协议上真正有意义，以及如何帮助他们有机会真正被采用。
5. We as an ecosystem need to build better tools and infrastructure for more widespread adoption of DApps. [Metamask](https://metamask.io/) is an awesome tool, but it is still a difficult onboarding step for most normal users. [Toshi](https://www.toshi.org/), [Status](https://status.im/), and [Cipher](https://www.cipherbrowser.com/) are all steps in the right direction and I’m really looking forward to the creation of other tools to simplify the user onboarding experience and improve general UI/UX for normal users.  
    作为一个生态系统，我们需要构建更好的工具和基础设施，以便更广泛地采用 DApp。[Metamask](https://metamask.io/) 是一个很棒的工具，但对于大多数普通用户来说，它仍然是一个困难的入门步骤。[Toshi](https://www.toshi.org/)、[Status](https://status.im/) 和 [Cipher](https://www.cipherbrowser.com/) 都是朝着正确方向迈出的一步，我真的很期待创建其他工具来简化用户入门体验并改善普通用户的通用 UI/UX。

What kind of DApps do you think we as a community should be building? Would love to hear your takeaways and thoughts about the state of DApps, feel free to comment below or tweet @mccannatron.  
您认为我们作为一个社区应该构建什么样的 DApp？很想听听您对 DApp 现状的见解和想法，请随时在下面发表评论或在 @mccannatron 推特上发表评论。

Also, if there are any DApps or UI/UX tools I should be paying attention to, let me know — I would love to check them out.  
此外，如果有任何我应该关注的 DApp 或 UI/UX 工具，请告诉我 — 我很想看看它们。

Thanks to [Noah Jessop](https://twitter.com/njess), Kim McCann, [Ricky Tan](https://twitter.com/rkstan), [Linda Xie](https://twitter.com/ljxie), [Anatoly Yakovenko](https://twitter.com/aeyakovenko), and [Edith Yeung](https://twitter.com/edithyeung) for providing feedback on this post.  
感谢 [Noah Jessop](https://twitter.com/njess)、Kim McCann、[Ricky Tan](https://twitter.com/rkstan)、[Linda Xie](https://twitter.com/ljxie)、[Anatoly Yakovenko](https://twitter.com/aeyakovenko) 和 [Edith Yeung](https://twitter.com/edithyeung) 对本文提供反馈。

P.S. — I also write a weekly newsletter of the best crypto events in the SF Bay Area. Subscribe here: > [https://www.cryptoweek.ly/](https://www.cryptoweek.ly/)  
P.S. — 我还每周写一份关于旧金山湾区最佳加密活动的时事通讯。在此处订阅： > [https://www.cryptoweek.ly/](https://www.cryptoweek.ly/)