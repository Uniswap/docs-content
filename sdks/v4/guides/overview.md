---
title: Guides Overview
description: Step-by-step guides for working with the Uniswap v4 SDK.
---

# v4 SDK Guides

These guides walk you through common operations with the Uniswap v4 SDK, from executing swaps to managing liquidity positions. Each guide includes working code examples using `@uniswap/v4-sdk` and `@uniswap/sdk-core`.

If you haven't already, install the SDK:

```bash
npm i --save @uniswap/v4-sdk
npm i --save @uniswap/sdk-core
```

For a broader look at what changed in v4 and why, see the [v4 SDK Overview](../overview).

## Swapping

Learn how to execute swaps through the Universal Router using v4Planner.

- [Getting a Quote](./swapping/quoting) -- Fetch a price quote for a token pair
- [Executing a Single-Hop Swap](./swapping/single-hop-swapping) -- Swap between two tokens in a single pool
- [Executing Multi-Hop Swaps](./swapping/multi-hop-swapping) -- Route a swap through multiple pools

## Managing Liquidity

Understand position lifecycle: minting, modifying, and collecting fees.

- [Minting a Position](./managing-liquidity/position-minting) -- Create a new concentrated liquidity position
- [Fetching Positions](./managing-liquidity/position-fetching) -- Retrieve position data via off-chain indexing
- [Collecting Fees](./managing-liquidity/collect-fees) -- Collect accrued fees from your positions
- [Modifying a Position](./managing-liquidity/modifying-position) -- Add or remove liquidity from an existing position

## Advanced

Explore pool state queries and pool creation with the singleton architecture.

- [Fetching Pool Data](./pool-data) -- Read pool state through the StateView contract
- [Create Pool](./create-pool) -- Deploy a new v4 pool
