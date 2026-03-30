---
id: overview
title: Protocols Overview
description: Navigate the Uniswap protocol documentation — from the core AMM versions to supporting infrastructure contracts.
---

# Protocols

Uniswap is a suite of onchain protocols. At its core are the automated market maker (AMM) contracts — the pool contracts that hold liquidity and execute swaps. Surrounding them are supporting protocols that handle routing, token approvals, resource locking, smart wallet delegation, and fee distribution.

This page helps you orient within the protocol documentation and find the right starting point for your integration.

---

## AMM Protocols

The AMM is the heart of Uniswap. Each version introduced architectural changes that improved capital efficiency, composability, and gas costs. **Uniswap V4 is the current and recommended version for new integrations.**

### Uniswap V4 (Recommended)

V4 consolidates all pools into a single `PoolManager` contract and introduces [hooks](/docs/get-started/concepts/hooks) — external contracts that can customize pool behavior at every stage of its lifecycle (initialization, swaps, liquidity changes, fee logic). It uses [flash accounting](/docs/protocols/v4/concepts/flash-accounting) to defer token transfers until the end of a transaction, enabling significant gas savings for multi-step operations.

V4 is the most flexible and gas-efficient version of the protocol. If you are building a new integration, start here.

| Resource | Link |
| :--- | :--- |
| Concepts | [Hooks](/docs/protocols/v4/concepts/hooks), [Flash Accounting](/docs/protocols/v4/concepts/flash-accounting), [Dynamic Fees](/docs/protocols/v4/concepts/dynamic-fees) |
| Guides | [Set Up Environment](/docs/protocols/v4/guides/hooks/getting-started), [Build Your First Hook](/docs/protocols/v4/guides/hooks/your-first-hook), [Security Framework](/docs/protocols/v4/security) |
| SDK | [V4 SDK docs](/docs/sdks/v4/overview) |
| Deployments | [V4 addresses](/docs/protocols/v4/deployments) |
| Repositories | [`v4-core`](https://github.com/Uniswap/v4-core), [`v4-periphery`](https://github.com/Uniswap/v4-periphery) |
| Audits | [Core audits](https://github.com/Uniswap/v4-core/tree/main/audits), [Periphery audits](https://github.com/Uniswap/v4-periphery/tree/main/audits) |

[Go to V4 documentation →](/docs/protocols/v4/overview)

---

<details>
<summary><strong>Uniswap V3</strong></summary>

V3 introduced [concentrated liquidity](/docs/get-started/concepts/liquidity-providers/concentrated-liquidity), allowing LPs to allocate capital to specific price ranges rather than across the entire curve. This dramatically improved capital efficiency and enabled new position management strategies. Positions are represented as NFTs via the `NonfungiblePositionManager`.

V3 remains widely deployed and actively used. Many existing integrations and SDKs target V3.

| Resource | Link |
| :--- | :--- |
| Concepts | [Architecture](/docs/protocols/v3/concepts/architecture), [Price Oracles](/docs/protocols/v3/concepts/price-oracles) |
| Guides | [Getting Started](/docs/protocols/v3/guides/getting-started), [Swapping](/docs/protocols/v3/guides/swapping/single-hop-swapping), [Liquidity](/docs/protocols/v3/guides/managing-liquidity/getting-started) |
| SDK | [V3 SDK docs](/docs/sdks/v3/overview) |
| Deployments | [V3 addresses](/docs/protocols/v3/deployments) |
| Repositories | [`v3-core`](https://github.com/Uniswap/v3-core), [`v3-periphery`](https://github.com/Uniswap/v3-periphery) |

[Go to V3 documentation →](/docs/protocols/v3/overview)

</details>

<details>
<summary><strong>Uniswap V2</strong></summary>

V2 is the original constant-product AMM (`x * y = k`) with full-range liquidity. It is the simplest version of the protocol and remains deployed on Ethereum mainnet and many other chains.

V2 is a good starting point for understanding AMM fundamentals, but new integrations should target V4 unless there is a specific reason to use V2.

| Resource | Link |
| :--- | :--- |
| Concepts | [Architecture](/docs/protocols/v2/concepts/architecture), [Swapping](/docs/protocols/v2/concepts/swapping), [Oracles](/docs/protocols/v2/concepts/oracles) |
| Guides | [Getting Started](/docs/protocols/v2/guides/getting-started), [Implement a Swap](/docs/protocols/v2/guides/swapping), [Providing Liquidity](/docs/protocols/v2/guides/providing-liquidity) |
| SDK | [V2 SDK docs](/docs/sdks/v2/overview) |
| Deployments | [V2 addresses](/docs/protocols/v2/deployments) |
| Repositories | [`uniswap-v2-core`](https://github.com/Uniswap/uniswap-v2-core), [`uniswap-v2-periphery`](https://github.com/Uniswap/uniswap-v2-periphery) |

[Go to V2 documentation →](/docs/protocols/v2/overview)

</details>

---

## Supporting Protocols

Beyond the AMM, Uniswap relies on a set of infrastructure contracts that handle routing, approvals, fee distribution, and more. These protocols are used across multiple AMM versions and are important for production integrations.

### Universal Router

The Universal Router is an unowned, non-upgradeable contract that composes swaps across V2, V3, and V4 in a single transaction. It uses a command-based encoding system and integrates with Permit2 for signature-controlled token approvals.

If you are executing swaps programmatically, the Universal Router is the recommended entry point.

[Universal Router documentation →](/docs/protocols/universal-router/overview)

### Permit2

Permit2 unifies signature-based token transfers and time-bound allowances into a single contract. It is used by the Universal Router, the PositionManager, and other Uniswap contracts to reduce repeated approval transactions and improve security.

[Permit2 documentation →](/docs/protocols/permit2/overview)

### Protocol Fees

[Fees](/docs/get-started/concepts/fees#protocol-fees) from all Uniswap protocol versions flow through Fee Adapter contracts into a per-chain TokenJar. Releaser contracts define how collected fees are accessed — for example, the Firepit Releaser burns UNI in exchange for collected assets.

[Protocol Fees documentation →](/docs/protocols/protocol-fee/overview)

### The Compact

The Compact is an ownerless ERC-6909 contract that enables [resource locks](/docs/protocols/the-compact/concepts/resource-locks) — tokens that are credibly committed for asynchronous conditions and claimed once those conditions are met. It supports single-chain and multichain flows and is used in cross-chain coordination.

[The Compact documentation →](/docs/protocols/the-compact/overview)

### Smart Wallet (Calibur)

Uniswap smart wallet features are powered by Calibur, a non-upgradeable contract implementation for EIP-7702 delegation. Users delegate to the implementation while keeping their existing EOA address.

[Smart Wallet documentation →](/docs/protocols/smart-wallet/overview)

---

## Security

Uniswap Labs maintains an active bug bounty program on Cantina for eligible vulnerability disclosures across all protocol versions.

> [View the bug bounty program](https://cantina.xyz/bounties/f9df94db-c7b1-434b-bb06-d1360abdd1be)