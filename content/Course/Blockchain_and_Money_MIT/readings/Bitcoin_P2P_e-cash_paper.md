---
title: 比特币 P2P 电子现金
link: https://www.metzdowd.com/pipermail/cryptography/2008-October/014810.html
draft: true
---
# Bitcoin P2P e-cash paper 比特币 P2P 电子现金

**Satoshi Nakamoto 中本聪** [satoshi at vistomail.com  Satoshi 在 vistomail.com](mailto:cryptography%40metzdowd.com?Subject=Re%3A%20Bitcoin%20P2P%20e-cash%20paper&In-Reply-To=%3CCHILKAT-MID-dd013ecc-8c7f-fc14-b1c5-cc9fd0181098%40server123%3E "Bitcoin P2P e-cash paper")  
_Fri Oct 31 14:10:00 EDT 2008  
2008 年 10 月 31 日星期五 14：10：00 EDT_

- Previous message: [Fw: SHA-3 lounge](https://www.metzdowd.com/pipermail/cryptography/2008-October/014808.html)上一条消息： [Fw： SHA-3 lounge](https://www.metzdowd.com/pipermail/cryptography/2008-October/014808.html) 
- **Messages sorted by:** [[ date ]](https://www.metzdowd.com/pipermail/cryptography/2008-October/date.html#14810) [[ thread ]](https://www.metzdowd.com/pipermail/cryptography/2008-October/thread.html#14810) [[ subject ]](https://www.metzdowd.com/pipermail/cryptography/2008-October/subject.html#14810) [[ author ]](https://www.metzdowd.com/pipermail/cryptography/2008-October/author.html#14810)  
    **邮件排序方式：**[[ 日期 ]](https://www.metzdowd.com/pipermail/cryptography/2008-October/date.html#14810)[[ 线程 ]](https://www.metzdowd.com/pipermail/cryptography/2008-October/thread.html#14810)[[ 主题 ]](https://www.metzdowd.com/pipermail/cryptography/2008-October/subject.html#14810)[[ 作者 ]](https://www.metzdowd.com/pipermail/cryptography/2008-October/author.html#14810)

---

I've been working on a new electronic cash system that's fully
peer-to-peer, with no trusted third party.  
我一直在开发一种新的电子现金系统，该系统完全
点对点，没有受信任的第三方。  
  
The paper is available at:
[http://www.bitcoin.org/bitcoin.pdf](http://www.bitcoin.org/bitcoin.pdf)  
论文可在以下网址获得：
[http://www.bitcoin.org/bitcoin.pdf](http://www.bitcoin.org/bitcoin.pdf)  
  
The main properties:
 Double-spending is prevented with a peer-to-peer network.
 No mint or other trusted parties.
 Participants can be anonymous.
 New coins are made from Hashcash style proof-of-work.
 The proof-of-work for new coin generation also powers the
    network to prevent double-spending.  
主要特性：
点对点网络可以防止双花。
没有铸币厂或其他受信任的方。
参与者可以是匿名的。
新硬币由 Hashcash 风格的工作量证明制成。
新硬币生成的工作量证明也为
网络以防止双重支出。  
  
Bitcoin: A Peer-to-Peer Electronic Cash System  
比特币：点对点电子现金系统  
  
Abstract.  A purely peer-to-peer version of electronic cash would
allow online payments to be sent directly from one party to another
without the burdens of going through a financial institution.
Digital signatures provide part of the solution, but the main
benefits are lost if a trusted party is still required to prevent
double-spending.  We propose a solution to the double-spending
problem using a peer-to-peer network.  The network timestamps
transactions by hashing them into an ongoing chain of hash-based
proof-of-work, forming a record that cannot be changed without
redoing the proof-of-work.  The longest chain not only serves as
proof of the sequence of events witnessed, but proof that it came
from the largest pool of CPU power.  As long as honest nodes control
the most CPU power on the network, they can generate the longest
chain and outpace any attackers.  The network itself requires
minimal structure.  Messages are broadcasted on a best effort basis,
and nodes can leave and rejoin the network at will, accepting the
longest proof-of-work chain as proof of what happened while they
were gone.  
抽象。 纯粹的点对点版本的电子现金将
允许在线支付直接从一方发送到另一方
无需通过金融机构的负担。
数字签名提供了解决方案的一部分，但主要的
如果仍然需要受信任的一方来防止
双花。 我们提出了一个解决双花的方法
使用对等网络时出现问题。 网络时间戳
通过将交易散列到一个持续的基于哈希的链中
工作量证明，形成一个没有
重做工作量证明。 最长的链条不仅用作
见证了事件顺序的证据，但证明了它来了
来自最大的 CPU 能力池。 只要诚实的节点控制
网络上的 CPU 功率最大，它们可以产生最长的
并超越任何攻击者。 网络本身需要
最小结构。 消息会尽最大努力进行广播，
节点可以随意离开和重新加入网络，接受
最长的工作量证明链，以证明他们
都消失了。  
  
Full paper at:
[http://www.bitcoin.org/bitcoin.pdf](http://www.bitcoin.org/bitcoin.pdf)  
全文见：
[http://www.bitcoin.org/bitcoin.pdf](http://www.bitcoin.org/bitcoin.pdf)  
  
Satoshi Nakamoto 中本聪  
  
---------------------------------------------------------------------
The Cryptography Mailing List
Unsubscribe by sending "unsubscribe cryptography" to [majordomo at metzdowd.com](http://www.metzdowd.com/mailman/listinfo/cryptography)  
---------------------------------------------------------------------
密码学邮件列表
通过在 [metzdowd.com 向 majordomo](http://www.metzdowd.com/mailman/listinfo/cryptography) 发送“unsubscribe cryptography”来取消订阅  
  

---

- Previous message: [Fw: SHA-3 lounge](https://www.metzdowd.com/pipermail/cryptography/2008-October/014808.html)上一条消息： [Fw： SHA-3 lounge](https://www.metzdowd.com/pipermail/cryptography/2008-October/014808.html) 
- **Messages sorted by:** [[ date ]](https://www.metzdowd.com/pipermail/cryptography/2008-October/date.html#14810) [[ thread ]](https://www.metzdowd.com/pipermail/cryptography/2008-October/thread.html#14810) [[ subject ]](https://www.metzdowd.com/pipermail/cryptography/2008-October/subject.html#14810) [[ author ]](https://www.metzdowd.com/pipermail/cryptography/2008-October/author.html#14810)  
    **邮件排序方式：**[[ 日期 ]](https://www.metzdowd.com/pipermail/cryptography/2008-October/date.html#14810)[[ 线程 ]](https://www.metzdowd.com/pipermail/cryptography/2008-October/thread.html#14810)[[ 主题 ]](https://www.metzdowd.com/pipermail/cryptography/2008-October/subject.html#14810)[[ 作者 ]](https://www.metzdowd.com/pipermail/cryptography/2008-October/author.html#14810)

---

[More information about the cryptography mailing list  
有关密码学邮件列表的更多信息](http://www.metzdowd.com/mailman/listinfo/cryptography)