---
id: hooks
title: Hooks
description: Discover Uniswap v4 hooks and how custom smart contract logic extends pool behavior.
---

## Introduction

Uniswap v4 keeps concentrated liquidity from Uniswap v3 and adds a hook system and singleton architecture. Together, these changes expand pool customization and improve execution efficiency.

## How Hooks Work

Hooks are external smart contracts attached to pools. They let developers customize pool behavior by running logic before and/or after core actions.

Hook callbacks can run around major operations such as pool initialization, liquidity changes, swaps, and donations.

Hooks can be used to build features such as custom pricing logic, dynamic fee strategies, custom oracle behavior, and advanced order mechanics. Hooks are optional, set at pool creation, and one hook contract can serve multiple pools.

## Singleton Architecture

The hook system in v4 is built on singleton architecture. Unlike previous versions where each pool was a separate smart contract, v4 manages pools through a single contract: [`PoolManager`](/docs/protocols/v4/concepts/poolmanager). This design enables:

- **Efficient Pool Creation**: Pools are created as state updates rather than contract deployments, significantly reducing gas costs
- **Gas Optimization**: Multi-hop swaps and complex operations are streamlined through a single contract
- **Flash Accounting**: Token balances are tracked internally and settled at the end of transactions, minimizing transfers
- **Native ETH Support**: Direct ETH trading without the need to wrap to WETH, improving user experience

These core features are just the beginning of what's possible with Uniswap v4.

To explore flash accounting, native ETH support, dynamic fees, and custom accounting in depth, see the [v4 whitepaper](https://uniswap.org/whitepaper-v4.pdf).

For technical implementations and detailed guides, visit the [v4 documentation](/docs/protocols/v4/overview).
