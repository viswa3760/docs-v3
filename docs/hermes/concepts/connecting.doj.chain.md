---
title : Connecting to HERMESChain
---

How to connect to Hermesgard, HERMESNode and the base Tendermint layer.

The Network Information comes from four sources:


1. **HERMESNode**: Raw blockchain data provided by the HERMESChain state machine. HERMESChain wallets and block explorers will query HERMESChain-specific information here.
2. **Cosmos RPC**: Used to query for generic CosmosSDK information.
3. **Tendermint RPC**: Used to query for consensus-related information.

### Cosmos RPC

The Cosmos RPC allows Cosmos base blockchain information to be returned.  However, not all endpoints have been enabled.

#### Endpoints guide

https://v1.cosmos.network/rpc/v0.45.1

#### Example URL

[https://api-test.h4s.dojima.network/cosmos/bank/v1beta1/balances/dojima1nh4y3gqxsn7ymm9t45zwsz3h8p9tm7pev8my62](https://api-test.h4s.dojima.network/cosmos/bank/v1beta1/balances/dojima1nh4y3gqxsn7ymm9t45zwsz3h8p9tm7pev8my62)

### Tendermint RPC

The Tendermint RPC allows Tendermint consensus information to be returned.

**Any Node Ports**

- MAINNET Port: `27147`
- STAGENET Port: `26657`
- TESTNET Port: `26657`

#### Endpoints guide

[https://docs.tendermint.com/master/rpc/#/](https://docs.tendermint.com/master/rpc/#/)

#### Rpc End Links

[https://rpc-test.h4s.dojima.network](https://rpc-test.h4s.dojima.network)

#### P2P

P2P is the network layer between nodes, useful for network debugging.

TESTNET Port: `26656`

P2P Guide

[https://docs.tendermint.com/master/spec/p2p/](https://docs.tendermint.com/master/spec/p2p/)