---
title: Hash 算法与数字摘要
aliases:
  - Hash 算法与数字摘要
draft: true
---


## 定义

Hash（哈希或散列）算法，又常被称为指纹（fingerprint）或摘要（digest）算法，是非常基础也非常重要的一类算法。可以将任意长度的二进制明文串映射为较短的（通常是固定长度的）二进制串（Hash 值），并且不同的明文很难映射为相同的 Hash 值。

例如计算 “hello blockchain world, this is yeasy@github” 的 SHA-256 Hash 值。


```bash
$ echo "hello blockchain world, this is yeasy@github"|shasum -a 256
db8305d71a9f2f90a3e118a9b49a4c381d2b80cf7bcef81930f30ab1832a3c90
```

对于某个文件，无需查看其内容，只要其 SHA-256 Hash 计算后结果同样为 `db8305d71a9f2f90a3e118a9b49a4c381d2b80cf7bcef81930f30ab1832a3c90`，则说明文件内容（极大的概率）就是 “hello blockchain world, this is yeasy@github”。

除了快速对比内容外，Hash 思想也经常被应用到基于内容的编址或命名算法中。

一个优秀的 Hash 算法，将能满足：

- 正向快速：给定原文和 Hash 算法，在有限时间和有限资源内能计算得到 Hash 值；

- 逆向困难：给定（若干）Hash 值，在有限时间内无法（基本不可能）逆推出原文；

- 输入敏感：原始输入信息发生任何改变，新产生的 Hash 值都应该发生很大变化；

- 碰撞避免：很难找到两段内容不同的明文，使得它们的 Hash 值一致（即发生碰撞）。

碰撞避免有时候又被称为“抗碰撞性”，可分为“弱抗碰撞性”和“强抗碰撞性”。给定原文前提下，无法找到与之碰撞的其它原文，则算法具有“弱抗碰撞性”；更一般地，如果无法找到任意两个可碰撞的原文，则称算法具有“强抗碰撞性”。

很多场景下，也往往要求算法对于任意长的输入内容，输出为定长的 Hash 结果。

## 常见算法

目前常见的 Hash 算法包括国际上的 Message Digest（MD）系列和 Secure Hash Algorithm（SHA）系列算法，以及国内的 SM3 算法。

MD 算法主要包括 MD4 和 MD5 两个算法。MD4（RFC 1320）是 MIT 的 Ronald L. Rivest 在 1990 年设计的，其输出为 128 位。MD4 已证明不够安全。MD5（RFC 1321）是 Rivest 于 1991 年对 MD4 的改进版本。它对输入仍以 512 位进行分组，其输出是 128 位。MD5 比 MD4 更加安全，但过程更加复杂，计算速度要慢一点。MD5 已于 2004 年被成功碰撞，其安全性已不足应用于商业场景。

SHA 算法由美国国家标准与技术院（National Institute of Standards and Technology，NIST）征集制定。首个实现 SHA-0 算法于 1993 年问世，1998 年即遭破解。随后的修订版本 SHA-1 算法在 1995 年面世，它的输出为长度 160 位的 Hash 值，安全性更好。SHA-1 设计采用了 MD4 算法类似原理。SHA-1 已于 2005 年被成功碰撞，意味着无法满足商用需求。

为了提高安全性，NIST 后来制定出更安全的 SHA-224、SHA-256、SHA-384 和 SHA-512 算法（统称为 SHA-2 算法）。新一代的 SHA-3 相关算法也正在研究中。

此外，中国密码管理局于 2010 年 12 月 17 日发布了 GM/T 0004-2012 《SM3 密码杂凑算法》，建立了国内商用密码体系中的公开 Hash 算法标准，已经被广泛应用在数字签名和认证等场景中。

*注：MD5 和 SHA-1 算法的破解工作都是由清华大学教授、中国科学院院士王小云主导完成。*

## 性能

大多数 Hash 算法都是计算敏感型算法，在强大的计算芯片上完成得更快。因此要提升 Hash 计算的性能可以考虑硬件加速。例如采用普通 FPGA 来计算 SHA-256 值，可以轻易达到数 Gbps 的吞吐量，使用专用芯片吞吐量甚至会更高。

也有一些 Hash 算法不是计算敏感型的。例如 scrypt 算法，计算过程需要大量的内存资源，因此很难通过选用高性能芯片来加速 Hash 计算。这样的算法可以有效防范采用专用芯片进行算力攻击。

## 数字摘要

数字摘要是 Hash 算法重要用途之一。顾名思义，数字摘要是对原始的数字内容进行 Hash 运算，获取唯一的摘要值。

利用 Hash 函数抗碰撞性特点，数字摘要可以检测内容是否被篡改过。

细心的读者可能会注意到，有些网站在提供文件下载时，会同时提供相应的数字摘要值。用户下载原始文件后可以在本地自行计算摘要值，并与所提供摘要值进行比对，以确保文件内容没有被篡改过。

## Hash 攻击与防护

Hash 算法并不是一种加密算法，不能用于对信息的保护。

但 Hash 算法可被应用到对登录口令的保存上。例如网站登录时需要验证用户名和密码，如果网站后台直接保存用户的口令原文，一旦发生数据库泄露后果不堪设想（事实上，网站数据库泄露事件在国内外都不少见）。

利用 Hash 的防碰撞特性，后台数据库可以仅保存用户口令的 Hash 值，这样每次通过 Hash 值比对，即可判断输入口令是否正确。即便数据库泄露了，攻击者也无法轻易从 Hash 值还原出口令。

然而，有时用户设置口令的安全强度不够，采用了一些常见的字符串，如 password、123456 等。有人专门搜集了这些常见口令，计算对应的 Hash 值，制作成字典。这样通过 Hash 值可以快速反查到原始口令。这一类型以空间换时间的攻击方法包括字典攻击和彩虹表攻击（只保存一条 Hash 链的首尾值，相对字典攻击可以节省存储空间）等。

为了防范这一类攻击，可以采用加盐（Salt）的方法。保存的不是原文的直接 Hash 值，而是原文再加上一段随机字符串（即“盐”）之后的 Hash 值。Hash 结果和“盐”分别存放在不同的地方，这样只要不是两者同时泄露，攻击者就很难进行破解。