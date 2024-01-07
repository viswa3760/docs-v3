---
title: Cosmos
---

# `@d11k-ts/cosmos`

Cosmos Module for `D11K` clients

## Installation

```
yarn add @d11k-ts/cosmos
```

Following dependencies have to be installed into your project. These are not included in `@d11k-ts/cosmos`.

```
yarn add axios @cosmos-client/core@^0.45.13
```
> **NOTE** : Make sure to install same version of @cosmos-client/core as @d11k-ts/cosmos is using (currently "@cosmos-client/core": "^0.45.13", ). In other case things might break.

## Cosmos Client Testing

```
yarn install
yarn test
```
## Documentation

Yet to be added.

## Service Providers

This package uses the following service providers:

| Function                    | Service    | Notes                                                               |
| --------------------------- | ---------- | ------------------------------------------------------------------- |
| Balances                    | Cosmos RPC | https://cosmos.network/rpc/v0.37.9 (`GET /bank/balances/{address}`) |
| Transaction history         | Cosmos RPC | https://cosmos.network/rpc/v0.37.9 (`GET /txs`)                     |
| Transaction details by hash | Cosmos RPC | https://cosmos.network/rpc/v0.37.9 (`GET /txs/{hash}`)              |
| Transaction broadcast       | Cosmos RPC | https://cosmos.network/rpc/v0.37.9 (`POST /txs`)                    |
| Explorer                    | BigDipper  | https://cosmos.bigdipper.live                                       |

Rate limits: No