---
title: 解读：区块链世界的路径依赖
draft: true
---
# 解读：区块链世界的路径依赖


路径依赖（Path－Dependence），它的特定含义是指人类社会中的技术演进或制度变迁均有类似于物理学中的惯性，即一旦进入某一路径（无论是“好”还是“坏”）就可能对这种路径产生依赖。一旦人们做了某种选择，就好比走上了一条不归之路，惯性的力量会使这一选择不断自我强化，并让你轻易走不出去。第一个使“路径依赖”理论声名远播的是道格拉斯·诺思，由于用“路径依赖”理论成功地阐释了经济制度的演进，道格拉斯·诺思于1993年获得诺贝尔经济学奖。

任何一项技术的发展，在历史上永远是路径依赖的。依据路径依赖的原理我们可以 **追溯一个事物的前生，理解它的今世，预测它的未来** 。如果从路径依赖的角度，不能找到一个事物的前生，大概率这个事物是个骗局，或者我们没有理解这个事物的本质。

区块链的产生是多种技术发展的必然结果，它也会符合路径依赖的理论。与区块链产生直接相关的知识领域，很多可以追溯到几十年以前。用我在《区块链经济模型》有一句重要的总结： **共识算法是区块链的灵魂，加密算法是区块链的骨骼，经济模型是区块链的核能** 。这三个方面的主要发展，决定着区块链的产生与未来。我会发现这三方面的发展居然都起源于1976年前后。

![img](file:///C:/Users/tomcat/AppData/Local/Temp/ksohtml43672/wps2.png)

**密码学领域** ：1976年，Bailey W. Diffie，Martin E. Hellman两位密码学的大师发表了论文《密码学的新方向》。论文覆盖了未来几十年密码学所有的新的进展领域，包括非对称加密、椭圆曲线算法、哈希等一些手段，奠定了迄今为止整个密码学的发展方向，对区块链的技术和比特币的诞生起到决定性作用。（注：左边那位就是Hellman，右边那位就是Diffie。）

![[../Images/Pasted image 20240826172517.png]]

1977年由美国麻省理工学院MIT（Massachusetts Institute of Technology）的Ronal Rivest，Adi Shamir和Len Adleman三位年轻教授提出，并以三人的姓氏Rivest，Shamir和Adlernan命名为RSA算法。该算法利用了数论领域的一个事实，那就是虽然把两个大质数相乘生成一个合数是件十分容易的事情，但要把一个合数分解为两个质数却十分困难。合数分解问题目前仍然是数学领域尚未解决的一大难题，至今没有任何高效的分解方法。与Diffie-Hellman算法相比，RSA算法具有明显的优越性，因为它无须收发双方同时参与加密过程，且非常适合于计算机信息的加密。

1980年，Merkle Ralf提出了Merkle-Tree这种数据结构和相应的算法，后来的主要用途之一是分布式网络中数据同步正确性的校验，这也是比特币中引入用来做区块同步校验的重要手段。

1982年，Lamport提出拜占廷将军问题，标志着分布式计算的可靠性理论和实践进入到了实质性阶段。同年，大卫·乔姆提出了密码学支付系统ECash，可以看出，随着密码学的进展，眼光敏锐的人已经开始尝试将其运用到货币、支付相关的领域了，应该说ECash是密码学货币最早的先驱之一。

1985年，Koblitz和Miller各自独立提出了著名的椭圆曲线加密（ECC）算法。由于此前发明的RSA的算法计算量过大很难实用，ECC的提出才真正使得非对称加密体系产生了实用的可能。因此，可以说到了1985年，也就是《密码学的新方向》发表10年左右的时候，现代密码学的理论和技术基础已经完全确立了。

**经济学领域** ：哈耶克的《货币的非国家化》在1976年出版，但并未在当时的经济学界引起多少反响。《货币的非国家化》主要从政府垄断铸币的起源，讲到政府垄断权一直遭到滥用，提出了让私人发行的货币流通起来，让这些不同的货币产生竞争。在全书中虽然很多观点，用传统经济学的理论衡量起来有非常多的问题，存在难以实现的可能性。但其中的一些观点有重要的价值。2009年比特币的诞生，使人们突然发现，这种新型的加密货币正在实现哈耶克当年的设想——私人货币。

![[../Images/Pasted image 20240826172529.png]]
经济学家哈耶克

弗里德里希·奥古斯特·冯·哈耶克(Friedrich August von Hayek，1899年5月8日—1992年3月23日），是奥地利出生的英国知名经济学家和政治哲学家。以坚持自由市场资本主义、反对社会主义、凯恩斯主义和集体主义而著称。他被广泛视为是奥地利经济学派最重要的成员之一，他对于法学和认知科学领域也有相当重要的贡献。哈耶克在1974年和他理论的对手纲纳·缪达尔（Gunnar Myrdal）一同获得了诺贝尔经济学奖，以“表扬他们在货币政策和商业周期上的开创性研究，以及他们对于经济、社会和制度互动影响的敏锐分析。”在1991年，哈耶克获颁美国总统自由勋章，以表扬他“终身的高瞻远瞩”。

**信息技术领域** ：计算机技术的发展为信息技术提供了坚实的基础。其中网络技术，分布式技术是将单个计算机连接起来，协同工作的两项重要技术。1969年，ARPAnet投入使用成为现代计算机网络诞生的标志。其中协同工作的主要理论方面是拜占庭将军问题（Byzantine Generals Problem），由莱斯利·兰波特于1982年在其同名论文《The Byzantine Generals Problem》中提出的分布式对等网络通信容错问题，对网络中存在作恶节点的情况进行建模。拜占庭将军问题并不是现实中存在的问题，是一个虚构场景。拜占庭是古代东罗马帝国的首都，由于地域宽广，假设其守卫边境的多个将军（系统中的多个节点）需要通过信使来传递消息，达成某些一致决定。由于作恶节点的存在，拜占庭将军问题被认为是容错性问题中最难的问题类型之一。

![[../Images/Pasted image 20240826172601.png]]

拜占庭问题之前，学术界就已经存在两将军问题的讨论（《Some constraints and trade offs in the design of network communications》，1975年）：两个将军要通过信使来达成进攻还是撤退的约定，但信使可能迷路或被敌军阻拦（消息丢失或伪造），如何达成一致，根据FLP不可能原理，这个问题无通用解。

通过对区块链中重要的三个方面（密码学、经济学、信息技术）分析，我们会发现，在数十年前，一个新事物发展的基础原理，已经开始形成与孕育。让人意外的是，这三个重要方面的理论支撑居然都是在同一时期产生的（1976和1975）.

