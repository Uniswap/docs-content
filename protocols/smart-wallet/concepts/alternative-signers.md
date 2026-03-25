---
title: Alternative Signers
description: Learn how Uniswap smart wallet supports alternative signer keys and related security caveats.
---

Calibur allows users to add any number of signers to their account, known as `keys`.

## Supported Key Types

- `Secp256k1`
- `Secp256r1 (P256)`
- `WebAuthn P256`

## Security Caveats

This is an **advanced** feature. Please be aware of the following:

- By default, added keys do not expire and have no hooks
- A malicious key could steal all of your ETH and tokens

Registering external signers on your account changes the security model. Proceed with caution!