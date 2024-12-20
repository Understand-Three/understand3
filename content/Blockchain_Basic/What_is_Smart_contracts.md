---
title: 智能合约是什么？
aliases:
  - 智能合约是什么？
draft: false
date: 2024-11-17
---
>[!NOTE] 
>自动售货机是现实中的“智能合约”

# 智能合约的定义

智能合约（smart contract）实际上并不是人工智能（artificial intelligence）的“智能”。智能合约是基于区块链技术的一种自动化程序。它的“智能”更多地体现在能够在预设条件满足时自动执行合约条款，而不是指人工智能那种具备学习、推理和决策能力的智能。

智能合约是一个自动执行的程序，可自动执行区块链交易中所需的操作。一旦完成，交易是可跟踪且不可逆的。设想智能合约的最佳方式是考虑自动售货机——当您投入正确金额并按下物品的按钮时，程序（智能合约）会激活机器来分配您选择的物品。


智能合约是区块链上的防篡改程序，其逻辑如下：“如果/当 x 事件发生时，则执行 y 操作。一个智能合约可以有多个不同的条件，一个应用程序可以有多个不同的智能合约来支持一组相互关联的流程。还有多种用于编程的智能合约语言，其中以太坊的 [Solidity](https://docs.soliditylang.org/en/v0.8.7/) 是最受欢迎的。

任何开发人员都可以创建一个智能合约并将其部署在公共区块链上以达到自己的目的，例如，一个个人收益聚合器，它会自动将他们的资金转移到收入最高的应用程序。然而，许多智能合约涉及多个独立的各方，这些各方可能彼此认识，也可能不认识，并且不一定相互信任。智能合约准确定义了用户如何与它交互，包括谁可以在什么时间与智能合约交互，以及哪些输入会产生哪些输出。结果是多方数字协议从今天的概率状态（它们可能会根据需要执行）演变为新的确定性状态，在这种状态中，它们可以保证根据其代码执行。

但是，并非所有区块链都可以运行智能合约。虽然包括 Arbitrum、Avalanche、Base、BNB Chain 和以太坊在内的区块链和第 2 层网络是智能合约兼容区块链的例子，但像基础比特币区块链这样的区块链不具备原生智能合约功能。这些区块链之间的主要区别在于底层区块链执行和存储任意逻辑的能力。

智能合约由美国计算机科学家 Nick Szabo 于 1994 年首次创造。在他的[开创性著作](https://www.fon.hum.uva.nl/rob/Courses/InformationInSpeech/CDROM/Literature/LOTwinterschool2006/szabo.best.vwh.net/smart.contracts.html)中，他给出了一个广泛的智能合约定义，如下所示：“_执行合同条款的计算机化交易协议”，_其总体目标是“_满足常见的合同条件，最大限度地减少恶意和意外的异常，并最大限度地减少对可信中介的需求”。_

虽然在自动售货机等系统（例如，特定代码会导致预期的零食）中可以看到智能合约的一般概念，但区块链构成了数字化、防篡改和无需许可的智能合约的基础。2009 年比特币区块链的推出可以说支持了第一个**协议智能合约**——建立了一组必须满足的条件，才能在网络上的用户之间转移比特币。这些条件包括用户使用与其公共地址匹配的正确[私钥](https://www.investopedia.com/terms/p/private-key.asp)（类似于链接到特定账户的密码）签署交易，以及用户拥有足够的资金来支付交易。

在接下来的几年里，区块链开始通过添加新的编程条件（称为操作代码或[操作码](https://academy.bit2me.com/en/what-is-an-op-code/)）进行实验。然而，智能合约的下一个重大飞跃是在 2013 年 Vitalik Buterin 发布[以太坊白皮书](https://ethereum.org/en/whitepaper/)时。2015 年，以太坊作为**一种用于可编程智能合约**的新型区块链推出。以太坊智能合约区块链不是有效地充当单个智能合约应用程序或提供一些有限的操作码，而是提供了一个可以同时运行许多独立智能合约的“世界计算机”。

智能合约无疑为世界提供了一种更安全、更可验证的方式来创建涉及价值和数据转移的社会协议。然而，区块链和智能合约的前景仍处于起步阶段，开发人员在寻求构建可验证 Web 的愿景时必须面对各种限制。

# 智能合约的好处

大多数传统的数字协议涉及彼此不认识的两方，这带来了任何一方无法履行承诺的风险。为了解决交易对手风险，数字协议通常由可以执行合同条款的大型中心化机构（如银行）托管和执行。这些数字合同可以直接在用户和大公司之间签订，也可以涉及大公司充当两个用户之间的可信中介。虽然这种动态允许存在许多合约，否则这些合约不会承担这种风险，但它也造成了一种情况，即更大的中心化机构对合约施加不对称的影响。


能合约通过提供多项优势来改进数字协议。  
- **安全性**：在去中心化的区块链基础设施上运行合约可确保没有中心故障点进行攻击，没有中心化的中介进行贿赂，也没有供任何一方或中央管理员用来篡改结果的机制。  

- **可靠性**：由去中心化的节点网络对合约逻辑进行冗余处理和验证，可提供强大的防篡改、正常运行时间和正确性，从而保证合约将根据其条款按时执行。  
- **公平** – 使用去中心化网络来托管和执行协议条款会降低营利性中间商利用其特权地位寻租和吸取价值的能力。  
- **效率** – 协议后端流程（托管、维护、执行和/或结算）的自动化意味着任何一方都不必等待手动输入数据、交易对方履行义务或中间人处理交易。

# 智能合约限制

智能合约开发的一个标志性限制是其不可变性：智能合约代码一旦创建就无法更改。这既可以被视为一项强大的功能，也可以被视为一个基本限制：只要不可变应用程序运行的区块链处于活动状态，它就会自动运行，但它们不能升级以获得新的特性、功能、错误修复或扩展。这凸显了智能合约的另一个限制和风险——部署了未发现的错误或漏洞的智能合约无法及时更改（有时甚至根本无法更改），这使得[智能合约审计](https://blog.chain.link/how-to-audit-smart-contract/)成为智能合约开发过程的核心部分。

许多开发人员用来克服此限制的一种解决方法是创建[可升级的智能合约](https://blog.chain.link/upgradable-smart-contracts/)，其中代理合约用于指向新的、更新的智能合约。这不会破坏智能合约的不变性，而是解锁了将用户引导至新的、升级的智能合约的能力。


# 智能合约和链下资源

区块链是隔离的网络，这意味着区块链没有与外界的内置连接。如果没有[外部连接](https://chain.link/education-hub/off-chain-data)，智能合约就无法与外部系统通信以确认真实世界事件的发生，也无法访问具有成本效益的计算资源。与没有 Internet 的计算机类似，如果没有实际连接，智能合约将受到极大的限制。例如，他们无法在执行交易之前知道资产的价格，无法在支付农作物保险索赔之前查看月平均降雨量，并且无法在与供应商结算之前验证货物是否已到达。

因此，区块链行业正在进行的重大演变是可编程智能合约，它与现实世界的数据和区块链之外的传统系统连接，从而扩展了智能合约逻辑中使用的输入和输出。这些[混合型智能合约](https://chain.link/education-hub/hybrid-smart-contracts)使用 Chainlink 将链上代码与链下基础设施相结合，例如，使用外部数据触发智能合约，或在传统支付轨道上链下结算合约。

# 智能合约审计

智能合约审计是对智能合约代码的详细分析，以先发制人地识别安全漏洞并找到防止恶意行为者利用的解决方案，并消除低效的编码做法。

智能合约审计在整个 [DeFi](https://chain.link/education/defi) 生态系统中用于提供对协议代码的深入审查，帮助识别错误、低效代码和这些问题的解决方案。[智能合约](https://chain.link/education/smart-contracts)的防篡改性至关重要，这使得审计成为任何区块链项目[安全流程](https://blog.chain.link/defi-security-best-practices/)的关键部分。

代码审计对任何应用程序都很重要，但对于去中心化应用程序 （dApp） 尤其重要，因为它们构建的区块链是不可变的。如果代码漏洞导致用户资金损失，则无法找回这些资金。迄今为止，DeFi 中的黑客攻击已损失[超过 $5B](https://defillama.com/hacks)。


# 参考

什么是区块链上的智能合约，它们如何运作？[investopedia.com](https://www.investopedia.com/terms/s/smart-contracts.asp)

智能合约：[liaoxuefeng.com](https://liaoxuefeng.com/books/blockchain/ethereum/smart-contract/)

什么是智能合约，它们如何运作？[chain.link](https://chain.link/education/smart-contracts)

如何审计智能合约：[chain.link](https://chain.link/education-hub/how-to-audit-smart-contract)

如何审计智能合约：深入了解 Hacken 的流程：[hacken.io](https://hacken.io/discover/smart-contract-audit-process/)

【论文阅读・SmartContract】Making Smart Contracts Smarter：[nexisato.github.io](https://nexisato.github.io/2021/07/16/paper-20210716/index.html)

什么是智能合约：[learnblockchain.cn](https://learnblockchain.cn/article/8319)

ZEUS：分析智能合约的安全性（论文）：[sukritkalra.github.io](https://sukritkalra.github.io/data/papers/zeus.pdf)

智能合约：[obyte.org](https://obyte.org/platform/smart-contracts)

一文看懂智能合约的现状与未来：[infoq.cn](https://www.infoq.cn/article/smart-contracts-the-path-to-mainstream-adoption)
