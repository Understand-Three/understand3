---
title: 分布式账本简介
draft: true
---
Ledgers are hard to distribute and keep updated without any central authority. Think of how hard it would be to share an excel spreadsheet between you and your friends that associates each of you with a number — let’s call it “friendcoin”. Each of you has to have a copy of the spreadsheet and it has to be kept up to date. You can only move friendcoin from your entry in the spreadsheet to someone else’s. When you do, you have to tell other people so they can change it too. Whenever you hear about a change, you also pass it on to a few people. Consider the following situations:  

账本在没有任何中央机构的情况下很难分发和保持更新。想想看，在你和你的朋友之间分享一个 excel 电子表格，将你们每个人都与一个数字相关联——让我们称之为 “朋友币”，那将是多么困难。你们每个人都必须拥有一份电子表格的副本，并且必须保持最新状态。您只能将朋友币从您在电子表格中的条目移动到其他人的条目中。当你这样做时，你必须告诉其他人，这样他们也可以改变它。每当你听到一个变化时，你也会把它传递给少数人。请考虑以下情况：

1. Alice lies to everyone about Steve transferring all his friendcoin to her. **(fraudulent transactions)**  
    爱丽丝向所有人撒谎，说史蒂夫把他所有的朋友币都转给了她。**（欺诈交易）**
2. Alice tells Bob she wants to transfer all of her friendcoin to Eve but tells everyone else that she wants to transfer it all to Steve. **(double spending)**  
    Alice 告诉 Bob 她想把她所有的朋友币都转给 Eve，但告诉其他人她想把所有 friendcoin 都转给 Steve。**（双倍消费）**
3. Alice and Steve have a fight. Steve’s friends refuse to update their spreadsheet with any transactions to her while others think it’s unfair and continue to allow her to receive transfers. **(censorship)**  
    爱丽丝和史蒂夫吵了一架。史蒂夫的朋友拒绝更新他们的电子表格中向她提供任何交易，而其他人则认为这不公平并继续允许她接收转账。**（审查制度）**

There are any number of ways the spreadsheets could become out of sync. There are possible social solutions, like voting to resolve disagreements or putting someone in charge for a week and rotating that person. These could work between you and your friends. They won’t work with a ledger containing millions or billions of people who don’t know or want to trust each other.  
电子表格不同步的方式有很多种。有一些可能的社会解决方案，比如投票解决分歧，或者让某人负责一周并轮换这个人。这些可以在您和您的朋友之间起作用。他们不会与包含数百万或数十亿不认识或不愿意相互信任的人的账本一起工作。

A solution to the fraudulent transaction problem, where Alice invents a transaction from someone else, has been known since 1978 with the publication of the [RSA paper](https://people.csail.mit.edu/rivest/Rsapaper.pdf) which introduced public key encryption and ˜cryptographic signatures. Instead of (or as well as) storing the name of a person in the ledger we can store their public key. That way, anyone wanting to make a transfer must sign their request with their private key.  
自 1978 年发表的 [RSA 论文](https://people.csail.mit.edu/rivest/Rsapaper.pdf)（引入公钥加密和加密签名）以来，Alice 发明了来自他人的交易，从而解决了欺诈易问题。我们可以存储他们的公钥，而不是（或同时）在账本中存储一个人的姓名。这样，任何想要进行转账的人都必须使用他们的私钥签署他们的请求。

## Bitcoin 比特币

A solution for the other problems wasn’t known until Satoshi Nakamoto anonymously published his/her [paper on bitcoin](https://bitcoin.org/bitcoin.pdf) in 2008. It solved both the censorship and the double spend problem. The solution was roughly this:  
直到 2008 年中本聪匿名发表了他/她[关于比特币的论文](https://bitcoin.org/bitcoin.pdf)，人们才知道其他问题的解决方案。它解决了审查制度和双花问题。解决方案大致是这样的：

- Update the the ledger with groups of transactions (called “blocks”). Only one party can add a block at a time. They have complete authority about what transactions gets included in their block.  
    使用交易组（称为 “区块”） 更新账本。一次只能有一个方添加区块。他们对哪些交易包含在他们的区块中拥有完全的权力。
- Each block has a header which has a hash of the previous block’s header as one of the fields. This makes the blocks into a linked list or a “blockchain”.  
    每个区块都有一个 Header，该 Headers 将前一个区块的 Header 的哈希值作为字段之一。这使得区块成为链表或 “区块链”。
- Choose who will be the next block creator by running a game: Whoever is the first to find a hash with a number of leading 0s, where the input is the header of block they want to add, gets to add their block. This computationally difficult task is called proof of work (PoW) and the people playing are called miners.  
    通过运行游戏来选择谁将成为下一个区块创建者：谁是第一个找到带有多个前导 0 的哈希值的人，其中输入是他们想要添加的区块的标头，谁就可以添加他们的区块。这项计算难度大的任务称为工作量证明 （PoW），玩游戏的人称为矿工。
- Whenever a miner is presented with two valid yet contradictory chains, they choose the longest one to work on top of.  
    每当矿工看到两条有效但相互矛盾的链时，他们都会选择最长的一条来工作。
- Parties are incentivised to play the game. The winner of the game is rewarded with the currency of the ledger (ie bitcoin). The reward usually comes from collecting transaction fees and/or the ability to add a predetermined amount of bitcoin out of thin air to their associated public key.  
    各方被激励玩游戏。游戏的获胜者将获得账本的货币（即比特币）作为奖励。奖励通常来自收取交易费用和/或将预定数量的比特币凭空添加到其相关公钥的能力。

That’s a rather shallow summary but it gives us the key principles. We can make a distributed ledger work if we represent it as a series of transaction blocks. The blocks are the only thing that modify the state of the ledger. Block creators are chosen probabilistically according to their hashing power. As long as a large proportion of the hashing power isn’t owned by one group a variety will add blocks, making censorship and double spending impossible under reasonable assumptions. You can’t censor transactions, you can only delay them, because even if you try, soon someone else is going to add a block that will include it. You can’t double spend because only one of your transactions will end up in the canonical blockchain.  
这是一个相当肤浅的总结，但它为我们提供了关键原则。如果我们将分布式账本表示为一系列交易区块，我们就可以让它工作。区块是唯一修改账本状态的东西。区块创建者是根据他们的哈希算力概率选择的。只要很大一部分哈希算力不由一个群体拥有，各种就会增加区块，从而在合理的假设下不可能进行审查和双重支出。你不能审查交易，你只能延迟它们，因为即使你尝试，很快其他人就会添加一个包含它的区块。您不能双花，因为您的交易中只有一笔最终会进入规范区块链。

Nakamoto’s paper didn’t contain any new mathematical discoveries or constructions. It was a genius work of cryptographic engineering rather than mathematics. Seven years after its publication, in 2015 a group of cryptographers [published a paper](https://eprint.iacr.org/2014/765) at Eurocrypt conference which formally demonstrated the security of the bitcoin protocol. Bitcoin was the first solution to the distributed ledger problem. As of writing, there have been over 300 million uncensorable trustless peer-to-peer transactions made through the bitcoin blockchain.  
中本聪的论文不包含任何新的数学发现或结构。这是密码工程而不是数学的天才作品。在它发表七年后，2015 年，一群密码学家在 Eurocrypt 会议上[发表了一篇论文](https://eprint.iacr.org/2014/765)，正式展示了比特币协议的安全性。比特币是分布式账本问题的第一个解决方案。截至撰写本文时，已经有超过 3 亿笔不可审查的无需信任的点对点交易通过比特币区块链进行。

## Ethereum — A notable innovation  
以太坊 — 一项值得注意的创新

Although it’s not related to consensus algorithms, it’s worth mentioning that ledger state transitions are not the only thing you can represent with blockchains. Ethereum uses a blockchain with a Turning complete language to represent a virtual machine. While it also has built-in ledger functionality, a programmer can embed code in the blockchain which can be called by them or by others. When these calls are made they are executed by every “miner” on the Ethereum network deterministically to produce the same state change. The biggest use of this seems to be for creating “tokens”, parallel ledgers within the Ethereum blockchain that have their own properties. For an proper explanation, see the [whitepaper](https://github.com/ethereum/wiki/wiki/White-Paper). For our purposes it is not important what exactly is being represented by the blockchain just how we can come to a decentralised trustless consensus about what is in the chain.  
虽然它与共识算法无关，但值得一提的是，账本状态转换并不是区块链唯一可以表示的东西。以太坊使用具有 Turning complete 语言的区块链来表示虚拟机。虽然它还具有内置的账本功能，但程序员可以在区块链中嵌入代码，这些代码可以由他们或其他人调用。当进行这些调用时，它们由以太坊网络上的每个“矿工”确定性地执行，以产生相同的状态变化。它的最大用途似乎是用于创建“代币”，即以太坊区块链中具有自身属性的并行账本。有关适当的解释，请参阅[白皮书](https://github.com/ethereum/wiki/wiki/White-Paper)。就我们的目的而言，区块链究竟代表什么并不重要，重要的是我们如何就链中的内容达成去中心化的、去信任的共识。

## Bitcoin’s problems 比特币的问题

Bitcoin has exploded in popularity and price. This has made the prize of the PoW game very valuable. In order to win, miners have engaged in an arms race of computational hashing power and cheap electricity. According to [Digiconomist](https://digiconomist.net/bitcoin-energy-consumption), bitcoin miners are consuming two billion dollars a year worth of electricity. All of this to process around seven transactions per second. It’s worth taking that in. The bitcoin network consumes about as much electricity as New Zealand to process seven transactions per second.  
比特币的受欢迎程度和价格都呈爆炸式增长。这使得 PoW 游戏的奖品非常有价值。为了获胜，矿工们参与了一场计算哈希能力和廉价电力的军备竞赛。根据 [Digiconomist](https://digiconomist.net/bitcoin-energy-consumption) 的数据，比特币矿工每年消耗 20 亿美元的电力。所有这些都是为了每秒处理大约 7 笔交易。值得一试。比特币网络每秒处理 7 笔交易消耗的电力与新西兰的电力差不多。

With that in mind remember that this is just a zero-sum game created to decide who gets produce the next block. Adding more hashing power to the network doesn’t improve its functioning at all. The system is just meant to provide a way to choose block creators that can’t be rigged to always choose the same group.  
考虑到这一点，请记住，这只是一个零和游戏，用来决定谁能产生下一个区块。向网络添加更多的哈希算力根本不会改善其功能。该系统只是为了提供一种选择区块创建者的方法，这些创建者不能纵为始终选择相同的组。

To make things worse PoW is not really doing its job. The high cost of mining created economies of scale pushing smaller players out of the game. Hashing power has been centralising. Now a worryingly small group of miners control a large share of the network’s hashing power. As far as we know none of them are using their hashing advantage maliciously, but the whole premise of bitcoin is we should only have to trust in cryptography, not people.  
更糟糕的是，PoW 并没有真正发挥作用。高昂的采矿成本创造了规模经济，将较小的参与者挤出了游戏。哈希算力一直在集中化。现在，令人担忧的是，一小群矿工控制着网络哈希能力的很大一部分。据我们所知，他们都没有恶意使用他们的哈希优势，但比特币的整个前提是我们应该只相信密码学，而不是人。

## Ouroboros — Proof of Stake  
Ouroboros — 权益证明

What if we didn’t have to play this game? What if we could pick parties to create blocks in some other way? If so, we’d have a distributed ledger with each block producer using no more electricity than a typical web server. Make no mistake, if we could do this without sacrificing security it would be magical. In my opinion, it would be the greatest distributed ledger discovery since the original invention on bitcoin.  
如果我们不必玩这个游戏会怎样？如果我们可以选择方以其他方式创建区块呢？如果是这样，我们将有一个分布式账本，每个区块生产者的用电量不超过典型的 Web 服务器。毫无疑问，如果我们可以在不牺牲安全性的情况下做到这一点，那将是神奇的。在我看来，这将是自比特币最初发明以来最伟大的分布式账本发现。

The claim is that Ouroboros can do it. It is one of a few protocols based on the idea that you can replace Proof of Work with Proof of Stake. That is, you can replace hashing power as the input to the block creator selection process with stake (the amount of currency you already own).  
声称衔尾蛇可以做到。它是基于可以用权益证明代替工作量证明的少数协议之一。也就是说，你可以用 stake（您已经拥有的货币数量）代替哈希算力作为区块创建者选择过程的输入。

Crypto candor outlines Proof of Work and a bunch of different Proof of Stake systems  
Crypto candor 概述了工作量证明和一系列不同的权益证明系统

In the next article I’ll go into more detail about how Ouroboros and Ouroboros Praos use stake to determine the block producers.  
在下一篇文章中，我将更详细地介绍 Ouroboros 和 Ouroboros Praos 如何使用 stake 来确定区块生产者。
