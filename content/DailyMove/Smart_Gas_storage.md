---
title: 聪明的 Gas 存储
aliases:
  - Smart 的作用
---
```yaml
original: 
  author: Greg
  url: https://x.com/Greg_Nazario/status/1760809623194677725
note: 已校对-simons
```


# 中文

你是否曾经想知道在Aptos中的向量（Vector）、表（Table）、SimpleMap等之间有什么区别？

让我们通过一个关于大家最喜欢的NFT话题WL（白名单）的快速比较代码来了解。跟随本期的 #DailyMove

在大多数语言中，向量（Vector）最类似于可调整大小的数组（Array）。

它们是通过索引进行检索的，通过索引的 $O(1)$ 查找，通过值的 $O(n)$ 查找；然而，这里涉及到一个最大的大小限制。大小有一个上限，当接近这个大小时，Gas 费会变得昂贵。

对于 WL 示例，这对于单个存储插槽中的**小**列表非常有效。在搜索和添加或移除方面，小列表的 Gas 成本最低。

尽管如此，要为一个地址拥有多个 WL，您需要多次提交它。并且没有任何机制阻止您多次输入 WL 地址。这在大规模铸币方面不太适用。

您可以在此处查看源代码，包括一些模拟的 Gas 数字。

[allowlist_vector.move](https://github.com/aptos-labs/daily-move/blob/main/snippets/storage/sources/allowlist_vector.move)

![https://pbs.twimg.com/media/GG-c-XFaAAAtKbk?format=png&name=small](https://pbs.twimg.com/media/GG-c-XFaAAAtKbk?format=png&name=small)

但是，如果您想使用一个长列表，比如有 $100,000$ 个项目呢？

SmartVector 通过在存储槽（slots）中进行分桶（bucketed），以提供存储更多数据的能力。这种存储方式将其直接分离到区块链存储槽的不同位置，一旦数据超过一定大小，它就会创建一个新的存储槽。

所有属性与向量完全相同，但是一些与整个列表交互的操作可能在 Gas 方面会非常昂贵。

[allowlist_smart_vector.move](https://github.com/aptos-labs/daily-move/blob/main/snippets/storage/sources/allowlist_smart_vector.move)

![https://pbs.twimg.com/media/GG-dalAaYAA2EVK?format=png&name=small](https://pbs.twimg.com/media/GG-dalAaYAA2EVK?format=png&name=small)

让我们简化这个过程，将地址移到 SimpleMap 中，以便我们可以支持多个 WL 存储槽。

SimpleMap 是直接放入 Vector 中的映射，并且具有 Vector 的所有优点和缺点。结果是不排序的，因此所有查找、插入和删除都是 $O(n)$。

它的优点是确保地址的唯一性，并允许每个地址有多个 WL 存储槽。

这是处理较大数据集的成本最高的方法，因为每次查找都必须**遍历**整个映射。

[allowlist_simple_map.move](https://github.com/aptos-labs/daily-move/blob/main/snippets/storage/sources/allowlist_simple_map.move)

![https://pbs.twimg.com/media/GG-ftX7aYAAA0-3?format=png&name=small](https://pbs.twimg.com/media/GG-ftX7aYAAA0-3?format=png&name=small)

那么，如果我的 WL 中有 $100,000$ 个地址怎么办？SimpleMap 行不通，可以使用表（Table）。

Table 为 Table 中的每个项目使用存储槽。在这种情况下，我们使用地址作为键（key），因此查找过程非常快速且 Gas 便宜 $O(1)$，但是添加和构建 WL 的成本是最高的。

当然，直到我们找到最喜欢的数据结构来替换它们前，这对于非常大规模的项目很有用，

它的缺点是 WL 的大小不会被跟踪，并且不能轻松地对所有项目进行迭代。

[allowlist_table.move](https://github.com/aptos-labs/daily-move/blob/main/snippets/storage/sources/allowlist_table.move)

![https://pbs.twimg.com/media/GG-hgsya0AA2xXd?format=png&name=small](https://pbs.twimg.com/media/GG-hgsya0AA2xXd?format=png&name=small)

欢迎使用SmartTable。SmartTable 是一个包含所有 Key 的桶状表。

与SmartVector类似，它在表存储槽中使用向量，以获得两全其美的效果。查找是O(bucket_size)，插入是O（bucket_size）。

这意味着对于非常大的数据集，操作是恒定时间的，并且可以轻松扩展。它提供了灵活性，并且是最接近 Map 的东西，并且提供了迭代。

在我的所有示例中，我都使用 SmartTable，因为它具有灵活性、高效率和简单性。

[allowlist_smart_table.move](https://github.com/aptos-labs/daily-move/blob/main/snippets/storage/sources/allowlist_smart_table.move)


![https://pbs.twimg.com/media/GG-iPLYbYAA6c9w?format=png&name=small](https://pbs.twimg.com/media/GG-iPLYbYAA6c9w?format=png&name=small)

但是，数字呢？那些感兴趣的人可以运行更大的数据集，但我运行了一些本地数据。


以下数字来自本地测试网上按顺序 `[0x1,0x2,...0x125]` 和与之对应的递增数字 `[1,1,1...]`（293项）。

创建 WL 对象时，我们发现 SmartTable 实际上存储了一些额外的数据：

- Vector：0.000504 APT
- SmartVector：0.000504 APT
- SimpleMap：0.000504 APT
- Table：0.000504 APT
- SmartTable：0.001505 APT

添加 293 个地址后，我们发现表创建了大量的存储槽，并且成本很高。而 SmartTable 实际上成本更低：

- Vector：0.00006193 APT
- SmartVector 0.00007042 APT
- SimpleMap：0.00006957 APT
- Table：0.00149538 APT
- SmartTable：0.00009723 APT

查找 293 个地址，我们可以看到通过值在 SmartTable 上的查找成本要便宜得多。

- Vector：0.00002268 APT
- SmartVector：0.00005354 APT
- SimpleMap：0.00002361 APT
- Table：0.00002090 APT
- SmartTable：0.00001963 APT

因此，你可能会问为什么 Gas 差异如此之大？

Gas 计算基于存储成本和执行成本，对于这些存储决策有复杂的权衡。

此外，您实际上可以调整 SmartTable 和 SmartVector 的桶大小，这可以帮助满足您的特定需求。

感谢阅读本期关于存储的[#DailyMove](https://twitter.com/hashtag/DailyMove?src=hashtag_click)。在您的合约使用了太多的燃气或不合适地扩展之前，请在这里查看一下。

---

# English

Ever wonder what's the difference between vector, Table, SimpleMap, and others on Aptos?

Let's go through a quick comparison code for everyone's favorite NFT topic, WLs.

Follow along on this episode of

[#DailyMove](https://twitter.com/hashtag/DailyMove?src=hashtag_click)

Vectors are most similar to resizable arrays in most languages.

They're indexed, O(1) lookup by index O(n) lookup by value; however, there is a maximum size involved. The size has an upper bound, and gas gets expensive as it approaches this size.

For the WL example, this works well for _small_ lists in a single storage slot. The cheapest gas for small lists, in search and add / removal.

Though, to have more than one WL for an address, you'd need to submit it more than once. And there's nothing protecting you from entering the WL address more than once. This doesn't really scale well for big mints.

You can check out the source here, with some simulated gas numbers.

[](https://t.co/u9xMCFlYwA)[https://github.com/aptos-labs/daily-move/blob/main/snippets/storage/sources/allowlist_vector.move](https://github.com/aptos-labs/daily-move/blob/main/snippets/storage/sources/allowlist_vector.move)

[https://pbs.twimg.com/media/GG-c-XFaAAAtKbk?format=png&name=small](https://pbs.twimg.com/media/GG-c-XFaAAAtKbk?format=png&name=small)

But, what if you want to use a long list, say 100,000 items in it?

SmartVector provides the ability to store a greater amount of data by bucketing it across storage slots. This storage separates it into different locations in the blockchain storage slots directly, once it goes over a certain size, it'll create a new slot.

All properties are exactly the same as vector, but some operations that interact with the whole list, may be very expensive in gas.

[](https://t.co/sJ1gUSSlL5)[https://github.com/aptos-labs/daily-move/blob/main/snippets/storage/sources/allowlist_smart_vector.move](https://github.com/aptos-labs/daily-move/blob/main/snippets/storage/sources/allowlist_smart_vector.move)

[https://pbs.twimg.com/media/GG-dalAaYAA2EVK?format=png&name=small](https://pbs.twimg.com/media/GG-dalAaYAA2EVK?format=png&name=small)

Let's simplify the process, by moving the addresses to a SimpleMap, so we can support multiple WL slots.

The SimpleMap is a mapping put into a vector directly and has all the benefits and downsides of the vector. The results are not sorted, so all lookups, insertions, and deletions are O(n).

It does have the advantage of ensuring uniqueness of the addresses, and allowing there to be a number of WL slots per address.

This is by far the most gas costly way to handle larger data sets as each lookup must _traverse_ _the whole_ map.

[](https://t.co/DFcXH0S48C)[https://github.com/aptos-labs/daily-move/blob/main/snippets/storage/sources/allowlist_simple_map.move](https://github.com/aptos-labs/daily-move/blob/main/snippets/storage/sources/allowlist_simple_map.move)

[https://pbs.twimg.com/media/GG-ftX7aYAAA0-3?format=png&name=small](https://pbs.twimg.com/media/GG-ftX7aYAAA0-3?format=png&name=small)

So, what if I have 100,000 addresses in my WL? A SimpleMap won't cut it, so a Table can be used instead.

A Table uses storage slots for each item in the table. In this case, we use the address as the key, so lookups are very fast and cheap O(1), but the costs of adding and building the WL are the highest of them all.

This can be useful for very high scale items, until of course we come to our favorite data structure to replace them all.

It comes with the downside that, the size of the WL is not tracked, and it can't be iterated over all the items easily.

[](https://t.co/NAS54zK0Bg)[https://github.com/aptos-labs/daily-move/blob/main/snippets/storage/sources/allowlist_table.move](https://github.com/aptos-labs/daily-move/blob/main/snippets/storage/sources/allowlist_table.move)

[https://pbs.twimg.com/media/GG-hgsya0AA2xXd?format=png&name=small](https://pbs.twimg.com/media/GG-hgsya0AA2xXd?format=png&name=small)

Welcome the SmartTable. SmartTable is a bucketed table of all the keys.

Similar to the SmartVector, it uses vectors in table storage slots, to get the best of both worlds. Lookups are O(bucket_size), Insertions are O(bucket_size).

This means for very large data sets, the operations are constant time, and can scale easily. It provides the flexibility and closest thing to a map that you can get, and it provides iteration.

All of my examples, I use SmartTables because of this flexibility, gas efficiency, and because of the simplicity associated.

[](https://t.co/kIsa52VS4T)[https://github.com/aptos-labs/daily-move/blob/main/snippets/storage/sources/allowlist_smart_table.move](https://github.com/aptos-labs/daily-move/blob/main/snippets/storage/sources/allowlist_smart_table.move)

[https://pbs.twimg.com/media/GG-iPLYbYAA6c9w?format=png&name=small](https://pbs.twimg.com/media/GG-iPLYbYAA6c9w?format=png&name=small)

But, what about the numbers. Those interested can run larger data sets, but I ran some local numbers with what I could get going.

The following numbers came from in-order [0x1,0x2,...0x125] and incrementing numbers that go with them [1,1,1...] (293 items) on a local testnet.

Creating the WL object, we see that SmartTable actually stores some extra data:

- vector: 0.000504 APT
- SmartVector: 0.000504 APT
- SimpleMap: 0.000504 APT
- Table: 0.000504 APT
- SmartTable: 0.001505 APT

Adding 293 addresses, we see that Tables create a lot of storage slots, and cost a lot more. While SmartTable actually costs less:

- vector: 0.00006193 APT
- SmartVector 0.00007042 APT
- SimpleMap: 0.00006957 APT
- Table: 0.00149538 APT
- SmartTable: 0.00009723 APT

Lookup of 293 adddresses, we can see here lookups can be much cheaper on the SmartTable by value.

- vector: 0.00002268 APT
- SmartVector: 0.00005354 APT
- SimpleMap: 0.00002361 APT
- Table: 0.00002090 APT
- SmartTable: 0.00001963 APT

So, you may ask why does the gas vary so much?

Gas calculations are based off of storage costs, and based on execution cost, and there are complex tradeoffs in storage decisions for these.

Additionally, you can actually tweak the bucket sizes for both the SmartTable and SmartVector, which can help for your specific needs.

Thanks for reading this episode of [#DailyMove](https://twitter.com/hashtag/DailyMove?src=hashtag_click) on storage. And before you have contracts that use too much gas or don't scale appropriately take a look here.

---
