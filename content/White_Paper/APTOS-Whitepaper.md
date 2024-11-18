---
title: APTOS 白皮书
draft: true
aliases:
  - aptos 白皮书
date: 2024-06-12
description: aptos 中文版白皮书，最新翻译，通俗版
tags:
  - whitepaper
cssclasses:
  - "1"
---
```yaml
original: 
  Aptos: "https://aptosfoundation.org/whitepaper/aptos-whitepaper_en.pdf"
  BuilderDao: "https://buidlerdao.notion.site/Aptos-Web3-fa04fe55b4364594ad0ee20e429cb3f6"
  simons: "https://github.com/caoyang2002/aptos_tutorial_quartz/blob/main/content/白皮书/APTOS-白皮书.md"
note: 这个版本是我翻译的，已校对
```

# 一、摘要

随着区块链作为一种新型互联网基础设施的崛起，开发者们正以迅猛的速度部署着数以万计的去中心化应用。然而，由于频繁的中断、高昂的成本、有限的吞吐量以及众多的安全问题，区块链的应用尚未普及。为了在 Web3 时代实现大规模使用，区块链基础设施需要像云基础设施一样，成为一个值得信赖、可扩展、经济高效且持续优化的平台，以构建能够被广泛使用的应用。

我们提出的 Aptos 区块链，以可扩展、安全、可靠和可升级作为核心原则，旨在解决这些问题。Aptos 区块链在过去三年中由全球350多名开发者共同开发[^1]。它在共识机制、智能合约设计、系统安全、性能和去中心化方面提供了新颖的创新。这些技术的结合将提供一个基础设施 —— 将Web3 带给大众：[^a]

- 首先，Aptos 区块链原生集成并使用 **Move 语言**，以实现快速且安全的方式执行交易[^2]。**Move 验证者**（Move prover），一个用 Move 语言编写的智能合约的形式化验证工具，为合约的稳定和行为（invariants and behavior）提供了额外的安全保障。这种注重安全的做法使得开发者能够更好地保护其软件，以免遭受恶意实体（malicious entities）的攻击。 

- 第二，Aptos 数据模型支持灵活的密钥管理和混合托管选项。这与交易签署前的透明性以及实用的轻量级客户端协议相结合，提供了一个更安全、更值得信赖的用户体验。 

- 第三，为了实现高吞吐量和低延迟，Aptos 区块链采用了流水线化和模块化的方法来处理交易的关键阶段。具体来说，交易传播（transaction dissemination）、区块元数据排序、并行交易执行、批量存储和账本认证都同时进行。这种方法充分利用了所有可用的物理资源，提高了硬件效率，并实现了高水平地并行执行。 
- 第四，不同于其他并行执行引擎需要预先了解要读取和写入的数据，Aptos 区块链不会对开发者施加这样的限制，这意它能够高效地支持具有任意复杂性的交易的原子性，为现实世界的应用实现更高的吞吐量和更低的延迟，并简化了开发工作。
- 第五，Aptos 的模块化架构设计能够支持更灵活的客户端，并对频繁升级和即时升级进行了优化。此外，为了快速部署新的创新的技术并支持新的 Web3 应用场景，Aptos 区块链提供了内置的链上变更管理协议。
- 总的来说，Aptos 区块链正探索新的发展道路，目标是实现比之前更强大的性能：其采用的模块化设计和并行处理机制不仅让一个验证节点能够更加高效地处理数据，还通过一种被称为"同质状态分片（homogeneous state sharding）"的技术，无需增加操作的复杂度，就能显著提升系统处理交易的能力。简而言之，这种技术让 Aptos 区块链的处理速度能够水平扩展，即随着节点数量的增加，其处理速度也会相应提升。

[^a]: 法律免责声明：本白皮书及其内容不是出售任何代币的要约，也不是诱导购买任何代币的要约。 我们发布这份白皮书只是为了接受公众的反馈和意见。 本文件中的任何内容都不应被理解为对 Aptos 区块链或其代币（若有）将如何发展、利用或累积价值的保证或承诺。 Aptos 仅概述了其目前的计划，这些计划可能会酌情改变，其成功与否将取决于其控制之外的许多因素。 这种未来的陈述必然涉及已知和未知的风险，这可能导致未来时期的实际表现和结果与我们在本白皮书中描述或暗示的有重大差异。 Aptos 不承担更新其计划的义务。 不能保证白皮书中的任何陈述将被证明是准确的，因为实际结果和未来事件可能有很大的不同。 请不要过分依赖未来的声明。



# 一、序言

在 Web2 的互联网时代，像消息通信、社交网络、金融、游戏、购物以及音视频流媒体这些服务，都是由拥有对用户数据直接控制权的中心化公司（如 Google、Amazon、Apple 和 Meta）提供的。这些公司开发了专门优化过的应用软件，以针对特定的应用场景，并且通过云基础架构将这些应用提供给用户。云基础架构允许对虚拟和物理的基础服务进行访问，比如租用的虚拟机和遍布全球数据中心的物理服务器（例如 AWS、Azure 和 Google Cloud）。这样一来，开发一个能为数十亿用户服务的 Web2 互联网服务变得前所未有地容易。然而，在 Web2 的模式下，用户需要明确地信任那些中心化的企业，这一点越来越引起社会的担忧。

为了解决这一信任问题，互联网步入了一个新的时代：web3 时代。在 web3 版本的互联网中，区块链技术以其去中心化、不可更改的账本特性，让用户之间的交互变得更加安全可靠，而且不再需要依赖于任何中介或中心化实体。正如 web2 互联网服务和应用依靠云基础设施作为基础构件，去中心化应用也可以将区块链作为基础设施层来使用，从而触及全球数十亿用户。

然而，尽管现已存在许多条区块链，但是 Web3 尚未得到广泛采纳[3]。 虽然技术不断地推动着行业发展，但现有的区块链仍是不可靠的。昂贵的交易费用，低吞吐量，因安全问题资产经常遭受损失，并且无法支持实时响应。 与云端基础设施赋能 Web2 服务，成功触达数十亿人群相比，区块链还并没有使得 Web3 应用达到同样的高度。

然而，尽管目前有很多区块链技术，但 web3 的广泛应用仍然未能实现[^3]。即使科技正不断推动该行业发展，现有的区块链还是存在问题 —— 不够可靠、让用户负担沉重的高交易费用、处理能力有限、安全漏洞导致的资产损失时有发生，而且还不支持即时反应。云基础设施能够支持 web2 服务触达数十亿用户，而区块链在 web3 应用方面还未能达到这样的规模。



# 二、Aptos 的愿景

Aptos 的目标是建立一种区块链，让 web3 能够接纳主流用户，并且建立一个去中心化的应用生态，旨在解决用户的实际问题。我们致力于通过开发一个既灵活又模块化的架构来推动区块链技术在可靠性、安全性和性能上的长足发展。这个架构设计能够支持频繁升级，迅速融入最新的创新技术，并且提供对新兴应用场景的一流支持。

我们预见未来的网络将是去中心化、安全、可扩展的，并由其用户社区来治理和运营。随着全球基础设施需求的增长，区块链将通过水平和垂直扩展其计算资源来满足这些需求。每当出现新的应用情景或技术突破时，区块链网络都能够频繁且无缝地进行更新升级，而无需打断用户的操作。基础设施相关的问题将会变得不那么突出。开发者和用户能够选用各种不同的密钥恢复（key recovery）、数据模型（data modeling）、智能合约标准（smart contract standards），同时在资源消耗、隐私保护及模块组合上进行权衡。用户对此感到放心，因为他们的资产是安全的，随时可用，并且交易费用极低。任何人都可以安全、便捷、固定地与全球的不认识的人进行交易。区块链技术将会变得如同今天的云基础设施一样普遍。



为了实现这一愿景，必须在技术方面取得重大进展。 过去三年里，我们开发，升级和部署 Diem 区块链（Aptos 区块链的前身）的经验已经证明，网络可以在不中断客户端的情况下持续升级协议[4]。 2020 年初，Diem 主网被部署到拥有多个钱包供应商的十几个节点上。 在之后一年，我们团队进行了共识协议和核心框架两次重大的升级。 两次升级都在用户不停机的情况下顺利完成。 在 Aptos 区块链中，我们对技术栈进行了一系列彻底的改进，同时还受 Diem 区块链启发将安全、透明、以及可频繁的升级作为核心功能。 我们特别强调新的交易处理方法（如第 7 节所述）以及去中心化和网络治理的新方法。



为了实现这个愿景，我们必须突破重要的技术难关。我们在 Diem 区块链（即 Aptos 区块链的前身）的构建、开发与部署过程中积累的三年经验证明了区块链网络可以不断升级其协议，且不会干扰客户端[^4]。2020年初，Diem 主网已经被部署在了超过十几个节点运营商和多家钱包提供商。在随后的一年里，我们完成了两项重大升级，升级包括共识协议和核心框架，并且都没有对用户造成任何中断。在 Aptos 区块链的开发中，我们在保持技术栈不断创新的同时，也将安全、透明和定期升级作为其核心特性，这一点受到了 Diem 的启发。特别值得一提的是，我们提出了交易处理的创新方法（详见[第七节](#七流水化批量并行的交易处理)）和去中心化与网络治理的新方向。

![[Aptos 生态系统的组件.png]]
图1：Aptos 生态系统的组件

随着Aptos区块链的不断发展与成熟，我们会推出白皮书的升级版，展示我们最新的协议和设计决策。文档剩余部分将介绍 Aptos 区块链目前的状态和未来的规划。

# 三、概述

正如图 1 所示，Aptos 区块链由一组核心 **验证者（Validator）**构成，这些验证者运用拜占庭容错（Byzantine Fault Tolerant，**BFT**）和权益证明（Proof of Stake，**PoS**）共识机制来共同接收和处理用户交易。Token 持有者会把 Token 质押给他们信任的验证者，而验证者的共识投票权重与质押给它的 Token 数量成正比。一个验证者可能是活跃的，参与到共识过程中；但某些验证者也可能处于非活跃状态，例如质押的 Token 不足、从验证者集合中被轮换出去、在同步区块链状态时离线，或者因为历史表现不佳被共识协议拒绝其参与，

在系统中，任何需要提交交易或者查询区块链状态及历史的任何参与者（any part）都可以称为 **客户端**。客户端有权选择下载并核实验证者签署的查询到的数据的证明（proofs）。全节点（**Full Node**）作为客户端的一种，会复制验证者或其他全节点的交易信息和区块链状态。全节点还可以按需清理交易历史记录和区块链数据，从而节省存储空间。轻量客户端（Light clients）仅保留当前验证者的信息，且能够安全地查询部分区块链状态——这通常通过全节点来完成。而钱包就是轻量客户端的一个典型代表。

Aptos区块链为了满足大规模应用中对安全、高速、可靠及可升级 web3 基础设施的要求，构建了基于一系列的核心设计原则：

- 通过引入全新的智能合约编程语言 Move [^5]，Aptos 区块链不仅可以实现高速且安全的执行链上逻辑，还能够轻松地进行审计和代码分析。Move 这一语言最早是为 Aptos 的前代区块链平台  Diem  所设计，并随着 Aptos 项目的演进而不断优化。
- Aptos区块链通过批量处理、数据流水线和并行处理等方式使交易处理达到极高的吞吐量和极低的延迟。
- 独创性的并行交易处理技术 Block-STM 高效地保证了即便交易极其复杂，也能实现交易原子性，这与那些需要提前了解读写数据位置的并行执行引擎不同。
- 进一步地，为了提升性能和实现更彻底的去中心化，Aptos 采取了基于权益质押的验证者集合轮换和声誉跟踪策略。
- 同时，系统可升级性和可配置性是其核心的设计原则，目的是支持不断涌现的新应用场景和前沿技术。
- 此外，Aptos还采用模块化的设计，不仅能够确保每个组件都经历严格的测试，还能进行合理的威胁模拟和无间断部署，保障了系统运作的安全性和可靠性。
- 在保持去中心化特性的同时，系统还在横向吞吐量上具备良好的可扩展性，并且将分片（sharding）技术作为一个重要功能，不仅对用户完全开放，而且天生就融入了编程和数据模型中。

[第四节](#四move-编程语言)阐述了开发者在 Aptos 区块链中如何利用 Move 语言进行交互操作。[第五节](#五逻辑模型)则深入到逻辑数据模型的细节。在[第六节](#六安全的用户体验)中，Aptos 区块链通过采用强大的验证方法，确保了用户体验的安全性。接着，[第七节](#七流水化批量并行的交易处理)探讨了通过流水线、批量处理及并行处理实现的性能上的关键性创新。[第八节](#八状态同步)给出了不同客户端如何与其他节点同步状态的各种选项。[第九节](#九社区治理)展示了我们关于促进社区所有权与加强治理结构的计划。最后，在[第十节](#十性能表现)中，我们讨论了如何在保持去中心化的基础上展望未来的性能提升方向。



# 四、Move 编程语言



Move 是一种新颖的智能合约编程语言，它强调安全性和灵活性。在 Aptos 区块链中，Move 的对象模型被用来表示其账本状态（参见[第 5.5 节](#55账本状态)），而 Move 代码（模块）则用于定义状态转换的规则。用户可以提交交易，这些交易能够发布新的模块、升级已有的模块、执行在模块内部定义的入口函数，或执行脚本来直接与模块的公共接口互动。

Move 生态系统包含了编译器、虚拟机以及众多的开发工具。Move 的设计灵感来源于 Rust 编程语言，后者通过线性类型（linear types）等概念在语言层面清晰界定了数据所有权。Move 特别强调资源的稀有性、持久性和访问控制。Move 的模块设定了每种资源的生命周期、存储方式和访问模式，从而确保了资源如 Coin 不会在无正当授权时被制造，避免资源的重复使用，并确保其不会凭空消失。

哪怕面临不可信代码的存在，Move 也能通过运用字节码验证器来保障类型和内存的安全性。Move 还包含一个名为 Move Prover[^6] 的形式验证器，它可以帮助开发者编写更为可靠的代码。Move Prover 是用来确认 Move 程序相对于特定规约功能性的正确性，而这些规约则是用 Move 内置的规约语言形式来提出的。

在用户账户及其内容的基础之上，分布式账本状态还涵盖了 Aptos 区块链的链上配置。这些网络配置内容广泛，从活跃的验证者集合、质押属性到 Aptos 区块链中多种服务的具体配置。得益于 Move 在模块可升级性和编程能力方面的强大支持，无需停机即可轻松实现配置的变更和对 Aptos 区块链本身的升级，这些升级在私有的主网络上已经无中断地执行了多次。

Aptos 团队通过拓展 Move，进一步加强了对广泛 Web3 应用场景的支持。如[5.5节](#55账本状态)所述，Aptos 区块链提供了精细的资源控制功能。这不只促进了执行任务的并行化，还保证了存取与修改数据的成本几乎是固定的。更重要的是，借助精细的存储机制，Aptos 区块链还能在单个账户中支持海量数据集（比如，大量 NFT 的集合）。另外，Aptos 区块链支持的共享或自主账户完全在线上表示，使得复杂的去中心化自治组织（DAO）能够协作共享账户，或作为装载各类资源集合的容器。



# 五、逻辑数据模型

Aptos 区块链上的 **账本状态** 反映了所有账户当前的情况。这个状态通过一个无符号的 64 位数值进行版本标记，该数值等同于系统已执行的交易数目。任何人均可向 Aptos 区块链提交交易请求，从而修改账本状态。交易被执行后，将生成 **交易输出**。一个交易的输出包含零个或多个操作来操纵账本状态（称为 _write sets_），一个产生事件结果的向量（详见[第5.1.1节](#511事件)），消耗的 gas 数量及交易执行的最终状态。



## 5.1 交易

每个已签名的交易都包含几个重要信息部分：

- **交易验证器**：发送方使用的交易验证器内含至少一个数字签名，用来确认交易是由合法发送方发起的。
- **发送方地址**：这是发起交易者在区块链上的账户地址。
- **负载**：包含执行交易所需执行的函数指令。这些指令可以是链接到已有链上函数的引用，也可以是被嵌入需要直接执行的字节码（一种被称作脚本的指令集）。此外，负载还包含了一系列被编码成字节阵列格式的输入参数。像点到点的款项转移这样的交易，会在输入参数中包含收款方的信息和转账金额。
- **Gas 价格（以指定货币或 Gas 单位计）**：这是发送方执行交易愿意支付的每个 Gas 单位的价格。Gas 在区块链上是执行计算、数据传输和储存所耗费的资源的度量单位。 
- **最大 Gas 量**：事务在被终止前所允许消耗的最大 Gas 单位。账户中必须有足够的资金来支付最大 Gas 量乘以 Gas 价格的费用，否则交易在初步验证阶段就会被拒绝。
- **序列号**：这是交易的编号。在交易执行时，此编号必须与发送方账户里记录的序列号对应。一旦交易成功执行，账户内的序列号会增加，以防止交易内容被复制并重复使用（重放攻击，Replay attack）。
- **过期时间**：交易有效期的终止时间戳，超过这个时间点，该交易将失效。
- **区块链 ID**：识别区块链中的交易有效性，为用户提供一层额外的保护，防止因签名错误而导致的安全问题。

在每一版本 $i$ 中，对账本状态的改变分别用一个三元组 $(T_i, O_i, S_i)$ 来描述，其中包括了交易本身 $(T_i)$、交易的结果输出 $(O_i)$ 以及改变之后的账本状态 $(S_i)$ 。通过一个名为 $Apply$ 的特定函数，我们可以将之前的账本状态 $(S_{i−1})$ 和当前交易 $(T_i)$ 相结合，从而产生一个新的交易输出 $(O_i)$ 和更新后的账本状态 $(S_i)$ 。换句话说，将前一个状态和当前的交易放入 $Apply$ 函数后，我们就可以得到新的交易输出和账本状态，公式表示：$Apply(S_{i−1},T_i)$ 将转换为$(O_i,S_i)$。



### 5.1.1 事件

交易进行的过程中，常常会发出一些标识环节的信息，我们称之为“事件”。每个 Move 模块都可以自定义自己要发出的事件，然后在执行交易的时候决定是否发出这些事件。举个例子，在进行币币转账（during a coin transfer）的时候，转账的发送方和接收方的账户会分别发出名为 "SentEvent"（发送事件）和 "ReceivedEvent"（接受事件）的事件。这些产生的事件信息会保存在区块链的账本中，可以通过 Aptos 节点来查询这些信息。在区块链系统中，每个事件都有一个独一无二的标识符，也就是 “键”（key），我们可以通过这个键来查询某个特定事件的详细信息。

当多个事件被指向同一个 “事件键”（same event key）时，它们就汇聚成一个 “事件流”（event streams）。它是一个日志列表，其中每个记录都包含一个编号（从0开始并依次递增）、事件的类型以及事件相关的具体信息。这种组织方式允许我们轻松跟踪事件的顺序。在定义事件时，每一个都需要指明是哪一类事件。有时，特别是在涉及到泛型编程时，多个事件可能会被同一类别或非常相似的类别定义。事件所携带的数据很关键，对于负责开发 Move 模块的开发者而言，他们的基本任务是确保在交易执行前后，资源发生的变化都能通过事件的数据清晰地传达给阅读者。这样，我们就能全面了解特定交易对系统资源产生的影响与变化。

交易本身仅能发出事件，而不能读取事件。这种设计使交易的执行只能以当前状态和当前交易的输入作为入参，完全独立于任何以往的历史数据，比如之前产生的事件记录。



## 5.2 账户

每个账户都有一个称为“账户地址”的唯一标识，这个地址由 256 位的数字组成。新账户的创建发生在一个已存在账户发送交易并调用一个名为`create_account(addr)`的 Move 函数时，这会在区块链的账本状态下生成一个新的账户记录（见[第 5.5 节](#55账本状态)）。最常见的情况是，当一笔交易试图向一个还没有在系统中创建的地址发送 Aptos Token 时，新账户就会被创建出来。为了简化用户操作，Aptos 平台提供了一个便捷的 `transfer(from, to, amount)` 功能，它在转账的时候如果检测到接收地址还未在账本中创建，就会自动帮你创建一个账户。

![[链上 Move 模块示例.png]]

图 2：链上 Move 模块示例

如果用户想要创建一个新的区块链账户，他们需要先做的就是生成一对密钥，包括一个公钥（vk）和一个私钥（sk）。接着，使用一个特定的签名算法 —— 新账户的地址可以通过对公钥（vk）和签名算法的标识码（ssid）进行加密计算得出，计算公式为 $addr = H(vk, ssid)$。

一旦在某个地址（addr）上创建了新账户，用户就可以利用私钥（sk）对从该账户发出的交易并加以签名。为了安全起见，或者在私钥可能被破解的情况下，用户也能够更换他们的私钥（sk），但这样做不会影响到账户地址。账户地址在创建的时候就已经确定，仅由一次性使用的公钥来生成，因此是不会改变的。

Aptos 区块链并不将账户与现实世界的身份联系起来。 一个用户可以通过生成多个密钥对创建多个账户。 由同一用户控制的账户彼此之间没有内在联系。 然而，为了资产管理的简便化，单个用户仍然可以在一个钱包中管理多个账户 这种灵活性为用户提供了匿名性，同时我们在未来的版本中尝试使用更多隐私保护原语（privacy-preserving primitives）。 如[第 7.4 节](#74并行交易执行)所述，由一个用户或一组用户拥有的多个账户也提供了增加执行并发性的渠道。

Aptos 区块链保证用户的匿名性，不会将任何账户直接关联到现实世界中的个人身份。用户可以通过制作不同的密钥组合，亦即密钥对（公钥和私钥），来创建多个独立的账户。这些账户之间没有内在联系，因此都是它们是独立运作的。尽管如此，用户依旧能够利用单一的数字钱包来同时管理多个账户，这种做法简化了资产管理过程。这种灵活性为用户提供了匿名性（pseudonymity，即用户身份的匿名化），同时我们正在为未来的版本开发中尝试使用保护隐私的基础技术（privacy-preserving primitives，即保护隐私的基本构件或原语）。此外，如[第 7.4 节](#74并行交易执行)所述，无论是单一用户还是多用户共同拥有的多账户系统，都能够提高交易执行的并行处理能力。



## 5.3 Move 模块

Move 模块包含用于定义数据类型（结构）和程序的 Move 字节码。每个模块都有一个独特的标识符，包括了它所在账户的地址和模块名。比如说，在图 2 中的第一个 coin 模块，就被标记为 `0x1::coin`。模块的一个便捷之处在于，它能使用其他已经存在于区块链上的模块，就像图 2 中的钱包模块那样，这允许开发者在不同的项目中复用已有代码。

对于单个区块链账户来说，每个模块的名字必须是唯一的。举个例子，如果账户地址为 `0x1` 的账户已经有一个叫做 `coin` 的模块了，那么它就不能再创建第二个叫做 `coin` 的模块。但是，账户地址为 `0x3` 的账户可以创建一个同样叫做 `coin` 的模块，模块标识符就会是 `0x3::coin`。需要注意的是，`0x1::coin::Coin`  和 `0x3::coin::Coin` 是两种独立的数据类型，它们不能互相替代，也不能共享模块代码。但是，`0x1::coin::Coin<0x2::wallet::USD>` 和 `0x1::coin::Coin<0x2::wallet::JPY>` 则是同一数据类型的不同版本，虽然它们也不能互相替代，但可以共享模块代码。

在相同的区块链地址下，相关的模块会被编排成一个模块包（packages）。地址的所有者将整个模块包作为一个整体发布到区块链上，其中包含了模块包的字节码和元数据。模块包的元数据会规定这个包是可以更新的，还是一旦发布后就无法更改。如果模块包允许更新，在正式更新前，系统会检查更新内容与原有内容的兼容性。例如，不能修改原有的入口函数，并且也不能更改已经在区块链上储存的资源。不过，发布者是可以向模块包中新增额外的功能和资源的。

Aptos 框架由 Aptos 区块链的核心库和配置组成，它被定义为一个可定期（regular）升级的模块包（见[第 9.2 节](#92网络治理)）。

![[链上数据示例.png]]

图3：链上数据示例



## 5.4 资源

与模块类似，账户地址也可以有与之相关的数据值。 在每个账户地址中，数据值是由其类型决定的，每个账户下，每种类型的数据值都应保持唯一。 以图 3 为例， 地址 0x50 持有一个单一值，其中 0x3::coin::Coin 是完全限定的类型。 0x3 是存储 coin 模块的地址，`coin` 是模块的名称， `Coin` 是数据类型的名称。 也可以使用泛型数据值，不同的泛型实例被视为不同的类型。 这对可扩展性至关重要，允许不同的实例共享相同的功能代码。

与模块类似，区块链账户的地址也可以关联具有特定的数据值。在每一个账户地址中，这些数据值是根据它们的类型来标记的，每种类型在账户中只能有一个相对应的值。以图 3 为例，地址 `0x50` 存储了一个特定的值，其类型的完整标记为 `0x3::coin::Coin`。这里，`0x3` 表示 `coin` 模块所处的地址，`coin` 是模块的名称，而 `Coin` 则是该数据的类型名称。也可以使用泛型数据值，不同的泛型实例将被视为不同的类型。这种设计使得区块链系统能够灵活地扩展，让功能相似但不完全相同的实例共用一套代码。

在 Move 编程语言中，像变更、删除和发布某个数据值这样的操作都必须遵循相应的规则 —— 其数据类型所在模块定义的规则。Move 为了确保安全性和正确性，制定了一系列规则，以确保无法直接通过外部代码或其他方式创建、更改或删除在其他模块中已经定义的数据类型。

一个账户地址下面每种类型只能有一个顶级数据值似乎非常受限，但实际上在开发中这并不是一个问题。因为开发者可以通过定义一个包装数据类型，将其他数据作为内部成员变量来实现所需功能，这样就能突破之前提到的限制。而图3展示的 Wallet（钱包）结构体，就是运用这种包装类型技术的典型示例。

还需要特别指出的是，并非所有类型的数据都能存储在区块链上。要想让一个数据实例有资格成为一个顶层的独立值，这类数据类型必须拥有“`key` 能力（key ability）”。而对于那些嵌套在其他数据结构内部的值，它们则需要具有“`store` 能力（store ability）”。具备了这两项能力的数据类型称之为“资源（`resources`）”。



## 5.5 账本状态

从Move虚拟机（Move VM）的角度来看，每一个区块链账户其实就是一些值和“键-值（key - value）”数据结构的集合。这些数据结构，我们称之为“表项（table entries）”，并以二进制规范化序列（Binary Canonical Serialization，BCS）的格式进行存储。这种数据结构的设计，使得开发者在编写智能合约时，无论是进行大量数据在少数账户间的操作，还是少量数据在大量账户间的操作，都能够十分高效。另外，Move 模块的存储方式与账户数据类似，只是它们位于一个独立的命名空间，用以保证数据的独立性不受其他模块数据的影响。同时在区块链系统初始化时，系统会定义一种名为“创世账本状态（genesis ledger state）”的特殊状态，用于确定初始时的账户集合及其相关状态。

在启动时，Aptos 区块链仅表现为一种单一（single）的账本状态。但是随着广泛的使用和技术的进步，Aptos 会增加分片（shards）的数量，这样做的目的是提高系统的处理能力（也就是说，支持多种不同的账本状态），并且支持那些需要在不同分片间转移或存取资产的交易操作。每一种账本状态都会包含特定分片上的所有链上资产，并利用一种精细的“键-值（key - value）”数据存储模型来维护相同的账户模型，这种模型能够以近乎不变的成本来访问存储空间。



# 六、安全的用户体验

为了覆盖数十亿互联网用户，web3 的用户体验需要同时兼顾安全性和易用性。在接下来的几个部分里，我们将介绍 Aptos 区块链带来的几项革命性创新，这些创新正为实现这一目标而不懈努力。

## 6.1 交易可行性保护



在区块链上，当一个人签名确认一笔交易时，就代表他们同意这笔交易在区块链上进行提交和执行（be committed and executed ）。但有时，用户会在不小心或者没有意识到交易会被操控的情况下签署交易。为了减少这样的风险，Aptos 区块链对交易的可行性进行限制，并保护签名者避免陷入无限确认的操作中。目前，Aptos区块链设置了三重保障：发送者的交易序列号、交易的失效时间，以及一个特定的链上标识。

- **交易序列号**：对于每个发送者账户而言，它们的每笔交易都有一个独一无二的序列号，且这个序列号只能被使用一次。因此，如果发送者发现当前账户序列号 ≥ 交易 _t_ 的序列号，那么说明 _t_ 已经被提交，或 _t_ 永远不会被提交（因为 _t_ 使用的序列号已经被另一个交易占用）。
- **交易的失效时间**：区块链的时间非常精确地向前推进，速度非常快（通常为亚秒），如果一笔交易 _t_ 的有效期已过，那么这笔交易要么已经被确认，要么就再也不会被确认了。
- **特定的链上标识**：为了避免不良行为者在不同的区块链环境（比如从测试网到主网）中重复利用相同的交易（replaying），每笔交易都被指定了一个特定的链识别码。



## 6.2 基于 Move 的密钥管理

如[第 5.2 节](#52账户)所述，Aptos 账户提供了密钥更新（key rotation）的功能，这是一项重要的特性，可以降低私钥泄漏，远程攻击以及现有密码算法未来被破解二带来的风险。 此外，Aptos 账户的设计也足够灵活，其允许采用新型的混合托管模型（new hybrid models of custody）。例如，在这种模式下，用户可以将自己账户的密钥更新权利委托给一个或多个指定的保管者或其它信任方。通过使用 Move 模块，可以制定特定的策略让这些信任方在一定条件下对密钥进行更新。举个例子，信任方可能通过一个由多个信任方共同持有的多签密钥（如 k-out-of-n 方案）来表示，并提供密钥恢复服务，以防止用户密钥丢失（比如，目前有约20%的比特币因账户无法恢复而被锁定[^7]）。

另外，许多数字钱包虽然提供了不同的密钥恢复方法，例如把私钥备份到云服务、通过多方计算或者是好友间帮助恢复等方式，但这些通常是在区块链系统之外独立实现的。这意味着每一款钱包都必须建立自己的密钥管理系统，使得这些重要操作对用户缺乏清晰的可见性。与此相反，Aptos  把密钥管理功能内置到区块链系统中，这可以让所有与密钥相关的操作对用户完全透明，同时也简化了带有高级密钥管理功能钱包的开发工作。



## 6.3 通过预签名提升交易透明度

现在，数字钱包对于用户所做的交易签名提供的信息极其有限，这就导致用户经常在不知情的情况下签名了恶意的交易，这些交易有可能窃取他们的资金并带来严重的后果。甚至就算是那些要求交易必须披露所有链上数据的区块链，这个问题依旧存在。目前，钱包为用户提供的保护措施少得可怜，这使用户面临着多种多样的攻击风险。

为应对这一挑战，Aptos 生态系统推出了一项创新服务：**交易预执行**。这是一种预防性措施，它在用户签名之前，用易于理解的方式展示交易的潜在结果。Aptos 将交易的预执行服务与以往已知的攻击和恶意智能合约的信息相结合，将有效地帮助减少被欺诈的风险。除此之外，Aptos 还为钱包增加了一项功能，即在交易执行过程中可以设置特定的限制条件。如果违反这些条件，则交易会自动停止，从而在更大程度上保护用户不受恶意软件或诈骗手段的侵害。





## 6.4 实用的轻量客户端协议

仅仅通过验证 API 提供商的安全证书（TLS/SSL证书）来确认区块链客户端和服务端之间的信任是远远不够的。即便证书是有效的，钱包和客户端也不能完全确定所获得的数据是真实可靠的。因此，存在这样一种风险：API 提供者可能会提供错误或有意编造的区块链数据，这不仅误导第三方，还可能导致重复支付等欺诈行为。

![[交易处理生命周期 所有阶段都是完全独立的并且可以各自并行.png]]

图4：交易处理生命周期 所有阶段都是完全独立的并且可以各自并行

为了防止这种情况发生，Aptos 提供状态证明和轻量客户端（light client）验证协议，钱包和客户端可以使用这些协议来验证由不可信的第三方服务器提供的数据的有效性。 此外，如第 7.6.2 节所述，使用基于时间戳的状态证明，轻客户端可以通过跟踪网络配置中的变化（*epoch变更）*或从当前受信任的节点（*锚点）*同步最新状态[8]，来保证账户状态的实时性（例如，在几秒钟内）。 通过高频时间戳和低成本的状态证明，Aptos 为客户提供了安全的服务。

为预防这些风险，Aptos 推出了状态证明和轻量客户端（light client）验证协议。这些工具使得钱包和客户端能够核实来自不可信第三方服务器的数据是否有效。更进一步，Aptos 区块链运用了[第7.6.2节](#762定期状态认证)提出的基于时间戳的状态证明技术，轻量客户端因此能够非常确信账户信息的实时性（比如说，确保信息是几秒钟之内的），它们只需要监控网络配置的更新，比如网络纪元（epoch）的变化，或从当前的可信校验点（waypoints）同步网络的最新状态[^8]。通过高频的时间戳和低成本的状态证明相结合，Aptos 为用户提供了更强的安全保障。

此外，Aptos 的节点还提供了丰富的高性能存储接口，未来进一步微调这些接口后，使用户能够订阅专门针对特定链上数据和账户的验证信息。这对于轻量客户端非常有利，因为它们可以只保留必要的、能够证实真实性的数据，而不必部署完整的节点或者处理庞大的交易量。



# 七、流水线、批量、并行的交易处理

为了最大限度提高吞吐量，增加并发性，并且降低工程复杂性，Aptos 区块链的交易处理过程被划分为不同的阶段。 每个阶段都是完全独立的并且可以各自并行，类似于现代的超标量处理器架构。 这不仅提供了显著的性能优势，而且让 Aptos 区块链能够提供新的验证者-客户端交互模式。 例如：

为了提升吞吐量，增强并发能力，并简化技术开发的复杂性，Aptos 区块链的交易处理过程被拆分成了几个独立的阶段。这些阶段各自独立，可以并行运作，这一点与现代的超级标量处理器的工作方式相似。这样的设计不仅显著提高了系统性能，而且为 Aptos 区块链带来了验证者与客户端之间进行互动的新方式。例如：

- 当特定的交易被纳入一组已保存的交易时，客户端将得到通知。这些已保存并确认有效的交易一般会被立即提交。

- 当一组已保存的交易被排序后，客户端会被通知。为了尽快了解交易执行的结果，客户端可以选择在本地直接执行这些交易，而不需等待验证节点在远端完成执行。
- 客户端可以选择等待验证者对交易执行进行认证，并在经过认证的结果上执行状态同步（请参阅[第八节](#八状态同步)）。

Aptos 的模块化设计不仅加快了开发进程，还使得产品更新更迅速，因为开发团队现在可以针对特定模块进行更改，而不必对整个庞大的系统结构进行全面调整。而且，模块化的设计理念还为扩展验证器的能力提供了明确的方向，能够跨越单一服务器的局限，有效增加计算能力、网络带宽和储存空间。图 4 展示了交易在不同处理阶段的生命周期。



## 7.1 批量处理

在 Aptos 区块链的每一阶段，批量处理技术都是提高效率不可缺少的一部分。在广播交易阶段，每个验证节点都会把多个交易打包成一组进行处理，而在达成共识的过程中，这些组合将形成区块（blocks）。无论是执行阶段、数据存储阶段，还是账本认证环节，都采用批量的方式工作，这样做可以重新排序、减少一些重复的操作诸如重复计算或重复进行签名验证，同时还可以实现交易的并行处理。

![[区块元数据排序独立于广播交易.png]]

图 5：区块元数据排序独立于广播交易

把交易打包成批次进行处理可能会稍微增加处理时间，比如说，需要等待 200 毫秒才能收集足够多的交易进行下一步处理。但是，批次的最大等待时间和大小都是可以调节的，这样一来，去中心化网络就能在延迟和处理效率之间找到一个最佳平衡。此外，批处理机制还促进了构建一个有效的交易费用市场，帮助区分优先级较高的交易，并防止因个别客户端的过度积极导致的拒绝服务（DoS）攻击。



## 7.2 持续的交易广播

顺应 Narwhal & Tusk [^9] 的核心理念，Aptos 区块链将交易的传递与共识过程分开实施（解耦，dissemination）。各个验证节点之间会连续不断地、全速使用网络资源来分批传送交易数据。每一个由验证节点 v 分发出去的数据批次都会被妥善地保存下来，并且会把对这些数据批次摘要，然后进行签名，并将凭证送回给节点 v。按照[第7.3节](#73区块元数据排序)所定义的共识规则，任何至少包含 $2f + 1$ 个有投票权重的签名的批次摘要，都会构成一份可用性证明（PoAv）。有了这份证明，就能确保至少有 $f + 1$ 的权重由诚实的验证器持有，这意味着在真正执行交易前，所有遵守规则的验证器都可以成功地获取这些交易数据。

如果不加限制地存储所有交易的数据，这可能会导致验证节点的存储空间被迅速占满，甚至可能引起宕机，从而导致拒绝服务攻击（DoS攻击）。为此，每一批交易数据都会附带一个时间戳，从而帮助验证节点有效地清理不再需要的数据。同时，以防万一，例如在受到复杂的网络攻击时（例如潜在的拜占庭攻击），系统还为每个验证节点设计了一个特别的空间配额制度，以确保它们的存储空间不会被耗尽。另外，交易数据批次的大小是有限制的，在数据被永久保存前，还必须经过确认。最终，一系列数据处理的优化措施，如冗余交易数据清理的优化和交易缓存，有助于减少存储成本，并确保与并行处理引擎的高性能集成。



## 7.3 区块元数据排序

许多人错误地认为，区块链的处理速度受限于共识的速度。实际上，Aptos 区块链的一项重要创新就是将许多非协议相关的任务分离出来，如交易的传播、执行和存储以及账本的验证等。也就是说，交易数据的传输并不必须在共识过程完成后再进行，这样，即使在低带宽的情况下（只需要元数据和各类证明数据），交易数据也可以有序地进行传输，从而提高交易处理的效率，降低等待延迟。

如今，Aptos 区块链采用了DiemBFTv4 [^10]的最新版，这是一种在共识过程中能够迅速做出反应的拜占庭容错协议。在大多数情况下，达成共识只需要两次网络通信往返（全网往返时间平均小于 300 毫秒），并且这个系统还会根据一个创新的领导者信誉机制[^11]来动态处理那些出现问题的验证节点。链上的领导者信誉系统将根据验证节点在一定时间内（a window）成功处理区块的记录来调整其等级，对表现不佳的节点进行降级。这种独特的设计显著提升了在分散的网络环境中的运行效率，以激励机制鼓励验证节点的积极参与，并且能在短时间内降低无法正常工作的验证节点对系统速度和数据处理量的负面影响。

DiemBFTv 4共识协议在部分同步网络条件下确保了系统的活跃性，并在异步网络条件下保障了系统的安全性。在异步环境下，只要所有验证者的总质押大于或等于 $3f+1$，并且最多不超过 $f$ 个质押权重的故障验证者，系统的安全性就能得到保证。自 2019 年以来，DiemBFTv4 已经经历了多轮的广泛测试，涉及数十个节点运营商和多钱包生态系统。我们还正在尝试将我们的最新研究成果（例如，Bullshark[^12]），以及其他一些利用区块历史记录和通讯数据来确定区块顺序和确立最终结果的协议。

如图 5 所展示的，一个共识块及其对应的提案时间戳是由某个领导节点提出，并得到其他验证节点的同意。值得注意的是，每个共识块仅包括元数据和相应的验证证明。这是因为交易校验与可用性验证 (PoAV) 机制将确保交易批次在区块元数据排序后的执行阶段可用（详情请参见第7.2节）。验证节点可以在核实了验证证明及检查块的元数据符合规定标准后（比如，提出的时间戳不超过块的过期时间），对该领导节点的提案进行投票。





### 7.3.1 区块链时间

Aptos 区块链为每一个提案的区块，以及该区块中的所有交易，分配了一个大致上达成共识的物理时间戳。这个时间戳对于许多关键应用场景至关重要。比如说：

- 智能合约能够实施依赖时间的逻辑控制。比方说，一名开发者可能会编写代码，确保所有在拍卖中的竞标都须在周四中午前提交。
- 随着预言机在链上发布数据，为了将现实世界中的数据事件相关联并处理可能出现的延迟，需要一个准确且可信的链上时间戳。 
- 客户端可以判断自己相对于区块链的最新状态。出于安全考虑，为了避免过时数据和远程攻击，客户端应该能够获取到一个高精度的时间戳，以了解账户状态是何时更新的。
- 使用值得高度信赖的时间戳对区块链进行审计，可以为链下事件提供强有力的关联性，例如确保合法强制要求的支付得到恪守。
- 交易的过期时间建立在最新确认的时间戳基础之上。为增强交易的安全性，客户端可以设定一个交易的到期时间。如[第 6.1 节](#61交易可行性保护)所述。

Aptos 区块链为区块内所有交易的时间戳提供以下保证：

- 区块链中的事件按照严格的时间顺序排列，即时间戳在区块链上是逐渐增加的。简单说，如果我们有两个区块 $B1$ 和 $B2$ ，且 $B1$ 在 $B2$ 之前（$B1 <B2$），则 $B1$ 的时间戳一定比 $B2$ 的时间戳小（$B1.Time < B2.Time$）。
- 如果一个大小为 $f$ 的验证者群体对一个获得时间戳 $T$ 的交易区块达成共识，这就意味着至少有$f+1$ 个诚实的验证者已经认定该时间戳 $T$ 已经过去。诚实的验证者只在其自身系统的时间达到或超过该时间戳 $T$ 时（$own-clock ≥ timestamp-T$），才会对区块投票。参见[第 7.2 节](#72持续的交易广播)。
- 如果一个交易区块在时间戳 $T$ 的情况下获得了足够多的诚实验证者的签名，那么，其他诚实验证者只在他们自己的系统时间等于或超过这个时间戳 $T$ 时（$own-clock ≥ timestamp-T$），才能将这个区块传播给其他验证者。

每个确认提交的区块都会更新最新的时间戳，并且这一时间戳适用于该区块中的所有交易。在网络状态良好、各个节点间信息交互同步时，每完成一次网络通讯的往返，都会提交一个包含交易的区块，从而达到快速更新时间戳并确保其高度的可靠性。如果有必要，我们还可以执行更精细的交易顺序排列，以达到对区块中交易的精确控制。

![[Block-STM（仅该组件）不同竞争程度与不同CPU核数下的基准测试。.png]]

图 6：Block-STM（仅该组件）不同竞争程度与不同CPU核数下的基准测试。



## 7.4 并行交易执行

一旦达成共识并确定区块元数据的顺序后，任何验证者、全节点（Full node）或客户端都有能力执行交易。为了确保交易的一致性和安全性，至少需要有超过一半的节点（具体来说是 $2f + 1$ 个具有投票权重的验证者）确认并保存了这些交易批次。鉴于交易信息是不断在网络中传播的，随着时间的推移，更多的诚实验证者也将逐步接收到这些交易批次。如果某个诚实的验证者在其准备执行交易之际还未接收到相关批次，它可以从那些已经确认交易的验证者（$2f + 1$ 个具有投票权重的验证者）那里下载，这样做的依据是至少有一半以上的验证者（即 $f + 1$ 个具有投票权重的 PoAV 验证者）是可信的。

对于区块链系统来说，能够实现高效的并行处理是其追求的关键目标之一。Aptos 区块链在这方面取得了显著进展，它不仅在数据模型上进行了创新，还在执行引擎方面实现了重大突破，以支持更加高效的并行交易执行。



### 7.4.1 并行数据模型

Move 数据模型原生支持数据和模块的全局寻址。意味着，没有数据和账户冲突的交易可以并行执行。考虑到 Aptos 区块链采用的流水线设计，对一组交易进行重新排序可以减少冲突数量，从而提高并发能力。

即便交易在进行中会对链上的相同数据集进行修改，大多数交易执行步骤依旧可以同时进行。Aptos 区块链推出了一个创新性的概念：“增量式写入(delta writes)”。这一概念关注的是描述账户状态的变更过程，而非单纯地确定变更后的状态（例如，实现一个数值的递增，而不是直接确定其最终值）。所有交易的处理流程都可以并行地执行，之后再应用这些 “增量式写入” 依据冲突值的正确顺序，以此确保结果的一致性和确定性。

随着时间的流逝，Aptos 区块链计划不断完善其数据模型，旨在通过各种方式提升系统处理交易的并行性能（例如，运用读取和写入操作的预提示机制），同时也优化开发体验，让开发者在创建、调整和配置链上数据时更加得心应手。Move 为这种持续创新提供了充分的灵活性，它不仅在编程语言层面上易于扩展，也能够结合 Aptos 平台独有的功能。



### 7.4.2 并行执行引擎

Block-STM 并行执行引擎通过精准地识别和处理按顺序执行的交易集中的冲突，以及采用乐观并发控制策略，旨在针对给定的交易排序情况下达到最高的并行执行效率[^13]。

Block-STM 通过一种称为“乐观并行执行”的机制，允许交易批次同时运行，并在执行完毕后进行验证。如果某个交易未通过验证，它将会被重新执行。为了解决交易过程中的写-写冲突（write-write conflicts）问题，Block-STM 采用了一种多版本数据结构。这意味着，对同一数据位置的所有写操作都会记录下来，同时标记上版本号，这个版本号包括了执行该操作的交易编号和该交易尝试乐观执行的次数。当交易 （tx） 尝试读取特定数据时，它会从这个多版本数据结构中找到在预定顺序中排在它（tx）前面的、具有最高版本号的那个交易写入的数据值，并取用这个数据值。

Block-STM 系统已经被成功地集成到了 Aptos 区块链当中。为了深入探究 Block-STM 在性能上的极致潜力，我们对 Move 语言编写的复杂点对点交易（具体表现为，每个交易包含 8 次读和 5 次写操作）进行了一项专门的执行测试。这次测试仅关注执行效率，并没有包含全链路性能评估，同时采用的是内存式数据库操作。图 6 展现了我们在这项测试中得到的 Block-STM 执行效果。测试中的每个区块包含了 10000 笔交易，而账户数量的变化直接关联到了交易之间的冲突和竞争程度。

当面临低程度的数据操作冲突时，Block-STM 能够在 32 线程的帮助下实现比顺序执行快 16 倍的速度；而在数据操作冲突较高的环境中，其速度提升也能超过 8 倍。与区块链领域中其它并行执行引擎不同，Block-STM 可以自动地、不需任何用户干预地处理并释放任意任务的并行潜力。这一点与那些需要事先了解数据操作位置的并行执行环境相比，Block-STM 能同时处理更加复杂的交易。这种能力不仅减少了交易数量，提高了交易效率，还降低了成本，并使得用户体验到更低的延迟。而最重要的是，把一个无法拆分的完整交易切分为多个小交易，避免了一笔复杂交易失败就整体失败的风险。Block-STM 通过结合灵活的交易定义和并行执行的技术，赋予了开发者在这两方面都取得优势的可能。

需要注意的是，即使在区块元数据进行排序的步骤后，也并不排除在并行执行阶段对交易进行重新排序的可能性。交易在一个或多个区块之间可以被重新排序，以便优化并行执行的时的并行度。唯一的前提是，这种重新排序的过程必须在所有遵守操作规则的验证节点间保持一致。加入更好地优化并行执行，我们可以在重新排序的过程中引入随机性，这不仅可以提升性能，也有可能阻止那些试图通过交易重新排序以实现最大化收益的"矿工可提取价值（MEV）"策略的发生。除此之外，"先排序再透露” 的防止 "MEV" 的策略也可以被融入到这个流水线式设计中。

Block-STM 和交易重新排序是两项可以相辅相成的技术，它们都旨在提高程序执行过程中的并行度。更进一步，这些技术还可以与交易的读/写操作提示相结合，这样就可以进一步拓展程序的并发处理能力。



## 7.5 批量存储

在并行执行阶段，系统会为一组交易创建对应的写入集，这些写入集可以临时存储在内存中，这样做可以极大地提升执行效率，并且这些写入集可以被用作为接下来要执行的区块的缓存使用。此外，任何可能发生重叠的写入操作，只需要实际写入到持久化存储中一次即可。如果验证节点在将写入集存储到内存之前出现故障，它可以从区块元数据排序的阶段重新开始并行执行过程。通过将写入集的储存与并行执行的步骤分开，能够确保并行处理过程运行得更加高效。总的来说，批量处理写入集合能够减少存储操作的频次，并能够更好地利用大型的I/O操作。

可以根据每台机器的需要手动设置为写集缓存预留多少内存空间，这样的配置方式天然就能起到一种控制流量的“回压作用（back - pressure）”。如果有必要为了特别的 I/O 和内存需求进行优化，我们还可以灵活调整批处理的大小。



## 7.6 账本认证

在这一步，每个验证节点都已经计算出了一批已确认交易的最新状态。不过，为了更高效地支持核验过的轻量客户端和状态同步功能，Aptos 区块链特别实施了对账本历史及当前状态的验证程序。Aptos 区块链有一个独到之处，就是这种账本验证过程并不是交易处理的必经之路，如果需要，这个过程甚至可以完全在常规处理流程（out-of-hand）之外进行。



### 7.6.1 账本历史认证

验证节点把交易及其执行结果记录下来，并将这些信息添加到一个全局的、经过身份验证的账本数据结构中。交易结果的一部分是状态写入集，这实际上是对 Move 语言可以访问的全局状态所做修改的记录。这个数据结构的简短验证器事实上是一份对账本历史记录的保证，内含最新执行的一批交易的信息。就像交易执行过程一样，这种数据结构的创建是有有迹可循的。

每个验证者将简短认证签名签署到所产生的数据库的新版本中。 验证者彼此共享他们最近一组简短认证签名，集体汇总法定的简短认证签名，并且还彼此共享最近的法定简短认证签名。

利用这种共同认证的签名，客户端可以放心地认为该数据库的版本准确地反映了一个完整、有效且最终确定无法更改的账本历史，这一点是遵循协议所具备的拜占庭容错（BFT）特性的。客户端可以向任意验证节点（或者任何一个拥有数据库副本的第三方，比如全节点）查询具体的数据库信息，并能够利用相应的认证码以及数据证明来核实查询结果的真实性。



### 7.6.2 定期状态认证

Move 可以访问的全局状态，在历史中的任何时间点都可以被压缩成一个简短的验证标识，这与账本历史的摘要类似。但因为全局状态可随机访问（不像账本历史那样只能添加），所以保持这种验证的代价相当高。即便如此，当我们批量更新数据结构时，可以通过并行处理来计算这些更新，并利用各部分更新之间可能存在的重叠部分。为了减少重复的更新开销，Aptos 区块链选择有意地仅在一定时间周期内对全局状态进行认证。

在预定并设定的时间间隔内，区块链网络会发布状态检查点交易，其特点是包含全局状态的验证标识作为交易结果的一部分。这样的特定版本就被称为 **状态检查点**（state checkpoints.）。两个状态检查点之间的时间间隔越长，每交易在更新状态认证数据结构上的分摊成本就相对越低。 

通过状态检查点，用户可以在不必存储整个全局状态的情况下，以一种无需信赖的方式读取任何状态的值。这种能力对于诸如增量状态同步、验证者间的分片存储、无状态验证节点以及存储空间有限的轻量客户端等应用尤其有用。 

但是，由于状态检查点是定期生成的，要获得特定版本账本状态的有效证明，就需要进行额外的交易执行来处理那些遗漏的状态变化，或者需要一个包含证明来证实这些变更是在经过验证的账本历史的一部分。

状态检查点与账本历史中的具体交易版本有着密切的关系，因此也与第七章节提到处理交易批次相关的时间戳相连。有了这个时间戳，轻量客户端便能了解到某一已验证状态值的时效性。若没有时间戳，轻客户端能证明的只是过去某一时刻的有效状态，且很可能是某一很久以前的状态，这对于状态当前相关性的保证力度会大大减弱。另外，对于追踪历史记录和进行审计，比如计算 token 储备中的平均每小时 token 余额等目的来说，状态证明中的时间戳是必不可少的。

状态检查点可以通过参考前一个状态检查点和之后交易产生的状态变化来生成。因此，将状态检查点保存到稳定的存储设备上并不是处理交易的一个紧迫步骤。此外，在保存状态检查点时，可以通过批量处理方式带来额外好处。把最近的状态检查点（或更确切地说，它们之间的差异）缓存在内存中，而仅把周期性的状态检查点保存到稳定存储中，能显著降低存储带宽的使用率。决定哪些检查点应当被保存的方法不会对认证数据结构的计算产生影响。因此，这取决于每个节点的抉择：节点操作者可以根据自身需求平衡内存容量和存储带宽的使用，进行相应配置。



# 八、状态同步

Aptos 区块链的目标是为其生态系统内的每一位参与者构建一个高吞吐量、低延迟的系统。为了达成这个目标，它需要部署一个高效的状态同步协议来保证区块链数据能够快速传播、验证以及稳定保存到轻量客户端、全节点和验证者 [^14]。此协议还必须考虑网络条件的多样性和资源的有限性，满足不同用户和应用场景的需求。这意味着，协议应当支持存储所有区块链历史信息和状态的存档型全节点，并确保它们的信息得到核实和保存；同时，它还应允许轻客户端只追踪 Aptos 区块链状态中的一小部分，以实现高效利用。

为达成这个目标，Aptos 区块链通过利用验证者、全节点以及其他数据复制器提供的经过认证的账本历史记录和认证的状态证明（详见[第 7.6.1 节](#761账本历史认证)）来支持一个灵活并且可定制的数据同步协议。这意味着，网络的参与者根据自己的特定需求和使用场景，可以自主选择不同的数据同步策略以达到最佳效果。

以全节点为例，Aptos 支持诸多数据同步策略，这些策略既包括从区块链创始之初就开始处理所有交易的方法，也包括完全放弃区块链历史，只通过航标来同步最新的区块链状态。对于轻客户端而言，同步策略可能会局限于区块链的特定部分，如某一特定账户或者数据项，并且确保数据的读取是经过核实的，比如执行账户余额的验证性查询。Aptos 允许所有用户根据自己的需求，设置获取、处理和存储数据的数量和陈旧程度。

Aptos 选择了一种灵活并且可以根据需要进行设置的状态同步方式，这让它能针对不同客户端的需求做出快速调整，并且为将来可能出现的需求提前铺路，以持续开发和推广更新、更加高效的同步策略。



# 九、社区治理

Aptos 区块链预计将归一个既广泛又多样化的社区所有，并由其管理和运作。Aptos 的原生 Token 将用于处理交易费、网络费用、治理投票（例如，决定协议的升级以及审查链上和链下的流程），同时也将利用权益证明模式来保护区块链网络的安全性。对于 Aptos Token 经济系统的全面阐述，我们将在未来作进一步详细说明。



## 9.1 交易和网络费用

Aptos 区块链上的每一笔交易都设有一定的 “Gas 单价”（用 Aptos Token 计价），这一机制使得验证者能根据交易价值的高低来决定其处理优先级。在这种管道处理模式下（pipelined model），低价值的交易在多个阶段都可能被剔除，这样做可以确保即便在系统负荷达到峰值时，区块链也能保持高效运作。随时间推移，通过调整网络费用，Aptos 力图使得在区块链上进行操作的成本能够与硬件部署、维护以及节点运营的实际成本相匹配。此外，Aptos 还为开发者提供了灵活性，允许他们在设计应用时，在计算资源、存储和网络之间做出不同的成本考虑，从而更好地满足特定需求。



## 9.2 网络治理

在 Aptos 区块链上，每项重要的功能更新或优化都必须按照既定流程进行，这包括提出方案、执行实施、进行测试和最终部署等环节。这样的流程设计确保了所有相关方和权益持有者能在各个环节中提供反馈、表达担忧以及提出建议。在部署的最后阶段，通常分为两个步骤：首先将包含新功能的软件版本部署到每个节点上，然后再通过特定方式比如功能开关或者是链上配置参数来正式启用这些功能。

为了确保新部署的软件能与现有版本兼容并协同工作，节点操作者所执行的每次软件更新必须支持向后兼容。部署一个新版本可能需要几天时间来完成，这考虑到了全球不同时区的操作者及可能出现的任何外部困难。一旦有足够多的节点完成了更新，就可以通过一个协调的时间点，比如约定的区块高度或纪元更迭来启动新功能。在发生紧急情况时（比如不得不停机时），节点操作者可能需要手动强制进行更改来应对，此时在极端情况下可能会导致网络产生硬分叉。

相较于其他区块链，Aptos 区块链的一个显著特点是它将配置信息直接嵌入到链上。这意味着每一个验证者都可以同步当前区块链的状态，并根据链上的数据自动挑选出最合适的设置项目（如共识协议和 Aptos 架构版本）。正因为此，Aptos 的升级能够无缝并即刻完成。

为了使启用过程更加灵活可配置，Aptos 实施了链上治理机制，允许代币持有人依据他们的代币投注权重来投票。这种链上投票制度是透明的、可验证的，甚至可以做到即时响应。链上治理不仅限于二选一的决策，无需部署新软件即可实施复杂决策。举个例子，链上领导者选举的协议参数可以经过链上治理进行调整，而依靠预设的同步点则无法适应这样的动态变更，因为必须事先了解所有变动。

随着时间发展，链上治理有望覆盖整个升级管理流程。如下例所示：

1. 代币持有者将通过链上投票决定是否采用一种新的防量子计算签名方案。这种方案旨在保护网络免受未来量子计算技术可能带来的威胁。
2. 开发团队随后着手实现这一方案，并经过严格的验证流程后，发布包含这一新特性的软件版本。
3. 接着，各节点的运营者会将他们操作的软件升级到这个最新版本，以确保整个网络的同步和安全性。
4. 最后，代币持有者再次通过链上投票正式启用这一新的签名方案。

作为一个开源项目，Aptos 区块链深刻认识到社区反馈的重要性，并打算通过链上治理机制来管理各种流程，确保项目的透明度和参与度。虽然在特定情况下，系统可能还需进行离链升级来应对突发状况，但这样的情况随着时间的推进和技术的完善，预计将逐渐减少。





## 9.3 权益质押证明共识

想要在 Aptos 区块链上执行交易验证的验证者，其必须至少持有最低限度的 Aptos Token 作为质押。这些质押额度会按比例影响事务传播以及区块元数据排序过程中的投票权重和领导者选择，具体体现在 $2f + 1$ 的权益加权 PoAv。验证者可以自行决定奖励的分配比例，也就是他们与各自的质押方（stakers）之间如何分配网络奖励。而质押者可以自由选择代表他们投票的验证者数量，并事先与其商定奖励分配比例。每个“纪元”结束后，验证者及其代理的投资者都会通过链上的 Move 模块获得各自的奖励。 

只要抵押额度足够，任何验证者都可以自由地加入 Aptos 区块链。涉及到网络运营的所有参数，包括最低抵押额度，都可以通过我们在[第 9.2 节](#)中的链上启用过程中进行设置。



# 十、性能表现

正如[第七节](#七流水线批量并行的交易处理)中所述，Aptos 区块链依靠其创新的并行架构、为批量处理优化的设计以及模块化的交易处理流水线来保证了高效的处理能力与硬件利用率。此外，一些更为先进的性能提升措施，如共识机制的升级、增量式数据写入、交易预处理提示以及关键数据的缓存方法都在不断被提出并实施，有效地提高了整个系统的处理吞吐量并进一步优化了系统效率。

现如今，人们习惯以每秒处理的交易数量来衡量一个区块链平台的处理能力。然而，鉴于不同的交易与基础架构之间所涉及的复杂度和资源消耗程度相差甚远，这样的衡量方法其实并不精确。同样，我们观察到交易的延迟问题，这主要是因为从交易提交到最终确认的全过程，其实验的起始点和结束点在不同的测试中并不一致，这也使得单凭延迟来评价系统性能存在局限性。

另一方面，一些系统需要提前了解交易的输入和输出，导致必须把复杂的交易拆成简单的多个小交易。这样的拆分行为会损害用户的使用体验，并且不自然地增加了交易的延迟和处理时间，而这并没考虑到开发者真正想要实现的目标。与此不同，Aptos 的设计理念是给予开发者最大的自由度来创造应用，并且通过真实世界的应用场景来评估系统的吞吐量和响应时间，而非仅凭合成的交易数据。 

Aptos 区块链将持续对单个验证者的性能进行优化，并探索通过增加验证者数量来扩展网络的技术。这两个方向各有利弊。任何有能力实行并行处理的区块链，都可以通过提高硬件要求，乃至把每个验证者设计成独立机器的集群，来进一步支持并行处理的需求。然而，全球验证者的数量因为运营成本和管理复杂性的考虑而有其现实的限制。云服务中无服务器数据库的崛起和流行为例，说明了只有少数组织能够高效地部署和管理这些复杂的分布式系统。



## 10.1 同质化的状态分片

在初始阶段，Aptos 区块链将启动一个单一（single）的账目状态。但随着时间的推移，Aptos 网络将以一种独特的方式实现了水平扩展性，同时仍然保持了去中心化特性。这主要通过运用称为“分片（sharded）”的策略在一个单一的账目中创造出多个独立的子账目状态，每个子账目都可以提供一致的 API，并且在其设计中就原生地支持分片策略。同时，Aptos 的 Token 将在所有的子账目中用于交易费用、质押以及治理。

各个子账目之间可以通过一个统一的数据传输链接进行通信，用户和开发者可以根据自身需要自由地选择适合的分片策略。例如，开发者可以提出新的分片或者在现有的分片中对用户进行分组，这样可以实现高效的子账目内部连接。此外，各个子账目也可以针对特殊需求进行优化。比如，某个子账目可能会专注于算力的优化并搭配 SSD 硬盘，而另一个子账目可能会针对大数据量的存储需求进行优化，使用大容量硬盘以及减少算力的需求。通过在不同的子账目间提供硬件配置的灵活性，开发者可以根据自己的应用需求选择最适合的系统配置。

总之，同质状态分片提供了横向吞吐量扩展的潜力，允许开发人员在分片中使用单一的通用状态进行编程，并使钱包能够为其用户轻松纳入分片数据。 这提供了显著的性能优势，以及统一的 Move 智能合约平台的简单性。

总的来说，使用同质化状态分片的技术，我们将具备横向吞吐能力扩展的可能性，它允许开发者在各个分片间统一地使用通用状态进行编程，这种技术也让钱包能够为其用户轻松地整合各种分片数据。这种设计同时带给了我们显著的性能优势，以及一种简单精确的开发方式，即通过单一通用的 Move 智能合约平台进行编程。



# 参考资料

[^1]:“Aptos-core”，2022年。 [查看在线资源](https://github.com/aptos-labs/aptos-core)
[^2]:“Move”，2022年。 [查看在线资源](https://github.com/move-language/move)
[^3]:Matsuoka、C. Dixon、E. Lazzarin和R. Hackett。 (2022) 2022年加密状态报告介绍。[查看在线资源](https://a16z.com/tag/state-of-crypto-2022/)
[^4]:Z. Amsden, R. Arora, S. Bano, M. Baudet, S. Blackshear, A. Bothra, G. Cabrera, C. Catalini, K. Chalkias, E. Cheng, A. Ching, A. Chursin, G. Danezis, G. D. Giacomo, D. L. Dill, H. Ding, N. Doudchenko, V. Gao, Z. Gao, F. Garillot, M. Gorven, P. Hayes, J. M. Hou, Y. Hu, K. Hurley, K. Lewi, C. Li, Z. Li, D. Malkhi, S. Margulis, B. Maurer, P. Mohassel, L. de Naurois, V. Nikolaenko, T. Nowacki, O. Orlov, D. Perelman, A. Pot, B. Proctor, S. Qadeer, Rain, D. Russi, B. Schwab, S. Sezer, A. Sonnino, H. Venter, L. Wei, N. Wernerfelt, B. Williams, Q. Wu, X. Yan, T. Zakian and R. Zhou, “libra 区块链,” 2019。 [查看在线文档](https://developers.diem.com/papers/the-diem-blockchain/2020-05-26.pdf)
[^5]:Blackshear, E. Cheng, D. L. Dill, V. Gao, B. Maurer, T. Nowacki, A. Pott, S. Qadeer, D. R. Rain, S. Sezer, T. Zakian和R. Zhou, “Move: 一种具有可编程资源的语言,” 2019。[查看在线文档](https://developers.diem.com/papers/diem-move-a-language-with-programmable-resources/2019-06-18.pdf)
[^6]:D.Dill, W. Grieskamp, J. Park, S. Qadeer, M. Xu和E. Zhong, “用Move验证器对智能合约进行快速、可靠的形式化验证，“ 发表在 _Tools and Algorithms for the Construction and Analysis of Systems_, D. Fisman and G. Rosu, Eds. Cham: Springer International Publishing, 2022, pp. 183-200。
[^7]:N. Popper. (2021) 丢失的密码将百万富翁们的比特币财富锁住了。 [查看在线文档](https://www.nytimes.com/2021/01/12/technology/bitcoin-passwords-wallets-fortunes.html)
[^8]: Diem小组，“重新配置的系统中状态同步和承诺信息的验证”，2020年。[查看在线文档](https://github.com/aptos-labs/aptos-core/blob/main/documentation/tech-papers/lbft-verification/lbft-verification.pdf)
[^9]: G. Danezis, L. Kokoris-Kogias, A. Sonnino和A. Spiegelman, “独角鲸和獠牙: 基于dag的mempool和高效bft共识,“ 发表于_Proceedings of the Seventeenth European Conference on Computer Systems_, ser. EuroSys ’22. New York, NY, USA: Association for Computing Machinery, 2022, p. 34-50. 查看在线文档](https://doi.org/10.1145/3492321.3519594)
[^10]: Diem小组，“Diembft v4：diem区块链中的状态机复制”，2021年。 [查看在线文档](https://developers.diem.com/papers/diem-consensus-state-machine-replication-in-the-diem-blockchain/2021-08-17.pdf)
[^11]: S. Cohen, R. Gelashvili, L. Kokoris-Kogias, Z. Li, D. Malkhi, A. Sonnino, and A. Spiegelman, “Be known of your leaders,” _CoR_, vol. abs/2110.00960, 2021。[查看在线文档](https://arxiv.org/abs/2110.00960)
[^12]: A. Spiegelman, N. Giridharan, A. Sonnino, and L. Kokoris-Kogias, “Bullshark: Dag bft协议的实用化,” in _Proceedings of the 20th Conference on Computer and Communications Security (CCS)_, ser. CCS [22]。 Los Angeles, CA, USA: Association for Computing Machinery, 2022.
[^13]: R. Gelashvili, A. Spiegelman, Z. Xiang, G. Danezis, Z. Li, Y. Xia, R. Zhou, and D. Malkhi, “Block-stm: 通过将排序的诅咒变成性能的祝福来扩展区块链的执行,” 2022。[查看在线文档](https://arxiv.org/abs/2203.06871)
[^14]: j. Lind, “状态同步的演变: 在aptos实现每秒10万次以上交易、亚秒级延迟的路径,” 2022. [查看在线文档](https://medium.com/aptoslabs/52e25a2c6f10)