---
title: Aptos 全方位解析
link: https://www.jinse.cn/blockchain/3671103.html
---

# Aptos全方位解析：技术、代币经济学、网络活动、生态系统

## 金色财经

 刚刚 ![](https://staticn.jinse.cn/w/img/868bf8c.svg)

作者：Peter Horton，L1协议分析师；翻译：金色财经xiaozou

## 1、关键见解

- Aptos是围绕可扩展性、安全性、可靠性和可升级性的核心原则设计的L1区块链。它诞生于Meta的Diem和Novi项目，于2022年10月问世。
    
- Aptos的技术栈具有很多新颖之处，例如AptosBFTv4共识机制、Quorum Store内存池协议、Block-STM并行执行引擎和编程语言Aptos Move。
    
- 自2023年7月以来，Aptos平均每天处理超475,000笔交易，日活地址超72,000个。网络活动受社交媒体平台Chingari、oracle Pyth和Graffio上为期一日的公共艺术创作活动推动。
    
- Aptos Labs和Aptos基金会已经与许多知名公司和集团建立了合作伙伴关系，例如微软、阿里云、NPIXEL、乐天集团、Coinbase Pay等等，许多增长计划都集中在亚太地区。
    

关于模块化与集成的争论已经烂大街了，总之，双方都趋向于一个类似的终局：模块化链最初是面向可验证性和去中心化而优化的，而集成链则是面向低延迟和高吞吐量而优化的。

Aptos是集成阵营中最大的参与者之一，其开发团队Aptos Labs已筹资大约4亿美元。自2022年10月上线以来，该网络迅速升级，已有40多个AIP和8个主要版本。Aptos生态相对来说比较年轻，但已经有了像链上订单簿、perp DEX和社交媒体平台这样的项目。在最近的主网测试环境中，Aptos实现了3万TPS的峰值以及超20亿笔日交易，其目标是超过100万TPS。如果能够继续进行技术升级，吸引开发者和用户，Aptos一定会成功。

## 2、背景介绍

Aptos诞生于Meta的Diem和Novi项目。2019年，Meta（当时名为Facebook）正式宣布即将推出基于区块链的支付网络。该项目由许可链Diem（最初叫做Libra）和Novi钱包（最初叫做Calibra）组成。由Diem Association和Facebook子公司Novi Financial主导开发。由于监管方面的阻力，Diem和Novi从未发布。Diem在2022年1将其资产出售给Silvergate Capital。2022年9月，Meta宣布结束Novi。

Aptos Labs成立于2021年12月，并于2022年2月正式推出。Aptos Labs由Novi战略合作伙伴主管Mo Sheikh和Novi首席软件工程师Avery Ching共同创立，前者曾在Consensys领导战略工作，并创立了基于区块链的房地产平台Meridio，后者则拥有超级计算背景。其余的创始团队成员有博士、研究人员、工程师、设计师和战略专家，他们当中有许多人也曾在Diem或Novi工作过。

2022年3月，Aptos Labs宣布筹资2亿美元，同时推出其公共devnet和开源代码库。此次融资包括股票和代币期权，由a16z领投，Multicoin Capital、ParaFi Capital、Coinbase Ventures和许多其他投资者参投。2022年7月，Aptos Labs宣布再次融资1.5亿美元，估值为20亿美元，由FTX Ventures和Jump Crypto领投。FTX Ventures也参与了第一轮融资；其投资现在由FTX破产程序控制管理。Binance Labs和Dragonfly Capital的进一步战略投资使融资总额达到约4亿美元。

在Aptos实验室于2022年8月发布Aptos白皮书，2022年10月上线主网。在完整的代币经济学信息公开发布之前，中心化交易所加大了对Aptos原生代币APT的支持，一些人对此表示担忧。Mo Sheikh在次日的一条推文中坦承了这些担忧。自主网上线以来，Aptos网络已经完成了几次升级，现在的版本是V1.8.0。非营利性的Aptos基金会领导Aptos生态系统的发展。

## 3、技术

Aptos技术栈是围绕可扩展性、安全性、可靠性和可升级性的核心原则而设计的。它为Aptos带来了很多方面的新机制。

### （1）共识

Aptos是一个使用AptosBFTv4共识协议的委托权益证明（DPoS）L1网络。

### （2）AptosBFT

AptosBFT（最初叫做DiemBFT）在Diem期间曾经历四次迭代，随后被用于无需许可的Aptos区块链。第一个AptosBFT基于HotStuff，HotStuff本身基于传统的实用拜占庭容错 (pBFT)协议。Aptos当前的部署——AptosBFTv4——现基于Jolteon，它通过一个pBFT形式的二次view change将HotStuff延迟提高了50%。

此外，为了减轻由领导错误引起的延迟，AptosBFT不仅根据质押选择leader，还根据表现（总之就是“声誉”）选择leader。验证者的表现用来衡量他们作为leader（他们的提案被提交的频率）和作为非leader（他们对提案的投票频率）的成功率。

在2023年7月18日完成的Aptos V1.5升级中，Quorum Store的部署进一步提高了Aptos吞吐量。Quorum Store是一个内存池协议Narwhale的实现。Quorum Store通过将数据传播与共识分离来优化共识。数据传播与共识的分离是《Narwhal和Tusk》一文的关键发现，该研究文章由Aptos Labs和Mysten Labs的研究人员共同撰写。

在Quorum Store之前，交易处理要经过内存池和共识阶段：

- 内存池阶段：将所有交易被广播给所有验证者。
    
- 共识阶段：leader将其创建区块中的所有交易广播给所有验证者。非leader通过发送签名的区块元数据来对区块进行投票。
    

这导致出现了两个瓶颈：

- 重复交易传播：在内存池和共识阶段，所有交易都向所有验证者传播两次。
    
- 工作分配不均：在共识阶段，leader比非leader完成更多的工作，因为leader必须发送原始交易而不是签名的区块元数据（相对较小的消息）。因此，总带宽以leader的带宽为上限，非leader的带宽未被充分利用。
    
- Store在内存池和共识协议之间添加了一个中间阶段。现在完整的过程如下：
    
- 内存池阶段：交易不再被广播给验证者，而是发送到Quorum Store。
    
- Quorum Store阶段：Quorum Store协议从内存池接收交易，并按照gas费将交易排序打包。Quorum Store将这些交易包发送给验证者。接收交易包后，验证者签署交易包并将其发送给其他验证者。一旦一个交易包收到超过2/3的验证者签名，Quorum Store就会创建一个可用性证明（Proof-of-Availability），保证该批次的唯一性和可用性。
    
- 共识阶段：共识协议是相同的，除了现在领导者使用来自Quorum Store的认证交易包创建区块，而不是来自内存池的原始交易。
    

解决了以上两个瓶颈：

- 重复交易传播：原始交易只传播一次（从内存池到Quorum Store），之后只传播交易包，从而减少消息中的数据量。
    
- 工作分配不均：在共识阶段，leader只需要发送交易包元数据（以及相应的PoAv）。这比以往的工作量要少得多，而且与非leader的工作量相当。此外，所有验证者在Quorum Store阶段的工作量都是平等的。
    

### （3）DPoS

验证者通过通胀的质押奖励得到补偿。目前，所有的交易费都被burn掉了。质押奖励和验证者的声誉（质押和表现）挂钩。奖励将于每epoch（将持续两个小时）内自动分配和组合。质押代币被全局锁定在30天的周期内。

每个验证者设置一个佣金率，剩余的代币被传递给它们的委托者。协议内委托质押于2023年4月20日在主网上部署。委托者至少需要质押11 APT才能加入。这将让更多的社区参与质押，而作为验证者参与质押的最低质押额是100万APT（截至2023年12月26日为1050万美元）。

对于验证者来说，质押上限为5000万APT，约占总供应量的5%，这并不是一个非常严格的上限。然而，如果验证者运营商获得足够的质押，将被激励启动多个验证节点。值得注意的是，锁定代币也能够用于质押并获得流动奖励（在全局30天解锁期后）。

目前还没有针对离线验证者或恶意验证者的罚没机制，但是将来可以通过治理来添加这样的机制。

### （4）执行

一旦验证者就区块顺序达成一致，他们就需要执行区块中的交易并将结果永久存储。许多区块链都有一个顺序交易引擎，其中交易被排序并逐一执行。为了加快执行速度，Aptos使用并行执行引擎。此外，Aptos与Solana和Sui等其他并行处理交易的网络不同，它不需要预先知晓用户声明的依赖项（dependencies）信息。

为了做到这一点，Aptos使用Block-STM，Block-STM建立在软件事务内存(STM)和optimistic并发控制(OCC)的原则之上。带有OCC的STM库遵循这样的通用框架：乐观地（optimistically）执行交易（即假设不存在依赖项），在执行后验证，在出现依赖项时中止，并最终再次执行。然而，由于管理依赖项和级联回滚导致的性能限制，这种方法在实践中很少使用。

为了迎合部署并克服OCC STM系统的这些限制，Block-STM利用预先设定的交易顺序来评估依赖项，减少回滚量。Bohm(2014)研究报告的主要发现之一是，预设交易顺序可能是件好事，不是什么诅咒。Block-STM甚至比Bohm更充分地利用了预设顺序，通过系统中的每次回滚来细化依赖项评估（因此，减少了进一步回滚的机会）。

Block-STM通过利用区块链的各个方面，进一步改进了通用STM，具体包括：

- VM安全性：Move VM（下文将详细介绍Move）确保未提交状态不会通过捕获错误和征收gas费而对其他正在进行的交易产生负面影响。
    
- 区块粒度：垃圾回收很简单，因为可以在区块之间进行。虽然Block-STM最初只是跟踪区块承诺（commitments）以降低同步成本，但Aptos Labs后来改进了算法。它现在支持区块内滚动提交，而且不会以牺牲性能为代价。
    

在介绍Block-STM的具体步骤之前，首先解释一个已经提到的术语——dependencies（依赖项）——将会有所帮助。区块链交易由智能合约代码组成，这些代码可以读写共享内存。在执行时，每个交易都有一个读写位置（分别叫做read-set和write-set）列表。如果Mo的交易从共享内存中的一个位置（首先由Avery交易写入）读取，那么Mo的交易依赖于Avery的交易。存在依赖项的交易必须按顺序执行，在这种情况下，Avery在Mo之前执行。

知道了这些，我们就可以深入来看Block-STM的各步过程，主要分为五个阶段：

**阶段1：交易预设排序**

从上一个共识阶段开始，就存在包含按顺序排列的交易块。如上所述，这种预设顺序是Block-STM的一个关键优势。并行执行结果必须产生与顺序执行结果相同的rea-set和write-set（读写集）。

**阶段2：optimistic执行**

Block-STM乐观地（optimistically）并行执行交易。换句话说，它是在不存在依赖项的情况下执行交易。

**阶段3：验证**

然后要验证已执行的交易，即检查依赖项。这是通过重新读取交易的read-set并将其与最近一次执行的read-set进行比较来实现的。如果两个read-set不相等，则交易回滚。

Block-STM的一个关键部分是以有效的方式连续调度执行和验证任务，尤其是：

- 按照预设顺序提前安排任务的优先级。
    
- 尽早调度验证波来检测漏掉的依赖项，以避免级联回滚。
    

请注意，验证比执行要便宜得多，因此连续验证（read-sets再读取）并不是主要瓶颈。

**阶段4：回滚和再执行**

当交易回滚时，将一个ESTIMATE tag应用到交易写入位置。然后，如果后来的交易读取该位置，它们将看到一个ESTIMATE tag。在读取ESTIMATE tag时，交易将暂停执行，直到值（value）覆盖ESTIMATE tag。一旦原始的、中止的交易被成功地重新执行，就会发生这种情况。每当重新执行交易时，调度（scheduling）确保预设顺序靠前且依赖其的任何交易都将被重新验证。

这种动态的依赖管理是Block-STM的一个关键概念。如果没有ESTIMATE tag，第二个交易就会被执行，然后可能会回滚，因为它的读取位置某被回滚交易的写入位置。因此，Block-STM避免了执行可能被回滚的交易所浪费的大量工作。此外，动态依赖管理对前期依赖系统进行了若干改进。首先是，用户不必声明依赖项，支持任意复杂交易的原子性（复杂交易不需要分解）。其次，它只在需要时管理依赖项，而不是存储所有交易的依赖项。最后，大多数依赖项都是基于相比区块开始时更新的状态。

**阶段5：提交**

一旦Block-STM检测到某交易的optimistic执行输出是正确的，它就由滚动提交机制提交。滚动提交依赖于轻量级同步，在处理下一波交易之前验证和提交每一波交易。

Block-STM在Aptos基准测试中通过32个线程达到了170,000 TPS。这比顺序执行提高了17倍。

### （5）存储

当一个区块被提交时，它的数据被永久存储在存储层。虽然提交是按各区块完成的，但每个单独的交易在执行后单独存储在Merkle树中。区块链上发生的所有事——包括交易、状态更新和事件——都可以根据称作“root hash”（根哈希）的摘要进行加密证明，该摘要由当前验证者签名进行身份验证。这种方法不同于其他区块链，在其他区块链中，人们需要跟踪区块链来验证历史交易，从而允许更细粒度的可证明数据访问。

为了处理大量数据，Aptos使用两种类型的Merkle树：Jellyfish Merkle树用于将数据存储在磁盘上，内存中的Sparse Merkle树用于快速更新。这些树经过优化，可以有效地存储数据并允许并发更新。Aptos Labs正在探索扩展存储的进一步途径，特别是在路线图部分中详细介绍的存储分片（storage sharding）。

### （6）Move语言

Move是一种字节码语言，灵感来源于Rust，由Diem和Novi团队创建。Move提供了比Solidity和其他Web3编程语言更大的灵活性和安全性。

Move由两类程序组成：事务脚本和模块。事务脚本是原子的，只能使用一次，而模块以全局状态发布，并无限期地存储在那里。

模块类似于其他编程语言中的智能合约。它们定义资源及其相关的过程。资源就像一个对象，过程是可以针对资源执行的操作，例如创建、修改或删除。资源是专门设计用来表示像代币这样的稀缺资产的。它们具有内置保护功能，可帮助这些资产避免被错误复制或丢弃。

模块强制执行数据抽象，其中类型在其声明模块内是透明的，在生命模块外是不透明的。换句话说，只有原始模块可以创建、销毁或更新值。对模块数据的外部访问仅限于模块公开的公共过程。这些保证由Move的字节码验证器在执行期间强制实施，所有模块和事务脚本都必须通过这个过程才能被Move VM执行。这种数据抽象在Move中比在Solidity/EVM中更加明显，后者有封装，但具体实施并不那么严格。

Move旨在消除Solidity和EVM中存在的攻击向量，特别是那些由于缺乏以太坊以外的一等资产和重入（re-entrancy）攻击而导致的攻击向量。

- 一等资产：在EVM上，ERC-20和其他资产不具有与Ether相同的内置稀缺性和访问控制属性。Solidity开发人员需要手动实现这些保护，以避免引入导致复制、重用或资产丢失的bug。相比之下，所有Move上的资源（而不仅仅是原生资产）都被视为具有这些保护的一等资产。
    
- 重入攻击：与EVM不同，Move没有不安全的动态调度。使用不安全的动态调度，在合约运行之前，VM（虚拟机）并不知道外部合约函数正在执行什么操作。动态调度带来重入攻击，这是区块链黑客攻击最普遍的根源之一，包括最近的Curve/Vyper漏洞攻击。在重入攻击中，合约调用外部合约，该外部合约在原始合约执行完成之前回调原始合约并更新余额，这可能一次又一次的资金损失。
    

Move的目标是让开发者更难犯错。除了字节码验证器，开发人员还可以使用Move Prover，这是一种正式的验证工具。当然，Move并不能消除智能合约漏洞的可能性。程序员们仍然需要在他们的模块中建立适当的安全不变量。此外，字节码验证器和Move Prover并不能取代审计的需求。审计公司CertiK观察到几例开发人员没有使用Move的内置保护机制或没有采用编程模式的例子，很可能是从与Move的设计理念背道而驰的遗留代码设计中移植过来的。

### （7）其他主要特性

**用户安全保障**

Aptos具有若干优化用户体验和安全性的特性，包括灵活的密钥管理、交易结果透明和轻客户端支持。

Aptos帐户将私钥与公钥分离，密钥管理灵活。用户可以轮换其帐户私钥，以此来先发制人或应对攻击，无需将所有资产转移到新帐户。用户还可以将其帐户设置为对各公钥具有不同权限的多重签名。例如，用户可以使用两个可以签署交易的热公钥和一个可以签署交易但也可以轮换私钥的冷公钥创建一个帐户。然后，该用户可以规定需要2/3的帐户密钥才能签署交易。

为了预防网络钓鱼攻击并提高透明度，钱包可以在用户签名之前使用交易预执行以可读的格式解释交易结果。

Aptos还通过向交易添加到期时间和序列号来加强交易保障。序列号的功能类似于EVM上的随机数（nonces），有助于预防重放攻击。

轻客户端允许人们通过仅下载区块头来轻松验证区块链状态。这最大限度地减少了访问区块链数据时的信任假设。这样做对于像Aptos这样具有更高节点硬件要求的高性能区块链来说尤其重要。

**可升级性**

![eZgwC6U8F8uvo9J2o7Y1YRavqBYxa7hsuHD5RyKN.jpeg](https://img.jinse.cn/7159787_watermarknone.png "7159787")

Aptos的设计支持频繁的协议升级。这在很大程度上是因为验证器管理是在链上，允许验证器轻松同步到新的升级。Aptos自身的一部分也是用Move语言编写的，这可以缩短上市时间，如上所述。自发布以来，Aptos已实施了约46项优化建议。

## 4、代币经济学

### （1）概述

Aptos的原生代币APT用于安全保障和抗Sybil攻击（验证器和委托者质押）、资源消耗（交易费）和链上治理。最初，10亿APT被分配到具有不同锁定期的几个篮子中。APT没有固定供应量，目前的年通胀率为6.895%。所有的交易费目前都被burn掉了。

### （2）初始分发

![bYff5jtYVbxLtEdPj4FEOiYG6Y0IHg6UvHxwpSeF.jpeg](https://img.jinse.cn/7159791_watermarknone.png "7159791")如前所述，最初只分发了10亿代币。另外，有13%的代币在一开始就未锁定，其余代币按分发时间表分发。具体分配如下：

- 生态系统（占初始总供应量的51.02%）：APT初始分配中的最大份额面向生态系统开发。这些代币中约有四分之一在创世阶段解锁，其余部分在接下来的10年里每月线性解锁。在分发之前，这些代币中约有80%由Aptos基金会持有，其余由Aptos Labs持有。创世阶段的APT空投从生态系统这个篮子中向超11万名参与者分发了2000多万代币。
    
- 团队（占初始总供应量的19%）：这些代币分发给了Aptos Labs，按照如下的四年分发时间表分发：一年锁定期，未来6个月内每月解锁6.25%，然后在未来30个月内每月解锁2.083%。请注意，如果Aptos Labs员工在创世后加入，他们仍将受同样的为期四年的分发时间表约束。
    
- 基金会（占初始总供应量的16.5%）：这些代币被分配给Aptos基金会，其中3%（500万代币）在创始阶段分发，其余的代币与分发给团队的代币一样，按照四年的分发时间表分发。该基金会计划使用这些代币举办活动，援助法律支持以及赞助研究。除其他计划外，基金会还将支付帮助验证节点运营商和推进更分散的验证节点地理分布的运营费用。
    
- 私募投资者（占初始代币供应量的13.48%）：这些代币将分发给Aptos Labs公司的私募投资者，他们选择购买代币，并遵守与团队和基金会代币分发相同的四年期分发时间表。
    

![bhTRqzTZlKWVvtcmcxe06z2FEjzim4WawwNjtzZV.jpeg](https://img.jinse.cn/7159792_watermarknone.png "7159792")如上所述，随着质押者获得持续回报，APT通胀。在创世后的第一年，年通胀率设定为7%，随后每年下降1.5%（即第二年为6.895%），直到稳定在3.25%。请注意，这个比率是基于10亿APT的初始总供应量设定的，并受治理影响。

APT初始分发的解锁时间表旨在避免重大解锁事件。APT流动性供应的最剧烈增长将出现在2023年11月中旬至2024年4月中旬的六个月解锁期。这段期间开始为团队和私募投资者解锁代币。在此期间，初始分发（即不包括押注奖励）的流动性代币供应量将增加约60%，从2.09亿增加到3.34亿。

锁定的代币可用于质押并获得流动性奖励。由于协议内委托直到4月中旬才启动，空投接受者和其他较小的代币持有者在主网上线的前六个月被稀释，除非他们自我协调，汇集超过100万代币。

## 5、网络活动

### （1）使用率

![WgHdL7f4G9OhLIksdllD8Bm9ehcUCYgRJdw1DKIw.jpeg](https://img.jinse.cn/7159793_watermarknone.png "7159793")在网络发布后的兴奋过后，网络使用率（以交易和活跃地址衡量）下降，直到2023年7月才有所回升。从那时起，Aptos平均每天处理超475,000笔交易，日活地址超过72,000个。促使使用率上升有几个因素，包括社交媒体平台Chingari和oracle Pyth的集成。

Chingari是一款视频分享手机应用，类似于TikTok，在Google Play Store的下载量超过1亿次。它最初于2018年作为一个Web2平台发布，后来增加了虚拟礼物等链上功能。

Pyth于7月13日与Aptos集成，带来其低延迟的价格feeds。自7月13日以来，Pyth已占Aptos总交易量的17.7%左右。请注意，这样的交易量规模对于Pyth所在的网络来说并不少见。

10月19日，在Graffio公共艺术创作活动的推动下，日活地址突破了60万。为了庆祝网络上线一周年，Aptos贡献者邀请社区成员在公共数字画布上涂鸦，为期24小时。每个单独的画作都被注册为一笔链上交易。然后，参与者收到了最终画布的NFT版本。该活动带来了60.5万个唯一地址和130万笔交易。

Graffio带来的活动增长导致网络中断，区块生产于10月18日停止。该事件在大约5小时内得到了解决。Aptos基金会在10月20日公布了一份报告，确定该事件根本原因在于非确定性代码，源于2023年8月22日对Aptos核心代码库进行的侧重性能的代码更改。

最近的交易活动是由铭文驱动的，这是许多区块链上的普遍趋势。NFT市场BlueMove在12月中旬推出了APT20标准。12月23日和24日，共有680万笔交易，主要是因为APT20铸造。

### （2）安全和去中心化

截至2023年12月26日，Aptos网络拥有来自27个国家和54个城市的123个活跃验证者。自网络发布以来，验证者的数量逐渐增加，最初的验证者数量大约为100个。验证者网络目前的中本系数（Nakamoto coefficient）为18，高于其他网络的中位数。由于Aptos基金会持有代币总供应量的大部分，可以帮助在验证者之间相当公平地分配权益。

共有9.07亿质押APT（截至2023年12月26日价值为98亿美元），占APT总供应量的84.6%。如上所述，锁定的代币可用于质押并获得流动性奖励。相对于其流通供应量来说，有296%的代币出于质押状态。10月5日，Coinbase Cloud向其验证者进行了APT授权，并在Coinbase Prime上增加了APT质押。

## 6、生态系统

### （1）DeFi

![xqeqv8sa0qgmK9N52L14WuPtqDfgTiWYSFDG6413.jpeg](https://img.jinse.cn/7159794_watermarknone.png "7159794")在问世一年多的时间里，Aptos DeFi协议已经从32个协议中积累了近1.27亿美元的TVL，在所有网络的TVL中排名第26位。Aptos的DeFi TVL主要来自五个协议：Thala Labs、Liquidswap、Aries Markets、PancakeSwap和SushiSwap。

Thala以4300万美元的TVL位于Aptos协议主导地位，占有45%的市场份额。Thala提供了一套DeFi产品，包括一个CDP、一个AMM、一个流动性质押协议和一个代币发行平台。Thala目前还在开发治理工具Parliament。它在22年第四季度的种子轮融资中筹集了600万美元，在23年3月底推出了治理代币THL，之后不久上线主网。其CDP铸造Move Dollar（MOD），截至2023年12月26日，流动代币共有830万枚。MOD和THL都是全链可替代代币（OFTs）。OFT是由LayerZero Labs创建的多链代币标准，可与可替代代币标准跨链互操作。MOD的大部分超额抵押支持都是基于LayerZero以及基于Wormhole的USDC。

就在第三季度末，Thala宣布与Aptos基金会合作成立DeFi孵化器Thala Foundry。Foundry获得了100万美元的初始资金，并将向Aptos DeFi项目分配5万至25万美元的资金，以及其他开发人员和业务开发支持。

LiquidSwap是最早在Aptos上运行的AMM之一。它是由Pontem Network开发的，该公司还为Aptos开发了Pontem钱包。它拥有2000万美元的TVL，占21%的市场份额。

Aries市场是一个借贷和保证金交易协议。它在Aptos主网发布不久后发布，于最近呈现出TVL的显著增长，2023年10月份TVL从不到200万美元跃升至1100多万美元。去年12月份的增长使Aries的TVL达到近2000万美元，占据了20%的市场份额。此前11月底，Aries推出了由Econia支持的交易产品。

Econia是一个链上订单簿引擎，在2021年首届Aptos黑客马拉松期间成形，于11月底推出。今年早些时候，它在Dragonfly领投的一笔融资中获得了650万美元的种子资金。除了Aries，Econia的基础设施目前还支持Kana Trade、Gator Trade（由Pontem开发）、SwapGPT和Hippo Labs上的交易。

BNB Chain的顶级DeFi协议PancakeSwap在Aptos上推出了AMM。从2022年底到2023年7月中旬，PancakeSwap是TVL最高的Aptos协议。然而，它现在位居第四，占6%的市场份额。

11月下旬，SushiSwap在Aptos上发布了V2 AMM，使Aptos成为SushiSwap支持的第一个非EVM。到目前为止，SushiSwap已经拥有近500万美元的TVL，占据5%的市场份额。

由于不质押的成本约为7%的稀释，因此流动性质押协议对于继续发展Aptos的DeFi生态系统至关重要。10月下旬，流动性质押协议Amnis Finance发布。它现在是Aptos上TVL领先的流动性质押协议，TVL近3300万美元，领先于Thala的2300万美元TVL的流动性质押协议。为了激励增长，Amnis推出了一个积分计划，将用于针对其即将发行代币的空投。

其他项目和集成还有：

- Merkle Trade：Merkle Trade是一个10月底推出的perp DEX。自推出以来，Merkle Trade的总交易量已超过2.77亿美元。
    
- Oasis Pro：11月中旬，Oasis Pro在FINRA（美国金融业监管局）注册的市场与Aptos集成。
    

### （2）消费者

**社交**

如上所述，Chingari是Aptos上从交易量和活跃地址来看最受欢迎的应用之一。其他正在运行或即将推出的社交应用还有TowneSquare和Overmind。

TowneSquare于2023年8月公开了建设计划。它正在建设一个与链上活动和身份验证系统相集成的移动应用，以支持链上社交feed、票务、白名单、联盟营销等用例。

Overmind是首个侧重Quests（任务）的平台：开发者可以在该平台上竞争编码挑战和奖励，以获得奖励和链上凭证。Overmind与Aptos基金会合作，通过其任务为开发者提供了大约5万美元的奖励。10月中旬，它开放了对其开源、去中心化的社交网络的早期访问，并在不久之后推出了“Race to Keys”计划，鼓励开发者建立friend.tech风格的密钥功能。

**游戏**

游戏一直是Aptos Labs和Foundation关注的另一个核心消费者领域。二月底，Aptos Labs发布了一个用于在Unity上进行开发建设的游戏软件开发工具包（SDK），Unity是最受欢迎的游戏引擎之一。Aptos Labs还正在开发一个可验证的链上随机性模块，这是游戏和其他应用的一个关键方面。AIP-41提议创建一个新的Move模块，使开发人员能够轻松地在他们的智能合约中添加链上随机性。一旦实施，将计划举办一个完全专注于使用链上随机性构建的黑客马拉松活动。

尽管许多游戏仍处于开发阶段，但也有一些游戏已经上线。十月底，街机风格射击游戏Aptos Arena发布，首周奖金超过1万美元。它在第一个周末就吸引了超过1.2万个地址，并正在根据初始玩家的反馈进行更新。

Aptos Labs和Aptos基金会与几家知名游戏公司和企业集团建立了合作关系，包括：

- NPIXEL：NPIXEL是一家韩国AAA级游戏公司。它在2022年第四季度与Aptos Labs建立合作，将其METAPIXEL游戏引入Aptos网络，于2023年第三季度结束了即将推出的游戏Gran Saga Unlimited的第二次试玩。
    
- NEOWIZ：NEOWIZ是一家韩国游戏开发和发行公司。Aptos基金会于八月中旬与NEOWIZ及其Web3子公司Intella X合作。
    
- MARBLEX：MARBLEX是Netmarble的Web3子公司，Netmarble是韩国最大的手游公司。MARBLEX在八月底与Aptos基金会合作，开发了MARBLEX WARP Bridge，并将其多链游戏与Aptos集成。该桥将连接Aptos与MARBLEX现有的生态系统，包括其MBX代币和游戏NFT。
    
- 乐天集团：乐天集团是韩国最大的零售企业集团之一。乐天集团在八月底与Aptos基金会建立合作关系，将其子公司大洪通信的Bellyland引入Aptos。
    
- Readygg：Readygg是一家基础设施公司，旨在将Web2玩家带到Web3世界。它与Web2游戏发行商合作，帮助他们的游戏与Web3集成。通过Aptos的努力，Minijuegos、ToroFun、CimuGames和Aeria Canada等四家发行商计划在今年年底之前与Aptos进行整合。
    
- BlockGames：BlockGames正在打造一个跨链、跨游戏的游戏和玩家网络。它最近宣布了与Aptos集成的计划。
    
- GuardianLink：Aptos Labs与GuardianLink合作，整合其Jump.trade NFT市场，用户可访问Meta板球联盟NFT游戏。
    

### NFT

自推出以来，NFT的交易量约为1940万美元，大部分活动集中在推出后不久。其中超过74%的交易量通过Topaz市场完成。自8月1日发布以来，Wapal占据了15%的交易量，而Topaz的交易量市场份额则为50%。Wapal是一个面向“专业交易员”的NFT市场，类似于Blur和Tensor，使用积分系统来激励活动，并将用于空投。Wapal最credentials近推出了一个无代码NFT发行平台。

自12月10日APT20标准推出以来，NFT交易量有所增加。BlueMove占据了41%的NFT交易量，总交易量为67.4万美元。

Aptos上的NFT还应用于若干现实用例。KYD Labs是一家Web3票务公司。它为一些现场活动提供票务服务，包括WonderBus音乐节和韩国区块链周闭幕活动SEOULBOUND。Aptos Labs曾两次与NBCUniversal合作，为电影Renfield和The Exorcist: Believer推出数字粉丝体验。在11月初，Aptos基金会与韩国游乐园和媒体集团Seoul Land合作。Seoul Land的数字化子公司RXMeta将在Aptos上发布一项名为Bloom的节日新体验，由NFT票务和会员资格提供支持。

8月底，Aptos Labs推出了Aptos数字资产标准（DA）。DA专注于NFT，具有动态NFT、灵魂绑定代币、较低的gas成本、赋予NFT拥有其他NFT的能力、简化的空投支持等功能。

## 7、路线图

### （1）技术优化

如上所述，Aptos旨在支持频繁升级。为了测试和突出几项正在进行的升级，Aptos Labs最近发布了Previewnet的研究结果，Previewnet是一个被设计为模拟Aptos主网的测试环境。从11月6日到21日，该环境支持了超90亿笔交易，其中有20亿笔交易发生在24小时内。每秒点对点交易峰值达到了30,000次，并且超过100万个NFT限量收藏是在90秒内铸造完成的。

解锁这种更高性能的主要升级之一是存储分片，即将状态存储分割为多个RocksDB实例。存储分片计划于2024年上线主网。另外还对执行引擎、状态同步算法和网络堆栈进行了改进，Aptos Labs将在以后进行详细介绍。

优化的NFT铸造性能来自于一个名为Aggregators的新解决方案。一直以来，限量供应的NFT铸造需要顺序执行，因为它们是按顺序命名的（例如，“Cryptopunk #4317”）。Aggregators是一种新颖的、无冲突的计数机制，可以实现限量供应的NFT铸造的并行执行。Aptos Labs最近发布了一篇详细介绍Aggregators的博文。

Aptos Labs接下来的目标是在实现超过100万TPS的旅程中首先实现10万TPS的阶段性目标。除了在Previewnet中测试的改进之外，另一个正在开发中的重大升级是一种新的共识机制Shoal。Shoal结合了DAG和BFT的特性，降低延迟的同时提高了吞吐量。

最后，Aptos Labs正在开发一个新的Aptos Move编译器，引入了一系列新的语言特性，旨在简化编码过程并扩展功能。其中包括接收器（receiver）样式的函数调用、一级高阶函数和用户定义的能力。Aptos Labs预计将在2024年上半年实现大部分新功能。

### （2）增长战略

为了发展Aptos生态系统，Aptos基金会举办了黑客马拉松活动并启动了资助计划。Aptos Labs和Aptos基金会还与许多合作伙伴建立了合作关系。除了这两家实体之外，还有其他团体也在进行增长活动，例如总部位于印度的开发者社区Move Developers DAO（MDD）。总的来说，许多增长努力都集中在亚太地区。

除了生态系统部分提到的合作伙伴关系，Aptos还与以下主要合作伙伴建立了合作关系：

- 微软：8月初，Aptos Labs宣布与微软合作。该合作将把微软Azure AI功能带入Aptos，首先是Aptos助手，一个旨在帮助用户和开发者登陆Aptos的聊天机器人。GitHub的Copilot功能也将支持Aptos Move。
    
- 谷歌云：Aptos Labs与谷歌云合作实施了多项计划和整合，例如谷歌云运行Aptos验证器以及为BigQuery索引Aptos数据，提供APT和谷歌云积分的加速器计划，以及共同举办黑客马拉松活动，等等。
    
- 阿里云：11月下旬，Aptos基金会与阿里云合作，发展亚太地区的Web3开发者社区。Aptos基金会成为阿里云新加坡创新加速器计划的主要区块链赞助商，计划在亚洲共同推出Move开发者社区，并共同举办一系列黑客马拉松活动及其他活动。
    
- SK电信：11月初，Aptos Labs与SK电信及其技术合作伙伴Atomrigs Labs合作，计划开发一项名为T钱包的Web3钱包服务。Aptos是SK电信的首个非EVM合作伙伴。
    
- Flowcarbon：9月中旬，Aptos基金会与Flowcarbon合作，将Aptos打造成一个负碳（carbon-negative）区块链。Aptos基金会将购买并注销由Flowcarbon代币化的碳积分。
    
- Coinbase Pay：9月中旬，Aptos Labs与Coinbase Pay合作，将Coinbase的法币入金功能整合到Aptos Labs开发的钱包Petra中。6月，Petra移动钱包在Google Play和苹果应用商店推出。10月底，它与硬件钱包Ledger集成。
    

黑客马拉松和资助计划如下：

- Aptos世界巡回黑客马拉松：2023年，Aptos基金会在首尔、荷兰和新加坡举办了黑客马拉松大赛，并计划在年底前再举办一届。这三届黑客马拉松大赛的奖金总额超过76万美元。
    
- Aptos资助计划：Aptos基金会在2022年主网上线之前宣布了Aptos资助计划。到2023年5月初，基金会宣布已向50个团队资助超过350万美元，并开放了第二轮申请。
    
- 艺术家资助计划：2022年4月，Aptos基金会推出了一项2000万美元的艺术家和创作者资助计划。
    
- 注册表资助计划：7月中旬，Aptos基金会发布了注册表资助计划。注册表列出了一些项目创意，最初包括主要与游戏和Move基础设施相关的七个项目。这七个项目的申请已经截止，项目已处于开发阶段。基金会计划定期增加新项目。
    
- Outlier Ventures加速器：8月初，Outlier Ventures宣布与Aptos基金会合作推出Move加速器。这个为期12周的项目于10月初结束，随后在当月举行了demo活动。
    
- Move开发者DAO（MDD）：MDD协助举办了几次黑客马拉松大赛和其他活动，最近的活动有Indore区块链日、Pune区块链日和REVA HACK。
    
- ABCDE Highlight：亚洲Web3风投和加速器工作室ABCDE Highlight与Aptos基金会合作推出一个面向亚洲的资助计划，促进社区粘性。
    
- Aptos冬季学校：Aptos基金会将在12月下旬举办一场为期两周的印度学生开发者加速器活动。
    
- Galxe任务：12月初，Aptos基金会宣布了一个为期四周的基于Galxe的链上任务活动。
    

## 8、结论

Aptos是一个L1区块链，围绕可扩展性、安全性、可靠性和可升级性的核心原则设计。Aptos诞生于Meta的Diem和Novi项目，于2022年10月发布。Aptos的技术栈具有许多创新之处，例如AptosBFTv4共识机制、Quorum Store内存池协议、Block-STM并行执行引擎和编程语言Aptos Move。

自2023年7月以来，Aptos平均每天处理超过475,000笔交易，日活地址超过72,000个。网络活动主要由社交媒体平台Chingari、oracle Pyth以及在Graffio上为期一天的公共艺术创作活动推动。发展生态系统的计划包括建立合作伙伴关系、黑客马拉松大赛、资助计划等，其中许多计划面向亚太地区。

![jinse.cn](data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiPz4KPHN2ZyB3aWR0aD0iMjVweCIgaGVpZ2h0PSIyNHB4IiB2aWV3Qm94PSIwIDAgMjUgMjQiIHZlcnNpb249IjEuMSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB4bWxuczp4bGluaz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94bGluayI+CiAgICA8IS0tIEdlbmVyYXRvcjogU2tldGNoIDYyICg5MTM5MCkgLSBodHRwczovL3NrZXRjaC5jb20gLS0+CiAgICA8dGl0bGU+5b2i54q257uT5ZCIQDN4PC90aXRsZT4KICAgIDxkZXNjPkNyZWF0ZWQgd2l0aCBTa2V0Y2guPC9kZXNjPgogICAgPGcgaWQ9Iumhtemdoi0xIiBzdHJva2U9Im5vbmUiIHN0cm9rZS13aWR0aD0iMSIgZmlsbD0ibm9uZSIgZmlsbC1ydWxlPSJldmVub2RkIj4KICAgICAgICA8ZyBpZD0iV0VCLeaWh+eroCIgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTQ5Mi4wMDAwMDAsIC0xODQ2LjAwMDAwMCkiIGZpbGw9IiNDN0M3Q0QiIGZpbGwtcnVsZT0ibm9uemVybyI+CiAgICAgICAgICAgIDxnIGlkPSLnvJbnu4QtNSIgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoNDQ0LjAwMDAwMCwgMTgzMi4wMDAwMDApIj4KICAgICAgICAgICAgICAgIDxwYXRoIGQ9Ik02NS45MDkwOTA5LDE0IEw2NC41NjE2NjIzLDIxLjYzNTQyODYgTDczLDIxLjYzNjM2MzYgTDcwLjI3MjcyNzMsMzggTDU0LjQ1NDU0NTUsMzggTDU0LjQ1NDU0NTUsMzcuOTk5IEw1NC41NDI4NTcxLDM4IEw1NC41NDI4NTcxLDIxLjYzNjM2MzYgTDU0LjQ1NDU0NTUsMjEuNjM2MzYzNiBMNTQuODcyNTE5NSwyMS42MzU0Mjg2IEw1OS4zNjM2MzY0LDE0IEw2NS45MDkwOTA5LDE0IFogTTUyLjU0Mjg1NzEsMjEuNjM2MzYzNiBMNTIuNTQyODU3MSwzOCBMNDgsMzggTDQ4LDIxLjYzNjM2MzYgTDUyLjU0Mjg1NzEsMjEuNjM2MzYzNiBaIiBpZD0i5b2i54q257uT5ZCIIj48L3BhdGg+CiAgICAgICAgICAgIDwvZz4KICAgICAgICA8L2c+CiAgICA8L2c+Cjwvc3ZnPg==)18

好文章，需要你的鼓励

参与评论

0/140

提交评论

声明：本文系金色财经原创稿件，版权属金色财经所有，未经授权不得转载，已经协议授权的媒体下载使用时须注明"稿件来源：金色财经"，违者将依法追究责任。

提示：投资有风险，入市须谨慎。本资讯不作为投资理财建议。
