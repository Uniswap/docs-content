---
id: math
title: Math
description: Understand the Uniswap v2 constant-product invariant and how reserve changes affect pricing and slippage.
---

Uniswap v2 pricing behavior is based on the constant-product invariant:

`x * y = k`

Here, `x` and `y` are pool reserves, and `k` is the product that must be preserved after swaps (accounting for fees).

## Core Invariant

When a trader buys one asset from the pool, they must sell enough of the other asset so the post-swap reserve product remains valid.

Large trades relative to pool depth move reserves more, causing higher slippage.

## Useful References

- Read the [Uniswap v2 whitepaper](https://uniswap.org/whitepaper.pdf) for derivations.
- See [Pricing](/docs/protocols/v2/concepts/pricing) for practical quote behavior.
- See [Understanding Returns](/docs/protocols/v2/concepts/understanding-returns) for LP outcomes.
