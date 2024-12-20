---
title: 无主之地：科学
draft: true
---

[![标识](https://dnapuzzles.org/wp-content/uploads/2020/04/LogoDark.png)
# 我玩《无主之地: 科学》真的有帮助吗？


![](https://dnapuzzles.org/wp-content/uploads/2013/10/C.jpg)

# 4 月 13 日

## 这些谜题的意义何在？

目标是对齐肠道细菌的 DNA 序列。DNA 序列包含有关这些细菌的功能和祖先的重要（但隐藏）信息。在游戏中，每列都是一个序列的片段。通过对齐这些列，可以找出哪些细菌与哪些细菌相关，从而更多地了解它们的历史和功能。也就是说，如果我们知道细菌 A 的作用，并且我们通过它了解到细菌 B 是它的近亲，我们就会了解很多关于细菌 B 的信息。这项计划是在与 [加州大学圣地亚哥分校的 Microsetta 计划](https://microsetta.ucsd.edu/about/)密切协商后进行的，

## 彩色砖块代表什么？

游戏中有两种类型的砖块。您可以移动的砖块是谜题的一部分，它们代表_核苷酸_。_核苷酸_与 DNA 序列的关系就像字母与句子的关系。每种颜色代表**A**、**C**、**G**和**T**之一。您无法移动的砖块位于谜题的左侧，用于引导对齐。它们代表计算机对齐的一百万种其他细菌的共识。因此，解决谜题相当于尝试将一些序列与一百万个其他序列对齐，如果您重复多次，您将获得数百万个对齐的序列！

## 目标分数和最高分数从何而来？

高分由其他玩家获得！每个谜题都会分配给许多玩家，您看到**的**高分是其他玩家在这个谜题上获得的最高分。**目标分数**是通过解决谜题来帮助科学的基本目标。目前，您看到的目标分数有时看起来很低，是由计算机获得的。

## 玩拼图如何有助于解决问题？

比对序列的任务包括尝试匹配两个序列的_核苷酸_（一次）。对于每对核苷酸_（_每个序列一对），计算机必须决定是将这两个_核苷酸_视为“对齐”（并根据它们的匹配程度分配分数），还是要添加一个_间隙_。例如，以下是序列_**AACAG**_和_**ATAG**_的比对。_**AACAG**_ _**AT – AG**_目标是最大化正确对齐的核苷酸数量（匹配，在游戏中实现为分数），同时最小化间隙数量（在游戏中实现为黄色标记）。计算机在这项任务上并不擅长，因为为了正确评估分数和间隙之间的权衡，必须考虑其他核苷酸和其他序列的背景。截至目前，最可靠的比对是由人类手动完成的。这就是我们要求您这样做的原因！  

## 为什么不能直接使用人工智能来解决 IT 问题？

这些小对齐的问题不在于它们本质上很难，而是我们不知道如何评估它们。如果我们不知道如何评估它们，我们就无法训练人工智能来为我们解决问题，因为我们没有“基本事实”来给它。你看到的分数是为了激励你解决谜题，但事实上，我们对玩家提供的解决方案比他们获得的分数更感兴趣，

## 等一下……这听起来很难！你确定我在帮忙吗？有些谜题看起来很简单！

我们的目标是了解人类如何直观地解决简单的对齐问题，并获得大量人类解决对齐的示例。游戏不需要太难，因为我们正在寻找人类关于如何解决简单问题的意见，然后将这些方法推广到大规模问题。

## 只有当我获得高分时我的谜题才有用吗？

不！首先，对齐难以评估的原因是存在两个主要的、相互冲突的目标：增加正确对齐的_核苷酸数量，并减少__间隙_数量。这意味着在最大化得分和最小化间隙数量之间存在权衡。很难教会计算机如何评估这种权衡，但人类非常直观地理解它（基于什么_是正确的_）。此外，计算机倾向于一次比较一对行，而人类可以看到整个肖像，这是关键。  
  
换句话说，未经训练的人通常比计算机更擅长解决这个问题。这就是我们需要你的帮助的原因，这也是公民科学的关键优势所在：_不同的玩家玩法不同_。一些玩家会玩游戏直到达到目标分数，然后立即继续前进，通常不会使用所有可用的黄色令牌。这些玩家正在_最小化操作数量_，而不关心分数。其他玩家会拼命争取高分，大多数时候会用尽他们所有的间隙。这些玩家不关心使用的代币数量，而是_追求得分最大化_。而许多玩家则介于两者之间。  
这三类玩家在我们的策略中都至关重要，因为他们将向我们展示解决问题的不同方法。

## 解决同一个问题有多种方法？这样做有什么意义？

通过获取不同人对大比对的许多不同局部背景的不同思考，我们可以查看每个人的答案，看看哪些解决方案在不同情况下更受欢迎。  
这将使我们能够训练人工智能_根据大多数人认为正确_的方式对序列进行比对。这听起来很简单，但它需要大量数据，这就是为什么到目前为止从未有人这样做过。

## 你确定这会有用吗？

好吧，在公民科学中没有什么是确定的，但我们非常有信心，我们很快就会分享结果！我们在本常见问题解答中描述的假设并非完全新颖，它们过去已在其他公民科学游戏中进行过测试，即我们小组制作的  
名为**Phylo**（[游戏网站](https://phylo.cs.mcgill.ca/)）（[学术论文）的游戏。](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0031362)

## 你还没有回答我的问题！

您可以在[我们的 subreddit](https://www.reddit.com/r/dnapuzzles/)上向我们询问任何问题！



# 产品设计

记分系统

![[Pasted image 20240910092947.png]]