---
title: 比特币的学术血统
draft: true
assets:
  - https://portal.acm.org/citation.cfm?id=3136559
---
## The concept of cryptocurrencies is built from forgotten ideas in research literature.  
加密货币的概念是从研究文献中被遗忘的想法建立起来的。

### Arvind Narayanan and Jeremy Clark  
Arvind Narayanan 和 Jeremy Clark

  

If you've read about bitcoin in the press and have some familiarity with academic research in the field of cryptography, you might reasonably come away with the following impression: Several decades' worth of research on digital cash, beginning with David Chaum,10,12 did not lead to commercial success because it required a centralized, banklike server controlling the system, and no banks wanted to sign on. Along came bitcoin, a radically different proposal for a decentralized cryptocurrency that didn't need the banks, and digital cash finally succeeded. Its inventor, the mysterious Satoshi Nakamoto, was an academic outsider, and bitcoin bears no resemblance to earlier academic proposals.  
如果你在报纸上读过关于比特币的信息，并且对密码学领域的学术研究有一定的了解，你可能会合理地得到以下印象：从 David Chaum 开始的几十年来，对数字现金的研究，10,12 并没有带来商业上的成功，因为它需要一个集中的、类似银行的服务器来控制系统。 而且没有银行愿意签约。随之而来的是比特币，这是一种完全不同的去中心化加密货币提案，不需要银行，数字现金最终成功了。它的发明者，神秘的中本聪，是一位学术界的局外人，比特币与早期的学术提议没有任何相似之处。

This article challenges that view by showing that nearly all of the technical components of bitcoin originated in the academic literature of the 1980s and '90s (see figure 1). This is not to diminish Nakamoto's achievement but to point out that he stood on the shoulders of giants. Indeed, by tracing the origins of the ideas in bitcoin, we can zero in on Nakamoto's true leap of insight—the specific, complex way in which the underlying components are put together. This helps explain why bitcoin took so long to be invented. Readers already familiar with how bitcoin works may gain a deeper understanding from this historical presentation. (For an introduction, see _Bitcoin and Cryptocurrency Technologies_ by Arvind Narayanan et al.36) Bitcoin's intellectual history also serves as a case study demonstrating the relationships among academia, outside researchers, and practitioners, and offers lessons on how these groups can benefit from one another.  
本文通过表明比特币的几乎所有技术组件都起源于 1980 年代和 90 年代的学术文献来挑战这一观点（见图 1）。这并不是要贬低中本聪的成就，而是要指出他站在巨人的肩膀上。事实上，通过追溯比特币中思想的起源，我们可以专注于中本聪真正的洞察力飞跃——将底层组件组合在一起的具体、复杂的方式。这有助于解释为什么比特币花了这么长时间才被发明出来。已经熟悉比特币如何运作的读者可能会从这个历史介绍中获得更深入的理解。（有关介绍，请参阅 Arvind Narayanan 等人的_比特币和加密货币技术_36）比特币的思想史也是一个案例研究，展示了学术界、外部研究人员和从业者之间的关系，并提供了关于这些群体如何从彼此中受益的经验教训。

![Bitcoins Academic Pedigree](https://dl.acm.org/cms/attachment/869e2b3b-094e-4a3f-a6a7-2e096245521a/narayanan1.png)

### The Ledger 账本

If you have a secure ledger, the process to leverage it into a digital payment system is straightforward. For example, if Alice sends Bob $100 by PayPal, then PayPal debits $100 from Alice's account and credits $100 to Bob's account. This is also roughly what happens in traditional banking, although the absence of a single ledger shared between banks complicates things.   
如果您有一个安全的分类账，那么将其用于数字支付系统的过程很简单。例如，如果 Alice 通过 PayPal 向 Bob 发送 100 美元，则 PayPal 会从 Alice 的账户中借记 100 美元，并将 100 美元记入 Bob 的账户。这也大致与传统银行业务发生的情况相同，尽管银行之间没有共享的单一账本使事情复杂化。

This idea of a ledger is the starting point for understanding bitcoin. It is a place to record all transactions that happen in the system, and it is open to and trusted by all system participants. Bitcoin converts this system for recording payments into a currency. Whereas in banking, an account balance represents cash that can be demanded from the bank, what does a unit of bitcoin represent? For now, assume that what is being transacted holds value inherently.  
这个账本的概念是理解比特币的起点。它是一个记录系统中发生的所有交易的地方，它对所有系统参与者开放并受到信任。比特币将这个用于记录付款的系统转换为货币。在银行业中，账户余额代表可以从银行索取的现金，而比特币单位代表什么？现在，假设正在交易的东西本质上具有价值。

How can you build a ledger for use in an environment like the Internet where participants may not trust each other? Let's start with the easy part: the choice of data structure. There are a few desirable properties. The ledger should be immutable or, more precisely, _append only_: you should be able to add new transactions but not remove, modify, or reorder existing ones. There should also be a way to obtain a succinct _cryptographic digest_ of the state of the ledger at any time. A digest is a short string that makes it possible to avoid storing the entire ledger, knowing that if the ledger were tampered with in any way, the resulting digest would change, and thus the tampering would be detected. The reason for these properties is that unlike a regular data structure that's stored on a single machine, the ledger is a _global_ data structure collectively maintained by a mutually untrusting set of participants. This contrasts with another approach to decentralizing digital ledgers,7,13,21 in which many participants maintain local ledgers and it is up to the user querying this set of ledgers to resolve any conflicts.  
如何构建一个账本，以便在像 Internet 这样参与者可能不信任的环境中使用？让我们从简单的部分开始：数据结构的选择。有一些理想的特性。账本应该是不可变的，或者更准确地说，_仅附加_：您应该能够添加新交易，但不能删除、修改或重新排序现有交易。还应该有一种方法可以随时获取账本状态的简洁_加密摘要_。摘要是一个短字符串，可以避免存储整个账本，因为知道如果账本以任何方式被篡改，生成的摘要将发生变化，从而检测到篡改。这些属性的原因是，与存储在单台计算机上的常规数据结构不同，账本是由一组相互不信任的参与者共同维护的_全局_数据结构。这与另一种去中心化数字账本的方法形成鲜明对比，7,13,21 在这种方法中，许多参与者维护本地账本，由查询这组账本的用户来解决任何冲突。

#### Linked timestamping 链接时间戳

Bitcoin's ledger data structure is borrowed, with minimal modifications, from a series of papers by Stuart Haber and Scott Stornetta written between 1990 and 1997 (their 1991 paper had another co-author, Dave Bayer).5,22,23 We know this because Nakamoto says so in his bitcoin white paper.34 Haber and Stornetta's work addressed the problem of document timestamping—they aimed to build a "digital notary" service. For patents, business contracts, and other documents, one may want to establish that the document was created at a certain point in time, and no later. Their notion of document is quite general and could be any type of data. They do mention, in passing, financial transactions as a potential application, but it wasn't their focus.  
比特币的账本数据结构借鉴了 Stuart Haber 和 Scott Stornetta 在 1990 年至 1997 年间撰写的一系列论文（他们 1991 年的论文有另一位合著者 Dave Bayer），进行了极少的修改。5,22,23 我们知道这一点，因为中本聪在他的比特币白皮书中是这么说的。34 Haber 和 Stornetta 的工作解决了文档时间戳的问题 — 他们的目标是构建“数字公证”服务。对于专利、商业合同和其他文档，您可能希望确定文档是在某个时间点创建的，而不是更晚。他们的文档概念非常笼统，可以是任何类型的数据。他们确实顺便提到了金融交易是一个潜在的应用，但这不是他们的重点。

In a simplified version of Haber and Stornetta's proposal, documents are constantly being created and broadcast. The creator of each document asserts a time of creation and signs the document, its timestamp, and the previously broadcast document. This previous document has signed its own predecessor, so the documents form a long chain with pointers backwards in time. An outside user cannot alter a timestamped message since it is signed by the creator, and the creator cannot alter the message without also altering the entire chain of messages that follows. Thus, if you are given a single item in the chain by a trusted source (e.g., another user or a specialized timestamping service), the entire chain up to that point is locked in, immutable, and temporally ordered. Further, if you assume that the system rejects documents with incorrect creation times, you can be reasonably assured that documents are at least as old as they claim to be. At any rate, bitcoin borrows only the data structure from Haber and Stornetta's work and reengineers its security properties with the addition of the proof-of-work scheme described later in this article.   
在 Haber 和 Stornetta 提案的简化版本中，文档不断被创建和广播。每个文档的创建者都会声明创建时间，并对文档、其时间戳和之前广播的文档进行签名。前一个文档已经签署了自己的前身，因此这些文档形成了一个长链，指针在时间上向后移动。外部用户无法更改带时间戳的消息，因为它是由创建者签名的，并且创建者无法在不更改随后的整个消息链的情况下更改消息。因此，如果受信任的来源（例如，另一个用户或专门的时间戳服务）为你提供了链中的单个项目，那么到该点的整个链都是锁定的、不可变的和时间排序的。此外，如果您假设系统拒绝创建时间不正确的文档，则可以合理地确保文档至少与它们声称的一样古老。无论如何，比特币只借用了 Haber 和 Stornetta 的工作中的数据结构，并通过添加本文后面描述的工作量证明方案重新设计了其安全属性。

In their follow-up papers, Haber and Stornetta introduced other ideas that make this data structure more effective and efficient (some of which were hinted at in their first paper). First, links between documents can be created using hashes rather than signatures; hashes are simpler and faster to compute. Such links are called hash pointers. Second, instead of threading documents individually—which might be inefficient if many documents are created at approximately the same time—they can be grouped into batches or blocks, with documents in each block having essentially the same timestamp. Third, within each block, documents can be linked together with a binary tree of hash pointers, called a Merkle tree, rather than a linear chain. Incidentally, Josh Benaloh and Michael de Mare independently introduced all three of these ideas in 1991,6 soon after Haber and Stornetta's first paper.  
在他们的后续论文中，Haber 和 Stornetta 提出了其他使这种数据结构更加有效和高效的想法（其中一些在他们的第一篇论文中有所暗示）。首先，可以使用哈希而不是签名创建文档之间的链接;哈希的计算更简单、更快速。此类链接称为哈希指针。其次，可以将它们分组为批次或块，每个块中的文档具有基本相同的时间戳，而不是单独线程化文档（如果许多文档是在同一时间创建的，这可能会效率低下）。第三，在每个块中，文档可以通过哈希指针的二叉树（称为 Merkle 树）而不是线性链链接在一起。顺便说一句，Josh Benaloh 和 Michael de Mare 在 1991 年独立提出了这三个想法，6 在 Haber 和 Stornetta 的第一篇论文之后不久。

#### Merkle trees Merkle 树

Bitcoin uses essentially the data structure in Haber and Stornetta's 1991 and 1997 papers, shown in simplified form in figure 2 (Nakamoto was presumably unaware of Benaloh and de Mare's work). Of course, in bitcoin, transactions take the place of documents. In each block's Merkle tree, the leaf nodes are transactions, and each internal node essentially consists of two pointers. This data structure has two important properties. First, the hash of the latest block acts as a digest. A change to any of the transactions (leaf nodes) will necessitate changes propagating all the way to the root of the block, and the roots of all following blocks. Thus, if you know the latest hash, you can download the rest of the ledger from an untrusted source and verify that it hasn't changed. A similar argument establishes another important property of the data structure—that is, someone can efficiently prove to you that a particular transaction is included in the ledger. This user would have to send you only a small number of nodes in that transaction's block (this is the point of the Merkle tree), as well as a small amount of information for every following block. The ability to efficiently prove inclusion of transactions is highly desirable for performance and scalability.  
比特币基本上使用了 Haber 和 Stornetta 在 1991 年和 1997 年论文中的数据结构，如图 2 所示（中本聪可能不知道 Benaloh 和 de Mare 的工作）。当然，在比特币中，交易取代了文件。在每个区块的 Merkle 树中，叶节点是交易，每个内部节点基本上由两个指针组成。此数据结构具有两个重要属性。首先，最新区块的哈希值充当摘要。对任何交易（叶节点）的更改都需要将更改一直传播到区块的根，以及所有后续区块的根。因此，如果您知道最新的哈希值，则可以从不受信任的来源下载账本的其余部分，并验证它是否没有更改。类似的论点建立了数据结构的另一个重要属性，即有人可以有效地向你证明特定交易包含在账本中。该用户只需向您发送该交易区块中的少量节点（这是 Merkle 树的要点），以及每个后续区块的少量信息。能够有效地证明包含事务对于性能和可伸缩性来说是非常可取的。

![Bitcoins Academic Pedigree](https://dl.acm.org/cms/attachment/ed711e3a-d5e7-4f92-9c8e-59b49d8c5d46/narayanan2.png)

Merkle trees, by the way, are named for Ralph Merkle, a pioneer of asymmetric cryptography who proposed the idea in his 1980 paper.33 His intended application was to produce a digest for a public directory of digital certificates. When a website, for example, presents you with a certificate, it could also present a short proof that the certificate appears in the global directory. You could efficiently verify the proof as long as you know the root hash of the Merkle tree of the certificates in the directory. This idea is ancient by cryptographic standards, but its power has been appreciated only of late. It is at the core of the recently implemented Certificate Transparency system.30 A 2015 paper proposes CONIKS, which applies the idea to directories of public keys for end-to-end encrypted emails.32 Efficient verification of parts of the global state is one of the key functionalities provided by the ledger in Ethereum, a new cryptocurrency.  
顺便说一句，默克尔树是以非对称密码学的先驱拉尔夫·默克尔 （Ralph Merkle） 的名字命名的，他在 1980 年的论文中提出了这个想法。33 他打算为数字证书的公共目录生成摘要。例如，当网站向您提供证书时，它还可以提供证书出现在全局目录中的简短证明。只要您知道目录中证书的 Merkle 树的根哈希，就可以有效地验证证明。按照密码学标准，这个想法很古老，但它的强大功能直到最近才得到重视。它是最近实施的 Certificate Transparency 系统的核心。30 2015 年的一篇论文提出了 CONIKS，它将这一想法应用于端到端加密电子邮件的公钥目录。32 对全球状态的某些部分进行有效验证是以太坊（一种新型加密货币）账本提供的关键功能之一。

Bitcoin may be the most well-known real-world instantiation of Haber and Stornetta's data structures, but it is not the first. At least two companies—Surety starting in the mid-'90s and Guardtime starting in 2007—offer document timestamping services. An interesting twist present in both of these services is an idea mentioned by Bayer, Haber, and Stornetta,5 which is to publish Merkle roots periodically in a newspaper by taking out an ad. Figure 3 shows a Merkle root published by Guardtime.  
比特币可能是 Haber 和 Stornetta 数据结构最著名的现实世界实例，但它不是第一个。至少有两家公司 — 90 年代中期开始的 Surety 和 2007 年开始的 Guardtime — 提供文档时间戳服务。这两项服务中都存在一个有趣的转折，即 Bayer、Haber 和 Stornetta 5 提到的一个想法，即通过投放广告定期在报纸上发布 Merkle 根源。图 3 显示了 Guardtime 发布的 Merkle 根。

![Bitcoins Academic Pedigree](https://dl.acm.org/cms/attachment/02a21c96-38e7-4afe-af48-98f2bd98e7c7/narayanan3.png)

#### Byzantine fault tolerance  
拜占庭容错

Of course, the requirements for an Internet currency without a central authority are more stringent. A distributed ledger will inevitably have forks, which means that some nodes will think block A is the latest block, while other nodes will think it is block B. This could be because of an adversary trying to disrupt the ledger's operation or simply because of network latency, resulting in blocks occasionally being generated near-simultaneously by different nodes unaware of each other's blocks. Linked timestamping alone is not enough to resolve forks, as was shown by Mike Just in 1998.26  
当然，对于没有中央机构的互联网货币的要求更为严格。分布式账本不可避免地会有分叉，这意味着一些节点会认为区块 A 是最新的区块，而另一些节点会认为它是区块 B。这可能是因为对手试图破坏账本的运行，或者仅仅是因为网络延迟，导致不同的节点偶尔几乎同时生成区块，而不知道彼此的区块。仅靠链接时间戳不足以解决分叉，正如 Mike Just 在 1998 年所证明的那样。26

A different research field, fault-tolerant distributed computing, has studied this problem, where it goes by different names, including _state replication_. A solution to this problem is one that enables a set of nodes to apply the same state transitions in the same order—typically, the precise order does not matter, only that all nodes are consistent. For a digital currency, the state to be replicated is the set of balances, and transactions are state transitions. Early solutions, including Paxos, proposed by Turing Award winner Leslie Lamport in 1989,28,29 consider state replication when communication channels are unreliable and when a minority of nodes may exhibit certain "realistic" faults, such as going offline forever or rebooting and sending outdated messages from when it first went offline. A prolific literature followed with more adverse settings and efficiency tradeoffs.  
另一个研究领域，容错分布式计算，已经研究了这个问题，它有不同的名称，包括_状态复制_。此问题的解决方案是使一组节点能够以相同的顺序应用相同的状态转换 — 通常，精确的顺序并不重要，重要的是所有节点都是一致的。对于数字货币，要复制的状态是余额集，交易是状态转换。图灵奖得主 Leslie Lamport 在 1989 年提出的包括 Paxos 在内的早期解决方案，28,29 在通信通道不可靠且少数节点可能表现出某些“现实”故障时考虑状态复制，例如永远离线或重新启动并发送首次离线时的过时消息。随后是多产的文献，其中包含更多不利的设置和效率权衡。

A related line of work studied the situation where the network is mostly reliable (messages are delivered with bounded delay), but where the definition of "fault" was expanded to handle _any_ deviation from the protocol. Such Byzantine faults include both naturally occurring faults as well as maliciously crafted behaviors. They were first studied in a paper also by Lamport, cowritten with Robert Shostak and Marshall Pease, as early as 1982.27 Much later, in 1999, a landmark paper by Miguel Castro and Barbara Liskov introduced PBFT (practical Byzantine fault tolerance), which accommodated both Byzantine faults and an unreliable network.8 Compared with linked timestamping, the fault-tolerance literature is enormous and includes hundreds of variants and optimizations of Paxos, PBFT, and other seminal protocols.  
一个相关的工作线研究了网络最可靠的情况（消息以有限延迟传递），但 “fault” 的定义被扩展以处理_任何_偏离协议的情况。这种拜占庭式的过错既包括自然发生的过错，也包括恶意制造的行为。早在 1982 年，兰波特也与罗伯特·肖斯塔克 （Robert Shostak） 和马歇尔·皮斯 （Marshall Pease） 合著的一篇论文中首次研究了它们。27 很久以后，在 1999 年，米格尔·卡斯特罗 （Miguel Castro） 和芭芭拉·利斯科夫 （Barbara Liskov） 的一篇具有里程碑意义的论文引入了 PBFT（实用拜占庭容错），它既可以容纳拜占庭故障，也可以容纳不可靠的网络。8 与链接时间戳相比，容错文献非常庞大，包括 Paxos、PBFT 和其他开创性协议的数百种变体和优化。

In his original white paper, Nakamoto does not cite this literature or use its language. He uses some concepts, referring to his protocol as a consensus mechanism and considering faults both in the form of attackers, as well as nodes joining and leaving the network. This is in contrast to his explicit reliance on the literature in linked timestamping (and proof of work, discussed next). When asked in a mailing-list discussion about bitcoin's relation to the Byzantine Generals' Problem (a thought experiment requiring BFT to solve), Nakamoto asserts that the proof-of-work chain solves this problem.35  
在他的原始白皮书中，Nakamoto 没有引用这些文献或使用其语言。他使用了一些概念，将他的协议称为共识机制，并考虑了攻击者以及节点加入和离开网络形式的故障。这与他在链接时间戳（以及功证明，接下来讨论）中对文献的明确依赖形成鲜明对比。当在邮件列表讨论中被问及比特币与拜占庭将军问题（一个需要 BFT 解决的思想实验）的关系时，Nakamoto 断言工作量证明链解决了这个问题。35

In the following years, other academics have studied Nakamoto consensus from the perspective of distributed systems. This is still a work in progress. Some show that bitcoin's properties are quite weak,43 while others argue that the BFT perspective doesn't do justice to bitcoin's consistency properties.40 Another approach is to define variants of well-studied properties and prove that bitcoin satisfies them.19 Recently these definitions were substantially sharpened to provide a more standard consistency definition that holds under more realistic assumptions about message delivery.37 All of this work, however, makes assumptions about "honest," i.e., procotol-compliant, behavior among a subset of participants, whereas Nakamoto suggests that honest behavior need not be blindly assumed, because it is incentivized. A richer analysis of Nakamoto consensus accounting for the role of incentives doesn't fit cleanly into past models of fault-tolerant systems.  
在接下来的几年里，其他学者从分布式系统的角度研究了 Nakamoto 共识。这项工作仍在进行中。一些人表明比特币的特性相当弱，43 而另一些人则认为 BFT 的观点并不能公正地评价比特币的一致性特性。40 另一种方法是定义经过充分研究的属性的变体，并证明比特币满足它们。19 最近，这些定义得到了大幅度的锐化，以提供更标准的一致性定义，该定义在有关消息传递的更现实的假设下成立。37 然而，所有这些工作都对一部分参与者的“诚实”行为做出了假设，即遵守 procotol 的行为，而 Nakamoto 则认为诚实的行为不需要盲目假设，因为它是有激励的。对 Nakamoto 共识的更丰富的分析解释了激励的作用，并不能完全适应过去的容错系统模型。

### Proof of Work 工作量证明

Virtually all fault-tolerant systems assume that a strict majority or supermajority (e.g., more than half or two-thirds) of nodes in the system are both honest and reliable. In an open peer-to-peer network, there is no registration of nodes, and they freely join and leave. Thus an adversary can create enough _Sybils_, or sockpuppet nodes, to overcome the consensus guarantees of the system. The Sybil attack was formalized in 2002 by John Douceur,14 who turned to a cryptographic construction called _proof of work_ to mitigate it.  
实际上，所有容错系统都假设系统中严格的多数或绝对多数（例如，超过一半或三分之二）的节点既诚实又可靠。在开放的点对点网络中，无需注册节点，节点可以自由加入和离开。因此，对手可以创建足够的 _Sybil_ 或 sockpuppet 节点，以克服系统的共识保证。Sybil 攻击于 2002 年由 John Douceur 正式确定，14 他转向一种称为_工作量证明_的加密结构来缓解它。

#### The origins 起源

To understand proof of work, let's turn to its origins. The first proposal that would be called proof of work today was created in 1992 by Cynthia Dwork and Moni Naor.15Their goal was to deter spam. Note that spam, Sybil attacks, and denial of service are all roughly similar problems in which the adversary amplifies its influence in the network compared to regular users; proof of work is applicable as a defense against all three. In Dwork and Naor's design, email recipients would process only those emails that were accompanied by proof that the sender had performed a moderate amount of computational work—hence, "proof of work." Computing the proof would take perhaps a few seconds on a regular computer. Thus, it would pose no difficulty for regular users, but a spammer wishing to send a million emails would require several weeks, using equivalent hardware.   
要了解工作量证明，让我们来看看它的起源。今天被称为工作量证明的第一个提案是由 Cynthia Dwork 和 Moni Naor 于 1992 年创建的。15 他们的目标是阻止垃圾邮件。请注意，垃圾邮件、女巫攻击和拒绝服务都是大致相似的问题，与普通用户相比，攻击者会放大其在网络中的影响力;工作量证明可用于对这三者进行辩护。在 Dwork 和 Naor 的设计中，电子邮件收件人将只处理那些附有发件人已执行适量计算工作的证明的电子邮件，因此，“工作量证明”。在普通计算机上计算证明可能需要几秒钟。因此，对于普通用户来说，这不会造成任何困难，但是希望发送 100 万封电子邮件的垃圾邮件发送者需要数周时间，使用等效的硬件。

Note that the proof-of-work _instance_ (also called a _puzzle_) has to be specific to the email, as well as to the recipient. Otherwise, a spammer would be able to send multiple messages to the same recipient (or the same message to multiple recipients) for the cost of one message to one recipient. The second crucial property is that it should pose minimal computational burden on the recipient; puzzle solutions should be trivial to verify_,_ regardless of how hard they are to compute. Additionally, Dwork and Naor considered functions with a _trapdoor_, a secret known to a central authority that would allow the authority to solve the puzzles without doing the work. One possible application of a trapdoor would be for the authority to approve posting to mailing lists without incurring a cost. Dwork and Naor's proposal consisted of three candidate puzzles meeting their properties, and it kicked off a whole research field, to which we'll return.   
请注意，工作量证明_实例_（也称为_拼图_）必须特定于电子邮件以及收件人。否则，垃圾邮件发送者将能够向同一收件人发送多封邮件（或向多个收件人发送同一封邮件），而成本相当于向一个收件人发送一封邮件的费用。第二个关键属性是它应该对接收者造成的计算负担最小;拼图解决方案应该很容易验证_，_无论它们计算起来有多难。此外，Dwork 和 Naor 考虑了带有_活板门_的功能，这是中央机构已知的秘密，它允许机构在不做工作的情况下解决谜题。活板门的一个可能应用是让当局批准发布到邮件列表而不产生成本。Dwork 和 Naor 的提案由三个符合其属性的候选谜题组成，它拉开了整个研究领域的序幕，我们将回到这个领域。

#### Hashcash 哈希现金

A very similar idea called hashcash was independently invented in 1997 by Adam Back, a postdoctoral researcher at the time who was part of the cypherpunk community. Cypherpunks were activists who opposed the power of governments and centralized institutions, and sought to create social and political change through cryptography. Back was practically oriented: he released hashcash first as software,2and five years later in 2002 released an Internet draft (a standardization document) and a paper.4  
1997 年，当时的博士后研究员 Adam Back 独立发明了一个非常相似的想法，称为 hashcash，他是密码朋克社区的一员。密码朋克是反对政府和中央机构权力的活动家，并寻求通过密码学创造社会和政治变革。Back 以实践为导向：他首先将 hashcash 作为软件发布，2五年后的 2002 年发布了互联网草案（标准化文件）和一篇论文。4

Hashcash is much simpler than Dwork and Naor's idea: it has no trapdoor and no central authority, and it uses only hash functions instead of digital signatures. It is based on a simple principle: a hash function behaves as a random function for some practical purposes, which means that the only way to find an input that hashes to a particular output is to try various inputs until one produces the desired output. Further, the only way to find an input that hashes into an arbitrary _set_ of outputs is again to try hashing different inputs one by one. So, if I challenged you to find an input whose (binary) hash value begins with 10 zeros, you would have to try numerous inputs, and you would find that each output had a 1/210 chance of beginning with 10 zeros, which means that you would have to try on the order of 210inputs, or approximately 1,000 hash computations.   
Hashcash 比 Dwork 和 Naor 的想法简单得多：它没有活板门，也没有中央机构，它只使用哈希函数而不是数字签名。它基于一个简单的原则：哈希函数在某些实际目的上表现为随机函数，这意味着找到哈希到特定输出的输入的唯一方法是尝试各种输入，直到产生所需的输出。此外，找到哈希成任意_一组_输出的 input 的唯一方法是再次尝试逐个对不同的 input 进行哈希处理。所以，如果我让你找到一个（二进制）哈希值以 10 个 0 开头的输入，你将不得不尝试大量的输入，你会发现每个输出都有 1/210 的机会以 10 个 0 开始，这意味着你将不得不尝试 2个 10个输入的顺序。 或大约 1000 次哈希计算。

As the name suggests, in hashcash Back viewed proof of work as a form of cash. On his web page he positioned it as an alternative to David Chaum's DigiCash, which was a system that issued untraceable digital cash from a bank to a user.3 He even made compromises to the technical design to make it appear more cashlike. Later, Back made comments suggesting that bitcoin was a straightforward extension of hashcash. Hashcash is simply not cash, however, because it has no protection against double spending. Hashcash tokens cannot be exchanged among peers.   
顾名思义，在 hashcash 中，Back 将工作量证明视为一种现金形式。在他的网页上，他将其定位为 David Chaum 的 DigiCash 的替代品，后者是一个从银行向用户发行无法追踪的数字现金的系统。3 他甚至对技术设计做出了妥协，使其看起来更像现金。后来，Back 发表评论称比特币是 hashcash 的直接延伸。然而，Hashcash 根本不是现金，因为它无法防止双重支出。Hashcash 代币不能在对等节点之间交换。

Meanwhile, in the academic scene, researchers found many applications for proof of work besides spam, such as preventing denial-of-service attacks,25 ensuring the integrity of web analytics,17 and rate-limiting password guessing online.38Incidentally, the term _proof of work_ was coined only in 1999 in a paper by Markus Jakobsson and Ari Juels, which also includes a nice survey of the work up until that point.24 It is worth noting that these researchers seem to have been unaware of hashcash but independently started to converge on hash-based proof of work, which was introduced in papers by Eran Gabber et al.18 and by Juels and Brainard.25 (Many of the terms used throughout this paragraph didn't become standard terminology until long after the papers in question were published.)  
与此同时，在学术界，研究人员发现了除垃圾邮件之外的许多工作证明应用，例如防止拒绝服务攻击，25 确保 Web 分析的完整性，17 以及限制在线密码猜测的速率。38 顺便说一句，_工作量证明_这个词是在 1999 年由 Markus Jakobsson 和 Ari Juels 撰写的一篇论文中创造的，该论文还包括对当时之前的工作的精彩调查。24 值得注意的是，这些研究人员似乎不知道哈希现金，但独立地开始趋向于基于哈希的工作量证明，这在 Eran Gabber 等人18以及 Juels 和 Brainard 的论文中都有介绍。25（本段中使用的许多术语直到相关论文发表很久之后才成为标准术语。

#### Proof of work and digital cash: A catch-22  
工作量证明和数字现金：第 22 条军规

You may know that proof of work did not succeed in its original application as an anti-spam measure. One possible reason is the dramatic difference in the puzzle-solving speed of different devices. That means spammers will be able to make a small investment in custom hardware to increase their spam rate by orders of magnitude. In economics, the natural response to an asymmetry in the cost of production is trade—that is, a market for proof-of-work solutions. But this presents a catch-22, because that would require a working digital currency. Indeed, the lack of such a currency is a major part of the motivation for proof of work in the first place. One crude solution to this problem is to declare puzzle solutions to _be_ cash, as hashcash tries to do.  
您可能知道，作为反垃圾邮件措施，工作量证明在其原始应用程序中并未成功。一个可能的原因是不同设备的解谜速度存在巨大差异。这意味着垃圾邮件发送者将能够对自定义硬件进行少量投资，以将其垃圾邮件率提高几个数量级。在经济学中，对生产成本不对称的自然反应是贸易，即工作量证明解决方案的市场。但这提出了第 22 条军规，因为这需要一种有效的数字货币。事实上，缺乏这种货币是最初产生工作量证明的主要动机。这个问题的一个粗略解决方案是将拼图解决方案声明_为_ cash，就像 hashcash 试图做的那样。

More coherent approaches to treating puzzle solutions as cash are found in two essays that preceded bitcoin, describing ideas called b-money13 and bit gold42respectively. These proposals offer timestamping services that sign off on the creation (through proof of work) of money, and once money is created, they sign off on transfers. If disagreement about the ledger occurs among the servers or nodes, however, there isn't a clear way to resolve it. Letting the majority decide seems to be implicit in both authors' writings, but because of the Sybil problem, these mechanisms aren't very secure, unless there is a gatekeeper who controls entry into the network or Sybil resistance is itself achieved with proof of work.   
在比特币之前的两篇文章中，可以找到将拼图解决方案视为现金的更连贯的方法，分别描述了称为 b-money13 和 bit gold42 的想法。这些提案提供时间戳服务，对货币的创建（通过工作量证明）进行签名，一旦货币被创建，它们就会签署转账。但是，如果服务器或节点之间对账本存在分歧，则没有明确的解决方法。让多数人决定似乎在两位作者的著作中都隐含着，但由于 Sybil 问题，这些机制不是很安全，除非有一个守门人控制着进入网络的入口，或者 Sybil 抵抗本身是通过工作量证明实现的。

### Putting it all together  把它们放在一起

Understanding all these predecessors that contain pieces of bitcoin's design leads to an appreciation of the true genius of Nakamoto's innovation. In bitcoin, for the first time, puzzle solutions don't constitute cash by themselves. Instead, they are merely used to secure the ledger. Solving proof of work is performed by specialized entities called _miners_ (although Nakamoto underestimated just how specialized mining would become).   
了解所有这些包含比特币设计的前辈，可以欣赏到中本聪创新的真正天才。在比特币中，拼图解决方案本身第一次不构成现金。相反，它们仅用于保护分类账。解决工作量证明由称为_矿工_的专业实体执行（尽管 Nakamoto 低估了挖矿的专业化程度）。

Miners are constantly in a race with each other to find the next puzzle solution; each miner solves a slightly different variant of the puzzle so that the chance of success is proportional to the fraction of global mining power that the miner controls. A miner who solves a puzzle gets to contribute the next batch, or block, of transactions to the ledger, which is based on linked timestamping. In exchange for the service of maintaining the ledger, a miner who contributes a block is rewarded with newly minted units of the currency. With high likelihood, if a miner contributes an invalid transaction or block, it will be rejected by the majority of other miners who contribute the following blocks, and this will also invalidate the block reward for the bad block. In this way, because of the monetary incentives, miners ensure each other's compliance with the protocol.  
矿工们一直在相互竞争，以寻找下一个谜题解决方案;每个矿工解决的谜题略有不同，因此成功的机会与矿工控制的全球采矿能力的比例成正比。解决难题的矿工可以将下一批或区块的交易贡献给账本，该账本基于链接时间戳。作为维护账本服务的交换，贡献区块的矿工将获得新铸造的货币单位作为奖励。很有可能，如果一个矿工贡献了一笔无效的交易或区块，它将被贡献以下区块的大多数其他矿工拒绝，这也将使坏区块的区块奖励失效。通过这种方式，由于金钱激励，矿工确保彼此遵守协议。

Bitcoin neatly avoids the double-spending problem plaguing proof-of-work-as-cash schemes because it eschews puzzle solutions themselves having value. In fact, puzzle solutions are _twice_ decoupled from economic value: the amount of work required to produce a block is a floating parameter (proportional to the global mining power), and further, the number of bitcoins issued per block is not fixed either. The block reward (which is how new bitcoins are minted) is set to halve every four years (in 2017, the reward is 12.5 bitcoins/block, down from 50 bitcoins/block). Bitcoin incorporates an additional reward scheme—namely, senders of transactions paying miners for the service of including the transaction in their blocks. It is expected that the market will determine transaction fees and miners' rewards.  
比特币巧妙地避免了困扰工作量证明即现金计划的双花问题，因为它回避了拼图解决方案本身具有价值。事实上，拼图解决方案与经济价值脱钩了_两次_：产生一个区块所需的工作量是一个浮动参数（与全球挖矿能力成正比），此外，每个区块发行的比特币数量也不是固定的。区块奖励（即新比特币的铸造方式）设置为每四年减半（2017 年，奖励为 12.5 个比特币/区块，低于 50 个比特币/区块）。比特币包含一个额外的奖励计划——即交易发送者向矿工支付将交易包含在其区块中的服务。预计市场将决定交易费用和矿工奖励。

Nakamoto's genius, then, wasn't any of the individual components of bitcoin, but rather the intricate way in which they fit together to breathe life into the system. The timestamping and Byzantine agreement researchers didn't hit upon the idea of incentivizing nodes to be honest, nor, until 2005, of using proof of work to do away with identities. Conversely, the authors of hashcash, b-money, and bit gold didn't incorporate the idea of a consensus algorithm to prevent double spending. In bitcoin, a secure ledger is necessary to prevent double spending and thus ensure that the currency has value. A valuable currency is necessary to reward miners. In turn, strength of mining power is necessary to secure the ledger. Without it, an adversary could amass more than 50 percent of the global mining power and thereby be able to generate blocks faster than the rest of the network, double-spend transactions, and effectively rewrite history, overrunning the system. Thus, bitcoin is bootstrapped, with a circular dependence among these three components. Nakamoto's challenge was not just the design, but also convincing the initial community of users and miners to take a leap together into the unknown—back when a pizza cost 10,000 bitcoins and the network's mining power was less than a trillionth of what it is today.  
因此，中本聪的天才之处不在于比特币的任何单个组件，而是它们以错综复杂的方式组合在一起，为系统注入活力。时间戳和拜占庭协议研究人员并没有想到激励节点诚实的想法，直到 2005 年，也没有想到使用工作量证明来消除身份。相反，hashcash、b-money 和 bit gold 的作者并没有采用共识算法来防止双重支出。在比特币中，一个安全的账本对于防止双重支出，从而确保货币有价值是必要的。奖励矿工需要有价值的货币。反过来，强大的采矿能力对于保护账本是必要的。没有它，对手可以积累超过 50% 的全球挖矿能力，从而能够比网络其他部分更快地生成区块，双花交易，并有效地改写历史，使系统超负荷运转。因此，比特币是自举的，这三个组成部分之间存在循环依赖。Nakamoto 面临的挑战不仅仅是设计，还在于说服最初的用户和矿工社区一起向未知领域飞跃——当时一个披萨要花费 10,000 个比特币，而网络的挖矿能力还不到今天的万亿分之一。

#### Public keys as identities  
作为身份的公钥

This article began with the understanding that a secure ledger makes creating digital currency straightforward. Let's revisit this claim. When Alice wishes to pay Bob, she broadcasts the transaction to all bitcoin nodes. A transaction is simply a string: a statement encoding Alice's wish to pay Bob some value, signed by her. The eventual inclusion of this signed statement into the ledger by miners is what makes the transaction real. Note that this doesn't require Bob's participation in any way. But let's focus on what's _not_ in the transaction: conspicuously absent are Alice and Bob's identities; instead, the transaction contains only their respective public keys. This is an important concept in bitcoin: public keys are the only kinds of identities in the system. Transactions transfer value from and to public keys, which are called _addresses_.  
本文首先了解到，安全账本使创建数字货币变得简单明了。让我们重新审视一下这个说法。当 Alice 希望向 Bob 付款时，她将交易广播到所有比特币节点。交易只是一个字符串：一个声明，编码 Alice 希望向 Bob 支付一些价值，由她签名。矿工最终将这份签署的声明纳入账本是使交易成为现实的原因。请注意，这不需要 Bob 以任何方式参与。但是，让我们关注交易_中没有_的内容：Alice 和 Bob 的身份明显缺失;相反，交易仅包含它们各自的公钥。这是比特币中的一个重要概念：公钥是系统中唯一的身份类型。交易在公钥（称为_地址_）之间转移价值。

In order to "speak for" an identity, you must know the corresponding secret key. You can create a new identity at any time by generating a new key pair, with no central authority or registry. You don't need to obtain a user name or inform others that you have picked a particular name. This is the notion of decentralized identity management. Bitcoin doesn't specify how Alice tells Bob what her pseudonym is—that is external to the system.   
为了 “代言” 身份，您必须知道相应的密钥。您可以随时通过生成新的密钥对来创建新身份，而无需中央机构或注册表。您无需获取用户名或通知其他人您已选择特定名称。这就是去中心化身份管理的概念。比特币没有指定 Alice 如何告诉 Bob 她的假名是什么——这是在系统外部的。

Although radically different from most other payment systems today, these ideas are quite old, dating back to David Chaum, the father of digital cash. In fact, Chaum also made seminal contributions to anonymity networks, and it is in this context that he invented this idea. In his 1981 paper, "Untraceable Electronic Mail, Return Addresses, and Digital Pseudonyms,"9 he states: "A digital pseudonym' is a public key used to verify signatures made by the anonymous holder of the corresponding private key."   
尽管与当今大多数其他支付系统截然不同，但这些想法相当古老，可以追溯到数字现金之父 David Chaum。事实上，Chaum 还对匿名网络做出了开创性的贡献，正是在这种背景下，他发明了这个想法。在他 1981 年的论文“无法追踪的电子邮件、返回地址和数字假名”9 中，他指出：“数字假名是用于验证相应私钥的匿名持有者所签名的公钥。

Now, having message recipients be known only by a public key presents an obvious problem: there is no way to route the message to the right computer. This leads to a massive inefficiency in Chaum's proposal, which can be traded off against the level of anonymity but not eliminated. Bitcoin is similarly exceedingly inefficient compared with centralized payment systems: the ledger containing every transaction is maintained by every node in the system. Bitcoin incurs this inefficiency for security reasons anyway, and thus achieves pseudonymity (i.e, public keys as identities) "for free." Chaum took these ideas much further in a 1985 paper,11 where he presents a vision of privacy-preserving e-commerce based on pervasive pseudonyms, as well as "blind signatures," the key technical idea behind his digital cash.  
现在，让消息收件人仅通过公钥知道会带来一个明显的问题：无法将消息路由到正确的计算机。这导致了 Chaum 的提案效率极低，这可以与匿名水平进行权衡，但不能消除。与中心化支付系统相比，比特币的效率同样极低：包含每笔交易的账本由系统中的每个节点维护。无论如何，比特币出于安全原因导致了这种低效率，因此“免费”实现了假名化（即作为身份的公钥）。Chaum 在 1985 年的一篇论文中进一步阐述了这些想法，11 他提出了基于普遍的假名以及“盲签名”的隐私保护电子商务的愿景，这是他的数字现金背后的关键技术理念。

The public-keys-as-identities idea is also seen in b-money and bit gold, the two precursor essays to bitcoin discussed earlier. However, much of the work that built on Chaum's foundation, as well as Chaum's own later work on ecash, moved away from this idea. The cypherpunks were keenly interested in privacy-preserving communication and commerce, and they embraced pseudonyms, which they called _nyms_. But to them, nyms weren't mere cryptographic identities (i.e., public keys), but rather, usually email addresses that were linked to public keys. Similarly, Ian Goldberg's dissertation, which became the basis of much future work on anonymous communication, recognizes Chaum's idea but suggests that nyms should be human-memorable nicknames with certificates to bind them.20 Thus Bitcoin proved to be the most successful instantiation of Chaum's idea.  
公钥作为身份的想法也出现在 b-money 和 bit gold 中，这是前面讨论的比特币的两篇前身文章。然而，建立在 Chaum 基础上的大部分工作，以及 Chaum 自己后来在 ecash 方面的工作，都偏离了这个想法。密码朋克对保护隐私的通信和商业非常感兴趣，他们接受了他们称之为 _nyms_ 的假名。但对他们来说，nyms 不仅仅是加密身份（即公钥），而通常是链接到公钥的电子邮件地址。同样，伊恩·戈德堡 （Ian Goldberg） 的论文成为未来许多匿名通信工作的基础，它承认 Chaum 的想法，但建议 nyms 应该是人类可记住的昵称，并带有证书来约束它们。20 因此，比特币被证明是 Chaum 想法最成功的实例。

### The Blockchain 区块链

So far, this article has not addressed the blockchain, which, if you believe the hype, is bitcoin's main invention. It might come as a surprise to you that Nakamoto doesn't mention that term at all. In fact, the term _blockchain_ has no standard technical definition but is a loose umbrella term used by various parties to refer to systems that bear varying levels of resemblance to bitcoin and its ledger.   
到目前为止，本文还没有讨论区块链，如果你相信这种炒作，它是比特币的主要发明。您可能会感到惊讶，中本聪根本没有提到这个词。事实上，_区块链_一词没有标准的技术定义，而是一个松散的总称，各方使用来指代与比特币及其账本具有不同程度相似的系统。

Discussing example applications that benefit from a blockchain will help clarify the different uses of the term. First, consider a database backend for transactions among a consortium of banks, where transactions are netted at the end of each day and accounts are settled by the central bank. Such a system has a small number of well-identified parties, so Nakamoto consensus would be overkill. An on-blockchain currency is not needed either, as the accounts are denominated in traditional currency. Linked timestamping, on the other hand, would clearly be useful, at least to ensure a consistent global ordering of transactions in the face of network latency. State replication would also be useful: a bank would know that its local copy of the data is identical to what the central bank will use to settle its account. This frees banks from the expensive reconciliation process they must currently perform.   
讨论受益于区块链的示例应用程序将有助于阐明该术语的不同用法。首先，考虑一个用于银行联盟之间交易的数据库后端，其中交易在每天结束时进行净额结算，账户由中央银行结算。这样的系统有少量明确识别的政党，因此中本聪共识是矫枉过正的。也不需要区块链上的货币，因为账户以传统货币计价。另一方面，链接时间戳显然是有用的，至少可以确保在面对网络延迟时交易的全局顺序一致。状态复制也很有用：银行会知道其数据的本地副本与中央银行用于结算其账户的数据相同。这使银行摆脱了他们目前必须执行的昂贵的对账流程。

Second, consider an asset-management application such as a registry of documents that tracks ownership of financial securities, or real estate, or any other asset. Using a blockchain would increase interoperability and decrease barriers to entry. We want a secure, global registry of documents, and ideally one that allows public participation. This is essentially what the timestamping services of the 1990s and 2000s sought to provide. Public blockchains offer a particularly effective way to achieve this today (the data itself may be stored off-chain, with only the metadata stored on-chain). Other applications also benefit from a timestamping or "public bulletin board" abstraction, most notably electronic voting.  
其次，考虑一个资产管理应用程序，例如跟踪金融证券、房地产或任何其他资产所有权的文件注册表。使用区块链将提高互操作性并降低进入门槛。我们想要一个安全的、全球的文档注册表，最好是一个允许公众参与的注册表。这基本上就是 1990 年代和 2000 年代的时间戳服务寻求提供的。如今，公共区块链提供了一种特别有效的方法来实现这一目标（数据本身可以存储在链下，只有元数据存储在链上）。其他应用程序也受益于时间戳或 “public bulletin board” 抽象，最明显的是电子投票。

Let's build on the asset-management example. Suppose you want to execute trades of assets via the blockchain, and not merely record them there. This is possible if the asset is issued digitally on the blockchain itself, and if the blockchain supports smart contracts. In this instance, smart contracts solve the "fair exchange" problem of ensuring that payment is made if and only if the asset is transferred. More generally, smart contracts can encode complex business logic, provided that all necessary input data (assets, their prices, and so on) are represented on the blockchain.  
让我们以资产管理为例。假设您想通过区块链执行资产交易，而不仅仅是在那里记录它们。如果资产在区块链本身上以数字方式发行，并且区块链支持智能合约，这是可能的。在这种情况下，智能合约解决了“公平交换”问题，即确保当且仅当资产被转移时才付款。更一般地说，智能合约可以编码复杂的业务逻辑，前提是所有必要的输入数据（资产、价格等）都在区块链上表示。

This mapping of blockchain properties to applications allows us not only to appreciate their potential, but also to inject a much-needed dose of skepticism. First, many proposed applications of blockchains, especially in banking, don't use Nakamoto consensus. Rather, they use the ledger data structure and Byzantine agreement, which, as shown, date to the '90s. This belies the claim that blockchains are a new and revolutionary technology. Instead, the buzz around blockchains has helped banks initiate collective action to deploy shared-ledger technology, like the parable of "stone soup." Bitcoin has also served as a highly visible proof of concept that the decentralized ledger works, and the Bitcoin Core project has provided a convenient code base that can be adapted as necessary.  
这种将区块链属性映射到应用程序的做法，不仅让我们能够欣赏它们的潜力，而且还能注入急需的怀疑。首先，许多拟议的区块链应用，尤其是在银行业，都没有使用中本聪共识。相反，他们使用账本数据结构和拜占庭协议，如图所示，这可以追溯到 90 年代。这掩盖了区块链是一项新的革命性技术的说法。相反，围绕区块链的嗡嗡声帮助银行发起了集体行动来部署共享账本技术，就像“石头汤”的寓言一样。比特币还作为去中心化账本工作的高度可见的概念证明，Bitcoin Core 项目提供了一个方便的代码库，可以根据需要进行调整。

Second, blockchains are frequently presented as more secure than traditional registries—a misleading claim. To see why, the overall stability of the system or platform must be separated from endpoint security—that is, the security of users and devices. True, the systemic risk of blockchains may be lower than that of many centralized institutions, but the endpoint-security risk of blockchains is far worse than the corresponding risk of traditional institutions. Blockchain transactions are near-instant, irreversible, and, in public blockchains, anonymous by design. With a blockchain-based stock registry, if a user (or broker or agent) loses control of his or her private keys—which takes nothing more than losing a phone or getting malware on a computer—the user loses his or her assets. The extraordinary history of bitcoin hacks, thefts, and scams doesn't inspire much confidence—according to one estimate, at least six percent of bitcoins in circulation have been stolen at least once.39  
其次，区块链经常被描述为比传统注册管理机构更安全——这是一个误导性的说法。要了解原因，必须将系统或平台的整体稳定性与端点安全性（即用户和设备的安全性）分开。诚然，区块链的系统性风险可能低于许多中心化机构，但区块链的端点安全风险远低于传统机构的相应风险。区块链交易是近乎即时的、不可逆的，并且在公共区块链中，在设计上是匿名的。使用基于区块链的股票登记处，如果用户（或经纪人或代理人）失去了对其私钥的控制（这只不过是丢失手机或在计算机上感染恶意软件），则用户将失去他或她的资产。比特币黑客攻击、盗窃和诈骗的非凡历史并没有激发太多信心——根据一项估计，至少有 6% 的流通比特币至少被盗过一次。39 元

### Concluding Lessons 总结性课程

The history described here offers rich (and complementary) lessons for practitioners and academics. Practitioners should be skeptical of claims of revolutionary technology. As shown here, most of the ideas in bitcoin that have generated excitement in the enterprise, such as distributed ledgers and Byzantine agreement, actually date back 20 years or more. Recognize that your problem may not require any breakthroughs—there may be long-forgotten solutions in research papers.   
这里描述的历史为从业者和学者提供了丰富（和互补）的经验教训。从业者应该对革命性技术的说法持怀疑态度。如图所示，比特币中大多数在企业中引起兴奋的想法，例如分布式账本和拜占庭协议，实际上可以追溯到 20 年前或更长时间。认识到您的问题可能不需要任何突破——研究论文中可能有早已被遗忘的解决方案。

Academia seems to have the opposite problem, at least in this instance: a resistance to radical, extrinsic ideas. The bitcoin white paper, despite the pedigree of many of its ideas, was more novel than most academic research. Moreover, Nakamoto didn't care for academic peer review and didn't fully connect it to its history. As a result, academics essentially ignored bitcoin for several years. Many academic communities informally argued that Bitcoin couldn't work, based on theoretical models or experiences with past systems, despite the fact that it _was_ working in practice.   
学术界似乎存在相反的问题，至少在这种情况下是这样：对激进的、外在的思想的抵制。比特币白皮书，尽管它的许多想法都有血统，但比大多数学术研究都更新颖。此外，中本聪并不关心学术同行评议，也没有将其与历史完全联系起来。因此，学术界基本上忽视了比特币好几年。许多学术界非正式地认为，根据理论模型或过去系统的经验，比特币无法运作，尽管它在实践中_是_有效的。

We've seen repeatedly that ideas in the research literature can be gradually forgotten or lie unappreciated, especially if they are ahead of their time, even in popular areas of research. Both practitioners and academics would do well to revisit old ideas to glean insights for present systems. Bitcoin was unusual and successful not because it was on the cutting edge of research on any of its components, but because it combined old ideas from many previously unrelated fields. This is not easy to do, as it requires bridging disparate terminology, assumptions, etc., but it is a valuable blueprint for innovation.  
我们一再看到，研究文献中的想法可能会逐渐被遗忘或不被欣赏，特别是如果它们领先于时代，即使在流行的研究领域也是如此。从业者和学者都应该重新审视旧观念，以收集对当前系统的见解。比特币之所以不同寻常和成功，不是因为它处于其任何组成部分研究的前沿，而是因为它结合了许多以前不相关领域的旧思想。这并不容易做到，因为它需要弥合不同的术语、假设等，但它是创新的宝贵蓝图。

Practitioners would benefit from being able to identify overhyped technology. Some indicators of hype: difficulty identifying the technical innovation; difficulty pinning down the meaning of supposedly technical terms, because of companies eager to attach their own products to the bandwagon; difficulty identifying the problem that is being solved; and finally, claims of technology solving social problems or creating economic/political upheaval.  
从业者将受益于能够识别被过度炒作的技术。炒作的一些指标：难以识别技术创新;很难确定所谓的技术术语的含义，因为公司急于将自己的产品附加到潮流中;难以识别正在解决的问题;最后，声称技术解决了社会问题或造成了经济/政治动荡。

In contrast, academia has difficulty selling its inventions. For example, it's unfortunate that the original proof-of-work researchers get no credit for bitcoin, possibly because the work wasn't well known outside academic circles. Activities such as releasing code and working with practitioners are not adequately rewarded in academia. In fact, the original branch of the academic proof-of-work literature continues today without acknowledging the existence of bitcoin! Engaging with the real world not only helps get credit, but will also reduce reinvention and is a source of fresh ideas.  
相比之下，学术界很难推销自己的发明。例如，不幸的是，最初的工作量证明研究人员没有得到比特币的赞誉，这可能是因为这项工作在学术界之外并不为人所知。在学术界，发布代码和与从业者合作等活动没有得到足够的回报。事实上，学术工作量证明文献的原始分支今天仍在继续，却没有承认比特币的存在！与现实世界互动不仅有助于获得赞誉，而且还会减少重塑，并且是新想法的来源。

### Sidebars 侧边栏

#### Sybil-resistant networks 抗女巫攻击网络

In his paper on Sybil attacks, John Douceur proposed that all nodes participating in a BFT protocol be required to solve hashcash puzzles. If a node were masquerading as N nodes, it would be unable to solve N puzzles in time, and the fake identities would be purged. A malicious node, however, could still obtain a moderate advantage over an honest node that claimed only a single identity. A follow-up paper in 20051suggested that honest nodes should instead mimic the behavior of malicious nodes and claim as many virtual identities as they computationally can afford to claim. With these virtual identities executing a BFT protocol, the assumption, "At most a fraction _f_of nodes are faulty" can be replaced with the assumption "The fraction of total computational power controlled by faulty nodes is at most _f_." Thus, it is no longer necessary to validate identities, and open peer-to-peer networks can run a BFT protocol. Bitcoin uses exactly this idea. But Nakamoto asks a further question: What motivates nodes to perform computationally expensive proof of work? The answer requires a further leap: digital currency.  
在他关于 Sybil 攻击的论文中，John Douceur 提议要求所有参与 BFT 协议的节点都解决 hashcash 难题。如果一个节点伪装成 N 个节点，则无法及时解开 N 个谜题，伪身份会被清除。但是，与仅声明单个身份的诚实节点相比，恶意节点仍然可以获得适度的优势。2005 年的一篇后续论文1 建议诚实节点应该模仿恶意节点的行为，并在计算上可以承受的范围内尽可能多地声明虚拟身份。通过这些虚拟身份执行 BFT 协议，“最多有一小部分节点有故障”的假设可以替换为“故障节点控制的总计算能力的分数最多为 _f_”的假设。因此，不再需要验证身份，开放的点对点网络可以运行 BFT 协议。比特币正是使用了这个想法。但 Nakamoto 提出了另一个问题：是什么促使节点执行计算成本高昂的工作量证明？答案需要进一步的飞跃：数字货币。

#### Smart contracts 智能合约

A smart contract takes the idea of putting _data_ in a secure ledger and extends it to _computation_. In other words, it is a consensus protocol for the correct execution of a publicly specified program. Users can invoke functions in these smart-contract programs, subject to any restrictions specified by the program, and the function code is executed in tandem by the miners. Users can trust the output without having to redo the computation and can write their own programs to act on the output of other programs. Smart contracts are especially powerful when combined with a cryptocurrency platform, because the programs in question can handle money—own it, transfer it, destroy it, and, in some cases, even print it.   
智能合约采用_将数据_放入安全账本的想法，并将其扩展到_计算_。换句话说，它是正确执行公开指定程序的共识协议。用户可以在这些智能合约程序中调用函数，但要遵守程序指定的任何限制，并且函数代码由矿工同步执行。用户可以信任输出，而不必重做计算，并且可以编写自己的程序来作用于其他程序的输出。智能合约在与加密货币平台结合使用时特别强大，因为相关程序可以处理资金——拥有它、转移它、销毁它，在某些情况下，甚至可以打印它。

Bitcoin implements a restrictive programming language for smart contracts. A "standard" transaction (i.e., one that moves currency from one address to another) is specified as a short script in this language. Ethereum offers a more permissive and powerful language.   
比特币为智能合约实现了一种限制性编程语言。在这种语言中，“标准”交易（即将货币从一个地址转移到另一个地址的交易）被指定为短脚本。以太坊提供了一种更宽松、更强大的语言。

The idea of smart contracts was proposed by Nick Szabo in 199441 and so named because he saw them as analogs of legal contracts, but with automated enforcement. (This view has been critiqued by Karen Levy31 and Ed Felten.16) Presciently, Szabo presented smart contracts as extensions of digital-cash protocols and recognized that Byzantine agreement and digital signatures (among others) could be used as building blocks. The success of cryptocurrencies has made smart contracts practical, and research on the topic has bloomed as well. For example, programming languages researchers have adapted their methods and tools to automatically discover bugs in smart contracts and to write verifiably correct ones.  
智能合约的想法是由 Nick Szabo 在 199441 年提出的，之所以这样命名，是因为他认为智能合约是法律合同的类似物，但具有自动执行功能。（这种观点受到了31 岁的 Karen Levy 和 Ed Felten 的批评。16） Szabo 有先见之明地将智能合约作为数字现金协议的扩展，并认识到拜占庭协议和数字签名（以及其他）可以用作构建块。加密货币的成功使智能合约变得实用，关于该主题的研究也蓬勃发展。例如，编程语言研究人员已经调整了他们的方法和工具，以自动发现智能合约中的错误并编写可验证的正确错误。

#### Permissioned blockchains  许可区块链

While this article has emphasized that private or permissioned blockchains omit most of bitcoin's innovations, this isn't meant to diminish the interesting work happening in this space. A permissioned blockchain places restrictions on who can join the network, write transactions, or mine blocks. In particular, if miners are restricted to a list of trustworthy participants, the proof of work can be dropped in favor of a more traditional BFT approach. Thus, much of the research is a rebirth of BFT that asks questions such as: Can we use hash trees to simplify consensus algorithms? What if the network can fail only in certain ways?   
虽然本文强调私有或许可的区块链省略了比特币的大部分创新，但这并不意味着要削弱这个领域发生的有趣工作。许可区块链对谁可以加入网络、写入交易或挖掘区块施加了限制。特别是，如果矿工被限制在可信赖的参与者名单中，则可以放弃工作量证明，转而采用更传统的 BFT 方法。因此，大部分研究都是 BFT 的重生，它提出了以下问题：我们可以使用哈希树来简化共识算法吗？如果网络只能以某些方式发生故障怎么办？

Further, there are important considerations around identity and public-key infrastructure, access control, and confidentiality of the data stored on the blockchain. These issues largely don't arise in public blockchain settings, nor are they studied in the traditional BFT literature.   
此外，围绕身份和公钥基础设施、访问控制以及区块链上存储的数据的机密性，还有一些重要的考虑因素。这些问题在很大程度上不会出现在公共区块链环境中，也不会在传统的 BFT 文献中进行研究。

Finally, there is also the engineering work of scaling blockchains for high throughput and adapting them to various applications such as supply-chain management and financial technology.   
最后，还有扩展区块链以实现高吞吐量并使其适应各种应用（如供应链管理和金融技术）的工程工作。

---

#### Acknowledgements 确认

The authors are grateful to Adam Back, Andrew Miller, Edward Felten, Harry Kalodner, Ian Goldberg, Ian Grigg, Joseph Bonneau, Malte Möser, Mike Just, Neha Narula, Steven Goldfeder, and Stuart Haber for valuable feedback on a draft.  
作者感谢 Adam Back、Andrew Miller、Edward Felten、Harry Kalodner、Ian Goldberg、Ian Grigg、Joseph Bonneau、Malte Möser、Mike Just、Neha Narula、Steven Goldfeder 和 Stuart Haber 对草稿的宝贵反馈。

#### References 引用

1. Aspnes, J., et al. 2005. Exposing computationally challenged Byzantine imposters. Yale University Department of Computer Science; [http://cs.yale.edu/publications/techreports/tr1332.pdf](http://cs.yale.edu/publications/techreports/tr1332.pdf).  
1. Aspnes， J. 等人，2005 年。揭露了计算挑战的拜占庭冒名顶替者。耶鲁大学计算机科学系;[http://cs.yale.edu/publications/techreports/tr1332.pdf](http://cs.yale.edu/publications/techreports/tr1332.pdf)。

2. Back, A. 1997. A partial hash collision based postage scheme; [http://www.hashcash.org/papers/announce.txt](http://www.hashcash.org/papers/announce.txt).  
2. Back， A. 1997 年。基于部分哈希冲突的邮资方案;[http://www.hashcash.org/papers/announce.txt](http://www.hashcash.org/papers/announce.txt)。

3. Back, A. 2001. Hash cash; [https://web.archive.org/web/20010614013848/http://cypherspace.org/hashcash/](https://web.archive.org/web/20010614013848/http://cypherspace.org/hashcash/).  
3. Back， A. 2001 年。哈希现金;[https://web.archive.org/web/20010614013848/http://cypherspace.org/hashcash/](https://web.archive.org/web/20010614013848/http://cypherspace.org/hashcash/)。

4. Back, A. 2002. Hashcash—a denial of service counter measure; [http://www.hashcash.org/papers/hashcash.pdf](http://www.hashcash.org/papers/hashcash.pdf).  
4. Back， A. 2002 年。Hashcash — 拒绝服务对策;[http://www.hashcash.org/papers/hashcash.pdf](http://www.hashcash.org/papers/hashcash.pdf)。

5. Bayer, D., Haber, S., Stornetta, W. S. Improving the efficiency and reliability of digital time-stamping. _Proceedings of Sequences_ 1991; [https://link.springer.com/chapter/10.1007/978-1-4613-9323-8_24](https://link.springer.com/chapter/10.1007/978-1-4613-9323-8_24).  
5. Bayer， D.， Haber， S.， Stornetta， WS 提高数字时间戳的效率和可靠性。_序列论文集_ 1991 年;[https://link.springer.com/chapter/10.1007/978-1-4613-9323-8_24](https://link.springer.com/chapter/10.1007/978-1-4613-9323-8_24)。

6. Benaloh, J., de Mare, M. 1991. Efficient broadcast timestamping; [http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.38.9199](http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.38.9199).  
6. Benaloh， J.， de Mare， M. 1991 年。高效的广播时间戳;[http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.38.9199](http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.38.9199)。

7. Boyle, T. F. 1997. GLT and GLR: Component architecture for general ledgers; [https://linas.org/mirrors/www.gldialtone.com/2001.07.14/GLT-GLR.htm](https://linas.org/mirrors/www.gldialtone.com/2001.07.14/GLT-GLR.htm).  
7. 博伊尔，TF 1997。GLT 和 GLR：总账的组件架构;[https://linas.org/mirrors/www.gldialtone.com/2001.07.14/GLT-GLR.htm](https://linas.org/mirrors/www.gldialtone.com/2001.07.14/GLT-GLR.htm)。

8. Castro, M., Liskov, B. 1999. Practical Byzantine fault tolerance. _Proceedings of the Third Symposium on Operating Systems Design and Implementation;_[http://pmg.csail.mit.edu/papers/osdi99.pdf](http://pmg.csail.mit.edu/papers/osdi99.pdf).  
8. 卡斯特罗，M.，利斯科夫，B. 1999。实用的拜占庭容错能力。_第三届操作系统设计和实施研讨会论文集;_[http://pmg.csail.mit.edu/papers/osdi99.pdf](http://pmg.csail.mit.edu/papers/osdi99.pdf)。

9. Chaum, D. 1981. Untraceable electronic mail, return addresses, and digital pseudonyms. _Communications of the ACM_ 24(2): 84-90; [https://dl.acm.org/citation.cfm?id=358563](https://dl.acm.org/citation.cfm?id=358563).  
9. Chaum， D. 1981 年。无法追踪的电子邮件、返回地址和数字假名。_ACM 通讯_ 24（2）：84-90;[https://dl.acm.org/citation.cfm?id=358563](https://dl.acm.org/citation.cfm?id=358563)。

10. Chaum, D. 1983. Blind signatures for untraceable payments. _Advances in Cryptology_: 199-203.  
10. Chaum， D. 1983 年。无法追踪的付款的盲签名。_密码学进展_：199-203。

11. Chaum, D. 1985. Security without identification: transaction systems to make Big Brother obsolete. _Communications of the ACM_ 28(10): 1030-1044; [https://dl.acm.org/citation.cfm?id=4373](https://dl.acm.org/citation.cfm?id=4373).  
11. Chaum， D. 1985 年。无需身份识别的安全性：使 Big Brother 过时的交易系统。_ACM 通讯_ 28（10）：1030-1044;[https://dl.acm.org/citation.cfm?id=4373](https://dl.acm.org/citation.cfm?id=4373)。

12. Chaum, D., et al. 1988. Untraceable electronic cash. _Advances in Cryptology_: 319-327; [https://dl.acm.org/citation.cfm?id=88969](https://dl.acm.org/citation.cfm?id=88969).  
12. Chaum， D. 等人，1988 年。无法追踪的电子现金。_密码学进展_：319-327;[https://dl.acm.org/citation.cfm?id=88969](https://dl.acm.org/citation.cfm?id=88969)。

13. Dai, W. 1998; [http://www.weidai.com/bmoney.txt](http://www.weidai.com/bmoney.txt).  
13. 戴，W. 1998;[http://www.weidai.com/bmoney.txt](http://www.weidai.com/bmoney.txt)。

14. Douceur, J. R. 2002. The Sybil attack; [https://dl.acm.org/citation.cfm?id=687813](https://dl.acm.org/citation.cfm?id=687813).  
14. Douceur， J. R. 2002 年。Sybil 袭击;[https://dl.acm.org/citation.cfm?id=687813](https://dl.acm.org/citation.cfm?id=687813)。

15. Dwork, C., Naor, M. 1992. Pricing via processing or combatting junk mail; [https://dl.acm.org/citation.cfm?id=705669](https://dl.acm.org/citation.cfm?id=705669).  
15. Dwork， C.， Naor， M. 1992 年。通过处理或打击垃圾邮件进行定价;[https://dl.acm.org/citation.cfm?id=705669](https://dl.acm.org/citation.cfm?id=705669)。

16. Felten, E. 2017. Smart contracts: neither smart nor contracts? Freedom to Tinker; [https://freedom-to-tinker.com/2017/02/20/smart-contracts-neither-smart-not-contracts/](https://freedom-to-tinker.com/2017/02/20/smart-contracts-neither-smart-not-contracts/).  
16. 费尔滕，E. 2017 年。智能合约：既不是智能还是合约？Freedom to Tinker;[https://freedom-to-tinker.com/2017/02/20/smart-contracts-neither-smart-not-contracts/](https://freedom-to-tinker.com/2017/02/20/smart-contracts-neither-smart-not-contracts/)。

17. Franklin, M. K., Malkhi, D. 1997. Auditable metering and lightweight security; [http://www.hashcash.org/papers/auditable-metering.pdf](http://www.hashcash.org/papers/auditable-metering.pdf).  
17. 富兰克林，MK，马尔基，D. 1997。可审计的计量和轻量级安全性;[http://www.hashcash.org/papers/auditable-metering.pdf](http://www.hashcash.org/papers/auditable-metering.pdf)。

18. Gabber, E., et al. 1998. Curbing Junk E-Mail via Secure Classiffication. [http://www.hashcash.org/papers/secure-classification.pdf](http://www.hashcash.org/papers/secure-classification.pdf).  
18. Gabber， E. 等人，1998 年。通过安全分类遏制垃圾邮件。[http://www.hashcash.org/papers/secure-classification.pdf](http://www.hashcash.org/papers/secure-classification.pdf)。

19. Garay, J. A., et al. 2015. The bitcoin backbone protocol: analysis and applications. _Advances in Cryptology_: 281-310; [https://eprint.iacr.org/2014/765.pdf](https://eprint.iacr.org/2014/765.pdf).  
19. Garay， J. A. 等人，2015 年。比特币骨干协议：分析和应用。_密码学进展_：281-310;[https://eprint.iacr.org/2014/765.pdf](https://eprint.iacr.org/2014/765.pdf)。

20. Goldberg, I. 2000. A pseudonymous communications infrastructure for the Internet. Ph.D. dissertation, University of California Berkeley; [http://moria.freehaven.net/anonbib/cache/ian-thesis.pdf](http://moria.freehaven.net/anonbib/cache/ian-thesis.pdf).  
20. 戈德堡，I. 2000 年。用于 Internet 的假名通信基础设施。博士论文，加州大学伯克利分校;[http://moria.freehaven.net/anonbib/cache/ian-thesis.pdf](http://moria.freehaven.net/anonbib/cache/ian-thesis.pdf)。

21. Grigg, I. 2005. Triple entry accounting; [http://iang.org/papers/triple_entry.html](http://iang.org/papers/triple_entry.html).  
21. 格里格，I. 2005 年。三式记账法;[http://iang.org/papers/triple_entry.html](http://iang.org/papers/triple_entry.html)。

22. Haber, S., Stornetta, W. S. 1991. How to timestamp a digital document. _Journal of Cryptology_ 3(2): 99-111; [https://link.springer.com/chapter/10.1007/3-540-38424-3_32](https://link.springer.com/chapter/10.1007/3-540-38424-3_32).  
22. 哈伯，S.，斯托内塔，WS 1991 年。如何为数字文档添加时间戳。_密码学杂志_ 3（2）：99-111;[https://link.springer.com/chapter/10.1007/3-540-38424-3_32](https://link.springer.com/chapter/10.1007/3-540-38424-3_32)。

23. Haber, S., Stornetta, W. S. 1997. Secure names for bit-strings. In _Proceedings of the 4th ACM Conference on Computer and Communications Security_: 28-35; [http://dl.acm.org/citation.cfm?id=266430](http://dl.acm.org/citation.cfm?id=266430).  
23. Haber， S.， Stornetta， WS 1997 年。保护位串的名称。第 _4届 ACM 计算机和通信安全会议论文集_：28-35;[http://dl.acm.org/citation.cfm?id=266430](http://dl.acm.org/citation.cfm?id=266430)。

24. Jakobsson, M., Juels, A. 1999. Proofs of work and bread pudding protocols; [http://www.hashcash.org/papers/bread-pudding.pdf](http://www.hashcash.org/papers/bread-pudding.pdf).  
24. Jakobsson， M.， Juels， A. 1999 年。工作量证明和面包布丁协议;[http://www.hashcash.org/papers/bread-pudding.pdf](http://www.hashcash.org/papers/bread-pudding.pdf)。

25. Juels, A., Brainard, J. 1999. Client puzzles: a cryptographic countermeasure against connection completion attacks. _Proceedings of Networks and Distributed Security Systems_: 151-165; [https://www.isoc.org/isoc/conferences/ndss/99/proceedings/papers/juels.pdf](https://www.isoc.org/isoc/conferences/ndss/99/proceedings/papers/juels.pdf).  
25. Juels， A.， Brainard， J. 1999 年。Client puzzles：针对连接完成攻击的加密对策。_网络和分布式安全系统论文集_：151-165;[https://www.isoc.org/isoc/conferences/ndss/99/proceedings/papers/juels.pdf](https://www.isoc.org/isoc/conferences/ndss/99/proceedings/papers/juels.pdf)。

26. Just, M. 1998. Some timestamping protocol failures; [http://www.isoc.org/isoc/conferences/ndss/98/just.pdf](http://www.isoc.org/isoc/conferences/ndss/98/just.pdf).  
26. 贾斯特，M. 1998 年。一些时间戳协议失败;[http://www.isoc.org/isoc/conferences/ndss/98/just.pdf](http://www.isoc.org/isoc/conferences/ndss/98/just.pdf)。

27. Lamport, L., et al. 1982. The Byzantine Generals Problem. _ACM Transactions on Programming Languages and Systems_ 4(3): 382-401; [https://dl.acm.org/citation.cfm?id=357176](https://dl.acm.org/citation.cfm?id=357176) .  
27. Lamport， L. 等人，1982 年。拜占庭将军问题。_ACM 编程语言和系统汇刊_ 4（3）：382-401;[https://dl.acm.org/citation.cfm?id=357176](https://dl.acm.org/citation.cfm?id=357176) .

28. Lamport, L. 1989. The part-time parliament. Digital Equipment Corporation; [https://computerarchive.org/files/mirror/www.bitsavers.org/pdf/dec/tech_reports/SRC-RR-49.pdf](https://computerarchive.org/files/mirror/www.bitsavers.org/pdf/dec/tech_reports/SRC-RR-49.pdf).  
28. 兰波特，L. 1989 年。兼职议会。数字设备公司;[https://computerarchive.org/files/mirror/www.bitsavers.org/pdf/dec/tech_reports/SRC-RR-49.pdf](https://computerarchive.org/files/mirror/www.bitsavers.org/pdf/dec/tech_reports/SRC-RR-49.pdf)。

29. Lamport, L. 2001. Paxos made simple; [http://lamport.azurewebsites.net/pubs/paxos-simple.pdf](http://lamport.azurewebsites.net/pubs/paxos-simple.pdf).  
29. 兰波特，L. 2001 年。Paxos 变得简单;[http://lamport.azurewebsites.net/pubs/paxos-simple.pdf](http://lamport.azurewebsites.net/pubs/paxos-simple.pdf)。

30. Laurie, B. 2014. Certificate Transparency. _acmqueue_ 12(8); [https://queue.acm.org/detail.cfm?id=2668154](https://queue.acm.org/detail.cfm?id=2668154).  
30. 劳里，生于 2014 年。证书透明度。_ACM队列_ 12（8）;[https://queue.acm.org/detail.cfm?id=2668154](https://queue.acm.org/detail.cfm?id=2668154)。

31. Levy, K. E. C. 2017. Book-smart, not street-smart: blockchain-based smart contracts and the social workings of law. _Engaging Science, Technology, and Society_3: 1-15; [http://estsjournal.org/article/view/107](http://estsjournal.org/article/view/107).  
31. 利维，KEC 2017 年。Book-smart，而不是 street-smart：基于区块链的智能合约和法律的社会运作。_参与科学、技术和社会_ 3：1-15;[http://estsjournal.org/article/view/107](http://estsjournal.org/article/view/107)。

32. Melara, M., et al. 2015. CONIKS: bringing key transparency to end users. _Proceedings of the 24th Usenix Security Symposium_; [https://www.usenix.org/system/files/conference/usenixsecurity15/sec15-paper-melara.pdf](https://www.usenix.org/system/files/conference/usenixsecurity15/sec15-paper-melara.pdf).  
32. Melara， M. 等人，2015 年。CONIKS：为最终用户带来关键的透明度。_第 24届 Usenix 安全研讨会论文集_;[https://www.usenix.org/system/files/conference/usenixsecurity15/sec15-paper-melara.pdf](https://www.usenix.org/system/files/conference/usenixsecurity15/sec15-paper-melara.pdf)。

33. Merkle, R. C. 1980. Protocols for public key cryptosystems. IEEE Symposium on Security and Privacy; [http://www.merkle.com/papers/Protocols.pdf](http://www.merkle.com/papers/Protocols.pdf).  
33. 默克尔，RC 1980 年。公钥密码系统的协议。IEEE 安全和隐私研讨会;[http://www.merkle.com/papers/Protocols.pdf](http://www.merkle.com/papers/Protocols.pdf)。

34. Nakamoto, S. 2008. Bitcoin: a peer-to-peer electronic cash system; [https://bitcoin.org/bitcoin.pdf](https://bitcoin.org/bitcoin.pdf).  
34. 中本聪，S. 2008 年。比特币：一种点对点的电子现金系统;[https://bitcoin.org/bitcoin.pdf](https://bitcoin.org/bitcoin.pdf)。

35. Nakamoto, S. 2008. Re: Bitcoin P2P e-cash paper; [http://satoshi.nakamotoinstitute.org/emails/cryptography/11/](http://satoshi.nakamotoinstitute.org/emails/cryptography/11/).  
35. 中本聪，S. 2008 年。回复：比特币 P2P 电子现金纸;[http://satoshi.nakamotoinstitute.org/emails/cryptography/11/](http://satoshi.nakamotoinstitute.org/emails/cryptography/11/)。

36. Narayanan, A., et al. 2016. _Bitcoin and Cryptocurrency Technologies: A Comprehensive Introduction_. Princeton University Press; [http://bitcoinbook.cs.princeton.edu/](http://bitcoinbook.cs.princeton.edu/).  
36. Narayanan， A. 等人，2016 年。_比特币和加密货币技术：全面介绍_。普林斯顿大学出版社;[http://bitcoinbook.cs.princeton.edu/](http://bitcoinbook.cs.princeton.edu/)。

37. Pass, R., et al. 2017. Analysis of the blockchain protocol in asynchronous networks. _Annual International Conference on the Theory and Applications of Cryptographic Techniques_; [https://link.springer.com/chapter/10.1007/978-3-319-56614-6_22](https://link.springer.com/chapter/10.1007/978-3-319-56614-6_22).  
37. Pass， R. 等人，2017 年。异步网络中的区块链协议分析。_密码技术理论与应用年度国际会议_;[https://link.springer.com/chapter/10.1007/978-3-319-56614-6_22](https://link.springer.com/chapter/10.1007/978-3-319-56614-6_22)。

38. Pinkas, B., Sander, T. 2002. Securing passwords against dictionary attacks. _Proceedings of the Ninth ACM Conference on Computer and Communications Security_: 161-170; [https://dl.acm.org/citation.cfm?id=586133](https://dl.acm.org/citation.cfm?id=586133).  
38. Pinkas， B.， Sander， T. 2002 年。保护密码免受字典攻击。_第九届 ACM 计算机与通信安全会议论文集_：161-170;[https://dl.acm.org/citation.cfm?id=586133](https://dl.acm.org/citation.cfm?id=586133)。

39. Reuters. 2014. Mind your wallet: why the underworld loves bitcoin; [http://www.cnbc.com/2014/03/14/mind-your-wallet-why-the-underworld-loves-bitcoin.html](http://www.cnbc.com/2014/03/14/mind-your-wallet-why-the-underworld-loves-bitcoin.html).  
39. 路透社。2014. 注意你的钱包：为什么黑社会喜欢比特币;[http://www.cnbc.com/2014/03/14/mind-your-wallet-why-the-underworld-loves-bitcoin.html](http://www.cnbc.com/2014/03/14/mind-your-wallet-why-the-underworld-loves-bitcoin.html)。

40. Sirer, E. G. 2016. Bitcoin guarantees strong, not eventual, consistency. Hacking, Distributed; [http://hackingdistributed.com/2016/03/01/bitcoin-guarantees-strong-not-eventual-consistency/](http://hackingdistributed.com/2016/03/01/bitcoin-guarantees-strong-not-eventual-consistency/).  
40. Sirer， EG 2016 年。比特币保证的是强大的一致性，而不是最终的一致性。黑客攻击，分布式;[http://hackingdistributed.com/2016/03/01/bitcoin-guarantees-strong-not-eventual-consistency/](http://hackingdistributed.com/2016/03/01/bitcoin-guarantees-strong-not-eventual-consistency/)。

41. Szabo, N. 1994. Smart contracts; [http://www.fon.hum.uva.nl/rob/Courses/InformationInSpeech/CDROM/Literature/LOTwinterschool2006/szabo.best.vwh.net/smart.contracts.html](http://www.fon.hum.uva.nl/rob/Courses/InformationInSpeech/CDROM/Literature/LOTwinterschool2006/szabo.best.vwh.net/smart.contracts.html).  
41. Szabo， N. 1994 年。智能合约;[http://www.fon.hum.uva.nl/rob/Courses/InformationInSpeech/CDROM/Literature/LOTwinterschool2006/szabo.best.vwh.net/smart.contracts.html](http://www.fon.hum.uva.nl/rob/Courses/InformationInSpeech/CDROM/Literature/LOTwinterschool2006/szabo.best.vwh.net/smart.contracts.html)。

42. Szabo, N. 2008. Bit gold. Unenumerated; [https://unenumerated.blogspot.com/2005/12/bit-gold.html](https://unenumerated.blogspot.com/2005/12/bit-gold.html).  
42. Szabo， N. 2008 年。比特金。未列举;[https://unenumerated.blogspot.com/2005/12/bit-gold.html](https://unenumerated.blogspot.com/2005/12/bit-gold.html)。

43. Wattenhofer, R. 2016. _The Science of the Blockchain_. Inverted Forest Publishing.  
43. 瓦滕霍夫，R. 2016 年。_区块链科学_。倒林出版社。

44. Rivest, R. L., Shamir, A. 1996. PayWord and MicroMint: Two simple micropayment schemes. _International Workshop on Security Protocols._  
44. Rivest， RL， Shamir， A. 1996 年。PayWord 和 MicroMint：两种简单的小额支付方案。_安全协议国际研讨会。_

**Arvind Narayanan** is an assistant professor of computer science at Princeton. He leads the Princeton Web Transparency and Accountability Project to uncover how companies collect and use our personal information. Narayanan also leads a research team investigating the security, anonymity, and stability of cryptocurrencies, as well as novel applications of blockchains. He co-created a massive open online course, and a textbook on bitcoin and cryptocurrency technologies. His doctoral research showed the fundamental limits of de-identification, for which he received the Privacy Enhancing Technologies Award. Narayanan is an affiliated faculty member at the Center for Information Technology Policy at Princeton and an affiliate scholar at Stanford Law School's Center for Internet and Society. You can follow him on Twitter at @random_walker.  
**Arvind Narayanan** 是普林斯顿大学计算机科学助理教授。他领导普林斯顿网络透明度和问责制项目，以揭示公司如何收集和使用我们的个人信息。Narayanan 还领导一个研究团队，调查加密货币的安全性、匿名性和稳定性，以及区块链的新颖应用。他与他人共同创建了一个大型开放式在线课程，以及一本关于比特币和加密货币技术的教科书。他的博士研究揭示了去标识化的基本局限性，为此他获得了隐私增强技术奖。Narayanan 是普林斯顿信息技术政策中心的附属教员，也是斯坦福法学院互联网与社会中心的附属学者。您可以在 Twitter 上关注他 @random_walker。

**Jeremy Clark** is an assistant professor at the Concordia Institute for Information Systems Engineering. He obtained his Ph.D. from the University of Waterloo, where his gold medal dissertation was on designing and deploying secure voting systems, including Scantegrity—the first cryptographically verifiable system used in a public-sector election. He wrote one of the earliest academic papers on bitcoin, completed several research projects in the area, and contributed to the first textbook. Beyond research, he has worked with several municipalities on voting technology and testified to the Canadian Senate on bitcoin. You can follow him on Twitter at @PulpSpy.  
**Jeremy Clark** 是 Concordia Institute for Information Systems Engineering 的助理教授。他在滑铁卢大学获得博士学位，在那里他的金牌论文是关于设计和部署安全投票系统，包括 Scantegrity——第一个用于公共部门选举的加密验证系统。他撰写了最早的比特币学术论文之一，完成了该领域的多个研究项目，并为第一本教科书做出了贡献。除了研究之外，他还与多个城市合作研究投票技术，并就比特币问题向加拿大参议院作证。您可以在 Twitter 上关注他 @PulpSpy。

Copyright © 2017 held by owner/author. Publication rights licensed to ACM.  
版权所有 © 2017 归所有者/作者所有。授权给 ACM 的出版权。

![acmqueue](https://queue.acm.org/img/q%20stamp_small.jpg)  
  
_Originally published in Queue vol. 15, no. 4_—  
_最初发表于 Queue vol. 15， no. 4_—  
Comment on this article in the [ACM Digital Library](http://portal.acm.org/citation.cfm?id=3136559)  
在 [ACM 数字图书馆](http://portal.acm.org/citation.cfm?id=3136559)中对本文发表评论

  
  
  

---

More related articles:

Jinnan Guo, Peter Pietzuch, Andrew Paverd, Kapil Vaswani - [**Trustworthy AI using Confidential Federated Learning**](https://queue.acm.org/detail.cfm?id=3665220)  
Jinnan Guo、Peter Pietzuch、Andrew Paverd、Kapil Vaswani - [**使用机密联邦学习的可信 AI**](https://queue.acm.org/detail.cfm?id=3665220)  
The principles of security, privacy, accountability, transparency, and fairness are the cornerstones of modern AI regulations. Classic FL was designed with a strong emphasis on security and privacy, at the cost of transparency and accountability. CFL addresses this gap with a careful combination of FL with TEEs and commitments. In addition, CFL brings other desirable security properties, such as code-based access control, model confidentiality, and protection of models during inference. Recent advances in confidential computing such as confidential containers and confidential GPUs mean that existing FL frameworks can be extended seamlessly to support CFL with low overheads.  
安全、隐私、问责制、透明度和公平性原则是现代 AI 法规的基石。Classic FL 的设计非常强调安全性和隐私性，但以牺牲透明度和问责制为代价。CFL 通过将 FL 与 TEE 和承诺仔细结合来解决这一差距。此外，CFL 还带来了其他理想的安全属性，例如基于代码的访问控制、模型机密性和推理期间的模型保护。机密计算的最新进展（例如机密容器和机密 GPU）意味着现有的 FL 框架可以无缝扩展，以较低的开销支持 CFL。

  

Raluca Ada Popa - [**Confidential Computing or Cryptographic Computing?**](https://queue.acm.org/detail.cfm?id=3664295)  
Raluca Ada Popa - [**机密计算还是加密计算？**](https://queue.acm.org/detail.cfm?id=3664295)  
Secure computation via MPC/homomorphic encryption versus hardware enclaves presents tradeoffs involving deployment, security, and performance. Regarding performance, it matters a lot which workload you have in mind. For simple workloads such as simple summations, low-degree polynomials, or simple machine-learning tasks, both approaches can be ready to use in practice, but for rich computations such as complex SQL analytics or training large machine-learning models, only the hardware enclave approach is at this moment practical enough for many real-world deployment scenarios.  
与 Hardware Enclaves 相比，通过 MPC/同态加密进行安全计算需要在部署、安全性和性能方面进行权衡。关于性能，您考虑的工作负载非常重要。对于简单的工作负载，例如简单求和、低次多项式或简单的机器学习任务，这两种方法都可以在实践中使用，但对于丰富的计算，例如复杂的 SQL 分析或训练大型机器学习模型，目前只有硬件 enclave 方法对于许多实际部署场景来说足够实用。

  

Matthew A. Johnson, Stavros Volos, Ken Gordon, Sean T. Allen, Christoph M. Wintersteiger, Sylvan Clebsch, John Starks, Manuel Costa - [**Confidential Container Groups**](https://queue.acm.org/detail.cfm?id=3664293)  
Matthew A. Johnson、Stavros Volos、Ken Gordon、Sean T. Allen、Christoph M. Wintersteiger、Sylvan Clebsch、John Starks、Manuel Costa - [**机密容器组**](https://queue.acm.org/detail.cfm?id=3664293)  
The experiments presented here demonstrate that Parma, the architecture that drives confidential containers on Azure container instances, adds less than one percent additional performance overhead beyond that added by the underlying TEE. Importantly, Parma ensures a security invariant over all reachable states of the container group rooted in the attestation report. This allows external third parties to communicate securely with containers, enabling a wide range of containerized workflows that require confidential access to secure data. Companies obtain the advantages of running their most confidential workflows in the cloud without having to compromise on their security requirements.  
此处介绍的实验表明，Parma（在 Azure 容器实例上驱动机密容器的体系结构）增加的性能开销比基础 TEE 增加的性能开销不到 1%。重要的是，Parma 可确保容器组的所有可访问状态的安全不变性（植根于认证报告）。这允许外部第三方与容器安全通信，从而支持需要对安全数据进行机密访问的各种容器化工作流。公司可以在云中运行其最机密的工作流，而无需在安全要求上妥协。

  

Charles Garcia-Tobin, Mark Knight - [**Elevating Security with Arm CCA**](https://queue.acm.org/detail.cfm?id=3664291)  
Charles Garcia-Tobin、Mark Knight - [**使用 Arm CCA 提升安全性**](https://queue.acm.org/detail.cfm?id=3664291)  
Confidential computing has great potential to improve the security of general-purpose computing platforms by taking supervisory systems out of the TCB, thereby reducing the size of the TCB, the attack surface, and the attack vectors that security architects must consider. Confidential computing requires innovations in platform hardware and software, but these have the potential to enable greater trust in computing, especially on devices that are owned or controlled by third parties. Early consumers of confidential computing will need to make their own decisions about the platforms they choose to trust.  
机密计算具有巨大的潜力，可以通过将监控系统从 TCB 中移除来提高通用计算平台的安全性，从而减少 TCB 的大小、攻击面和安全架构师必须考虑的攻击向量。机密计算需要平台硬件和软件方面的创新，但这些创新有可能提高对计算的信任，尤其是在第三方拥有或控制的设备上。机密计算的早期使用者需要自己决定他们选择信任的平台。

  

---

---

[![](https://queue.acm.org/img/logo_acm.gif)](https://queue.acm.org/detail.cfm?id=3136559#)  
© ACM, Inc. All Rights Reserved.  
© ACM 公司保留所有权利。