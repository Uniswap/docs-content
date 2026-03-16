---
id: Glossary
title: "Glossary"
---

## Common Terms
There are a few terms used throughout these documents which are helpful to understand:
- **Uniswap Protocols** refers to the pools of liquidity created through [protocol smart contracts](/docs/get-started/concepts/how-uniswap-works). These are sometimes referred to as **V2**, **V3**, and **V4** pools. (V1 is not supported by the APIs.) In rare instances these protocols collectively are called **Classic**.
- **UniswapX** refers to the intent-based RFQ swap mechanism. UniswapX has two versions: **UniswapX_V2** and **UniswapX_V3**. UniswapX is alternately referred to as **DutchQuoteV2** and **DutchQuoteV3** (respectively) in the API documentation. Additionally, UniswapX_V2 can be referred to as a **PriorityQuote** (when a UniswapX_V2 request is made on Base or Unichain chains).
- **Permit2** is a smart contract which simplifies sharing and managing token approvals. [All Uniswap workflows utilize Permit2](/api/concepts/permit2), with Uniswap Protocols taking advantage of the AllowanceTransfer properties of Permit2 and UniswapX taking advantage of the SignatureTransfer properties of Permit2. In short, users sign Permit2 messages which allow the Permit2 contract to spend tokens from the user's wallet. Permit2 messages can include permissions including limiting spending to one transaction, to a time window, and to a specific amount of tokens. [Click here to read a more detailed explanation of how Permit2 works](https://github.com/dragonfly-xyz/useful-solidity-patterns/tree/main/patterns/permit2).