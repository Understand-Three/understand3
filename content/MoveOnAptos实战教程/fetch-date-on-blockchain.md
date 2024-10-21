---
title: 获取链上数据
aliases:
  - 获取链上数据
tags:
  - aptos
---
# TypeScript

## 使用 indexer
```ts
const fetchBalance = useCallback(async () => {
    const config = new AptosConfig({ network: Network.TESTNET })
    const aptos = new Aptos(config)
    // console.log('获取余额: ', account?.address)
    if (!account?.address) return

	// indexer 对象
    const variablesObj = {
      address: account.address,
      offset: 0,
    }

	// indexer 的查询语句
    const query_syntax = `query GetFungibleAssetBalances($address: String, $offset: Int) {
    current_fungible_asset_balances(
      where: {owner_address: {_eq: $address}},
      offset: $offset,
      limit: 100,
      order_by: {amount: desc}
    ) {
      asset_type
      amount
      __typename
    }
  }`

    try {
      const response = await aptos.queryIndexer({
        query: {
          query: query_syntax,
          variables: variablesObj,
        },
      })
      const amountOriginal = (response as ResponseBalanceType)
        .current_fungible_asset_balances[0].amount
      const amount = new BigNumber(amountOriginal)
      // console.log('the response is ', amount)
      const factor = new BigNumber(10).pow(8)
      setBalance(amount.dividedBy(factor).toString())
    } catch (error) {
      console.error('fetchBalance error', error)
    }
},[account]);
```