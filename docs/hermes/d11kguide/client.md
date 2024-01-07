---
title: Client
---

# `@d11k-ts/client`

## Installation

```
yarn add @d11k-ts/client
```

Initialise and set up the client to connect to its necessary third-party services to fulfil basic functionality. The third-party services used must be at a minimum to fulfil the wallet functionality, such as displaying balances and sending transactions.

## D11K-ts Wallet Client Interface

A specification for a generalised interface for crypto wallets clients, to be used by D11K-ts implementations. The client should not have any functionality to generate a key, instead, the `asgardex-crypto` library should be used to ensure cross-chain compatible keystores are handled. The client is only ever passed a master BIP39 phrase, from which a temporary key and address is decoded.