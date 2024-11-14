---
title: zkLedger：分布式账本的隐私保护审计
assets:
  - https://www.usenix.org/system/files/conference/nsdi18/nsdi18-narula.pdf
  - https://www.usenix.org/sites/default/files/conference/protected-files/nsdi18_slides_narula.pdf
draft: true
---
# zkLedger: Privacy-Preserving Auditing for Distributed Ledgers  
zkLedger：分布式账本的隐私保护审计

Authors:  作者：

Neha Narula, _MIT Media Lab;_ Willy Vasquez, _University of Texas at Austin;_ Madars Virza, _MIT Media Lab_  
_麻省理工学院媒体实验室_的 Neha Narula;_德克萨斯大学奥斯汀分校_的 Willy Vasquez;Madars Virza，_麻省理工学院媒体实验室_

Abstract:  抽象：

Distributed ledgers (e.g. blockchains) enable financial institutions to efficiently reconcile cross-organization transactions. For example, banks might use a distributed ledger as a settlement log for digital assets. Unfortunately, these ledgers are either entirely public to all participants, revealing sensitive strategy and trading information, or are private but do not support third-party auditing without revealing the contents of transactions to the auditor. Auditing and financial oversight are critical to proving institutions are complying with regulation.  
分布式账本（例如区块链）使金融机构能够有效地核对跨组织交易。例如，银行可能会使用分布式账本作为数字资产的结算日志。不幸的是，这些账本要么对所有参与者完全公开，泄露敏感的策略和交易信息，要么是私有的，但不支持第三方审计，而不向审计师透露交易内容。审计和财务监督对于证明机构遵守法规至关重要。

This paper presents zkLedger, the first system to protect ledger participants’ privacy and provide fast, provably correct auditing. Banks create digital asset transactions that are visible only to the organizations party to the transaction, but are publicly verifiable. An auditor sends queries to banks, for example “What is the outstanding amount of a certain digital asset on your balance sheet?” and gets a response and cryptographic assurance that the response is correct. zkLedger has two important benefits over previous work. First, zkLedger provides fast, rich auditing with a new proof scheme using Schnorr-type non-interactive zero-knowledge proofs. Unlike zk-SNARKs, our techniques do not require trusted setup and only rely on widely-used cryptographic assumptions. Second, zkLedger provides _completeness_; it uses a columnar ledger construction so that banks cannot hide transactions from the auditor, and participants can use rolling caches to produce and verify answers quickly. We implement a distributed version of zkLedger that can produce provably correct answers to auditor queries on a ledger with a hundred thousand transactions in less than 10 milliseconds.  
本文介绍了 zkLedger，这是第一个保护账本参与者隐私并提供快速、可证明正确的审计的系统。银行创建的数字资产交易仅对交易的组织方可见，但可公开验证。审计师向银行发送查询，例如“您的资产负债表上某个数字资产的未偿金额是多少”，并获得响应和加密保证，证明响应是正确的。与以前的工作相比，zkLedger 有两个重要的好处。首先，zkLedger 使用 Schnorr 类型的非交互式零知识证明，通过新的证明方案提供快速、丰富的审计。与 zk-SNARK 不同，我们的技术不需要可信设置，只依赖于广泛使用的加密假设。其次，zkLedger 提供了_完整性_;它使用列式账本结构，因此银行无法向审计师隐藏交易，并且参与者可以使用滚动缓存快速生成和验证答案。我们实现了 zkLedger 的分布式版本，它可以在不到 10 毫秒的时间内为拥有 10 万笔交易的账本上的审计员查询生成可证明的正确答案。

NSDI '18 Open Access Videos Sponsored by  
NSDI '18 开放获取视频赞助  
King Abdullah University of Science and Technology (KAUST)   
阿卜杜拉国王科技大学 （KAUST）

## Open Access Media 开放获取媒体

USENIX is committed to Open Access to the research presented at our events. Papers and proceedings are freely available to everyone once the event begins. Any video, audio, and/or slides that are posted after the event are also free and open to everyone. [Support USENIX](https://www.usenix.org/annual-fund) and our commitment to Open Access.  
USENIX 致力于开放获取我们活动中展示的研究成果。活动开始后，每个人都可以免费获得论文和会议记录。活动结束后发布的任何视频、音频和/或幻灯片也是免费的，对所有人开放。[支持 USENIX](https://www.usenix.org/annual-fund) 和我们对开放获取的承诺。

BibTeX 比布TeX

[Narula PDF 纳鲁拉 PDF](https://www.usenix.org/system/files/conference/nsdi18/nsdi18-narula.pdf "nsdi18-narula.pdf")

[View the slides 查看幻灯片](https://www.usenix.org/sites/default/files/conference/protected-files/nsdi18_slides_narula.pdf)

## Presentation Video  演示视频
