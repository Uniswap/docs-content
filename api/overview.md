---
id: Introduction
title: "Getting Started with Uniswap APIs"
---

## What Are the Uniswap APIs?
The Uniswap APIs are a suite of endpoints which make it easy to integrate swapping, lping, and more through a traditional RESTful integration. These APIs abstract away many of the complexities of interacting with smart contracts by exposing swap routing logic, intent-based swapping, and calldata generation. 

The API has four main suites groups:
* **Swapping:** Swapping is the ability to swap one token for another token, to bridge a token from one chain to another chain, and to wrap and unwrap tokens. The swapping endpoints externalize Uniswap's powerful routing service, helping to find the most efficient path to swap a token across Uniswap AMMs and UniswapX liquidity.
* **Liquidity Providing (LPing):** LPing includes the ability to create, modify, and remove liquidity positions from Uniswap protocol pools, to migrate positions between protocol versions, and to claim liquidity providing fees.
* **Reference Data:** These endpoints provide useful data so that you do not need to integrate additional data sources. These endpoints can provide pool information and provide lists of tokens and their metadata.
* **Utility Endpoints:** These endpoints can generate validated calldata or perform contract information lookup for common use cases, such as sending tokens from one wallet to another wallet or checking if a wallet has an EIP-7702 delegation.

## How Do I Get Started?
If you are ready to build, you can grab an API key from the [Uniswap Developer Portal](https://developers.uniswap.org/dashboard/). To get familiar with how to build a swapping app quickly, we recommend first reading the [Building Prerequisites](/docs/api/guides/swapping/building-prerequisites) and then starting to code with the [Integration Guide](/docs/api/guides/swapping/integration-guide).

If you are a market maker interested in filling UniswapX orders, visit our [UniswapX quoter API documentation](/docs/liquidity/uniswapx-filling/become-a-quoter) for more information.

