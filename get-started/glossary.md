---
id: glossary
title: Glossary
description: Common terms for the Uniswap protocol, its AMM design, permissionless architecture, and protocol versions.
---

## Common Terms

There are a few terms used throughout these documents which are helpful to understand:

- **Uniswap Protocols** refers to the pools of liquidity created through [protocol smart contracts](/docs/protocols/v4/overview). These are sometimes referred to as **v2**, **v3**, and **v4** pools. (v1 is not supported by the APIs.) In rare instances these protocols collectively are called **Classic**.

- **UniswapX** refers to the intent-based RFQ swap mechanism. UniswapX has two versions: **UniswapX_V2** and **UniswapX_V3**. In API responses, the `routing` field will return **DUTCH_V2** or **DUTCH_V3** (respectively) for UniswapX quotes. Additionally, on Base and Unichain chains, the `routing` field may return **PRIORITY** for UniswapX_V2 quotes.

- **Permit2** is a smart contract which simplifies sharing and managing token approvals. [All Uniswap workflows utilize Permit2](/guides/permit2), with Uniswap Protocols taking advantage of the AllowanceTransfer properties of Permit2 and UniswapX taking advantage of the SignatureTransfer properties of Permit2. In short, users sign Permit2 messages which allow the Permit2 contract to spend tokens from the user's wallet. Permit2 messages can include permissions including limiting spending to one transaction, to a time window, and to a specific amount of tokens. [Click here to read a more detailed explanation of how Permit2 works](https://github.com/dragonfly-xyz/useful-solidity-patterns/tree/main/patterns/permit2).


## Core Protocol Concepts

- An **Automated Market Maker (AMM)** is a smart contract on Ethereum that holds liquidity reserves. Users can trade against these reserves at prices determined by a fixed formula. Anyone may contribute liquidity to these smart contracts, earning pro-rata trading fees in return.

- The **Constant Product Formula** is the automated market making algorithm used by Uniswap. In v1 and v2, this was x\*y=k and the **invariant** is the “k” value in the constant product formula x\*y=k

- A **Pool** is a contract deployed by the v4 factory that pairs two ERC-20 assets. Different pools may have different fees despite containing the same token pair. Pools were previously called Pairs before the introduction of multiple fee options.

- **Liquidity** are digital assets that are stored in a Uniswap pool contract, and are able to be traded against by traders.

- **Liquidity Provider (LP)** is someone who deposits ERC20 tokens into a given liquidity pool. Liquidity providers take on price risk and are compensated with trading fees.

- **Concentrated Liquidity** is liquidity that is allocated within a determined price range. 

- **Position** is an instance of liquidity defined by upper and lower tick. And the amount of liquidity contained therein.

- **Swap** is the act of exchanging one token for another through a liquidity pool.

- **Swap Fees** are the fees collected upon swapping which are rewarded to liquidity providers.

- **Protocol Fees** are the fees that are rewarded to the protocol itself, rather than to liquidity providers.

- **Price Impact** is the difference between the mid-price and the execution price **caused by your trade size relative to the pool’s liquidity**. This is an expected result of the constant product formula in AMMs.

- **Slippage** is the total difference between the expected price at the time of submitting a transaction and the actual execution price, which may include price impact and other market movements that occur before the transaction is mined.

- **Impermanent Loss** is the opportunity cost experienced by liquidity providers when token prices change relative to simply holding the tokens.

- **Tick** is the boundaries between discrete areas in price space. And **Tick Interval** the price space between two nearest ticks.

- **Range** is any interval between two ticks of any distance. And **Range Order** is an approximation of a limit order, in which a single asset is provided as liquidity across a specified range, and is continuously swapped to the destination address as the spot price crosses the range.

- **Reserves** is the liquidity available within a pair. This was more commonly referenced before concentrated liquidity was introduced.

## Smart Contract Architecture

- [**Core Contracts**](https://github.com/Uniswap/v4-core) are smart contracts that are considered foundational, and are essential for Uniswap to exist. Upgrading to a new version of core would require deploying an entirely new set of smart contracts on Ethereum and would be considered a new version of the Uniswap Protocol.

- [**Periphery Contracts**](https://github.com/Uniswap/v4-periphery) are external smart contracts that simplify interactions with the protocol (e.g., routers and position managers).

- [**Universal Router**](https://github.com/Uniswap/universal-router) is a routing contract that enables complex, multi-step token operations across different Uniswap systems in a single transaction.

- **Factory** is a smart contract that deploys a unique smart contract for any ERC20/ERC20 trading pair.


## Uniswap v4 Concepts

- **Singleton Architecture** is a design introduced in v4 where all pools are managed within a single contract, reducing deployment costs and enabling advanced composability.

- **PoolManager** is the central contract in v4 responsible for managing all pools within the singleton architecture.

- **Hooks** are customizable smart contracts that executes logic before or after pool actions such as swaps or liquidity modifications. 

- **Flash Accounting** is a v4 mechanism that allows temporary token imbalances within a transaction, provided all balances settle correctly by the end of execution.

## Token Standards

- **ERC-20** is a standar for fungible tokens on Ethereum. Uniswap supports all standard ERC20 implementations.

- **ERC-721** is a standard for non-fungible tokens. In v3 and v4, liquidity positions are represented as ERC-721 NFTs.

- **ERC-6909** is a multi-token standard used in v4 to represent internal claims within the singleton architecture.

## Trading Infrastructure

- **Flash Swap** is a swap where tokens are received before repayment, provided the borrowed tokens are returned within the same transaction.

- **Routing** in API responses, the `routing` field describes the execution mechanism used for a quote, such as Classic pools or UniswapX Dutch auctions.

## Ecosystem Terms

- **Unichain** is an EVM-compatible chain designed to support high-performance DeFi applications and Uniswap-native infrastructure.

- **UNI Token** it the governance token that enables participation in Uniswap governance decisions.



