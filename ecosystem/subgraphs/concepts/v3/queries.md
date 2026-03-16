---
title: Queries
description: Key entities and query patterns for the Uniswap v3 subgraph.
---

The Uniswap v3 subgraph indexes on-chain events from Factory and Pool contracts and exposes them as a GraphQL API via [The Graph](https://thegraph.com/). You can use it to query pool state, swap history, token metrics, position data, and aggregated statistics.

The full schema is available in the [v3-subgraph repository](https://github.com/Uniswap/v3-subgraph/blob/main/src/v3/schema.graphql).

## Key Differences from v2

The v3 subgraph reflects the architectural changes in v3:

- **Factory replaces UniswapFactory** -- Global protocol metrics are queried from the `factory` entity. The Factory address on Ethereum mainnet is `0x1F98431c8aD98523631AE4a59f267346ea31F984`.
- **Pools are individual contracts** -- Each pool has its own contract address, used as the entity ID.
- **Concentrated liquidity** -- Positions specify `tickLower` and `tickUpper` bounds. Mint, Burn, and Collect events include tick range data.
- **Multiple fee tiers** -- Pools can have different fee tiers (0.01%, 0.05%, 0.30%, 1.00%).
- **Flash loans** -- A `Flash` entity tracks flash loan events.

## Core Entities

| Entity | Description |
|---|---|
| **Factory** | Global protocol metrics: pool count, transaction count, total volume |
| **Pool** | Individual pool state: liquidity, price, fee tier, tick, volume |
| **Token** | Token metadata and aggregated metrics across all pools |
| **Swap** | Individual swap events with amounts, sender, recipient, and transaction details |
| **Mint** | Liquidity addition events with tick range and amounts |
| **Burn** | Liquidity removal events with tick range and amounts |
| **Collect** | Fee collection events |
| **Flash** | Flash loan events |
| **PoolDayData / PoolHourData** | Time-series aggregations of pool metrics |
| **TokenDayData / TokenHourData** | Time-series aggregations of token metrics |

## Common Query Patterns

### Protocol-wide Metrics

Query the Factory entity for aggregate protocol data:

```graphql
{
  factory(id: "0x1F98431c8aD98523631AE4a59f267346ea31F984") {
    poolCount
    txCount
    totalVolumeUSD
    totalVolumeETH
  }
}
```

### Pool State

Fetch current state for a specific pool by its contract address:

```graphql
{
  pool(id: "0x8ad599c3a0ff1de082011efddc58f1908eb6e6d8") {
    token0 { symbol }
    token1 { symbol }
    feeTier
    liquidity
    sqrtPrice
    tick
  }
}
```

### Recent Swaps

Query swap events filtered by pool, ordered by recency:

```graphql
{
  swaps(orderBy: timestamp, orderDirection: desc, where: {
    pool: "0x8ad599c3a0ff1de082011efddc58f1908eb6e6d8"
  }) {
    sender
    recipient
    amount0
    amount1
    timestamp
  }
}
```

### Token Data

Aggregate metrics for a token across all v3 pools:

```graphql
{
  token(id: "0x1f9840a85d5af5bf1d1762f925bdaddc4201f984") {
    symbol
    name
    decimals
    volumeUSD
    poolCount
  }
}
```

### Position Data (Fees Collected)

Query collected fees for a position by NFT tokenId. In v3, positions are ERC-721 NFTs managed by the NonfungiblePositionManager:

```graphql
{
  position(id: 3) {
    id
    collectedFeesToken0
    collectedFeesToken1
    liquidity
    token0 { id, symbol }
    token1 { id, symbol }
  }
}
```

## Pagination

The Graph limits query results to 1000 items per request. Use `first` and `skip` to paginate through larger result sets:

```graphql
{
  pools(first: 1000, skip: 0, orderBy: liquidity, orderDirection: desc) {
    id
    token0 { symbol }
    token1 { symbol }
    liquidity
  }
}
```

Increment `skip` by 1000 in each subsequent request until fewer than 1000 results are returned.

## Historical Data

You can query data at a specific block number by passing a `block` parameter:

```graphql
{
  factory(
    id: "0x1F98431c8aD98523631AE4a59f267346ea31F984"
    block: { number: 13380584 }
  ) {
    poolCount
    totalVolumeUSD
  }
}
```

For time-series analysis, use the `PoolDayData` and `TokenDayData` entities which provide pre-aggregated daily snapshots.

## Next Steps

For complete query examples covering global data, pools, swaps, tokens, and positions, see the [v3 query examples](/docs/ecosystem/subgraphs/guides/v3-query-examples) guide.
