---
title: Uniswap
description: An introduction to the Uniswap protocol, its AMM design, permissionless architecture, and protocol versions.
---

## What is Uniswap?

The Uniswap protocol is a peer-to-peer system designed for exchanging cryptocurrencies ([ERC-20 Tokens](https://ethereum.org/en/developers/docs/standards/tokens/erc-20/)) on the [Ethereum](https://ethereum.org/) blockchain. The protocol is implemented as a set of persistent, non-upgradable smart contracts; designed to prioritize censorship resistance, security, self-custody, and to function without any trusted intermediaries who may selectively restrict access.

There are currently four versions of the Uniswap protocol. v1 and v2 are open source and licensed under GPL. v3 introduced concentrated liquidity and is open source with slight modifications. v4 introduces the singleton pool architecture and hooks system, enabling unprecedented protocol customization. Each version of Uniswap, once deployed, will function in perpetuity, with 100% uptime, provided the continued existence of the Ethereum blockchain.

## Protocol, Interface, Labs

To begin, we should make clear the distinctions between the different areas of "Uniswap", some of which may confuse new users.

- **[Uniswap Labs](https://x.com/Uniswap)**: The company which developed the Uniswap protocol, along with the web interface.
- **[Uniswap Foundation](https://x.com/Uniswapfnd)**: A non-profit organization that supports the development of the Uniswap protocol and its DeFi ecosystem.
- **[Uniswap Protocol](https://github.com/Uniswap/contracts)**: A suite of persistent, non-upgradable smart contracts that together create an automated market maker, a protocol that facilitates peer-to-peer market making and swapping of ERC-20 tokens on the Ethereum blockchain.
- **[Uniswap Interface](https://app.uniswap.org/)**: A web interface that allows for easy interaction with the Uniswap protocol. The interface is only one of many ways one may interact with the Uniswap protocol.
- **[Uniswap Governance](https://gov.uniswap.org/)**: A governance system for governing the Uniswap Protocol, enabled by the UNI token.

## Where to go from here

- To execute your first swap, see [your first swap](/docs/get-started/quickstart) guide.
- For core protocol concepts like AMMs, fees, and hooks, see [concepts](/docs/get-started/concepts/amms).
- Ready to trade or integrate swaps? Visit the [trading guides](/docs/trading/overview) or the [API reference](/docs/api/overview).
- Want to provide liquidity or build LP tooling? Explore the [liquidity section](/docs/liquidity/overview).
- Building on the protocol? Start with [protocols](/docs/protocols/v4/overview) (v4 recommended for new integrations), or explore UniswapX, Liquidity Launchpad, and more.
- Deploying or building on Unichain? Visit [unichain](/docs/unichain/).
- Looking for builder support, AI tools, and ecosystem resources? Explore [resources](/docs/resources/agents).
