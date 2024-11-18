---
title: 自动做市商是什么？
aliases:
  - 自动做市商是什么？
draft: false
---
>[!NOTE]
>想象一下，你生活在一个岛上，你生活的那个区域只能靠打渔为生。
> 
>有一天，你再也忍受不了每天吃鱼了，你决定换点水果吃。不久后，一个远洋捕捞的渔夫说在东边的一座岛上有很多果农，他们想换一些鱼吃。
>
>他们希望用 $1,000$ 个苹果换 $1,000$ 条鱼，你很爽快地答应了。但鱼的价格会根据供求关系而波动，而你们现在不清楚价格，为了维持这个交易比例，你们决定将这两个数量相乘 $1,000 \times 1,000 = 1,000,000$，将这个数作为一个不变的值。
>
>如果市场上充斥着大量鱼，比如 $10,000$ 条鱼，为了兑换这 $10,000$ 条鱼的苹果数量就会减少，从而压低鱼的价格，此时需要的苹果数量就是 $1,000,000 / 10,000 = 100$ 个。反之，如果苹果变得稀缺，需要的鱼的数量就会飙升。AMM 的运作方式类似，价格发现的概念取决于供需机制。


自动做市商 （AMM） 是[去中心化金融 （DeFi）](https://www.gemini.com/cryptopedia/what-is-defi-crypto-decentralized-finance-projects) 生态系统的一部分。它们允许通过使用流动性池而不是传统的买家和卖家市场，以无需许可和自动的方式交易数字资产。AMM 用户为加密代币提供流动性池，其价格由常数数学公式决定。[流动性池](https://www.gemini.com/cryptopedia/what-is-a-liquidity-pool-crypto-market-liquidity)可以针对不同目的进行优化，并被证明是 DeFi 生态系统中的重要工具。

# 什么是做市商？

自动做市商 （AMM） 是为所有去中心化交易所 （DEX） 提供动力的底层协议，DEX 通过直接连接用户来帮助用户交换加密货币，无需中介。简而言之，自动做市商是自主交易机制，无需中心化交易所和相关做市技术。在本指南中，我们将探讨 AMM 的工作原理。

做市商促进了为中心化交易所的交易对提供流动性所需的过程。中心化交易所监督交易者的运营并提供自动化系统，确保交易订单得到相应的匹配。换句话说，当交易者 A 决定以 34,000 美元的价格购买 1 [BTC](https://coindesk.com/price/bitcoin) 时，交易所会确保找到愿意以交易者 A 的首选汇率出售 1 BTC 的交易者 B。因此，中心化交易所或多或少是交易者 A 和交易者 B 之间的中间人。它的工作是使流程尽可能无缝，并在创纪录的时间内匹配用户的买卖订单。

那么，如果交易所无法立即找到合适的买卖订单匹配项怎么办？

在这种情况下，我们说相关资产的流动性很低。

> 流动性，就交易而言，是指资产买卖的难易程度。高流动性表明市场活跃，有很多交易者买卖特定资产。相反，低流动性意味着活动较少，买卖资产更加困难。
    
当流动性较低时，往往会发生滑点。换句话说，在交易完成之前，资产在执行交易时的价格会发生很大变化。这通常发生在加密市场等动荡的领域。因此，交易所必须确保交易即时执行，以减少价格滑点。

为了实现流畅的交易系统，中心化交易所依靠专业的交易员或金融机构为交易对提供流动性。这些实体创建多个买卖订单以匹配零售交易者的订单。有了这个，交易所可以确保[交易对手](https://www.coindesk.com/learn/what-is-counterparty-risk-in-crypto/)始终可用于所有交易。在这个系统中，流动性提供者扮演做市商的角色。换句话说，做市商促进了为交易对提供流动性所需的流程。

# 什么是自动做市商 （AMM）？

与中心化交易所不同，[DEX](https://www.coindesk.com/learn/what-is-a-dex-how-decentralized-crypto-exchanges-work/) 希望根除加密交易中涉及的所有中间流程。它们不支持订单匹配系统或托管基础设施（交易所持有所有钱包私钥）。因此，DEX 促进了自主性，以便用户可以直接从非托管钱包（个人控制私钥的钱包）发起交易。

此外，DEX 用称为 AMM 的自主协议取代了订单匹配系统和订单簿。这些协议使用[智能合约](https://www.coindesk.com/learn/how-do-ethereum-smart-contracts-work/)（自动执行的计算机程序）来定义数字资产的价格并提供流动性。在这里，协议将流动性汇集到智能合约中。从本质上讲，从技术上讲，用户并不是在与交易对手进行交易——相反，他们是在与智能合约中锁定的流动性进行交易。这些智能合约通常被称为流动性池。

值得注意的是，只有高净值个人或公司才能在传统交易所中担任流动性提供者的角色。至于 AMM，任何实体都可以成为流动性提供者，只要它满足硬编码到智能合约中的要求。AMM 的示例包括 [Uniswap](https://uniswap.org/)、[Balancer](https://balancer.fi/) 和 [Curve](https://curve.fi/)。

# AMM 示例

加密货币中的 AMM 主要有两种类型。首先，有由专业做市商创建和控制的 AMM。其次，一些 AMM 是通过算法完全自动化的，使任何加密持有者都可以通过将资产锁定到智能合约中来参与。考虑到这一点，我们将讨论五种常见的 AMM 协议。

## Kyber Network

[Kyber Network](https://www.coingecko.com/en/coins/kyber-network-crystal) 是 2018 年首批使用自动流动性池的 AMM 之一。Kyber 团队或专业做市商部署 Kyber 的流动性池。与 Uniswap 等其他制造商不同，Kyber 池的访问权限有限。外部预言机或智能合约功能在设置期间调节池中资产的价格。

## Uniswap 

[Uniswap](https://www.coingecko.com/en/exchanges/uniswap) 是 2019 年第一个采用去中心化 AMM 的 DEX。它允许任何人在协议上运行流动性池，并允许任何加密投资者贡献流动性。与 Kyber Network 不同，Uniswap 流动性池中的代币价格不受配置或控制。相反，代币价格基于资产之间的余额比率。

## Balancer
 
与上述两种协议不同，[Balancer](https://www.coingecko.com/en/exchanges/balancer) 是一种具有独特功能的较新协议。它的工作原理类似于 Uniswap，但提供了更多的动态功能，使其除了充当简单的流动性池之外，还可以拥有更多应用程序。例如，它支持自定义矿池比率、多资产池和动态矿池费用。多资产池充当加密中的索引，并充当 Balancer 的独特功能。

## Curve

[Curve](https://www.coingecko.com/en/exchanges/curve) 是 DeFi 领域最新的 AMM 协议之一。它于 2020 年推出，包含仅限管理员的流动性池。任何人都可以为矿池做出贡献，并且他们只支持稳定币。该协议将其仅支持[稳定币](https://www.coingecko.com/learn/what-are-stablecoins-top-5-stablecoins-by-market-cap)的决定视为一项功能，而不是障碍。通过支持纯稳定币或纯包装币池（例如 [WETH/ETH](https://www.coingecko.com/learn/weth-vs-eth-what-s-the-distinction) 或 WBTC/SBTC），Curve 可以有效地处理大额交易请求，并将滑点降至最低。

## Bancor

您可以使用一种代币向 [Bancor](https://www.coingecko.com/en/exchanges/bancor_v3) 池提供流动性，并保持对资产的 100% 敞口。这与其他要求您保持对许多代币的敞口的 AMM 协议不同。借助基于单一代币的流动性，您可以长期持有资产并有资格获得“[HODL](https://www.coingecko.com/learn/a-brief-history-of-hodl)”回报，同时赚取交易费用。费用在矿池中自动复利，并以质押资产支付。

# 自动做市商 （AMM） 如何运作？
 
首先需要了解关于 AMM 的两件重要事情：

- 您通常在中心化交易所上找到[的交易对](https://www.coindesk.com/learn/what-are-crypto-trading-pairs/)在 AMM 中作为单独的“[流动性池](https://www.coindesk.com/learn/what-are-liquidity-pools/)”存在。例如，如果您想用[以太币](https://coindesk.com/price/ethereum)换取 [Tether](https://coindesk.com/price/tether)，您需要找到一个 ETH/USDT 流动性池。
- 任何人都可以通过存入池中代表的两种资产来为这些池提供流动性，而不是使用专门的做市商。例如，如果您想成为 ETH/USDT 池的流动性提供者，您需要存入一定预定比例的 ETH _和_ USDT。
    

为了确保流动性池中的资产比率尽可能保持平衡并消除集合资产定价的差异，AMM 使用预设的数学方程式。例如，[Uniswap](https://coindesk.com/business/2021/02/04/what-is-uniswap-a-complete-beginners-guide/) 和许多其他 DeFi 交易协议使用简单的 $$x \times y=k$$方程来设置流动性池中持有的特定资产之间的数学关系。

其中，x 表示资产 A 的值，y 表示资产 B 的值，而 k 是常数，表示存在一个恒定的资产余额，它决定了流动性池中代币的价格。

值得注意的是，K 需要是常数。如果池中的 x 数量发生变化，则 y 的数量也需要以特定比例变化，以确保 k 保持不变。

让我们以 [DAI](https://beincrypto.com/learn/dai-crypto/)/WBTC 为例。

假设 DAI/WBTC 池有 $10,000$ 个 DAI 和 $10$ 个 [WBTC](https://beincrypto.com/learn/wrapped-bitcoin-wbtc/)，则常数 $10,000 \times 10 = 100,000$

现在，如果一个人从池中提取 1 个 [WBTC](https://beincrypto.com/learn/wrapped-bitcoin-wbtc)，改变 y，x 的值也会根据 k/y 比率而变化。因此，池中应存在的新 DAI 数量为 $100,000/9 = 1,111.11$

因此，想要提取 1 个 WBTC 的交易者应将 1,111.11 个 DAI 代币存入池中。另一种看待它的方式是将 1 个 WBTC（特定于矿池）的价格等同于 1,111.11 个 DAI 代币。这就是 AMM 的运作方式，尤其是在流动性供应和代币交换方面。

如果 AMM 拥有以太币 （ETH） 和比特币 （BTC），这两种波动性资产，则每次购买 ETH 时，ETH 的价格都会上涨，因为池中的 ETH 比购买前少。相反，BTC 的价格会随着池中的 BTC 增加而下跌。矿池保持恒定余额，其中矿池中的 ETH 总价值将始终等于矿池中 BTC 的总价值。只有当新的流动性提供者加入时，资金池的规模才会扩大。从视觉上看，AMM 池中的代币价格遵循由公式确定的曲线。

从本质上讲，Uniswap 的流动性池始终保持一种状态，即资产 A 的价格与 B 的价格相乘始终等于相同的数字。

要了解其运作方式，让我们以 ETH/USDT 流动性池为例。当交易者购买 ETH 时，他们会将 USDT 添加到池中并从中取出 ETH。这会导致池中的 ETH 数量下降，进而导致 ETH 的价格上涨，以实现 $$x\times y=k$$ 的平衡效果。相反，由于池中添加了更多的 USDT，USDT 的价格下降。当购买 USDT 时，情况正好相反——ETH 的价格在池中下跌，而 USDT 的价格上涨。

![Automated market maker equation](https://www.coindesk.com/resizer/xqpwthv-dw3iFsU09KcNOgfXMz0=/811x458/filters:quality(80):format(jpg)/cloudfront-us-east-1.images.arcpublishing.com/coindesk/2JYSUKBZKJDLPAOVBQT2EH2IHI.png)
> 自动做市商方程式

当在 AMM 中下达大额订单并且大量代币被删除或添加到池中时，可能会导致资产在池中的价格与其市场价格（它在多个交易所的交易价格）之间出现显着差异。例如，ETH 的市场价格可能是 3,000 美元，但在矿池中，它可能是 2,850 美元，因为有人向矿池中添加了大量 ETH 以删除另一个代币。

这意味着 ETH 将在池中以折扣价交易，从而创造套利机会。套利交易是一种在多个交易所寻找资产价格差异的策略，在价格略便宜的平台上购买，然后在价格略高的平台上出售。


对于 AMM，套利交易者在经济上受到激励，在流动性池中寻找以折扣交易的资产并购买它们，直到资产的价格回报与其市场价格一致。

例如，如果流动性池中的 ETH 价格与其他市场的汇率相比下跌，套利交易者可以通过以较低的汇率购买池中的 ETH 并在外部交易所以更高的价格出售来获利。在每笔交易中，汇集的 ETH 的价格将逐渐回升，直到达到标准市场汇率。

请注意，Uniswap 的 $$x \times y=k$$只是当今 AMM 使用的数学公式之一。例如，[Balancer](https://coindesk.com/business/2021/02/02/one-big-pool-balancers-new-version-cuts-down-transactions-and-gas-fees/) 使用一种更复杂的数学关系形式，允许用户将多达 8 种数字资产组合在一个流动性池中。另一方面，[Curve](https://coindesk.com/tech/2021/06/09/defis-curve-eyes-more-tokens-with-white-paper-for-version-2/) 采用适合配对[稳定币](https://coindesk.com/markets/2020/12/29/what-is-a-stablecoin/)或类似资产的数学公式。

**请注意，虽然 $x \times y = k$ 是标准公式，但不同的 AMM 具有不同的版本来证明池运行状况的合理性。** 例如，余额遵循 $k = (余额 1 / 权重 1) \times (余额 2 / 权重 2)...... \times (余额 n / 权重 n)$ 的加权方法

[curve](https://beincrypto.com/learn/curve-crv/)遵循 $D = A \times S + S^N / N^N$ 作为首选公式，其中 D 是常数，S 是所有储备金的总和，A 是用于放大的特殊系数，N 是池特定资产的数量。

即使是 Uniswap V3 和 Bancor 之类的公司也有特定的数学计算来支持他们的算法。

# 流动性提供者在 AMM 中的作用

如前所述，AMM 需要[流动性](https://coindesk.com/tech/2019/12/08/decentralized-liquidity-is-the-backbone-of-defi/)才能正常运行。资金不足的资金池很容易出现滑点。为了减少滑点，AMM 鼓励用户将数字资产存入流动性池（liquidity pool (LP)），以便其他用户可以使用这些资金进行交易。作为激励措施，该协议奖励流动性提供者 （LP ） 为在矿池上执行的交易支付的费用的一小部分。换句话说，如果您的存款占池中锁定的流动性的 1%，您将收到一个 LP 代币，它代表该池应计交易费用的 1%。当流动性提供者希望退出矿池时，他们会赎回他们的 LP 代币并获得他们应得的交易费用。

除此之外，AMM 还向 LP 和交易员发行[治理代币](https://www.coindesk.com/learn/what-is-a-governance-token/)。顾名思义，治理代币允许持有者对与 AMM 协议的治理和开发相关的问题拥有投票权。

# AMM 的流动性挖矿机会

除了上面强调的激励措施外，LP 还可以利用有望增加收入的[流动性挖矿](https://www.coindesk.com/learn/what-is-yield-farming-the-rocket-fuel-of-defi-explained/)机会。要享受这一好处，您需要做的就是将适当比例的数字资产存入 AMM 协议上的流动性池中。确认存款后，AMM 协议将向您发送 LP 代币。在某些情况下，您可以将此代币存入或“质押”到单独的借贷协议中并赚取额外利息。

通过这样做，您将通过利用去中心化金融 （DeFi） 协议的可组合性或互操作性来最大化您的收入。但请注意，您需要赎回流动性提供者代币才能从初始流动性池中提取您的资金。

# 什么是无常损失？
 
与流动性池相关的风险之一是无常损失。当集合资产的价格比率波动时，就会发生这种情况。当集合资产的价格比率偏离其存入资金的价格时，LP 将自动蒙受损失。价格变动越大，造成的损失就越大。无常损失通常会影响包含易失性数字资产的矿池。

然而，这种损失是无常的，因为价格比率有可能回归。只有当 LP 在价格比率恢复之前提取上述资金时，损失才会成为永久性的。另外，请注意，交易费用和 LP 代币质押的潜在收益有时可以弥补此类损失


# AMM 有哪些不同类型？

自动做市商可能会因他们使用的算法和它们所服务的目的而异。以下是需要注意的不同类型：

## 虚拟 AMM

这些是自动做市商，池中没有任何实际资产。相反，只有一个数学模型控制价格。这些做市商可能很复杂。 **一个这样的例子是 Perpetual Protocol，其中交易事件结果。**

看待虚拟 AMM 的另一种方法是认为它们加载了虚拟余额，以降低大额交易的影响。Bancor 的 V2 是使用虚拟余额的一个例子。

## 概率 AMM

这些 AMM 使用概率数学公式来控制交易价格。这些是智能合约主导的 AMM，其中使用了复杂的数学模型。这些 AMM 可以作为其他需要专有公式帮助的 AMM 的基准。Tokemak 就是概率 AMM 的一个这样一个例子。

## 恒定 AMM
 
这些是最常见的 AMM 形式，通常用 $x \times y = k$ 公式表示。在这些 AMM 中，如果一种资产的价格因供应减少而上涨，另一种资产的价格必须下跌以保持平衡。[Uniswap](https://beincrypto.com/learn/top-cryptocurrency-exchanges-usa-2020/) 是恒定产品 AMM 的一个例子。

Uniswap 最近推出了 [UniswapX 协议](https://blog.uniswap.org/uniswapx-protocol)——一种更好的跨 AMM 交易方式，提供更高的流动性、零交易失败，甚至无 gas 交换。这将使恒定积 AMM 的概念提升到一个全新的水平。

## 混合 AMM

**混合自动化做市商能够根据场景改变其运营原则。** 它们可以作为标准交易的恒定产品 AMM，但当资产价格变得过于波动，从而增加清算风险时，它们可能会变成概率型 AMM。Balancer 用作混合 AMM。

## 加权平均价格 AMM

这些 AMM 的运行原理依赖于一个特殊的公式，其中资产的价格由池中两种资产的数量表示，而不仅仅是一种资产。一个这样的例子是 [Curve Finance](https://beincrypto.com/learn/curve-crv/)，一个用于交易[稳定币的](https://beincrypto.com/learn/what-is-a-stablecoin/)平台。

## 自定义均值 AMM

在这些自动做市商中，有一个自定义的平均公式控制资产价格。这样，就可以自定义资产的价格以满足特定的 AMM 要求。名义是自定义均值 AMM 的一个示例。

## 动态 AMM

这些自动做市商，顾名思义，根据市场条件改变生态系统参数。[1inch](https://beincrypto.com/learn/1inch-exchange/) 就是一个例子。

## NFT AMMs 

这些是专门的做市商，旨在简化 NFT 交易。这些 AMM 旨在为原本缺乏流动性的 NFT 空间注入流动性。**NFTX 就是这种 NFT AMM 的一个例子。**

SeaCows 是另一个旨在通过让人们更容易获得 NFTFi 来提高 NFT 流动性的项目。

## 借贷 AMM

这些 AMM 的核心是促进借贷。 **用户向池中供应或存入资产，在此过程中赚取利息。另一方面，借款人可以按预定的利率借出资产。**[Aave](https://beincrypto.com/learn/what-is-aave/) 和 Compound 是借出 AMM 的主要例子。

## 保险 AMM

确保资产属于他人的资产的池化性质是保险 AMM 的核心。Nexus Mutual 就是一个例子。

## 期权 AMM

顾名思义，这些 AMM 允许期权交易，其中不是资产而是资产的衍生品用于交易。Opyn 是期权 AMM 的一个示例。

## 预测 AMM

有一些 AMM 允许您交易特定场景，甚至押注特定事件相关结果。Augur 就是这样一种广受欢迎的预测 AMM。

## 流动性即服务 AMM

这些 AMM 擅长从不同的 DeFi 协议中聚合流动性。1inch 提供流动性即服务作为其 AMM 产品的一部分。

## 合成 AMM

如果您想交易代表股票甚至黄金等现实世界资产的合成资产，您可以考虑像 Synthetix 这样的合成 AMM。


# AMM 的历史

早在 AMM 甚至 [DEX](https://beincrypto.com/learn/decentralized-exchanges/) 出现之前，[订单簿](https://beincrypto.com/learn/order-book/)系统就促进了传统市场的交易。您可以将订单簿视为记录买卖双方对给定资产的兴趣的日记。

这些传统做市商为传统市场提供流动性，从买卖价差中获利。对于外行来说，价差表示卖方要价与买方支付价差之间的差额。 **这些做市商低买高卖，向任一类别的交易参与者提供资产以获取微薄利润。**

![History of AMM: BIC](https://beincrypto.com/wp-content/uploads/2023/07/AMM-history-850x263.png.webp)

History of AMMs: BIC AMM 的历史：BIC

**虽然传统做市商在股票等其他高贝塔资产中仍然有用，但它们在加密市场中效果不佳。**加密市场高度波动，流动性通常是一个问题，尤其是对于更难以捉摸的代币对。

## AMM 的兴起

AMM 于 2017 年与 Bancor 一起正式出现。然而，Uniswap 使 AMM 流行起来，于 2018 年出现。**Uniswap 基于以太坊构建，由[智能合约](https://beincrypto.com/learn/smart-contracts-explainer/)提供支持，并自动执行做市过程。**自 2018 年以来，AMM 领域发生了重大发展，尤其是在流动性供应、价格发现和处理无常损失等风险方面。

然而，加密社区的愿望远不止于此。

> “我想要更多的加密项目，试图利用加密超能力来破坏流行的 web2 应用程序，以发现新的用例，而不是在少数现有用例（AMM、贷款等）上构建边际改进。”
> 
> **Hayden Adams （hayden.eth） Uniswap 协议的创建者：**[**Twitter**](https://twitter.com/haydenzadams/status/1682718268568788993)


然而，**Hayden 的看法并不是一致的，并且确实面临一些反对意见**：

在 UniSwap 之后，[PancakeSwap](https://beincrypto.com/learn/how-to-use-pancakeswap/) 和 [SushiSwap](https://beincrypto.com/learn/how-to-use-sushiswap/) 等几个由 AMM 驱动的 DEX 也浮出水面。新的和改进的自动做市商模型，如概率 AMM、恒定积 AMM 等，已经脱颖而出，为 [DeFi 领域](https://beincrypto.com/learn/decentralized-finance-and-use-cases/)带来了新的可能性。

**2023 年，即使是像 Polygon 这样的第 2 层解决方案也开始以 UniSwap V3 的形式部署 AMM，重点是降低加密交易费用。** 


# AMM：概念

看待 AMM 的一种简单方法是考虑专门的 DEX 协议。管理协议是一种数学算法，为每种资产定价并控制它在 [DeFi](https://beincrypto.com/learn/decentralized-finance-and-use-cases/) 空间中的移动方式。

![The concept behind AMM: BIC](https://beincrypto.com/wp-content/uploads/2023/07/how-AMM-works-850x428.png.webp)
自动做市商背后的概念：BeInCrypto

您可以将自动做市商视为推动 DEX 运营的引擎。

这是一个详细的线程，它捕获了 AMM 的概念。

#  DeFi 中的应用

如果您打算进一步探索 AMM，则必须牢记以下一些特定于 DeFi 的应用程序：

![Market maker for traders and liquidity providers: KPMG](https://beincrypto.com/wp-content/uploads/2023/07/AMM-for-traders-and-LPs-850x790.png.webp)

Market maker for traders and liquidity providers: KPMG  
交易者和流动性提供者的做市商：毕马威会计师事务所

## 流动性挖矿

**这是流动性提供者将特定资产存入池子的地方，在此过程中赚取收益和费用。**有几个流动性挖矿平台正在玩，包括 Compound 和 [SushiSwap](https://beincrypto.com/learn/how-to-use-sushiswap/) 等。

S

![AMM and yield farming](https://beincrypto.com/wp-content/uploads/2023/07/AMM-farming-infographic-850x370.png.webp)
流动性挖矿如何运作：BeInCrypto

## 流动性供应

这段路，或者更确切地说是自动做市商的用例，是流动性池的核心。流动性提供者提供流动性，他们在此基础上建立流动性，通过流动性挖矿产生更高的收益。**如果您仅将流动性供应视为一个用例，那么 Cure Finance 和 Uniswap 等平台是值得关注的平台。**

## 交易手续费激励
 
自动做市商的另一个应用是使用该平台来激励流动性提供者。**做市商协议作为标准交易接口，每笔交易都会产生某种交易费用。** AMM 与流动性提供者有一个内置的交易费用分享时间表，这让他们保持兴趣和动力。

## 套利交易

自动做市商还允许您持有[套利交易](https://beincrypto.com/learn/how-does-arbitrage-trading-in-crypto-work/)头寸，因为 AMM 流动性池中的资产价格可能会因倾向于遵守常数值 k 而与市场不同。**例如，如果您计划在 AMM 上购买 ETH，在大多数交易所的交易价格为 1,900 美元，您可能必须在入住前考虑 ETH/USDT 余额。** 

**注意：** 这是特定于我们正在处理 ETH/USDT 池的事实。

现在，如果由于人们为 ETH 购买大量 USDT 而导致池的 ETH 供应量更高，则 ETH 的价格可能会低于市场的 1,900 美元。**这种价格差异产生了套利交易机会。**

## 损失管理

无常损失是困扰大多数做市商的独特问题。

![Impermanent loss in market making: BIC](https://beincrypto.com/wp-content/uploads/2023/07/AMM-and-impermenant-loss-850x560.png.webp)
做市商中的无常损失：BeInCrypto

这是指流动性提供者提供的资产价格向另一个方向移动，将他们推向清算风险。**尽管是无常损失的来源，但 AMM 也提供了相同的解决方案。** 这些可以是概率 AMM 的形式，并带有专门的数学算法。

像 Balancer 这样的 AMM 具有针对权重的解决方案，降低了资产的价格敏感性和固[有波动](https://beincrypto.com/learn/what-causes-bitcoins-volatility/)性。然后是 Curve Finance，那里的矿池主要交易稳定币，旨在保持稳定的价值。

## 自动交易

AMM 消除了对传统市场标记和订单簿的需求，实现了 P2P 和自动化交易。由于**智能合约管理整个交易场景，因此不会遇到订单大小和中间商问题。** 

## 价格预言机

一些 AMM（如 Uniswap）充当去中心化的价格[预言机](https://beincrypto.com/learn/blockchain-oracle/)，允许其他 DeFi 协议访问基于价格的实时信息。

## 跨链交易


几个流行的跨链做市商，如 Synapse 协议、THORChain、任 协议等，允许用户跨链交换代币。**此功能使 AMM 适合用作跨链桥。**

## 资产创建

AMM 也非常适合创建资产，前提是您能找到合适的 AMM。Synthetix 之类的应用程序可以通过模仿现实世界的资产来帮助创建合成资产。

做市空间已经显着成熟，**Uniswap V4** 和 **Curve V2** 等较新的协议引领市场。此外，**ZK-Rollups** 和 **Optimistic Rollups** 已成为首选的扩展解决方案，许多 AMM 过渡到这些 Rollup 以提高效率并降低成本。

# AMM 的好处和风险是什么？

以下是快速列出的好处和风险，它们抓住了自动做市商的真正本质：


| Benefits 好处                   | Risks 风险                                                                                               |
| ----------------------------- | ------------------------------------------------------------------------------------------------------ |
| **无需许可**：无需中介或集中控制。           | **Impermanent loss**: Risk of assets losing value within the pool.  <br>**无常损失**：资产池内资产贬值的风险。          |
| **没有订单簿复杂性**：自动价格发现和交易。       | **智能合约漏洞**：代码中可能存在[的安全](https://beincrypto.com/learn/top10-must-have-cryptocurrency-security-tips/)问题。 |
| **流动性提供者的奖励**：通过提供流动性赚取费用和奖励。 | **高昂的 gas 费用**：交易可能很昂贵，尤其是在拥塞的网络上。                                                                     |
| **透明度**：在具有明确规则的开源智能合约上运行。    | **监管风险**：全球监管机构的审查日益严格。                                                                                |
| **价格效率**： 确保通过数学方程式进行适当的价格发现。 | **低流动性风险**：可能导致[滑点](https://beincrypto.com/learn/what-is-slippage-in-crypto/)和更高的交易成本                  |
| **互操作性**：支持跨链交互和交易。           | **波动性风险**：加密货币市场的波动性会影响矿池价值。                                                                           |

# 下一代 AMM？

**Velodrome** 和 **Radiant Capital** 等 AMM 通过引入动态费用和直观的流动性激励等新颖机制，树立了新的行业标准。此外，**DeFi 3.0** 的兴起导致了更可持续和资本效率更高的 AMM 的发展，专注于降低无常损失等风险。一些 AMM 现在正在整合 **AI 驱动的算法**来优化流动性池并改善交易结果，这代表了去中心化金融的前沿。

# AMM 的未来之路

自动做市商正在通过将流动性注入生态系统来改变 DeFi，从而简化加密交易。它们还支持套利交易、流动性挖矿等。**尽管 AMM 的潜力仍未得到充分开发，但它们已准备好推动 DeFi 的创新，包括新的金融资产和增强的 DEX。**随着 NFT 和虚拟做市商的出现，未来 AMM 将进一步扩展到贷款、保险和实物资产等领域。

# 参考

恒定乘积如何自动化做市商：[bilibili.com](https://www.bilibili.com/video/BV1FG411w7bm/?spm_id_from=333.337.search-card.all.click)  [youtube.com](https://www.youtube.com/c/WhiteboardCrypto)

什么是自动做市商？[coindesk.com](https://www.coindesk.com/learn/what-is-an-automated-market-maker/)

什么是自动做市商 （AMM）？[gemini.com](https://www.gemini.com/cryptopedia/amm-what-are-automated-market-makers)

什么是自动做市商 （AMM）？[beincrypto.com](https://beincrypto.com/learn/amm-explained/)

什么是自动做市商？[phemex.com](https://phemex.com/academy/what-is-an-automated-market-maker-amm)

什么是 DeFi 中的 AMM（自动做市商）：[whitebit](https://blog.whitebit.com/en/what-is-amm-automated-market-makers-in-defi/)

自动做市商 （AMM）：促进 DeFi 交易：[coingecko.com](https://www.coingecko.com/learn/what-is-an-automated-market-maker-amm)

AMM解释：自动化做市商及其运作方式：[learncrypto.com](https://learncrypto.com/knowledge-base/basics/amm-explained-automated-market-makers-how-they-work)

什么是自动做市商，它们如何运作？AMM 101：[testycrypto.com]https://www.tastycrypto.com/defi/automated-market-maker/
