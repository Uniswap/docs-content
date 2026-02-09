---
title: Uniswap Overview
description: An introduction to the Uniswap protocol, its AMM design, permissionless architecture, and protocol versions.
---

## What is Uniswap?

The Uniswap protocol is a peer-to-peer system designed for exchanging cryptocurrencies ([ERC-20 Tokens](https://ethereum.org/en/developers/docs/standards/tokens/erc-20/)) on the [Ethereum](https://ethereum.org/) blockchain. The protocol is implemented as a set of persistent, non-upgradable smart contracts; designed to prioritize censorship resistance, security, self-custody, and to function without any trusted intermediaries who may selectively restrict access.

There are currently four versions of the Uniswap protocol. v1 and v2 are open source and licensed under GPL. v3 introduced concentrated liquidity and is open source with slight modifications. v4 introduces the singleton pool architecture and hooks system, enabling unprecedented protocol customization. Each version of Uniswap, once deployed, will function in perpetuity, with 100% uptime, provided the continued existence of the Ethereum blockchain.

## Protocol, Interface, Labs

To begin, we should make clear the distinctions between the different areas of "Uniswap", some of which may confuse new users.

- **[Uniswap Labs](https://x.com/Uniswap)**: The company which developed the Uniswap protocol, along with the web interface.
- **[Uniswap Foundation](https://www.uniswapfoundation.org/)**: A non-profit organization that supports the development of the Uniswap protocol and its DeFi ecosystem.
- **[Uniswap Protocol](https://github.com/Uniswap/contracts)**: A suite of persistent, non-upgradable smart contracts that together create an automated market maker, a protocol that facilitates peer-to-peer market making and swapping of ERC-20 tokens on the Ethereum blockchain.
- **[Uniswap Interface](https://app.uniswap.org/)**: A web interface that allows for easy interaction with the Uniswap protocol. The interface is only one of many ways one may interact with the Uniswap protocol.
- **[Uniswap Governance](https://gov.uniswap.org/)**: A governance system for governing the Uniswap Protocol, enabled by the UNI token.

## How does Uniswap compare to a typical market?

To understand how the Uniswap protocol differs from a traditional exchange, it is helpful to first look at two subjects: how the Automated Market Maker design deviates from traditional central limit order book-based exchanges, and how permissionless systems depart from conventional permissioned systems.

### Order Book vs AMM

Most publicly accessible markets use a central limit [order book](https://www.investopedia.com/terms/o/order-book.asp) style of exchange, where buyers and sellers create orders organized by price level that are progressively filled as demand shifts. Anyone who has traded stocks through brokerage firms will be familiar with an order book system.

The Uniswap protocol takes a different approach, using an Automated Market Maker (AMM), sometimes referred to as a Constant Function Market Maker, in place of an order book. At a very high level, an AMM replaces the buy and sell orders in an order book market with a liquidity pool of two assets, both valued relative to each other. As one asset is traded for the other, the relative prices of the two assets shift, and a new market rate for both is determined. In this dynamic, a buyer or seller trades directly with the pool, rather than with specific orders left by other parties.

Through its evolution, the protocol has enhanced this model: v3 introduced concentrated liquidity for capital efficiency, and v4's singleton pool architecture and hooks system enable unprecedented customization of pool behavior while maintaining the core AMM principles.

The advantages and disadvantages of Automated Market Makers versus their traditional order book counterparts are under active research by a growing number of parties. We have collected some notable examples on our [research page](./research).

### Permissionless Systems

The second departure from traditional markets is the permissionless and immutable design of the Uniswap protocol. These design decisions were inspired by Ethereum's core tenets, and a commitment to the ideals of permissionless access and immutability as indispensable components of a future in which anyone in the world can access financial services without fear of discrimination or counter-party risk.

Permissionless design means that the protocol's services are entirely open for public use, with no ability to selectively restrict who can or cannot use them. Anyone can swap, provide liquidity, or create new markets at will. This is a departure from traditional financial services, which typically restrict access based on geography, wealth status, and age.

The protocol is also immutable, in other words not upgradeable. No party is able to pause the contracts, reverse trade execution, or otherwise change the behavior of the protocol in any way.

## Where to go from here

- For core protocol concepts like AMMs, fees, and hooks, see [Concepts](./concepts/amms).
- Ready to integrate swaps? Head to the [Trading guides](/docs/trading) for quickstarts and advanced swap patterns.
- Want to provide liquidity or build LP tooling? See the [Liquidity guides](/docs/liquidity).
- For research into the economics of AMMs, game theory, or optimization, check out our [research page](./research).
- To start building, jump to the [SDK documentation](/docs/sdks/v4/overview) or the [API documentation](/docs/api/overview).
