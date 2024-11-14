---
title: 分片区块链
draft: true
---
# Danksharding

**Danksharding** is how Ethereum becomes a truly scalable blockchain, but there are several protocol upgrades required to get there. **Proto-Danksharding** is an intermediate step along the way. Both aim to make transactions on Layer 2 as cheap as possible for users and should scale Ethereum to >100,000 transactions per second.  
**Danksharding** 是以太坊成为真正可扩展的区块链的方式，但需要多次协议升级才能实现这一目标。**Proto-Danksharding** 是一路中的中间步骤。两者都旨在使用户尽可能便宜地进行第 2 层交易，并且应该将以太坊扩展到每秒 >100,000 笔交易。

## [](https://ethereum.org/en/roadmap/danksharding/#what-is-protodanksharding)What is Proto-Danksharding?  
什么是 Proto-Danksharding？

Proto-Danksharding, also known as [EIP-4844(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-4844), is a way for [rollups](https://ethereum.org/en/layer-2/#rollups) to add cheaper data to blocks. The name comes from the two researchers who proposed the idea: Protolambda and Dankrad Feist. Historically, rollups had been limited in how cheap they can make user transactions by the fact that they post their transactions in `CALLDATA`.  
Proto-Danksharding，也称为 [EIP-4844（opens in a new tab），](https://eips.ethereum.org/EIPS/eip-4844)是[卷叠](https://ethereum.org/en/layer-2/#rollups)向区块添加更便宜数据的一种方式。这个名字来自提出这个想法的两位研究人员：Protolambda 和 Dankrad Feist。从历史上看，rollup 在进行用户交易的成本方面受到限制，因为它们在 `CALLDATA` 中发布交易。

This is expensive because it is processed by all Ethereum nodes and lives on-chain forever, even though rollups only need the data for a short time. Proto-Danksharding introduces data blobs that can be sent and attached to blocks. The data in these blobs is not accessible to the EVM and is automatically deleted after a fixed time period (set to 4096 epochs at time of writing, or about 18 days). This means rollups can send their data much more cheaply and pass the savings on to end users in the form of cheaper transactions.  
这很昂贵，因为它由所有以太坊节点处理并永远存在于链上，即使 rollup 只需要短时间内的数据。Proto-Danksharding 引入了可以发送并附加到区块的数据 blob。EVM 无法访问这些 blob 中的数据，并在固定时间段后自动删除（在撰写本文时设置为 4096 个纪元，或大约 18 天）。这意味着 rollup 可以更便宜地发送他们的数据，并以更便宜的交易形式将节省的费用转嫁给最终用户。

### 

### Why do blobs make rollups cheaper?  
为什么 blob 会使 rollup 更便宜？

More 更多

### 

### Why is it OK to delete the blob data?  
为什么可以删除 blob 数据？

More 更多

### [](https://ethereum.org/en/roadmap/danksharding/#how-are-blobs-verified)How is blob data verified?  
如何验证 blob 数据？

Rollups post the transactions they execute in data blobs. They also post a "commitment" to the data. They do this by fitting a polynomial function to the data. This function can then be evaluated at various points. For example, if we define an extremely simple function `f(x) = 2x-1` then we can evaluate this function for `x = 1`, `x = 2`, `x = 3` giving the results `1, 3, 5`. A prover applies the same function to the data and evaluates it at the same points. If the original data is changed, the function will not be identical, and therefore neither are the values evaluated at each point. In reality, the commitment and proof are more complicated because they are wrapped in cryptographic functions.  
汇总发布它们在数据 blob 中执行的事务。他们还发布了对数据的 “承诺”。它们通过对数据拟合多项式函数来实现此目的。然后可以在不同的点评估此函数。例如，如果我们定义一个非常简单的函数 `f（x） = 2x-1`，那么我们可以计算该函数的 `x = 1`， `x = 2`， `x = 3`，结果为 `1， 3， 5`。证明器将相同的函数应用于数据，并在相同的点对其进行计算。如果原始数据发生更改，则函数将不相同，因此也不会在每个点计算值。实际上，承诺和证明更加复杂，因为它们被包装在加密函数中。

### [](https://ethereum.org/en/roadmap/danksharding/#what-is-kzg)What is KZG? 什么是 KZG？

KZG stands for Kate-Zaverucha-Goldberg - the names of the three [original authors(opens in a new tab)](https://link.springer.com/chapter/10.1007/978-3-642-17373-8_11) of a scheme that reduces a blob of data down to a small [cryptographic "commitment"(opens in a new tab)](https://dankradfeist.de/ethereum/2020/06/16/kate-polynomial-commitments.html). The blob of data submitted by a rollup has to be verified to ensure the rollup is not misbehaving. This involves a prover re-executing the transactions in the blob to check that the commitment was valid. This is conceptually the same as the way execution clients check the validity of Ethereum transactions on layer 1 using Merkle proofs. KZG is an alternative proof that fits a polynomial equation to the data. The commitment evaluates the polynomial at some secret data points. A prover would fit the same polynomial over the data and evaluate it at the same values, checking that the result is the same. This is a way to verify the data that is compatible with zero-knowledge techniques used by some rollups and eventually other parts of the Ethereum protocol.  
KZG 代表 Kate-Zaverucha-Goldberg - 一个方案的三[位原始作者（opens in a new tab）](https://link.springer.com/chapter/10.1007/978-3-642-17373-8_11)的名字，该方案将一团数据简化为一个小的[加密“承诺”（opens in a new tab）。](https://dankradfeist.de/ethereum/2020/06/16/kate-polynomial-commitments.html)必须验证 rollup 提交的数据 blob，以确保 rollup 没有行为异常。这涉及证明者重新执行 blob 中的事务，以检查承诺是否有效。这在概念上与执行客户端使用 Merkle 证明检查第 1 层以太坊交易有效性的方式相同。KZG 是将多项式方程拟合到数据的替代证明。承诺在一些秘密数据点处计算多项式。证明器将对数据拟合相同的多项式，并以相同的值对其进行评估，检查结果是否相同。这是一种验证数据的方法，它与某些 rollup 以及最终 Ethereum 协议的其他部分使用的零知识技术兼容。

### [](https://ethereum.org/en/roadmap/danksharding/#what-is-a-kzg-ceremony)What was the KZG Ceremony?  
什么是 KZG 仪式？

The KZG ceremony was a way for many people from across the Ethereum community to collectively generate a secret random string of numbers that can be used to verify some data. It is very important that this string of numbers is not known and cannot be recreated by anyone. To ensure this, each person that participated in the ceremony received a string from the previous participant. They then created some new random values (e.g. by allowing their browser to measure the movement of their mouse) and mix it in with the previous value. They then sent the value on to the next participant and destroyed it from their local machine. As long as one person in the ceremony did this honestly, the final value will be unknowable to an attacker.  
KZG 仪式是以太坊社区中的许多人集体生成一个秘密随机数字字符串的一种方式，可用于验证某些数据。非常重要的一点是，这串数字是未知的，任何人都不能重新创建。为了确保这一点，每个参加仪式的人都收到了前一个参与者的字符串。然后，他们创建了一些新的随机值（例如，允许浏览器测量鼠标的移动）并将其与之前的值混合。然后，他们将该值发送给下一个参与者，并从本地计算机中销毁它。只要仪式中有一个人诚实地这样做，攻击者就无法知道最终的价值。

The EIP-4844 KZG ceremony was open to the public and tens of thousands of people participated to add their own entropy (randomness). In total there were over 140,000 contributions, making it the world's largest ceremony of its kind. For the ceremony to be undermined, 100% of those participants would have to be actively dishonest. From the perspective of the participants, if they know they were honest, there is no need to trust anyone else because they know that they secured the ceremony (they individually satisfied the 1-out-of-N honest participant requirement).  
EIP-4844 KZG 仪式向公众开放，数万人参与添加自己的熵（随机性）。总共有超过 140,000 份捐款，使其成为世界上同类仪式中规模最大的一次。要破坏仪式，这些参与者中 100% 必须积极不诚实。从参与者的角度来看，如果他们知道自己是诚实的，就没有必要信任其他人，因为他们知道他们确保了仪式（他们个人满足了 N 人中 1 分之 1 的诚实参与者要求）。

### 

### What is the random number from the KZG ceremony used for?  
KZG 仪式的随机数是做什么用的？

Less 少

When a rollup posts data in a blob, they provide a "commitment" that they post on-chain. This commitment is the result of evaluating a polynomial fit to the data at certain points. These points are defined by the random numbers generated in the KZG ceremony. Provers can then evaluate the polynomial at the same points in order to verify the data - if they arrive at the same values then the data is correct.  
当 rollup 在 blob 中发布数据时，他们会提供在链上发布的 “承诺”。此承诺是评估在某些点与数据的多项式拟合的结果。这些点由 KZG 仪式中生成的随机数定义。然后，证明者可以在相同的点评估多项式以验证数据 - 如果它们得出相同的值，则数据是正确的。

### 

### Why does the KZG random data have to stay secret?  
为什么 KZG 随机数据必须保密？

Less 少

If someone knows the random locations used for the commitment, it is easy for them to generate a new polynomial that fits at those specific points (i.e. a "collision"). This means they could add or remove data from the blob and still provide a valid proof. To prevent this, instead of giving provers the actual secret locations, they actually receive the locations wrapped in a cryptographic "black box" using elliptic curves. These effectively scramble the values in such a way that the original values cannot be reverse-engineered, but with some clever algebra provers and verifiers can still evaluate polynomials at the points they represent.  
如果有人知道用于承诺的随机位置，他们很容易生成适合这些特定点的新多项式（即“碰撞”）。这意味着他们可以在 blob 中添加或删除数据，并且仍然提供有效的证明。为了防止这种情况，证明者实际上不是给证明者实际的秘密位置，而是使用椭圆曲线接收包装在加密“黑盒”中的位置。这些方法有效地对值进行打乱，使得原始值无法进行逆向工程，但通过一些聪明的代数证明器和验证器，仍然可以在它们所表示的点处计算多项式。

Neither Danksharding nor Proto-Danksharding follow the traditional "sharding" model that aims to split the blockchain into multiple parts. Shard chains are no longer part of the roadmap. Instead, Danksharding uses distributed data sampling across blobs to scale Ethereum. This is much simpler to implement. This model has sometimes been referred to as "data-sharding".  
Danksharding 和 Proto-Danksharding 都不遵循传统的“分片”模型，该模型旨在将区块链拆分为多个部分。分片链不再是路线图的一部分。相反，Danksharding 使用跨 blob 的分布式数据采样来扩展以太坊。这更容易实现。此模型有时称为 “数据分片”。

## [](https://ethereum.org/en/roadmap/danksharding/#what-is-danksharding)What is Danksharding? 什么是 Danksharding？

Danksharding is the full realization of the rollup scaling that began with Proto-Danksharding. Danksharding will bring massive amounts of space on Ethereum for rollups to dump their compressed transaction data. This means Ethereum will be able to support hundreds of individual rollups with ease and make millions of transactions per second a reality.  
Danksharding 是从 Proto-Danksharding 开始的 rollup 扩展的完全实现。Danksharding 将在以太坊上为 rollup 带来大量空间来转储其压缩的交易数据。这意味着以太坊将能够轻松支持数百个单独的 rollup，并使每秒数百万笔交易成为现实。

The way this works is by expanding the blobs attached to blocks from six (6) in Proto-Danksharding, to 64 in full Danksharding. The rest of the changes required are all updates to the way consensus clients operate to enable them to handle the new large blobs. Several of these changes are already on the roadmap for other purposes independent of Danksharding. For example, Danksharding requires proposer-builder separation to have been implemented. This is an upgrade that separates the tasks of building blocks and proposing blocks across different validators. Similarly, data availability sampling is required for Danksharding, but it is also required for the development of very lightweight clients that do not store much historical data ("stateless clients").  
其工作方式是将附加到区块的 blob 从 Proto-Danksharding 中的六 （6） 个扩展到完全 Danksharding 中的 64 个。其余所需的更改是对共识客户端操作方式的所有更新，以使它们能够处理新的大型 blob。其中一些更改已经在路线图上，用于独立于 Danksharding 的其他目的。例如，Danksharding 要求已经实现提议者-构建者分离。这是一种升级，它将构建区块和跨不同验证者提出区块的任务分开。同样，Danksharding 需要数据可用性采样，但开发不存储太多历史数据的非常轻量级的客户端（“无状态客户端”）也需要数据可用性采样。

### 

### Why does Danksharding require proposer-builder separation?  
为什么 Danksharding 需要提议者 - 构建者分离？

Less 少

Proposer-builder separation is required to prevent individual validators from having to generate expensive commitments and proofs for 32MB of blob data. This would put too much strain on home stakers and require them to invest in more powerful hardware, which hurts decentralization. Instead, specialized block builders take responsibility for this expensive computational work. Then, they make their blocks available to block proposers to broadcast. The block proposer simply chooses the block that is most profitable. Anyone can verify the blobs cheaply and quickly, meaning any normal validator can check that the block builders are behaving honestly. This allows the large blobs to be processed without sacrificing decentralization. Misbehaving block builders could simply be ejected from the network and slashed - others will step into their place because block building is a profitable activity.  
需要将提议者-构建者分开，以防止单个验证者不得不为 32MB 的 blob 数据生成昂贵的承诺和证明。这将给家庭质押者带来太大的压力，并要求他们投资更强大的硬件，从而损害去中心化。相反，专门的区块构建者负责这项昂贵的计算工作。然后，他们将他们的区块提供给阻止提议者进行广播。区块提议者只需选择最有利可图的区块。任何人都可以廉价而快速地验证 blob，这意味着任何普通的验证者都可以检查区块构建者的行为是否诚实。这允许在不牺牲去中心化的情况下处理大型 blob。行为不端的区块构建者可以简单地被逐出网络并被罚没——其他人会取代他们的位置，因为区块构建是一项有利可图的活动。

### 

### Why does Danksharding require data availability sampling?  
为什么 Danksharding 需要数据可用性采样？

Less 少

Data availability sampling is required for validators to quickly and efficiently verify blob data. Using data availability sampling, the validators can be very certain that the blob data was available and correctly committed. Every validator can randomly sample just a few data points and create a proof, meaning no validator has to check the entire blob. If any data is missing, it will be identified quickly and the blob rejected.  
验证程序需要数据可用性采样才能快速有效地验证 blob 数据。使用数据可用性采样，验证者可以非常确定 blob 数据可用并正确提交。每个验证者都可以随机采样几个数据点并创建一个证明，这意味着没有验证者必须检查整个 blob。如果缺少任何数据，将快速识别并拒绝 blob。

### [](https://ethereum.org/en/roadmap/danksharding/#current-progress)Current progress 当前进度

Full Danksharding is several years away. In the meantime, the KZG ceremony has concluded with over 140,000 contributions, and the [EIP(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-4844) for Proto-Danksharding has matured. This proposal has been fully implemented in all testnets, and went live on Mainnet with the Cancun-Deneb ("Dencun") network upgrade in March 2024.  
完全 Danksharding 还需要几年时间。与此同时，KZG 仪式已经结束，贡献超过 140,000 次，Proto-Danksharding 的 [EIP（opens in a new tab）](https://eips.ethereum.org/EIPS/eip-4844) 已经成熟。该提案已在所有测试网中全面实施，并于 2024 年 3 月随着 Cancun-Deneb（“Dencun”）网络升级在主网上上线。

### [](https://ethereum.org/en/roadmap/danksharding/#further-reading)