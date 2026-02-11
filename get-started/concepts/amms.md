---
id: how-uniswap-works
title: How Uniswap works
description: Learn how Uniswap AMMs work across all protocol versions.
---

![](./images/anatomy.jpg)

Uniswap is an automated liquidity protocol powered by the constant product formula
and implemented in a system of non-upgradeable smart contracts on the [Ethereum](https://ethereum.org/) blockchain.
It obviates the need for trusted intermediaries, prioritizing **decentralization**, **censorship resistance**,
and **security**. Uniswap is **open-source software** licensed under the
[GPL](https://en.wikipedia.org/wiki/GNU_General_Public_License).

Each Uniswap smart contract, or pair, manages a liquidity pool made up of reserves of two [ERC-20](https://eips.ethereum.org/EIPS/eip-20) tokens.

Anyone can become a liquidity provider (LP) for a pool by depositing an equivalent value of each underlying token in return for pool tokens. These tokens track pro-rata LP shares of the total reserves, and can be redeemed for the underlying assets at any time.

![](./images/lp.jpg)

Pairs act as automated market makers, standing ready to accept one token for the other as long as the “constant product” formula is preserved. This formula, most simply expressed as `x * y = k`, states that trades must not change the product (`k`) of a pair’s reserve balances (`x` and `y`). Because `k` remains unchanged from the reference frame of a trade, it is often referred to as the invariant. This formula has the desirable property that larger trades (relative to reserves) execute at exponentially worse rates than smaller ones.

In practice, Uniswap applies a 0.30% fee to trades, which is added to reserves. As a result, each trade actually increases `k`. This functions as a payout to LPs, which is realized when they burn their pool tokens to withdraw their portion of total reserves. In the future, this fee may be reduced to 0.25%, with the remaining 0.05% withheld as a protocol-wide charge.

![](./images/trade.jpg)

Because the relative price of the two pair assets can only be changed through trading, divergences between the Uniswap price and external prices create arbitrage opportunities. This mechanism ensures that Uniswap prices always trend toward the market-clearing price.

## How does the Uniswap protocol compare to a typical market?

To understand how the Uniswap protocol differs from a traditional exchange, it is helpful to first look at two subjects: how the Automated Market Maker design deviates from traditional central limit order book-based exchanges, and how permissionless systems depart from conventional permissioned systems.

### Order Book VS AMM

Most publicly accessible markets use a central limit [order book](https://www.investopedia.com/terms/o/order-book.asp) style of exchange, where buyers and sellers create orders organized by price level that are progressively filled as demand shifts. Anyone who has traded stocks through brokerage firms will be familiar with an order book system.

The Uniswap protocol takes a different approach, using an Automated Market Maker (AMM), sometimes referred to as a Constant Function Market Maker, in place of an order book. Through its evolution, the protocol has enhanced this model: [v3](/docs/protocols/v3/overview) introduced concentrated liquidity for capital efficiency, and [v4](/docs/protocols/v4/overview)'s singleton pool architecture and hooks system enable unprecedented customization of pool behavior while maintaining the core AMM principles.

At a very high level, an AMM replaces the buy and sell orders in an order book market with a liquidity pool of two assets, both valued relative to each other. As one asset is traded for the other, the relative prices of the two assets shift, and a new market rate for both is determined. In this dynamic, a buyer or seller trades directly with the pool, rather than with specific orders left by other parties. The advantages and disadvantages of Automated Market Makers versus their traditional order book counterparts are under active research by a growing number of parties. We have collected some notable examples on our [research page](/docs/get-started/research).

### Permissionless Systems

The second departure from traditional markets is the permissionless and immutable design of the Uniswap protocol. These design decisions were inspired by Ethereum's core tenets, and our commitment to the ideals of permissionless access and immutability as indispensable components of a future in which anyone in the world can access financial services without fear of discrimination or counter-party risk.

Permissionless design means that the protocol's services are entirely open for public use, with no ability to selectively restrict who can or cannot use them. Anyone can swap, provide liquidity, or create new markets at will. This is a departure from traditional financial services, which typically restrict access based on geography, wealth status, and age.

The protocol is also immutable, in other words not upgradeable. No party is able to pause the contracts, reverse trade execution, or otherwise change the behavior of the protocol in any way. It is worth noting that Uniswap Governance has the right (but no obligation) to divert a percentage of swap fees on any pool to a specified address. However, this capability is known to all participants in advance, and to prevent abuse, the percentage is constrained between 10% and 25%.

## Where to go from here

- To go deeper on the AMM model, see [concentrated liquidity](/docs/get-started/concepts/liquidity-providers/concentrated-liquidity) (v3) and [hooks](/docs/get-started/concepts/hooks) (v4) or visit our [research page](/docs/get-started/research). 
- Ready to build? Start with [your first swap](/docs/get-started/quickstart), or visit the [API](/docs/api/overview) to integrate.
