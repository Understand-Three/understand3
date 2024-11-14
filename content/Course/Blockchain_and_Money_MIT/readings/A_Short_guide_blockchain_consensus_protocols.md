---
title: 区块链共识协议的（简短）指南
draft: true
link: https://www.coindesk.com/markets/2017/03/04/a-short-guide-to-blockchain-consensus-protocols/
---
Bitcoin's consensus mechanism is great, but it isn't perfect. This article looks at some of the more viable public blockchain alternatives.  

比特币的共识机制很棒，但并不完美。本文着眼于一些更可行的公共区块链替代方案。

By Amy Castor 作者：Amy Castor

![AccessTimeIcon](https://www.coindesk.com/pf/resources/images/icons/AccessTimeIcon.svg?d=371)Mar 4, 2017 at 7:50 p.m.   
3月 4， 2017 在 7：50 下午

Updated Sep 11, 2021 at 9:08 p.m.   
更新时间：2021 年 9 月 11 日晚上 9：08

![gum, candy](https://www.coindesk.com/resizer/VhxbJd3vpR0gTdRQiPqcBnpKRzM=/1056x704/filters:quality(80):format(jpg)/cloudfront-us-east-1.images.arcpublishing.com/coindesk/FHRIBGZ75VHYFOPNEDDRPOG4OA.jpg)

We hear plenty of talk of how public blockchains are going to change the world, but to function on a global scale, a shared public ledger needs a functional, efficient and secure consensus algorithm.  
我们听到了很多关于公共区块链将如何改变世界的讨论，但要在全球范围内运行，共享公共账本需要一种功能强大、高效且安全的共识算法。

A consensus algorithm, like bitcoin's [proof of work](https://www.coindesk.com/learn/how-bitcoin-mining-works-2/) (the one we hear about most often), does two things: it ensures that the next block in a blockchain is the one and only version of the truth, and it keeps powerful adversaries from derailing the system and successfully forking the chain.  
共识算法，就像比特币的[工作量证明](https://www.coindesk.com/learn/how-bitcoin-mining-works-2/)（我们最常听到的那个）一样，做两件事：它确保区块链中的下一个区块是唯一的事实版本，并防止强大的对手使系统脱轨并成功分叉链。

In proof of work, miners compete to add the next block (a set of transactions) in the chain by racing to solve a extremely difficult cryptographic puzzle. The first to solve the puzzle, wins the lottery. As a reward for his or her efforts, the miner receives 12.5 newly minted bitcoins – and a small transaction fee.  
在工作量证明中，矿工通过竞相解决一个极其困难的密码难题，竞争在链中添加下一个区块（一组交易）。第一个解开谜题的人，赢得彩票。作为对他或她努力的奖励，矿工会收到 12.5 个新铸造的比特币——以及一小笔交易费。

Yet, although a masterpiece in its own right, bitcoin's proof of work isn't quite perfect.  
然而，尽管比特币本身就是一件杰作，但它的工作量证明并不完美。

Common criticisms include that it requires enormous amounts of [computational energy](http://steamgreen.unibo.it/2016/09/20/the-colour-of-bitcoin-certainly-not-green/), that it does not scale well (transaction confirmation takes about 10-60 minutes) and that the majority of mining is centralized in areas of the world where electricity is cheap.  
常见的批评包括它需要大量的[计算能量](http://steamgreen.unibo.it/2016/09/20/the-colour-of-bitcoin-certainly-not-green/)，它不能很好地扩展（交易确认大约需要 10-60 分钟），以及大多数挖矿都集中在世界上电力便宜的地区。

Bitcoin creator Satoshi Nakamoto woke us up to the potential of the blockchain, but that doesn't mean we can't keep searching for faster, less centralized and more energy-efficient consensus algorithms to carry us into the future.  
比特币的创造者中本聪唤醒了我们区块链的潜力，但这并不意味着我们不能继续寻找更快、更少中心化和更节能的共识算法来带领我们走向未来。

While not a comprehensive list, the following are a few of the alternative approaches being kicked around out there.  
虽然不是一个完整的列表，但以下是一些正在推出的替代方法。

## Proof of stake 权益证明

The most common alternative to proof of work is proof of stake.  
工作量证明最常见的替代方案是权益证明。

In this type of consensus algorithm, instead of investing in expensive computer equipment in a race to mine blocks, a 'validator' invests in the coins of the system.  
在这种类型的共识算法中，“验证者”不是投资于昂贵的计算机设备来开采区块，而是投资于系统的硬币。

Note the term validator. That's because no coin creation (mining) exists in proof of stake. Instead, all the coins exist from day one, and validators (also called stakeholders, because they hold a stake in the system) are paid strictly in transaction fees.  
请注意术语 validator。那是因为权益证明中不存在硬币创建（挖矿）。相反，所有硬币从第一天起就存在，验证者（也称为利益相关者，因为他们在系统中持有股份）严格以交易费用支付。

In proof of stake, your chance of being picked to create the next block depends on the fraction of coins in the system you own (or set aside for staking). A validator with 300 coins will be three times as likely to be chosen as someone with 100 coins.  
在权益证明中，您被选中创建下一个区块的机会取决于您拥有的（或留作权益质押）的系统中的硬币比例。拥有 300 个硬币的验证者被选中的可能性是拥有 100 个硬币的验证者的三倍。

Once a validator creates a block, that block still needs to be committed to the blockchain. Different proof-of-stake systems vary in how they handle this. In Tendermint, for example, every node in the system has to sign off on a block until a majority vote is reached, while in other systems, a random group of signers is chosen.  
一旦验证者创建了一个区块，该区块仍然需要提交到区块链。不同的权益证明系统处理这个问题的方式各不相同。例如，在 Tendermint 中，系统中的每个节点都必须在区块上签字，直到获得多数票，而在其他系统中，则随机选择一组签名者。

Now, we run into a problem. What is to discourage a validator from creating two blocks and claiming two sets of transaction fees? And what is to discourage a signer from signing both of those blocks? This has been called the '[nothing-at-stake](https://www.coindesk.com/markets/2017/01/18/wheres-casper-inside-ethereums-race-to-reinvent-its-blockchain/)' problem. A participant with nothing to lose has no reason not to behave badly.  
现在，我们遇到了一个问题。如何阻止验证者创建两个区块并索取两组交易费用？是什么阻止了签名者同时签署这两个区块呢？这被称为“[无利害关系](https://www.coindesk.com/markets/2017/01/18/wheres-casper-inside-ethereums-race-to-reinvent-its-blockchain/)”问题。一个没有什么可失去的参与者没有理由不表现得不好。

In the burgeoning field of '[crypto-economics](https://www.coindesk.com/markets/2017/02/22/ethereum-economics-gets-spotlight-in-vitalik-buterin-edcon-keynote/)', blockchain engineers are exploring ways to tackle this and other problems. One answer is to require a validator to lock their currency in a type of virtual vault.  
在新兴的“[加密经济学](https://www.coindesk.com/markets/2017/02/22/ethereum-economics-gets-spotlight-in-vitalik-buterin-edcon-keynote/)”领域，区块链工程师正在探索解决这个问题和其他问题的方法。一个答案是要求验证者将其货币锁定在某种类型的虚拟保险库中。

If the validator tries to double sign or fork the system, those coins are slashed.  
如果验证者试图对系统进行双重签名或分叉，这些硬币将被罚没。

Peercoin was the first coin to implement proof of stake, followed by blackcoin and NXT. Ethereum currently relies on proof of work, but is planning a move to proof of stake in early 2018.  
Peercoin 是第一个实施权益证明的代币，其次是 blackcoin 和 NXT。以太坊目前依赖于工作量证明，但计划在 2018 年初转向权益证明。

## Proof of activity 活动证明

To avoid hyperinflation (what happens when too much of a currency floods the system) bitcoin will only ever produce 21m bitcoins. That means, at some point, the bitcoin block reward subsidy will end and bitcoin miners will only receive transaction fees.  
为避免恶性通货膨胀（当过多的货币充斥系统时会发生什么），比特币将只生产 21m 个比特币。这意味着，在某个时候，比特币区块奖励补贴将结束，比特币矿工将只收到交易费用。

Some have speculated this might cause security issues resulting from a '[tragedy of the commons](https://en.wikipedia.org/wiki/Tragedy_of_the_commons)', where people act in self-interest and spoil the system. So, [proof of activity](https://eprint.iacr.org/2014/452.pdf) was created as an alternative incentive structure for bitcoin. Proof of activity is a hybrid approach that combines both proof of work and proof of stake.  
一些人推测这可能会导致“[公地悲剧](https://en.wikipedia.org/wiki/Tragedy_of_the_commons)”导致安全问题，人们为了自身利益行事并破坏系统。因此，创建[活动证明](https://eprint.iacr.org/2014/452.pdf)作为比特币的替代激励结构。活动证明是一种结合了工作量证明和权益证明的混合方法。

In proof of activity, mining kicks off in a traditional proof-of-work fashion, with miners racing to solve a cryptographic puzzle. Depending on the implementation, blocks mined do not contain any transactions (they are more like templates), so the winning block will only contain a header and the miner's reward address.  
在活动证明中，挖矿以传统的工作量证明方式开始，矿工们竞相解决密码难题。根据实现方式的不同，挖出的区块不包含任何交易（它们更像是模板），因此获胜的区块将只包含一个标头和矿工的奖励地址。

At this point, the system switches to proof of stake. Based on information in the header, a random group of validators is chosen to sign the new block. The more coins in the system a validator owns, the more likely he or she is to be chosen. The template becomes a full-fledged block as soon as all of the validators sign it.  
此时，系统切换到权益证明。根据标头中的信息，随机选择一组验证者来签署新区块。验证者拥有的硬币越多，他或她被选中的可能性就越大。一旦所有验证者都签署了模板，它就会成为一个成熟的区块。

If some of the selected validators are not available to complete the block, then the next winning block is selected, a new group of validators is chosen, and so on, until a block receives the correct amount of signatures. Fees are split between the miner and the validators who signed off on the block.  
如果一些选定的验证者无法完成区块，则选择下一个获胜的区块，选择一组新的验证者，依此类推，直到区块收到正确数量的签名。费用在矿工和签署区块的验证者之间分配。

Criticisms of proof of activity are the same as for both proof of work (too much energy is required to mine blocks) and proof of stake (there is nothing to deter a validator from double signing).  
对活动证明的批评与对工作量证明（挖掘区块需要太多能量）和权益证明（没有什么可以阻止验证者进行双重签名）的批评相同。

Decred is the only coin right now using a variation of proof of activity.  
Decred 是目前唯一使用活动证明变体的代币。

## Proof of burn 燃烧证明

With proof of burn, instead of pouring money into expensive computer equipment, you 'burn' coins by sending them to an address where they are irretrievable. By committing your coins to never-never land, you earn a lifetime privilege to mine on the system based on a random selection process.  
使用销毁证明，您无需将钱投入昂贵的计算机设备，而是通过将硬币发送到无法恢复的地址来“销毁”硬币。通过将您的硬币投入到永不落地，您将获得基于随机选择过程在系统上挖矿的终身特权。

Depending on how proof of burn is implemented, miners may burn the native currency or the currency of an alternative chain, like bitcoin. The more coins you burn, the better chance you have of being selected to mine the next block.  
根据销毁证明的实施方式，矿工可能会销毁原生货币或替代链（如比特币）的货币。您燃烧的硬币越多，您被选中开采下一个区块的机会就越大。

Over time, your stake in the system decays, so eventually you will want to burn more coins to increase your odds of being selected in the lottery. (This mimics bitcoin's mining process, where you have to continually invest in more modern computing equipment to maintain hashing power.)  
随着时间的推移，您在系统中的赌注会衰减，因此最终您会想要燃烧更多的硬币以增加您在彩票中被选中的几率。（这模仿了比特币的挖矿过程，您必须不断投资更现代的计算设备来维持哈希算力。

While proof of burn is an interesting alternative to proof of work, the protocol still wastes resources needlessly. Another criticism is that mining power simply goes to those who are willing to burn more money.  
虽然燃烧证明是工作量证明的有趣替代方案，但该协议仍然不必要地浪费资源。另一个批评是，挖矿权只是流向了那些愿意烧更多钱的人。

The only coin that uses proof of burn is slimcoin, a cryptocurrency based on peercoin. It uses a combination of proof of work, proof of stake and proof of burn, but is only [semi-active](https://www.reddit.com/r/slimcoin/comments/4su0ti/slimcoin_is_dead/) at this time.  
唯一使用销毁证明的硬币是 slimcoin，这是一种基于 peercoin 的加密货币。它结合使用了工作量证明、权益证明和销毁证明，但目前仅[处于半活跃状态](https://www.reddit.com/r/slimcoin/comments/4su0ti/slimcoin_is_dead/)。

## Proof of capacity 容量证明

As we’ve seen, most of these alternative protocols employ some type of pay-to-play scheme. Proof of capacity is no different, but here you 'pay' with hard drive space. The more hard drive space you have, the better your chance of mining the next block and earning the block reward.  
正如我们所看到的，这些替代协议中的大多数都采用某种类型的付费游戏计划。容量证明也不例外，但在这里您“支付”了硬盘空间。您拥有的硬盘空间越多，您挖掘下一个区块并获得区块奖励的机会就越大。

Prior to mining in a proof-of-capacity system, the algorithm generates large data sets known as 'plots', which you store on your hard drive. The more plots you have, the better your chance of finding the next block in the chain.  
在容量证明系统中进行挖矿之前，该算法会生成称为“绘图”的大型数据集，并将其存储在硬盘上。您拥有的地块越多，找到链中下一个区块的机会就越大。

By investing in terabytes of hard drive space, you buy yourself a better chance to create duplicate blocks and fork the system. But with proof of capacity, we still have the problem of nothing at stake to deter bad actors.  
通过投资 TB 级的硬盘空间，您可以为自己赢得更好的机会来创建重复块和分叉系统。但是，有了能力证明，我们仍然存在一个问题，即没有任何风险来阻止不良行为者。

Variations of proof of capacity include proof of storage and [proof of space](https://eprint.iacr.org/2013/796.pdf). Burstcoin is the only cryptocurrency to use a form of proof of capacity.  
容量证明的变体包括存储证明和[空间证明](https://eprint.iacr.org/2013/796.pdf)。Burstcoin 是唯一使用容量证明形式的加密货币。

## Proof of elapsed time 经过时间的证明

Chipmaker Intel has come up with its own alternative consensus protocol called [proof of elapsed time](https://www.coindesk.com/markets/2016/12/05/intel-is-winning-over-blockchain-critics-by-reimagining-bitcoins-dna/). This system works similarly to proof of work, but consumes far less electricity.  
芯片制造商英特尔提出了自己的替代共识协议，称为[运行时间证明](https://www.coindesk.com/markets/2016/12/05/intel-is-winning-over-blockchain-critics-by-reimagining-bitcoins-dna/)。该系统的工作原理类似于工作量证明，但耗电量要少得多。

Further, instead of having participants solve a cryptographic puzzle, the algorithm uses a trusted execution environment (TEE) – such as SGX – to ensure blocks get produced in a random lottery fashion, but without the required work.  
此外，该算法不是让参与者解决密码难题，而是使用可信执行环境 （TEE）（例如 SGX）来确保以随机抽签方式生成区块，但不需要所需的工作。

Intel’s approach is based on a guaranteed wait time provided through the TEE. According to Intel, the poof-of-elapsed-time algorithm scales to thousands of nodes and will run efficiently on any Intel processor that supports SGX.  
Intel 的方法基于通过 TEE 提供的保证等待时间。据 Intel 称，Poof-of-elapsed-time 算法可扩展至数千个节点，并将在任何支持 SGX 的 Intel 处理器上高效运行。

The one problem with this protocol is it requires you to put your trust in Intel – and isn’t putting trust in third parties what we were trying to get away from with public blockchains?  
这个协议的一个问题是它需要你信任英特尔——而信任第三方不正是我们试图通过公共区块链摆脱的吗？

_[Gumballs image](https://www.shutterstock.com/image-photo/brightly-colored-gum-balls-laying-flat-140455963?src=j9JZsG9MsAb5phg5JGXZ5Q-1-42) via Shutterstock  
[Gumballs 图片](https://www.shutterstock.com/image-photo/brightly-colored-gum-balls-laying-flat-140455963?src=j9JZsG9MsAb5phg5JGXZ5Q-1-42)来自 Shutterstock_