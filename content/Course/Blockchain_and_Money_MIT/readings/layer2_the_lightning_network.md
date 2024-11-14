---
title: 2 层｜闪电网络
draft: true
---
# layer 2 | the lightning network  
第 2 层 |闪电网络

## a lightweight software solution for scaling public blockchains and cryptocurrency interoperability  
用于扩展公共区块链和加密货币互操作性的轻量级软件解决方案

The Lightning Network is a decentralized system for instant, high-volume micropayments that removes the risk of delegating custody of funds to trusted third parties. As an example, Bitcoin, the world's most widely used and valuable digital currency, allows anyone to send value without a trusted intermediary or depository. Bitcoin contains an advanced scripting system allowing users to program instructions for funds. There are, however, some drawbacks to Bitcoin's decentralized design. Users must wait tens of minutes or even an hour to have confidence their transactions won't be reversed. Micropayments, or payments less than a few cents, are inconsistently confirmed, and fees render such transactions unviable on the network today. The Lightning Network solves these problems. It is one of the first implementations of a multi-party Smart Contract (programmable money) using Bitcoin's built-in scripting. The lightweight Lightning Network software developed at MIT’s Media Lab (called [lit](https://github.com/mit-dci/lit)) initially focuses on Bitcoin, but it can work on all Bitcoin-like blockchains.  
闪电网络是一个去中心化的系统，用于即时、大批量的小额支付，消除了将资金托管委托给受信任的第三方的风险。例如，比特币是世界上使用最广泛和最有价值的数字货币，它允许任何人在没有受信任的中介或存管的情况下发送价值。比特币包含一个高级脚本系统，允许用户对资金指令进行编程。然而，比特币的去中心化设计也存在一些缺点。用户必须等待数十分钟甚至一个小时才能确信他们的交易不会被撤销。小额支付或少于几美分的付款的确认不一致，费用使此类交易在当今网络上不可行。Lightning Network 解决了这些问题。它是使用比特币内置脚本的多方智能合约（可编程货币）的首批实现之一。麻省理工学院媒体实验室（称为 [lit](https://github.com/mit-dci/lit)）开发的轻量级闪电网络软件最初专注于比特币，但它可以在所有类似比特币的区块链上运行。

### Instant Payments 即时付款

Bitcoin aggregates transactions into blocks spaced ten minutes apart. Payments are widely regarded as secure on Bitcoin after confirmation of six blocks, or about one hour. On the Lightning Network, payments don't need block confirmations, and are instant and atomic. Lightning can be used at retail point-of-sale terminals, with user device-to-device transactions, or anywhere instant payments are needed.  
比特币将交易聚合成间隔 10 分钟的区块。在确认 6 个区块或大约 1 小时后，比特币的付款被广泛认为是安全的。在闪电网络上，支付不需要区块确认，并且是即时和原子的。Lightning 可用于零售销售点终端、用户设备到设备交易或任何需要即时支付的地方。

### Micropayments 小额支付

New markets can be opened with the possibility of micropayments. Lightning enables one to send funds down to 0.00000001 bitcoin (<0.01 cents) without custodial risk. The Bitcoin blockchain currently enforces a minimum output size many hundreds of times higher, and a fixed per-transaction fee which makes micropayments impractical. Lightning allows minimal payments denominated in bitcoin, using actual bitcoin transactions.  
可以通过小额支付的可能性打开新市场。Lightning 使人们能够将资金发送到 0.00000001 比特币（<0.01 美分），而不会有托管风险。比特币区块链目前执行的最低输出大小高出数百倍，并且每笔交易收取固定的费用，这使得小额支付不切实际。Lightning 允许使用实际的比特币交易以比特币计价的最小支付。

### Scalability 可扩展性

The bitcoin network will need to support orders of magnitude higher transaction volume to meet demand from automated payments. The coming increase in internet-connected devices needs a platform for machine-to-machine payments and automated micropayment services. Lightning Network transactions are conducted off the blockchain without delegation of trust and ownership, allowing users to conduct nearly unlimited transactions between other devices.  
比特币网络将需要支持数量级的交易量，以满足自动支付的需求。即将到来的互联网连接设备的增长需要一个用于机器对机器支付和自动小额支付服务的平台。Lightning Network 交易在区块链外进行，无需委托信任和所有权，允许用户在其他设备之间进行几乎无限的交易。

### How it Works 运作方式

Funds are placed into a two-party, multisignature "channel" Bitcoin address. This channel is represented as an entry on the Bitcoin public ledger. In order to spend funds from the channel, both parties must agree on the new balance. The current balance is stored as the most recent transaction signed by both parties, spending from the channel address. To make a payment, both parties sign a new exit transaction spending from the channel address. All old exit transactions are invalidated by doing so. The Lightning Network does not require cooperation from the counterparty to exit the channel. Both parties have the option to unilaterally close the channel, ending their relationship. Since all parties have multiple multisignature channels with many different users on this network, one can send a payment to any other party across this network. By embedding the payment conditional upon knowledge of a secure cryptographic hash, payments can be made across a network of channels without the need for any party to have unilateral custodial ownership of funds. The Lightning Network enables what was previously not possible with trusted financial systems vulnerable to monopolies—without the need for custodial trust and ownership, participation on the network can be dynamic and open for all.   
资金被放入一个两方、多重签名的“通道”比特币地址中。此通道表示为 Bitcoin public ledger 上的一个条目。为了使用来自通道的资金，双方必须就新的余额达成一致。当前余额存储为双方签署的最新交易，从通道地址消费。为了进行支付，双方都签署了一笔新的退出交易 spending 来自频道地址。这样做会使所有旧的退出交易失效。闪电网络不需要交易对手的配合即可退出通道。双方都可以选择单方面关闭频道，结束他们的关系。由于所有方都有多个多重签名通道，在这个网络上有许多不同的用户，因此可以通过这个网络向任何其他方发送付款。通过嵌入基于安全加密哈希的支付，可以通过通道网络进行支付，而无需任何一方拥有资金的单方面托管所有权。闪电网络实现了以前易受垄断影响的可信金融系统无法实现的事情——无需托管信任和所有权，网络参与可以是动态的，对所有人开放。
