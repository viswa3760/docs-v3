---
title : Hermes
---


# `@d11k-ts/hermes`

Hermes Module for Dojima chain

## Installation

```
yarn add @d11k-ts/hermes
```

Following dependencies have to be installed into your project. These are not included in `@d11k-ts/hermes`.

```
yarn add axios @cosmos-client/core@^0.45.13 bech32-buffer@^0.2.1
```

> **NOTE**: Make sure to install same version of @cosmos-client/core and bech32-buffer as @d11k-ts/cosmos is using (
> currently "@cosmos-client/core": "^0.45.13", "bech32-buffer": "^0.2.1"). In other case things might break.

## Service Providers

This package uses the following service providers:

| Network | Node                                | RPC                                 |
|---------|-------------------------------------|-------------------------------------|
| Testnet | https://api-test.h4s.dojima.network | https://rpc-test.h4s.dojima.network |
| Mainnet | NA                                  | NA                                  |

> **Note** : 'Mainnet' is currently under process. Not applicable yet.

| Function                    | Service        | Notes                                                               |
| --------------------------- | -------------- | ------------------------------------------------------------------- |
| Balances                    | Cosmos RPC     | https://cosmos.network/rpc/v0.37.9 (`GET /bank/balances/{address}`) |
| Transaction history         | Tendermint RPC | https://docs.tendermint.com/master/rpc/#/Info/tx_search             |
| Transaction details by hash | Cosmos RPC     | https://cosmos.network/rpc/v0.37.9 (`GET /txs/{hash}`)              |
| Transaction broadcast       | Cosmos RPC     | https://cosmos.network/rpc/v0.37.9 (`POST /txs`)                    |

Rate limits: No

## Documentation: Basic usage example

### Connect wallet to new Hermes Client

- Create new HermesChain client
- Network default is `Mainnet`

```ts

// Imports 
import {Network} from '@d11k-ts/client'
import {DOJ_DECIMAL, HermesClient} from '@d11k-ts/hermes'
import {AssetDOJNative, assetAmount, assetToBase, baseToAsset} from '@d11k-ts/utils'


// Create new instance of the client and query chain for balances. 
const connectWallet = async () => {

  let phrase = "phrase"
  // mainnet
  const hermesClient = new HermesClient({phrase})
  // testnet
  // const hermesClient = new HermesClient({ phrase, network: Network.Testnet })

  let address = hermesClient.getAddress()
  console.log(`Address: ${address}`)
  try {
    const balance = await hermesClient.getBalance(address, [AssetDOJNative])
    let assetAmount = (baseToAsset(balance[0].amount)).amount()
    console.log(`With balance: ${assetAmount}`)
  } catch (error) {
    console.log(`Caught ${error}`)
  }
}

```

### Transfer doj using Hermes Client

- Default feeRate is `fast`
- Create new HermesChain client instance
- Convert amount to transfer to base amount
- Build transaction
- Returns txHash as string

```ts
const transferDoj = async () => {

  // First initiate HermesClient
  let amountToTransfer = 0.1
  let amount = assetToBase(assetAmount(amountToTransfer, DOJ_DECIMAL))
  let recipient = "insert address"
  try {
    const txid = await hermesClient.transfer({
      "amount": amount,
      "recipient": recipient,
      "memo": "test",             // optional
      "asset": AssetDOJNative,    // optional (default)
      "walletIndex": 0            // optional (default)
    })
    console.log(`Transaction sent: ${txid}`)
  } catch (error) {
    console.log(`Caught ${error}`)
  }
}


```

### Get transaction Data & transaction History

- Create new HermesClient instance
- Call getTransactionData(hash) returns hash-details
- Call getTransactions(address) returns list of transactions (if any)

```ts

const transactionData = async () => {

  // First initiate HermesClient
  let hash = "insert hash"
  let address = hermesClient.getAddress()
  try {
    const txData = await hermesClient.getTransactionData(hash, address)
    console.log(txData)
  } catch (error) {
    console.log(`Caught ${error}`)
  }
}
// By default getTransactions() returns the transactions for the current address
// Optional param - any dojima address
const transactionHistory = async () => {
  try {
    const txHistory = await hermesClient.getTransactions(address)
    console.log(`Found ${txHistory.total}`)
    txHistory.txs.forEach(tx => console.log(tx.hash))
  } catch (error) {
    console.log(`Caught ${error}`)
  }
}
```

### Get transfer Fees

- Hermeschain runs on fee type of Flatfee set to `0.02` DOJ

```ts
// Returns Fees Fast: 0.02 Fastest: 0.02 Average: 0.02
const fee = async () => {

  // First initiate HermesClient
  try {
    const {fast, fastest, average} = await hermesClient.getFees()
    console.log(`Fees Fast: ${baseToAsset(fast).amount()} Fastest: ${baseToAsset(fastest).amount()} Average: ${baseToAsset(average).amount()}`)
  } catch (error) {
    console.log(`Caught ${error}`)
  }
}
```

### Deposit doj using Hermes Client

- Create new HermesChain client instance
- Convert amount to transfer to base amount
- Deposit transaction
- Returns txHash as string

```ts
import {SwapAssetList} from '@d11k-ts/utils'

const transferDoj = async () => {

  // First initiate HermesClient
  let amountToTransfer = 0.1
  let amount = assetToBase(assetAmount(amountToTransfer, DOJ_DECIMAL))
  // amount: number     Note: convert amount to 'BaseAmount' before passing to transfer function
  // memo: string
  'ADD:{SwapAssetList}:{respective-token-address}'
  'SWAP:{SwapAssetList}:{receiver-token-address}'
  try {
    // 'memo' with ADD
    const txid = await hermesClient.deposit({
      amount,
      memo: `ADD:{SwapAssetList}:{respective-token-address}`,
    })
    // 'memo' with SWAP
    // const depositHash = await hermesClient.deposit({
    //   amount,
    //   memo: `SWAP:{SwapAssetList}:{receiver-token-address}`,
    // })
    console.log(`Deposit tx hash: ${txid}`)
  } catch (error) {
    console.log(`Caught ${error}`)
  }
}

```

### Example Code

For sample code check out example test case in [`Hermes`](https://github.com/dojimanetwork/d11k-ts/blob/main/packages/d11k-hermes/examples/test.ts)