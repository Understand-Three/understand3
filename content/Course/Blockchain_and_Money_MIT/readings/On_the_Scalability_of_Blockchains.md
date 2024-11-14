---
title: 关于区块链的可扩展性
link: https://thecontrol.co/on-the-scalability-of-blockchains-ec76ed769405
draft: true
---
作者：[Nick Tomaino](https://ntmoney.medium.com/?source=post_page---byline--ec76ed769405--------------------------------)

Bitcoin and Ethereum, the most widely used blockchains, cannot currently support mainstream transaction usage. They are both supporting mainstream investment usage today, but if blockchains ever become useful for anything beyond investment, solutions that allow them to maintain performance as throughput increases must exist. $300B+ worth of speculative value is a big number for a category of technologies that can’t yet support transaction usage at any scale, but the good news is **there are various approaches attempting to allow blockchains to support mainstream transactional usage.**  
比特币和以太坊是应用最广泛的区块链，目前无法支持主流交易使用。它们都支持当今的主流投资用途，但如果区块链对投资以外的任何事情都有用，那么必须存在允许它们在吞吐量增加时保持性能的解决方案。价值 $300B+ 的投机价值对于一类尚不支持任何规模交易使用的技术来说是一个很大的数字，但好消息是**有多种方法试图让区块链支持主流交易使用。**

> _Use cases are fun to talk about, but use cases beyond investment can’t work well unless scalability is solved  
> 使用案例谈论起来很有趣，但除非解决可扩展性问题，否则超出投资范围的使用案例将无法很好地工作_

## What is the problem? 问题是什么？

Creating a centralized network that supports transaction scalability is not difficult from a technical perspective. Paypal, Visa, and Mastercard and many others have done that before. What is difficult is creating a blockchain system that offers users the optimal combination of scalability, decentralization, and security. Vitalik coined the scalability trilemma [here](https://github.com/ethereum/wiki/wiki/Sharding-FAQ), which states that blockchain systems fundamentally can only have two out of the three following properties:  
从技术角度来看，创建一个支持交易可扩展性的集中式网络并不困难。PayPal、Visa 和 Mastercard 以及许多其他公司以前都这样做过。难的是创建一个区块链系统，为用户提供可扩展性、去中心化和安全性的最佳组合。Vitalik [在这里](https://github.com/ethereum/wiki/wiki/Sharding-FAQ)创造了可扩展性三难困境，它指出区块链系统基本上只能具有以下三个属性中的两个：

- **Decentralization:** defined as the system being able to run in a scenario where each participant only has access to O(c) resources, ie. a regular laptop or small VPS  
    **去中心化：**定义为系统能够在每个参与者只能访问 O（c） 资源的场景中运行，即。普通笔记本电脑或小型 VPS
- **Scalability:** defined as being able to process O(n) > O(c) transactions  
    **可扩展性：**定义为能够处理 O（n） > O（c） 交易
- **Security:** defined as being secure against attackers with up to O(n) resources  
    **安全性：**定义为对拥有多达 O（n） 个资源的攻击者进行安全攻击

Bitcoin and Ethereum were built first and foremost to be decentralized and secure, but sacrificed scalability (Bitcoin supports ~3 transactions per second and Ethereum supports ~12 transactions per second). That has proven to be an effective way to bootstrap a network to date, but also has limitations as the network grows (which we are now starting to see).  
比特币和以太坊首先是为了去中心化和安全而构建的，但牺牲了可扩展性（比特币支持每秒 ~3 笔交易，以太坊支持每秒 ~12 笔交易）。迄今为止，这已被证明是引导网络的有效方法，但随着网络的增长，这也存在局限性（我们现在开始看到）。

There are a variety of newer blockchains sacrificing decentralization or security for scalability and trying to bootstrap a network that way. It remains to be seen how effective that approach will be. But to date, no one has found the combination of decentralization, scalability, and security necessary to create a fully functioning cryptocurrency network at scale.  
有各种较新的区块链为了可扩展性而牺牲去中心化或安全性，并试图以这种方式引导网络。这种方法的效果如何还有待观察。但迄今为止，还没有人发现去中心化、可扩展性和安全性的结合是大规模创建功能齐全的加密货币网络所必需的。

## How to create a network that generates transaction demand at scale and is also capable of supporting that demand?  
如何创建一个能够大规模产生交易需求并能够支持该需求的网络？

There are several ways that cryptocurrency network scalability could end up playing out:  
加密货币网络可扩展性最终可能以多种方式发挥作用：

## **1.) The communities with the largest network effects and developer mindshare (Bitcoin and Ethereum) will solve scalability  
1.） 具有最大网络效应和开发者心智份额的社区（比特币和以太坊）将解决可扩展性问题**

The most widely known projects that are seeking to increase the scalability of Bitcoin and Ethereum are [Lightning Network](https://lightning.network/) (Bitcoin), [Plasma](https://plasma.io/)(Ethereum), and [Casper](https://github.com/ethereum/casper) (Ethereum). Lightning and Plasma are both Layer 2 solutions that allow transactions to occur off-chain and then ultimately settle on-chain, while Casper seeks to implement sharding to increase on-chain scalability at the consensus layer.  
寻求提高比特币和以太坊可扩展性的最广为人知的项目是 [Lightning Network](https://lightning.network/)（Bitcoin）、[Plasma](https://plasma.io/) （Ethereum） 和 [Casper](https://github.com/ethereum/casper) （Ethereum）。Lightning 和 Plasma 都是第 2 层解决方案，允许交易在链下进行，然后最终在链上结算，而 Casper 则寻求实施分片以提高共识层的链上可扩展性。

There are other projects that are less well-known building at the second layer of Ethereum ([Truebit](https://truebit.io/), [Raiden](https://raiden.network/), and [Counterfactual](https://counterfactual.com/)) and one that is building at the peer-to-peer networking layer for all blockchains ([bloXroute](https://bloxroute.com/), announced this week). These efforts are early but also promising.  
还有其他一些不太知名的项目构建在以太坊的第二层（[Truebit](https://truebit.io/)、[Raiden](https://raiden.network/) 和 [Counterfactual](https://counterfactual.com/)），还有一个项目正在所有区块链的点对点网络层构建（[bloXroute](https://bloxroute.com/)，本周宣布）。这些努力是早期的，但也是有希望的。

![](https://miro.medium.com/v2/resize:fit:1388/1*3_kzcUPlmRYPBc1RvaodJg.png)

Core scalability solutions for Bitcoin and Ethereum  
比特币和以太坊的核心可扩展性解决方案

The solutions described above seek to achieve scalability at various layers of the stack for the largest networks with the most mindshare and the most passionate communities. The BTC and ETH communities have a strong belief in the cryptocurrencies native to their respective networks and the strongest inherent demand to scale now.  
上述解决方案旨在为拥有最多心智份额和最热情社区的最大网络在堆栈的各个层实现可扩展性。BTC 和 ETH 社区对各自网络原生的加密货币有着坚定的信念，并且现在对扩展有着最强烈的内在需求。

They also have the strongest technical minds working on these problems. ==In my view, the most likely path forward is that a variety of solutions end up enabling Ethereum and Bitcoin to scale on-chain and off-chain and Bitcoin and Ethereum end up being the core networks the masses converge on.==  
他们也拥有最强大的技术人才来解决这些问题。==在我看来，最可能的前进道路是，各种解决方案最终使以太坊和比特币能够在链上和链下扩展，而比特币和以太坊最终成为大众聚集的核心网络。==

## **2.) New networks emerge that are fundamentally built to be scalable and users gravitate to them  
2.） 新网络的出现从根本上说是可扩展的，用户被它们所吸引**

**Scalability-first blockchains.** Several new scalability-first blokchains have emerged to serve users and developers as more scalable payment networks (i.e. [Bitcoin Cash](https://www.bitcoincash.org/), [Algorand](https://www.algorand.com/)) and dApp platforms (i.e. [Cosmos](https://cosmos.network/), [Dfinity](https://dfinity.org/), [EOS](https://eos.io/), etc). There’s likely a few quality projects I’m missing, but for the most part there are a lot of low quality projects making big claims about scalability and raising massive amounts of money from unsophisticated investors on these claims. I’m skeptical of most of these, but there are some diamonds in the rough led by teams that have deep historical context and knowledge and have made compromises on security or decentralization, which could pay off.  
**可扩展性优先的区块链。** 已经出现了几个新的可扩展性优先的区块链，作为更具可扩展性的支付网络（即[比特币现金](https://www.bitcoincash.org/)、[Algorand](https://www.algorand.com/)）和 dApp 平台（即 [Cosmos](https://cosmos.network/)、[Dfinity](https://dfinity.org/)、[EOS](https://eos.io/) 等）为用户和开发人员提供服务。我可能错过了一些高质量的项目，但在大多数情况下，有很多低质量的项目对可扩展性提出了很大的主张，并从不成熟的投资者那里筹集了大量资金。我对其中的大多数都持怀疑态度，但有一些未加工的钻石是由具有深厚历史背景和知识的团队领导的，他们在安全性或去中心化方面做出了妥协，这可能会得到回报。

![](https://miro.medium.com/v2/resize:fit:632/1*Ht_g0jDUi83zv0r41_ts7w.png)

Scalability-first blockchains  
可扩展性优先的区块链

While these scalability-first projects generally lack the passionate, grassroots communities that have the strong inherent demand to use these platforms for transactions today, they have constructed blockchains that are fundamentally more scalable than Bitcoin and Ethereum now. If solutions don’t emerge to help scale Bitcoin and Ethereum before the demand for transactions increases significantly, it’s quite possible that users shift to these next-generation blockchains.  
虽然这些可扩展性优先的项目通常缺乏热情的草根社区，这些社区在当今使用这些平台进行交易具有强烈的内在需求，但他们已经构建了比现在的比特币和以太坊更具可扩展性的区块链。如果在交易需求显着增加之前没有出现解决方案来帮助扩展比特币和以太坊，那么用户很可能会转向这些下一代区块链。

**New consensus constructs.** There’s another category of scalability-first projects that is even earlier and less proven than the projects listed above that seek to achieve consensus via mechanisms that lie outside the construct of a blockchain (gossip protocols, directed acyclic graphs, etc). Projects like [Hashgraph](https://www.hederahashgraph.com/) and [DAG Labs](https://www.daglabs.com/) are championing these ideas. I think they are worthwhile initiatives but early and highly speculative.  
**新的共识结构。** 还有另一类可扩展性优先的项目，它比上面列出的项目更早，也更不成熟，这些项目试图通过区块链结构之外的机制（八卦协议、有向无环图等）来达成共识。[Hashgraph](https://www.hederahashgraph.com/) 和 [DAG Labs](https://www.daglabs.com/) 等项目正在倡导这些想法。我认为它们是值得的举措，但处于早期阶段且高度投机。

## **3.) Cryptocurrency networks don’t scale  
3.） 加密货币网络无法扩展**

As bullish as I am about the future of blockchains, I do recognize that there is a small probability that they don’t scale for transactions, either because the tech is not figured out or users demand just doesn’t increase to the scale we hope.  
尽管我对区块链的未来持乐观态度，但我确实认识到，它们无法扩展交易的可能性很小，要么是因为技术没有弄清楚，要么是因为用户需求没有增加到我们希望的规模。

## What to expect? 期待什么？

My view is that the network effects and mindshare of Bitcoin and Ethereum, and the caliber of the teams working on scalability solutions for these networks make it highly likely that solutions on Bitcoin and Ethereum enable widespread transaction usage of the networks.  
我的观点是，比特币和以太坊的网络效应和心智份额，以及为这些网络开发可扩展性解决方案的团队的素质，使得比特币和以太坊的解决方案极有可能实现网络的广泛交易使用。

It’s also possible (albeit much less likely) that a critical mass of developers and users will shift to next-generation networks that fundamentally support more throughput ([Cosmos](https://cosmos.network/), [Dfinity](https://dfinity.org/), [EOS](https://eos.io/), or something else). If we see demand for transactions increase significantly (i.e. we see a few more Cryptokitties-like apps) before better solutions exist on Bitcoin and Ethreum, that could happen.  
也有可能（尽管可能性很小）大量开发人员和用户将转向从根本上支持更高吞吐量的下一代网络（[Cosmos](https://cosmos.network/)、[Dfinity](https://dfinity.org/)、[EOS](https://eos.io/) 或其他网络）。如果我们看到交易需求显着增加（即我们看到更多类似 Cryptokitties 的应用程序），那么在比特币和 Ethreum 出现更好的解决方案之前，这种情况可能会发生。

It’s also possible (albeit even less likely) that cryptocurrency networks don’t scale. I’d put that probability at less than 5% because of all the momentum and talent currently focused on solving the problem. But it’s not a foregone conclusion that people will want to use cryptocurrency networks for transactions at scale and the right combination of decentralization, security and scalability will be found. The industry has a lot more work to do on both fronts.  
加密货币网络也有可能（尽管可能性更小）无法扩展。我认为这个概率低于 5%，因为目前所有专注于解决问题的动力和人才都在这里。但是，人们希望使用加密货币网络进行大规模交易并不是一个必然的结论，并且会找到去中心化、安全性和可扩展性的正确组合。该行业在这两个方面都有很多工作要做。

## **Learn more 了解更多信息**

- Vitalik On Sharding Blockchains: [https://github.com/ethereum/wiki/wiki/Sharding-FAQ](https://github.com/ethereum/wiki/wiki/Sharding-FAQ)  
    Vitalik 谈分片区块链：[https://github.com/ethereum/wiki/wiki/Sharding-FAQ](https://github.com/ethereum/wiki/wiki/Sharding-FAQ)
- [The Bitcoin Lightning Network Whitepaper  
    Bitcoin Lightning Network 白皮书](https://lightning.network/lightning-network-paper.pdf)
- [The Plasma Whitepaper Plasma 白皮书](https://plasma.io/plasma.pdf)
- [The bloXroute Whitepaper bloXroute 白皮书](https://bloxroute.com/wp-content/uploads/2018/03/bloXroute-whitepaper.pdf)
- [Join the bloXroute subreddit to discuss scalability  
    加入 bloXroute subreddit 讨论可扩展性](https://www.reddit.com/r/bloXrouteLabs/)
- Token Summit SF Panel with Joseph Poon (Plasma), Jason Teutsch (Truebit), and Jae Kwon (Cosmos)  
    Token 峰会 SF 小组讨论，主讲人：Joseph Poon （Plasma）、Jason Teutsch （Truebit） 和 Jae Kwon （Cosmos）

![](https://miro.medium.com/v2/resize:fit:478/1*9xpbawhF3BhtX6s97kPWuA.png)

**About the author:** Nick runs [1confirmation](http://www.1confirmation.com/), an early stage crypto fund. Sign up for the [newsletter](https://www.getrevue.co/profile/control) and check out the next [Token Summit in NYC](https://www.eventbrite.ca/e/token-summit-iii-new-york-2018-tickets-38874437489) in May 2018 (scalability will be a big topic of discussion).  
**关于作者：** Nick 经营着 [1confirmation](http://www.1confirmation.com/)，这是一家早期加密基金。注册[时事通讯并查看](https://www.getrevue.co/profile/control) 2018 年 5 月[在纽约举行的下一届代币峰会](https://www.eventbrite.ca/e/token-summit-iii-new-york-2018-tickets-38874437489)（可扩展性将是一个重要的讨论话题）。

[

Blockchain

](https://medium.com/tag/blockchain?source=post_page-----ec76ed769405--------------------------------)

[](https://medium.com/tag/ethereum?source=post_page-----ec76ed769405--------------------------------)