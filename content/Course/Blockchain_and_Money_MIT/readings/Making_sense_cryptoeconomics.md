---
title: 理解加密经济学
draft: true
---
## Josh Stark argues that "cryptoeconomics" is widely misunderstood, despite being a concept crucial to understanding the blockchain industry.  
Josh Stark 认为，“加密经济学”被广泛误解，尽管它是理解区块链行业的关键概念。

By Josh Stark

![AccessTimeIcon](https://www.coindesk.com/pf/resources/images/icons/AccessTimeIcon.svg?d=371)Aug 19, 2017 at 4:40 p.m. 

Updated Sep 13, 2021 at 2:50 p.m. 

![little people with coins](https://www.coindesk.com/resizer/wlC9LqFcvQNXntn0IO0IqV26QsA=/1056x704/filters:quality(80):format(jpg)/cloudfront-us-east-1.images.arcpublishing.com/coindesk/ZGL2M5XZMJCOXPTN6S5S2XTA3M.jpg)

_Josh Stark ([@0xstark](https://twitter.com/0xstark)) is a member of [Ledger Labs](https://ledgerlabs.com/) and [Blockgeeks Lab](http://blockgeekslab.com/), a blockchain co-creation company in Toronto, Canada.  
Josh Stark （[@0xstark](https://twitter.com/0xstark)） 是 [Ledger Labs](https://ledgerlabs.com/) 和 [Blockgeeks Lab](http://blockgeekslab.com/)（一家位于加拿大多伦多的区块链共创公司）的成员。_

_In this CoinDesk opinion piece, Stark argues that the term "cryptoeconomics" is widely misunderstood, despite being a crucial concept needed to understand and analyze the blockchain industry.  
在这篇 CoinDesk 评论文章中，Stark 认为“加密经济学”一词被广泛误解，尽管它是理解和分析区块链行业所需的关键概念。_

# Bitcoin Eyes $70,000, Vitalik Buterin Outlines Ethereum 'Scourge' Upgrade  
比特币瞄准 70,000 美元，Vitalik Buterin 概述以太坊“灾难”升级

- ![Len Sassaman-Themed Memecoins Surge Ahead of HBO Bitcoin Creator Documentary](https://cdn.jwplayer.com/v2/media/FxUqtXCv/poster.jpg?width=720)
    
    00:56
    
    Len Sassaman-Themed Memecoins Surge Ahead of HBO Bitcoin Creator Documentary  
    Len Sassaman 主题的模因币在 HBO 比特币创作者纪录片之前激增
    
- ![Private Transactions Surge on Ethereum](https://cdn.jwplayer.com/v2/media/Tv2r9vW6/poster.jpg?width=720)
    
    01:11
    
    Private Transactions Surge on Ethereum  
    以太坊上的私人交易激增
    
- ![Many DeFi Protocols 'Flagrantly Disregard' Regulations: Gavin Wood](https://cdn.jwplayer.com/v2/media/roY2uuaP/poster.jpg?width=720)
    
    00:59
    
    Many DeFi Protocols 'Flagrantly Disregard' Regulations: Gavin Wood  
    许多 DeFi 协议“公然无视”规定：Gavin Wood
    
- ![Gavin Wood on the Problem With Layer 1s](https://cdn.jwplayer.com/v2/media/5lxZLbt3/poster.jpg?width=720)
    
    00:53
    
    Gavin Wood on the Problem With Layer 1s  
    Gavin Wood 谈 Layer 1 的问题
    

---

A few months ago Parker Thompson, a well known Silicon Valley VC, [tweeted](https://twitter.com/pt/status/871473661101850624)that "the concept of crypto-economics is stupid. It's economics. Inventing your own word is just an excuse to ignore well-understood concepts."  
几个月前，硅谷知名风险投资人帕克·汤普森 （Parker Thompson） [在推特上表示](https://twitter.com/pt/status/871473661101850624)，“加密经济学的概念是愚蠢的。这是经济学。发明自己的词只是忽视广为人知的概念的借口。

The term "cryptoeconomics" causes a lot of confusion and people are often unclear on what it is supposed to mean. The word itself can be misleading, as it suggests that there is a parallel "crypto" version of the whole of economics. This is wrong, and Parker is right to mock such a generalization.  
“加密经济学”一词引起了很多混淆，人们往往不清楚它应该是什么意思。这个词本身可能具有误导性，因为它暗示整个经济学有一个平行的“加密”版本。这是错误的，帕克嘲笑这种概括是正确的。

In simple terms, cryptoeconomics is the use of incentives and cryptography to design new kinds of systems, applications, and networks. Cryptoeconomics is specifically about _building_ things, and has most in common with [mechanism design](https://en.wikipedia.org/wiki/Mechanism_design) – an area of mathematics and economic theory. 简单来说，加密经济学就是使用激励和密码学来设计新型的系统、应用程序和网络。加密经济学专门研究_构建_事物，与[机制设计](https://en.wikipedia.org/wiki/Mechanism_design)  （数学和经济理论的一个领域）最相似。 

Cryptoeconomics is not a subfield of economics, but rather an area of applied cryptography that takes economic incentives and economic theory into account. Bitcoin, ethereum, zcash and all other public blockchains are products of cryptoeconomics.  
密码经济学不是经济学的一个子领域，而是考虑经济激励和经济理论的应用密码学领域。比特币、以太坊、zcash 和所有其他公共区块链都是加密经济学的产物。

Cryptoeconomics is what makes blockchains interesting, what makes them _different_ from other technologies. As a result of [Satoshi's white paper](https://bitcoin.org/bitcoin.pdf), we have learned that through the clever combination of cryptography, networking theory, computer science and economic incentives that we can build new kinds of technologies. These new cryptoeconomic systems can accomplish things that these disciplines could not achieve on their own. Blockchains are just one product of this new practical science.   
加密经济学是区块链有趣的原因，也是它们_与其他技术不同的_原因。作为 [Satoshi 白皮书](https://bitcoin.org/bitcoin.pdf)的结果，我们了解到，通过密码学、网络理论、计算机科学和经济激励的巧妙结合，我们可以构建新型技术。这些新的加密经济系统可以完成这些学科无法单独完成的事情。区块链只是这门新的实用科学的一个产品。

This article aims to explain cryptoeconomics in clear, simple terms. First, we examine bitcoin as an example of cryptoeconomic design. Second, we consider how cryptoeconomics relates to economic theory in general. Third, we look at three different areas of cryptoeconomic design and research that are active today.  
本文旨在用清晰、简单的术语解释加密经济学。首先，我们将比特币作为加密经济设计的一个例子来研究。其次，我们考虑加密经济学与一般经济理论的关系。第三，我们研究了当今活跃的加密经济设计和研究的三个不同领域。

## 1. What is cryptoeconomics? Bitcoin as a case study  
1. 什么是加密经济学？比特币作为案例研究

Bitcoin is a product of cryptoeconomics.   
比特币是加密经济学的产物。

Bitcoin's innovation is that it allows many entities who do not know one another to reliably reach consensus about the state of the bitcoin blockchain. This is achieved using a combination of economic incentives and basic cryptographic tools.  
比特币的创新之处在于，它允许许多彼此不认识的实体可靠地就比特币区块链的状态达成共识。这是通过经济激励和基本加密工具的组合来实现的。

Bitcoin's design relies on economic incentives and penalties. Economic rewards are used to enlist miners to support the network. Miners contribute their hardware and electricity because if they produce new blocks, they are rewarded with amounts of bitcoin.  
比特币的设计依赖于经济激励和惩罚。经济奖励用于招募矿工来支持网络。矿工贡献他们的硬件和电力，因为如果他们生产新区块，他们就会获得大量比特币的奖励。

Second, economic costs or _penalties_ are part of bitcoin’s security model. The most obvious way to attack the bitcoin blockchain would be to gain control of a majority of the network's hashing power – [a so-called 51 percent attack](https://bitcoin.stackexchange.com/questions/658/what-can-an-attacker-with-51-of-hash-power-do) – which would let an attacker reliably censor transactions and even change the past state of the blockchain. 其次，经济成本或_处罚_是比特币安全模型的一部分。攻击比特币区块链最明显的方法是控制网络的大部分哈希算力—— [即所谓的 51% 攻击](https://bitcoin.stackexchange.com/questions/658/what-can-an-attacker-with-51-of-hash-power-do) ——这将使攻击者能够可靠地审查交易，甚至改变区块链的过去状态。 

But gaining control of hashing power costs money, in the form of hardware and electricity. Bitcoin’s protocol _intentionally_ makes mining difficult, meaning that gaining control of a majority of the network is extremely expensive – enough that it would be hard to profit from the attack. As of August 16, 2017, the [cost of a 51 percent attack on bitcoin](https://gobitcoin.io/tools/cost-51-attack/) would be around $1.88 billion in hardware and $3.4 million in electricity every day. 但是获得对哈希算力的控制权需要花钱，以硬件和电力的形式。比特币的协议_故意_使挖矿变得困难，这意味着获得大部分网络的控制权非常昂贵——足以从攻击中获利。截至 2017 年 8 月 16 日，[对比特币的 51% 攻击每天的成本](https://gobitcoin.io/tools/cost-51-attack/)约为 18.8 亿美元的硬件和 340 万美元的电力。 

Without these carefully calibrated economic incentives, bitcoin wouldn’t work. If mining did not come with a high cost, it would be easy to launch a 51 percent attack. If there were no mining reward, there would be no industry of people who buy hardware and pay for electricity to contribute to the network.  
如果没有这些精心校准的经济激励措施，比特币就不会运作。如果挖矿成本不高，那么很容易发起 51% 攻击。如果没有挖矿奖励，就不会有购买硬件并支付电费为网络做出贡献的人的行业。

Bitcoin also relies on cryptographic protocols. [Public-private key cryptography](https://security.stackexchange.com/questions/25741/how-can-i-explain-the-concept-of-public-and-private-keys-without-technical-jargo) is used to give individuals safe, exclusive control of their bitcoin. [Hash functions](https://medium.com/@ConsenSys/blockchain-underpinnings-hashing-7f4746cbd66b) are used to "link" each block in the bitcoin blockchain, proving an order of events and the integrity of past data. 比特币还依赖于加密协议。 [公私密钥加密](https://security.stackexchange.com/questions/25741/how-can-i-explain-the-concept-of-public-and-private-keys-without-technical-jargo)技术用于让个人安全、独家地控制他们的比特币。 [哈希函数](https://medium.com/@ConsenSys/blockchain-underpinnings-hashing-7f4746cbd66b)用于“链接” 比特币区块链中的每个区块，证明事件的顺序和过去数据的完整性。 

Cryptographic protocols like these give us the basic tools necessary to build reliable, secure systems like Bitcoin. Without something like public-private key infrastructure, we could not guarantee to a user that they have _exclusive_control over their bitcoin. Without something like hashing functions, nodes would not be able to guarantee the integrity of the history of bitcoin transactions contained in Bitcoin’s blockchain.  
像这样的加密协议为我们提供了构建像比特币这样可靠、安全的系统所必需的基本工具。如果没有像公私密钥基础设施这样的东西，我们就无法 向用户保证他们对自己的比特币拥有_独家_控制权。如果没有哈希函数之类的东西，节点将无法 保证比特币区块链中包含的比特币交易历史的完整性。

Without the _hardness_ of cryptographic protocols like hashing functions or public-private key cryptography, we would have no secure unit of account with which to reward miners - no confidence that our record of past accounts was authentic and exclusively controlled by a rightful owner. Without a carefully calibrated set of incentives to reward an industry of miners, that unit of account could have no market value because there would be no confidence that the system could persist into the future.  
如果没有_哈希_函数或公私密钥加密等加密协议的严格要求，我们将没有安全的账户单位来奖励矿工 - 无法确信我们过去账户的记录是真实的，并且完全由合法所有者控制。如果没有一套精心校准的激励措施来奖励一个矿工行业，那么这个记账单位就没有市场价值，因为人们就没有信心认为该系统能够持续到未来。

In this way, bitcoin's design requires an understanding of both cryptography and how incentives affect the security properties and functionality of systems built with cryptography. Cryptoeconomics is strange and counterintuitive. Most of us are not used to thinking of money as a design or engineering problem, nor are we used to economic incentive design being an essential component of a new technology. Cryptoeconomics requires us to [think about information security problems in _economic terms_](https://youtu.be/u6VSPD5TrP4?t=6m11s). 通过这种方式，比特币的设计需要了解密码学以及激励如何影响使用密码学构建的系统的安全属性和功能。加密经济学是奇怪且违反直觉的。我们大多数人不习惯将金钱视为设计或工程问题，也不习惯 将经济激励设计视为新技术的重要组成部分。加密经济学要求我们从[_经济角度_考虑信息安全问题](https://youtu.be/u6VSPD5TrP4?t=6m11s)。 

One of the most common mistakes in this industry is made by those who view blockchains only through a lens of computer science or applied cryptography. We have a strong tendency to prioritize the things we are most comfortable with, and see things outside of our domain of expertise as less important.   
这个行业最常见的错误之一是那些仅通过计算机科学或应用密码学的视角来看待区块链的人所犯的。我们有一种强烈的倾向，即优先考虑我们最熟悉的事情，而认为我们专业领域之外的事情不那么重要。

In blockchain technology, this leads many people to assume or abstract away the crucial role of economic incentives. This is one reason we see meaningless phrases like "[blockchains are trustless](https://medium.com/@ntmoney/trustless-is-a-misnomer-956066661b79)," "[bitcoin is backed only by math](https://bitcoin.org/en/faq#why-do-bitcoins-have-value)" or "[blockchains are immutable](https://www.coindesk.com/markets/2017/05/09/the-blockchain-immutability-myth/)." These are all wrong in their own way, but all have the effect of obfuscating the essential role of a large network of people whose necessary participation in the network is maintained through economic incentives. 

Cryptoeconomic systems like bitcoin _feel_ like magic to someone who views them only as a product of computer science, because bitcoin can do things that computer-science alone could never accomplish. Cryptoeconomics isn’t magic – it’s just interdisciplinary.  
像比特币这样的加密经济系统 对于仅将其视为计算机科学产品的人来说感觉就像魔法，因为比特币可以做计算机科学本身永远无法完成的事情。加密经济学不是魔法——它只是跨学科的。

## 2. How does it relate to economics more generally?  
2. 它与更普遍的经济学有什么关系？

The term cryptoeconomics can be misleading because it suggests a comparison to economics as a whole. This is part of what leads people like Parker to dismiss the term. Economics is the study of choice: how people and groups of people respond to incentives. The invention of cryptocurrency and blockchain technology does not require a new theory of human choice – the humans haven’t changed. Cryptoeconomics is _not_ the application of macroeconomic and microeconomic theory to cryptocurrency or token markets.  
加密经济学 一词可能具有误导性，因为它建议与整个经济学进行比较。这是导致像 Parker 这样的人不屑一顾这个词的部分原因。经济学是一门关于选择的研究：人们和群体如何对激励措施做出反应。加密货币和区块链技术的发明不需要新的人类选择理论—— 人类并没有改变。加密经济学_不是_宏观经济和微观经济理论对加密货币或代币市场的应用。

Cryptoeconomics has most in common with _mechanism design_, a field related to game theory. In game theory, we look at a given strategic interaction (a "game") and then try to understand the best strategies for each player, and the likely outcome if both players follow those strategies. For instance, we might use game theory to look at a negotiation between two firms, relations between countries or even evolutionary biology.   
加密经济学与_机制设计_最相似，这是一个与博弈论相关的领域。在博弈论中，我们着眼于给定的战略互动（“博弈”），然后尝试了解每个玩家的最佳策略，以及如果两个玩家都遵循这些策略可能的结果。例如，我们可能会使用博弈论来研究两家公司之间的谈判、国家之间的关系，甚至是进化生物学。

Mechanism design is often referred to as _reverse_ game theory because we start with a desired outcome and then work backwards to design a game that, if players pursue their own self interest, will produce the outcome we want. For instance, imagine we are responsible for designing the rules of an auction. We have an objective that we want bidders to actually bid the real value they place on an item. To achieve this, we apply economic theory to design the auction as a game [where the dominant strategy for any player is to always bid their true value](https://en.wikipedia.org/wiki/Vickrey_auction#Proof_of_dominance_of_truthful_bidding). One solution to this problem is called a [Vickrey auction](https://en.wikipedia.org/wiki/Vickrey_auction#Proof_of_dominance_of_truthful_bidding), where bids are secret and the winner of the auction (defined as the player with the highest bid) only pays the second highest amount that was bid.  
机制设计通常被称为_反向_博弈论，因为我们从一个期望的结果开始，然后逆向工作来设计一个游戏，如果玩家追求自己的利益，就会产生我们想要的结果。例如，假设我们负责设计拍卖规则。我们有一个目标，即希望出价者实际出价他们为物品赋予的实际价值。为了实现这一目标，我们应用经济理论将拍卖设计成一个游戏 [，其中任何玩家的主导策略都是始终出价他们的真实价值](https://en.wikipedia.org/wiki/Vickrey_auction#Proof_of_dominance_of_truthful_bidding)。此问题的一种解决方案称为 [Vickrey 拍卖](https://en.wikipedia.org/wiki/Vickrey_auction#Proof_of_dominance_of_truthful_bidding)，其中出价是秘密的，拍卖的获胜者（定义为出价最高的玩家）只需支付出价第二高的金额。

Cryptoeconomics, like mechanism design, focuses on designing and creating systems. Like in our auction example, we use economic theory to design "rules" or mechanisms that produce a certain equilibrium outcome. But in cryptoeconomics, the mechanisms used to create economic incentives are [built using cryptography and software](https://docs.google.com/presentation/d/1-2NMcrqWOvrjcDTjiYfLHc5cNNsMpzq6FodDVkfDNZE/edit#slide=id.g6eb8cd7660a986c30) and the systems we are designing are almost always [distributed or decentralized](https://medium.com/@VitalikButerin/the-meaning-of-decentralization-a0c92b76a274). 加密经济学与机制设计一样，专注于设计和创建系统。就像我们的拍卖示例一样，我们使用经济理论来设计产生某种均衡结果的“规则”或机制。但在加密经济学中，用于创建经济激励的机制是使用 [密码学和软件构建的](https://docs.google.com/presentation/d/1-2NMcrqWOvrjcDTjiYfLHc5cNNsMpzq6FodDVkfDNZE/edit#slide=id.g6eb8cd7660a986c30)，我们正在设计的系统几乎总是[分布式或去中心化](https://medium.com/@VitalikButerin/the-meaning-of-decentralization-a0c92b76a274)的。 

Bitcoin is a product of this approach. Satoshi wanted bitcoin to have certain properties – for instance, that it be able to reach consensus about its internal state and that it be censorship-resistant. Then, Satoshi set out to design a system that would achieve those properties, assuming people responded in rational ways to economic incentives.

Most often, cryptoeconomics is used to provide a _security guarantee_ about a distributed system. For instance, we have a cryptoeconomic security guarantee that the bitcoin blockchain is secure against a 51 percent attack unless someone is [willing to spend a few billion dollars](https://gobitcoin.io/tools/cost-51-attack/). Or, in a state channel – a topic we discuss later – we can have a cryptoeconomic security guarantee that an off-chain process is nearly as secure and final as an on-chain transaction.  
大多数情况下，加密经济学用于提供有关分布式系统_的安全保证_。例如，我们有一个加密经济安全保证，除非有人[愿意花几十亿美元](https://gobitcoin.io/tools/cost-51-attack/)，否则比特币区块链可以抵御 51% 的攻击。或者，在状态通道中（我们稍后讨论的话题）， 我们可以有一个加密经济安全保证，即链下过程几乎与链上交易一样安全和最终。

It is worth noting that mechanism design is not a panacea. There is a limit to how much we can rely on incentives to predictably shape future behaviour. As [Nick Szabo rightly points out](https://twitter.com/nickszabo4/status/882738070616809472), ultimately we are speculating about people's future mental states and making assumptions about how they react to certain incentives. A cryptoeconomic system's security guarantee depends in part on the strength of its assumptions about how people react to economic incentives.  
值得注意的是，机构设计并不是万能的。我们可以依赖激励措施来预测性地塑造未来行为的程度是有限的。正如 [Nick Szabo 正确指出](https://twitter.com/nickszabo4/status/882738070616809472)的那样，最终我们是在推测人们未来的心理状态，并假设他们对某些激励措施的反应。加密经济系统的安全保证部分取决于其对人们如何对经济激励做出反应的假设的强度。

## Three examples of cryptoeconomics  
加密经济学的三个例子

There are at least three different kinds of systems being designed today that could be called “cryptoeconomic”.  
今天至少有三种不同类型的系统可以称为“加密经济学”。

### Example 1: Consensus protocols  
示例 1：共识协议

Blockchains are able to reach reliable consensus without having to rely on a central trusted party – a product of cryptoeconomic design. Bitcoin's solution, which we surveyed above, is called "proof-of-work" consensus because miners must commit _work_ – in the form of hardware and electricity – in order to be participate in the network and receive mining rewards. 区块链能够达成可靠的共识，而不必依赖中央可信方——加密经济设计的产物。我们上面调查的比特币解决方案被称为“工作量证明”共识，因为矿工必须以硬件和电力的形式投入工作 ， 才能参与网络并获得挖矿奖励。 

Improving proof-of-work systems and designing alternatives to them is one active area of cryptoeconomic research and design. Ethereum’s current proof-of-work consensus mechanism includes many variations and improvements on the original design, enabling [faster block times](https://blog.ethereum.org/2015/09/14/on-slow-and-fast-block-times/) and being more [resistant to the mining centralization that can result from ASICs](https://ethereum.stackexchange.com/questions/16811/is-ethereum-asic-resistant).  
改进工作量证明系统并设计替代方案是加密经济学研究和设计的一个活跃领域。以太坊目前的工作量证明共识机制包括对原始设计的许多变化和改进，从而实现[更快的区块时间](https://blog.ethereum.org/2015/09/14/on-slow-and-fast-block-times/)，并更[能抵抗 ASIC 可能导致的挖矿集中化](https://ethereum.stackexchange.com/questions/16811/is-ethereum-asic-resistant)。

In the near future, ethereum plans to migrate to a "proof-of-stake" consensus protocol called Casper. This is an alternative to proof-of-work that does not require "mining" in the usual sense: there is no need for specialized mining hardware or huge expenditures of electricity.   
在不久的将来，以太坊计划迁移到名为 Casper 的“权益证明”共识协议。这是工作量证明的替代方案，不需要通常意义上的“挖矿”：不需要专门的挖矿硬件或巨大的电力支出。

Remember that the whole point of requiring miners to buy hardware and spend electricity is to impose a cost on miners, as a way of raising the cumulative cost of attempting a 51 percent attack sufficiently high that it becomes too expensive. The idea behind proof-of-stake systems is to use deposits of cryptocurrency to create the same disincentive, rather than real-world investments like hardware and electricity.   
请记住，要求矿工购买硬件和花电的全部意义在于给矿工带来成本，以此将尝试 51% 攻击的累积成本提高到足够高的程度，以至于它变得太昂贵了。权益证明系统背后的想法是使用加密货币存款来产生相同的抑制作用，而不是硬件和电力等现实世界的投资。

In order to mine in a proof-of-stake system, you must commit a certain amount of ether into a smart contract "bond." Just like in proof-of-work, this raises the cost of a 51 percent attack – an attacker would have to commit a very large amount of ether to successfully attack the network, which they would then lose forever.  
为了在权益证明系统中挖矿，您必须将一定量的以太币投入到智能合约“债券”中。就像在工作量证明中一样，这增加了 51% 攻击的成本——攻击者必须投入大量以太币才能成功攻击网络，然后他们将永远失去这些网络。

Casper is being designed by Vlad Zamfir, Vitalik Buterin, and others at the Ethereum Foundation. You can read more about the history of Casper's design [in this series of posts by Zamfir](https://medium.com/@Vlad_Zamfir/the-history-of-casper-part-1-59233819c9a9) or hear him talk about it on a [recent podcast](https://www.youtube.com/watch?v=9nQPcNY32JQ). Buterin wrote a long post about Casper's design philosophy [here](https://medium.com/@VitalikButerin/a-proof-of-stake-design-philosophy-506585978d51), and there is a useful FAQ on the ethereum GitHub wiki [here](https://github.com/ethereum/wiki/wiki/Proof-of-Stake-FAQ).  
Casper 由以太坊基金会的 Vlad Zamfir、Vitalik Buterin 和其他人设计。您可以在 [Zamfir 的这一系列文章中](https://medium.com/@Vlad_Zamfir/the-history-of-casper-part-1-59233819c9a9)阅读有关 Casper 设计历史的更多信息，或者在[最近的播客](https://www.youtube.com/watch?v=9nQPcNY32JQ)中 聆听他的讨论。 Buterin 在这里写了一篇关于 Casper 设计理念的长文[](https://medium.com/@VitalikButerin/a-proof-of-stake-design-philosophy-506585978d51)，以太坊 GitHub wiki 上有一个有用的常见问题解答[](https://github.com/ethereum/wiki/wiki/Proof-of-Stake-FAQ)。

### Example 2: Cryptoeconomic application design  
示例 2：加密经济应用程序设计

Once we have solved the fundamental problem of blockchain consensus, we are able to build applications that sit "on top" of a blockchain like ethereum. The underlying blockchain gives us (1) a unit of value that can be used to create incentives and penalties, and (2) a toolkit with which we can design conditional logic in the form of "[smart contract code](https://www.coindesk.com/markets/2016/06/04/making-sense-of-blockchain-smart-contracts/)." The applications we build with these tools can also be a product of cryptoeconomic design.  
一旦我们解决了区块链共识的基本问题，我们就能够构建位于以太坊等区块链“之上”的应用程序。底层区块链为我们提供了 （1） 一个可用于创建激励和惩罚的价值单位，以及 （2） 一个工具包，我们可以使用它以“[智能合约代码](https://www.coindesk.com/markets/2016/06/04/making-sense-of-blockchain-smart-contracts/)”的形式设计条件逻辑。我们使用这些工具构建的应用程序也可以是加密经济设计的产物。

For instance, the prediction market [Augur](https://augur.net/) requires cryptoeconomic mechanisms in order to function. Using its native token REP, Augur creates a [system of incentives](http://blog.augur.net/faq/how-does-reputation-rep-work/) that rewards users for reporting the "truth" to the application, which is then used to settle bets in the prediction market. This is the innovation that makes a decentralized prediction market possible. Another prediction market, [Gnosis](https://blog.gnosis.pm/introducing-the-gnosis-tokens-gno-and-wiz-5295a65c3822), uses a similar method, though also lets users specify other mechanisms for determining true outcomes (commonly called "oracles").  
例如，预测市场 [Augur](https://augur.net/) 需要加密经济机制才能运作。Augur 使用其原生代币 REP 创建了一个[激励系统](http://blog.augur.net/faq/how-does-reputation-rep-work/)，奖励用户向应用程序报告“真相”，然后用于在预测市场中结算赌注。这就是使去中心化预测市场成为可能的创新。另一个预测市场 [Gnosis](https://blog.gnosis.pm/introducing-the-gnosis-tokens-gno-and-wiz-5295a65c3822) 使用类似的方法，但也允许用户指定其他机制来确定真实结果（通常称为“预言机”）。

Cryptoeconomics is also applied to design token sales or ICOs. Gnosis, for instance, [used a "Dutch auction"](https://blog.gnosis.pm/introducing-the-gnosis-token-launch-3cc4cffb5098) as a model for its token auction, on the theory that this would result in a more fair distribution (an experiment that had [mixed results](http://vitalik.ca/general/2017/06/09/sales.html)). We mentioned earlier that one area where mechanism design has been applied is in the design of auctions, and token sales gives us a new opportunity to apply some of that theory.  
加密经济学也应用于设计代币销售或 ICO。例如，Gnosis [使用 “Dutch auction”](https://blog.gnosis.pm/introducing-the-gnosis-token-launch-3cc4cffb5098) 作为其代币拍卖的模型 ，其理论上这会导致更公平的分配（一个[结果喜忧参半](http://vitalik.ca/general/2017/06/09/sales.html)的实验）。我们之前提到过，应用机制设计的一个领域是拍卖的设计，而代币销售给了我们一个新的机会来应用一些该理论。

These are a different kind of problem than building the underlying consensus protocols, but they share enough similarities that both can be fairly seen as cryptoeconomic. Building these applications requires an understanding of how incentives shape users' behaviour and careful design of economic mechanisms that can reliably produce a certain result. They also require an understanding of the capabilities and limitations of the underlying blockchain on which the application is built.  
这些与构建底层共识协议的问题不同，但它们具有足够的相似之处，以至于两者都可以公平地被视为加密经济学。构建这些应用程序需要了解激励措施如何影响用户的行为，并仔细设计能够可靠地产生特定结果的经济机制。他们还需要了解构建应用程序的底层区块链的功能和限制。

Many blockchain applications are not products of cryptoeconomics; for instance, applications like [Status](http://status.im/) and [Metamask](https://metamask.io/) – wallets or platforms that let users interact with the ethereum blockchain. These do not involve any additional cryptoeconomic mechanisms beyond those that are already part of the underlying blockchain.  
许多区块链应用程序不是加密经济学的产品;例如，[Status](http://status.im/) 和 [Metamask](https://metamask.io/) 等应用程序——允许用户与以太坊区块链交互的钱包或平台。这些不涉及除了已经是底层区块链一部分的机制之外的任何其他加密经济机制。

### Example 3: State channels  
示例 3：状态通道

Cryptoeconomics also includes the practice of designing much smaller sets of interactions between individuals. The most notable of these are [state channels](http://www.jeffcoleman.ca/state-channels/). State channels are not an application but a valuable technique that can be used by most blockchain applications to become more efficient.  
加密经济学还包括设计个人之间更小的交互集的实践。其中最值得注意的是 [state channels](http://www.jeffcoleman.ca/state-channels/)。状态通道不是一个应用程序，而是一种有价值的技术，大多数区块链应用程序都可以使用它来提高效率。

A fundamental limitation of blockchain applications is that blockchains are expensive. Sending transactions requires fees, and using ethereum to run smart-contract code is [comparatively costly](https://hackernoon.com/ether-purchase-power-df40a38c5a2f) to other kinds of computation. The idea behind state channels is that we can make blockchains more efficient by moving many processes off-chain, while still retaining a blockchain's characteristic trustworthiness, through the use of cryptoeconomic design.  
区块链应用程序的一个基本限制是区块链成本高昂。发送交易需要费用，并且使用以太坊运行智能合约代码比其他类型的计算[成本相对较高](https://hackernoon.com/ether-purchase-power-df40a38c5a2f)。状态通道背后的想法是，我们可以通过使用加密经济设计将许多流程转移到链下，同时仍然保持区块链特有的可信度，从而提高区块链的效率。

Imagine Alice and Bob want to exchange a large number of small payments of cryptocurrency. The normal way for them to do this would be to send transactions to the blockchain. This is inefficient – it requires paying transaction fees and waiting for the confirmation of new blocks.  
想象一下 Alice 和 Bob 想要兑换大量小额加密货币。他们这样做的正常方式是将交易发送到区块链。这是低效的——它需要支付交易费用并等待新区块的确认。

Instead, imagine that Alice and Bob sign transactions that [could be submitted to the blockchain, but are not](http://www.jeffcoleman.ca/state-channels/). They pass these back and forth between one another, as fast as they want – there are no fees, because nothing is actually hitting the blockchain yet. Each update "trumps" the last one, updating the balance between the parties.   
相反，假设 Alice 和 Bob 签署[了可以提交到区块链的交易，但实际上并非](http://www.jeffcoleman.ca/state-channels/)如此。他们以最快的速度在彼此之间来回传递这些信号—— 没有费用，因为还没有任何东西真正进入区块链。每次更新都“胜过”上一次，更新了各方之间的平衡。

When Alice and Bob have finished exchanging small payments, they "close out" the channel by submitting the final state (i.e. the most recent signed transaction) to the blockchain, paying only a single transaction fee for an unlimited number of transactions between themselves. They can trust this process because both Alice and Bob know that each update passed between them could be sent to the blockchain. If the channel is properly designed, there is no way to cheat – say, by trying to submit a previous update as though it were the most recent – since recourse to the blockchain is always available.  
当 Alice 和 Bob 完成小额支付交换后，他们通过将最终状态（即最近签署的交易）提交到区块链来“关闭”通道，只需为他们之间的无限数量的交易支付单笔交易费用。他们可以信任这个过程，因为 Alice 和 Bob 都知道他们之间传递的每个更新都可以发送到区块链。如果通道设计得当，就没有办法作弊——比如，试图提交以前的更新，就好像它是最新的一样——因为区块链的求助权总是可用的。

For illustrative purposes, you can think of this as similar to how we interact with other trusted sources, like a legal system. When two parties sign a contract, most of the time they never need to take that contract to court and ask a judge to interpret and enforce it. If the contract is properly designed, both parties simply do what they promised to do, and never interact with the courts at all. The fact that either party could go to the court and have the contract enforced is enough to make the contract useful.  
为了便于说明，您可以将其视为类似于我们与其他可信来源（如法律系统）的交互方式。当双方签订合同时，大多数时候他们不需要将该合同告上法庭并要求法官解释和执行它。如果合同设计得当，双方都只是按照他们承诺的事情去做，根本不与法院互动。任何一方都可以诉诸法院并要求执行合同的事实足以使合同有用。

This technique is not just useful for payments, but for any update to the state of an ethereum program – hence the more general term "state channel" rather than the narrow "payment channel." Instead of sending payments back and forth, we can send updates to a smart contract back and forth. We can even send entire ethereum smart contracts that, if needed, will be sent to the blockchain and executed. These programs never have to be executed to be useful. All that is needed is a sufficiently high guarantee that they [_could be executed if necessary_](https://github.com/ledgerlabs/state-channels/wiki/Counterfactual-Terminology)_._  
这种技术不仅适用于支付，而且对以太坊程序状态的任何更新都很有用——因此更通用的术语是 “状态通道” ，而不是狭义的 “支付通道”。我们可以来回发送对智能合约的更新，而不是来回发送付款。我们甚至可以发送整个以太坊智能合约，如果需要，这些合同将被发送到区块链并执行。这些程序永远不必执行才有用。所需要的只是一个足够高的保证，以便在[_必要时可以执行_](https://github.com/ledgerlabs/state-channels/wiki/Counterfactual-Terminology)_它们。_

In the future, most blockchain applications will use state channels in some form. It is almost always a strict improvement to require less on-chain operation, and many things done on-chain today can be moved into state channels while still preserving a sufficiently high guarantee to be useful.  
未来，大多数区块链应用程序将以某种形式使用状态通道。要求更少的链上操作几乎总是一个严格的改进，今天在链上完成的许多事情都可以转移到状态通道中，同时仍然保持足够高的保证以发挥作用。

The description above skips over many important details and nuances of how state channels work. For a more detailed description, Ledger Labs [built a toy implementation last summer](https://github.com/ledgerlabs/state-channels/wiki/Example-State-Channel) that demonstrates the basic concept. 上面的描述跳过了 state 通道工作原理的许多重要细节和细微差别。有关更详细的描述，Ledger Labs [在去年夏天构建了一个玩具实现](https://github.com/ledgerlabs/state-channels/wiki/Example-State-Channel)，演示了基本概念。 

## Conclusion 结论

Thinking about the blockchain space through the lens of cryptoeconomics is helpful. Once you understand the idea, it helps to clarify many of the controversies and debates in our industry.  
通过加密经济学的视角来思考区块链空间是有帮助的。一旦你理解了这个想法，它就会有助于澄清我们行业中的许多争议和辩论。

For instance, "permissioned" blockchains that are centrally managed and do not use proof-of-work have been a source of constant controversy since they were first proposed. This area of work is often referred to as "distributed ledger technology" and is focused on financial and enterprise use cases. [Many partisans of blockchain technology dislike them](https://www.reddit.com/r/Bitcoin/comments/316sdy/to_ibm_stop_this_blockchain_nonsense_it_will/) – they may be blockchains in the literal sense, but there is something about them that feels wrong. They seem to reject the thing that many people see as the whole point of blockchain technology: being able to produce consensus _without_ relying on a central party or traditional financial systems.  
例如，集中管理且不使用工作量证明的“许可”区块链自首次提出以来一直是争议的来源。这个工作领域通常被称为 “分布式账本技术”，专注于金融和企业用例。[许多区块链技术的拥护者不喜欢它们](https://www.reddit.com/r/Bitcoin/comments/316sdy/to_ibm_stop_this_blockchain_nonsense_it_will/) ——它们可能是字面意义上的区块链，但它们有一些地方让人感觉不对劲。他们似乎拒绝了许多人认为区块链技术的全部意义所在：能够在_不_依赖中央政党或传统金融系统的情况下产生共识。

A cleaner way to make this distinction is between blockchains that are products of cryptoeconomics and blockchains that are not. Blockchains that are simply distributed ledgers and do not rely on cryptoeconomic design to produce consensus or align incentives might be useful for some applications. But they are distinct from blockchains whose whole purpose is to use cryptography and economic incentives to produce consensus that could not exist before, like bitcoin and ethereum. These are two _different_ technologies, and the clearest way of distinguishing between them is whether or not they are products of cryptoeconomics.  
区分这种区别的更清晰的方法是区分属于加密经济学产品的区块链和非加密经济学产品的区块链。简单的分布式账本且不依赖加密经济设计来产生共识或调整激励措施的区块链可能对某些应用程序有用。但它们与区块链不同，区块链的全部目的是使用密码学和经济激励来产生以前不存在的共识，例如比特币和以太坊。这是两种_不同的_技术，区分它们最清晰的方法是它们是否是加密经济学的产物。

Secondly, we should expect that there will be cryptoeconomic consensus protocols that do not rely on a literal chain of blocks. Obviously, such a technology would have something in common with blockchain technology as we call it today, but labelling them blockchains would be inaccurate. Again, the relevant organizing concept is whether such a protocol is the product of cryptoeconomics, not whether it is a blockchain.  
其次，我们应该预期会有不依赖于字面意义上的区块链的加密经济共识协议。显然，这种技术与我们今天所说的区块链技术有一些共同之处，但将它们标记为区块链是不准确的。同样，相关的组织概念是这样的协议是否是加密经济学的产物，而不是它是否是区块链。

The ICO craze has also focused attention on this distinction, though few have articulated it clearly. [Many](https://news.21.co/thoughts-on-tokens-436109aabcbe) [people](https://thecontrol.co/tokens-tokens-and-more-tokens-d4b177fbb443) [independently](https://medium.com/@datarade/criterion-for-high-fidelity-token-sales-1391ff20af20) [identified](https://www.coindesk.com/markets/2017/03/03/a-framework-for-valuing-crypto-tokens/) that one of the strongest signs of a token's value is whether it forms a necessary component of the application to which it is connected. To put this in clearer terms, the question should be: is the token part of a necessary cryptoeconomic mechanism in the application? Understanding the mechanism design of a project holding an ICO is an essential tool in determining that token's utility and likely value.  
ICO 热潮也使人们的注意力集中在这种区别上，尽管很少有人清楚地阐明它。 [许多人](https://news.21.co/thoughts-on-tokens-436109aabcbe)[](https://thecontrol.co/tokens-tokens-and-more-tokens-d4b177fbb443)[独立](https://medium.com/@datarade/criterion-for-high-fidelity-token-sales-1391ff20af20)[地发现](https://www.coindesk.com/markets/2017/03/03/a-framework-for-valuing-crypto-tokens/)，代币价值的最强标志之一是它是否构成它所连接的应用程序的必要组成部分。为了更清楚地说明这一点，问题应该是：代币是应用程序中必要的加密经济机制的一部分吗？了解持有 ICO 的项目的机制设计是确定该代币的效用和可能价值的重要工具。

In the past years, we've moved from thinking about this new field solely through the lens of one application (bitcoin), to thinking about it in terms of one underlying technology (blockchains). What needs to happen now is to step back once again and view this industry in terms of a unifying approach to solving problems: cryptoeconomics.   
在过去的几年里，我们已经从仅仅通过一个应用程序（比特币）的视角来思考这个新领域，转变为从一种底层技术（区块链）的角度来思考它。现在需要做的是再次退后一步，从解决问题的统一方法的角度来看待这个行业：加密经济学。

_Thanks to Jeff Coleman, Ethan Wilding, and Vlad Zamfir for their comments on an earlier draft of this article.  
感谢 Jeff Coleman、Ethan Wilding 和 Vlad Zamfir 对本文早期草稿的评论。_

_**Disclosure**: CoinDesk is a subsidiary of Digital Currency Group, which has an ownership stake in Zerocoin Electric Coin Company, developer of zcash.  
**披露**：CoinDesk 是 Digital Currency Group 的子公司，该集团拥有 zcash 开发商 Zerocoin Electric Coin Company 的所有权股份。_

_[Understanding economics](https://www.shutterstock.com/image-photo/concept-business-negotiation-businessmen-talking-about-471922493) image via Shutterstock  
通过 Shutterstock [了解经济学](https://www.shutterstock.com/image-photo/concept-business-negotiation-businessmen-talking-about-471922493)图片_

[Newsletter  通讯](https://www.coindesk.com/newsletters/)Archived 存档

[MoneyReimagined  
重新构想货币](https://www.coindesk.com/newsletters/money-reimagined)

Sign up for Money Reimagined, was a weekly newsletter exploring the transformation of value in the digital age.  
注册 Money Reimagined，这是一份探索数字时代价值转型的周报。

Enter your Email 输入您的电子邮件

Sign Up 登记

By clicking ‘Sign Up’, you agree to receive newsletter from CoinDesk as well as other partner offers and accept our [terms of services](https://www.coindesk.com/terms/) and [privacy policy](https://www.coindesk.com/privacy/).

DISCLOSURE

Please note that our [privacy policy](https://www.coindesk.com/privacy/), [terms of use](https://www.coindesk.com/terms/), [cookies](https://www.coindesk.com/privacy/#cookies), and [do not sell my personal information](https://www.coindesk.com/privacy/#dnsmpi) have been updated.  
  
CoinDesk is an [award-winning](https://www.coindesk.com/business/2023/02/20/coindesk-wins-a-polk-award-a-top-journalism-prize-for-explosive-ftx-coverage/) media outlet that covers the cryptocurrency industry. Its journalists abide by a strict set of [editorial policies](https://www.coindesk.com/ethics/). CoinDesk has adopted a set of principles aimed at ensuring the integrity, editorial independence and freedom from bias of its publications. CoinDesk is part of the Bullish group, which owns and invests in digital asset businesses and digital assets. CoinDesk employees, including journalists, may receive Bullish group equity-based compensation. Bullish was incubated by technology investor Block.one.

![Author placeholder image](https://www.coindesk.com/resizer/jNh5B6WmVaNKBHR7zDOmXB8JbG0=/192x192/filters:quality(80):format(jpg)/downloads.coindesk.com/arc/failsafe/user/1x1.png)

Josh Stark

---

Read more about

[Blockchain Technology](https://www.coindesk.com/tag/blockchain-tech/)[Ethereum](https://www.coindesk.com/tag/ethereum/)[Bitcoin](https://www.coindesk.com/tag/markets-bitcoin/)[Cryptoeconomics](https://www.coindesk.com/tag/cryptoeconomics/)[Features](https://www.coindesk.com/tag/features/)[other-public-protocols](https://www.coindesk.com/tag/other-public-protocols/)

[![Coindesk Logo](https://www.coindesk.com/pf/resources/images/logos/coindesk_logo_190x32.svg?d=371)](https://www.coindesk.com/)

About

[About](https://www.coindesk.com/about/)[Masthead](https://www.coindesk.com/masthead/)[Careers](https://bullish.wd3.myworkdayjobs.com/CoinDesk)[CoinDesk News](https://www.coindesk.com/coindesk-news/)

Stay Updated

[Consensus](http://consensus.coindesk.com/)[CoinDesk Studios](https://www.coindesk.com/coindeskstudios)[Newsletters](https://www.coindesk.com/newsletters/)[Follow](https://www.coindesk.com/follow/)

Get In Touch

[Contact Us](https://www.coindesk.com/contact-us/)[Advertise](https://www.coindesk.com/advertise/)[Accessibility Help](https://www.coindesk.com/accessibility-help/)[Sitemap](https://www.coindesk.com/sitemap/)

The Fine Print

[Ethics Policy](https://www.coindesk.com/ethics/)[Privacy](https://www.coindesk.com/privacy/)[Terms Of Use](https://www.coindesk.com/terms/)

###### Update My Cookie Consent

[Do Not Sell My Personal Information](https://www.coindesk.com/privacy/#dnsmpi)

---

Please note that our [privacy policy](https://www.coindesk.com/privacy/), [terms of use](https://www.coindesk.com/terms/), [cookies](https://www.coindesk.com/privacy/#cookies), and [do not sell my personal information](https://www.coindesk.com/privacy/#dnsmpi) have been updated.  
  
CoinDesk is an [award-winning](https://www.coindesk.com/business/2023/02/20/coindesk-wins-a-polk-award-a-top-journalism-prize-for-explosive-ftx-coverage/) media outlet that covers the cryptocurrency industry. Its journalists abide by a strict set of [editorial policies](https://www.coindesk.com/ethics/). CoinDesk has adopted a set of principles aimed at ensuring the integrity, editorial independence and freedom from bias of its publications. CoinDesk is part of the Bullish group, which owns and invests in digital asset businesses and digital assets. CoinDesk employees, including journalists, may receive Bullish group equity-based compensation. Bullish was incubated by technology investor Block.one.

©2024 CoinDesk

English![MenuUpIcon](https://www.coindesk.com/pf/resources/images/icons/MenuUpIcon.svg?d=371)

[](https://twitter.com/coindesk)[](https://www.facebook.com/coindesk)[](https://www.linkedin.com/company/coindesk/)

[](https://www.coindesk.com/arc/outboundfeeds/rss/)[](https://www.instagram.com/coindesk/)[](https://www.youtube.com/coindesk)

[![TikTokIcon](https://www.coindesk.com/pf/resources/images/icons/TikTokIcon.svg?d=371)](https://www.tiktok.com/@coindesk/)[](https://discord.com/invite/tRuUMkkQd9)[](https://t.me/CoinDeskGlobal)