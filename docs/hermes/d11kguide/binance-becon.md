---
title : Binance-Beacon
---

# `@d11k-ts/binance-beacon`

## Modules

- `client` - Custom client for communicating with Binance Chain by
  using [`binance-chain/javascript-sdk`](https://github.com/binance-chain/javascript-sdk)
- `types` - TypeScript type definitions
  for [`binance-chain/javascript-sdk`](https://github.com/binance-chain/javascript-sdk) (not completed)
  and [`Binance WebSocket Streams`](https://docs.binance.org/api-reference/dex-api/ws-streams.html).
- `util` - Utitilies for using [`binance-chain/javascript-sdk`](https://github.com/binance-chain/javascript-sdk)

## Installation

```
yarn add @d11k-ts/binance-beacon
```

Following dependencies have to be installed into your project. These are not included in `@d11k-ts/binance-beacon`.

```
yarn add @binance-chain/javascript-sdk
```

## Service Providers

This package uses the following service providers:

| Function                     | Service              | Notes                                                                         | Rate limits                   |
|------------------------------| -------------------- | ----------------------------------------------------------------------------- | ----------------------------- |
| Balances                     | Binance Dex          | https://docs.binance.org/api-reference/dex-api/paths.html#apiv1accountaddress | 5 requests per IP per second. |
| Transaction history          | Binance Dex          | https://docs.binance.org/api-reference/dex-api/paths.html#apiv1transactions   | 60 requests per IP per minute |
| Transaction details by hash  | Binance Dex          | https://docs.binance.org/api-reference/dex-api/paths.html#apiv1txhash         | 10 requests per IP per second |
| Transaction fees             | Binance Dex          | https://docs.binance.org/api-reference/dex-api/paths.html#apiv1fees           | 1 request per IP per second   |
| Transaction broadcast        | Binance Dex          | https://docs.binance.org/api-reference/dex-api/paths.html#apiv1broadcast      | 5 requests per IP per second  |
| Explorer                     | Binance Dex Explorer | https://explorer.binance.org                                                  |                               |

This package gets the node information (`https://docs.binance.org/api-reference/dex-api/paths.html#apiv1node-info`) to
transfer tokens.

## Documentation : Basic Usage Example

### Connect wallet to new Binance-beacon Chain Client

- Create new BinanceBeaconChain client
- Network default is `Mainnet`

```ts
//Imports 
import {BinanceBeaconClient} from '@d11k-ts/binance-beacon'
import {Network} from '@d11k-ts/client'
import {AssetBNB, assetAmount, assetToBase, baseToAsset} from '@d11k-ts/utils'

// Connect wallet to new btc client 
const connectWallet = async () => {
  let phrase = "phrase"
  // mainnet
  const bnbClient = new BinanceBeaconClient({phrase})
  // testnet
  // const bnbClient = new BinanceBeaconClient({ phrase, network: Network.Testnet })
  let address = bnbClient.getAddress()
  console.log(`Asset Address is: ${address}`)

  let balances = await bnbClient.getBalance(address, [AssetBNB])
  try {
    let assetAmount = (baseToAsset(balances[0].amount)).amount()
    console.log(`with balance: ${assetAmount}`)
  } catch (error) {
    console.log('no balance')
  }
}
```

### Transfer bnb using Binance-beacon Client

- Default feeRate is `fast`
- Create new Binance-beaconClient instance
- Convert amount to transfer to base amount
- Build transaction
- Returns txHash as string

```ts
const transferBnb = async () => {
  // First initiate BinanceBeaconClient
  let amountToTransfer = 0.0001
  let recipient = 'insert address'
  let amount = assetToBase(assetAmount(amountToTransfer, 8))
  console.log("Building transaction")
  try {
    const txid = await bnbClient.transfer({
      "amount": amount,
      "recipient": recipient,
      "memo": "memo",             // optional
      "walletIndex": 0,            // optional (default)
      "asset": AssetBNB,          // optional (default)

    })
    console.log(`Amount ${amount.amount().toString()} ${AssetBNB.symbol} TransactionId: ${txid}`)
  } catch (error) {
    console.log(`Transfer failed: ${error}`)
  }
}
```

### Get transaction Data & transaction History

- Create new Binance-beaconClient instance
- Call getTransactionData(hash) returns hash-details
- Call getTransactions(address) returns list of transactions (if any)

```ts
let hash = "insert hash string"
try {
  const txData = await bnbClient.getTransactionData(hash)
  console.log(txData)

} catch (error) {
  console.log(`Error: ${error}`)
}

// Retrieve transaction history for a set address
// txHistoryParams > address, offset, startTime, asset? 
try {
  const txHistory = await bnbClient.getTransactions({address: Address, limit: 4})
  console.log(`Found ${txHistory.total.toString()}`)
  txHistory.txs.forEach(tx => console.log(tx))

} catch (error) {
  console.log(`Error: ${error}`)
}
```

### Get transfer fees

- Bnb has fixed fee client, average, fast and fastest return the same value.
- getFees() returns current fees for the network

```ts
try {
  const fee = await bnbClient.getFees()
  console.log(`Fees average:  ${baseToAsset(fee.average).amount()}`)
  console.log(`Fees fast:  ${baseToAsset(fee.fast).amount()}`)
  console.log(`Fees fastest:  ${baseToAsset(fee.fastest).amount()}`)

} catch (error) {
  console.log(error)
}

```

### Example Code

For sample code check out example test case in [`Binance-Beacon`](https://github.com/dojimanetwork/d11k-ts/blob/main/packages/d11k-binance-beacon/examples/test.ts)