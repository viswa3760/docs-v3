---
title : Bitcoin
---

# `@d11k-ts/bitcoin`

## Modules

- `client` - Client for communicating with Bitcoin using [BIP39](https://github.com/bitcoinjs/bip39)
  , [bitcoinjs-lib](https://github.com/bitcoinjs/bitcoinjs-lib) and [WIF](https://github.com/bitcoinjs/wif)
- `types` - TypeScript type definitions based on `@d11k-ts/client` and `@d11k-ts/utils`
- `utils` - Utitilies for using `haskoin` and `sochain` endpoints in Bitcoin client

## Installation

```
yarn add @d11k-ts/bitcoin
```

Following dependencies have to be installed into your project. These are not included in `@d11k-ts/bitcoin`.

```
yarn add axios coinselect
```

## Service Providers

This package uses the following service providers:

| Function                      | Service           | Notes                                                                            |
|-------------------------------|-------------------|----------------------------------------------------------------------------------|
| Balances                      | Sochain           | https://chain.so/api/v2#get-balance                                              |
| Transaction history           | Sochain           | https://chain.so/api/v2#get-display-data-address, https://chain.so/api/v2#get-tx |
| Transaction details by hash   | Sochain           | https://chain.so/api/v2#get-tx                                                   |
| Transaction fees              | Bitgo             | https://app.bitgo.com/docs/#operation/v2.tx.getfeeestimate                       |
| Transaction broadcast / utxos | Sochain / Haskoin | https://chain.so/api/v2#send-transaction,    https://haskoin.ninerealms.com/btc  |
| Explorer                      | Blockstream       | https://blockstream.info                                                         |

Sochain API rate limits: https://chain.so/api/v2#rate-limits (300 requests/minute)

Bitgo API rate limits: https://app.bitgo.com/docs/#section/Rate-Limiting (10 requests/second)

Haskoin API : https://haskoin.ninerealms.com/btc

## Documentation : Basic Usage Example

### Connect wallet to new BitcoinClient

- Create new Bitcoin client
- Network default is `Mainnet`

```ts
//Imports
import {BTC_DECIMAL, BitcoinClient} from '@d11k-ts/bitcoin'
import {Network} from '@d11k-ts/client'
import {AssetBTC, assetAmount, assetToBase, baseToAsset} from '@d11k-ts/utils'

// Connect wallet to new btc client 
const connectWallet = async () => {
  let phrase = "phrase"
  // Mainnet
  const btcClient = new BitcoinClient({phrase})
  // testnet
  // const bnbClient = new BitcoinClient({ phrase, network: Network.Testnet })
  let address = btcClient.getAddress()
  console.log(`Asset Address is: ${address}`)

  let balances = await btcClient.getBalance(address, [AssetBTC])
  try {
    let assetAmount = (baseToAsset(balances[0].amount)).amount()
    console.log(`Asset address balance: ${assetAmount}`)
  } catch (error) {
    console.log('Address has no balance')
  }
}
```

### Transfer btc using BitcoinClient

- Default feeRate is `fast`
- Create new BitcoinClient instance
- Convert amount to transfer to base amount
- Build transaction
- Returns txHash as string

```ts
const transfer = async () => {
  // First initiate BitcoinClient
  let amountToTransfer = 0.0001
  let recipient = 'insert address'
  let amount = assetToBase(assetAmount(amountToTransfer, BTC_DECIMAL))
  try {
    const txid = await btcClient.transfer({
      asset: AssetBTC,
      recipient: recipient,
      amount: amount,
      memo: "payment"         // optional
    })
    console.log(`Amount: ${amount.amount().toString()} ${AssetBTC.symbol} Transaction id: ${txid}`)
  } catch (error) {
    console.log(`Transfer failed ${error}`)
  }
}

```

### Transfer by setting feeRate

- Build transaction using parameters
- Set feeRate in transaction parameters Or use getFeeRates()

```ts
//Returns FeeRates > this allows for dynamic feeRate adjustment on selection
const {fast, fastest, average} = await btcClient.getFeeRates()

try {
  const txid = await btcClient.transfer({
    'asset': AssetBTC,
    'recipient': recipient,
    'amount': amount,
    'memo': "test transfer",        // optional
    feeRate: fast
  })
  console.log(`Amount ${baseToAsset(amount).amount()} ${AssetBTC.symbol} Transaction id ${txid}`)
} catch (error) {
  console.log(`Transfer failed ${error}`)
}
```

### Get Fees & FeeRates estimations

```ts
//Get Fees - returns FeeOption & fee in BaseAmount 
` Fees Fast: 0.00001 Fastest: 0.0000468 Average: 0.00001 `
try {
  const {fast, fastest, average} = await btcClient.getFees()
  console.log(`Fees Fast: ${baseToAsset(fast).amount()} Fastest: ${baseToAsset(fastest).amount()} Average: ${baseToAsset(average).amount()}`)

} catch (error) {
  console.log(error)
}

//Get FeeRates - returns FeeOption & rate  
` Fast: 12, Fastest 60, Average: 6 `

try {
  const {fast, fastest, average} = await btcClient.getFeeRates()
  console.log(`Fast: ${fast}, Fastest ${fastest}, Average: ${average}`)

} catch (error) {
  console.log(error)
}

```

### Get transaction data

- Create new BitcoinClient instance
- Call getTransaction(hash) returns hashDetails

```ts
const transactionData = async () => {
  let hash = "txhash string"
  try {
    const txData = await btcClient.getTransactionData(hash)
    console.log(`From ${JSON.stringify(txData)}`)

  } catch (error) {
    console.log(`Error: ${error}`)
  }
}

```

### Get Transaction History

- Create new Binance-beaconClient instance
- Call getTransactions(address) returns list of transactions (if any)

```ts
const transactionHistory = async () => {
  // Retrieve transaction history for a set address
  // txHistoryParams > address, offset, startTime, asset?
  try {
    const txHistory = await btcClient.getTransactions({address: Address, limit: 4})
    console.log(`Found ${txHistory.total.toString()}`)
    txHistory.txs.forEach(tx => console.log(tx))

  } catch (error) {
    console.log(`Error: ${error}`)
  }
}

```

### Example Code

For sample code check out example test case in [`Bitcoin`](https://github.com/dojimanetwork/d11k-ts/blob/main/packages/d11k-bitcoin/examples/test.ts)