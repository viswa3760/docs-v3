---
title : Arweave
---


# `@d11k-ts/arweave`


## Modules

- `client` - Custom client for communicating with arweave by using [`arweave`](https://github.com/ArweaveTeam/arweave-js)

## Installation

```
yarn add @d11k-ts/arweave
```

## Documentation : Basic usage examples

### Connect wallet to new ArweaveClient

- Create new Arweave client
- Network default is `Mainnet`

```ts
// Imports
import { ArweaveClient } from '@d11k-ts/arweave'
import { Network } from '@d11k-ts/client'

//Connect wallet, get address and check balance 
const connectWallet = async () => {
  let phrase = "phrase"
  // Mainnet
  const arClient = new ArweaveClient({phrase})
  // testnet
  // const arClient = new ArweaveClient({
  //   phrase,
  //   network: Network.Testnet,
  //   config:{
    //   host: "ar-test.h4s.dojima.network",
    //   protocol: "https",
    //   timeout: 100000,
    // }
  // })
  let address = arClient.getAddress()
  try {
      const balance = await arClient.getBalance(address)
      console.log(`Adress: ${address} with balance ${balance}`)

    } catch (error) {
      console.log(`Caught: ${error} `)
    }
}
```

### Mint testnet 'ar' tokens using ArweaveClient

- Create new Arweave client
- Network is set to `Testnet`
- By default `2 AR` tokens were added to address on every call
- `Note: Testnet tokens are not useful in Mainnet`

```ts
//Connect wallet, get address, mint tokens and check balance 
const mintTokensToWallet = async () => {
  let phrase = "phrase"
  // testnet
  const arClient = new ArweaveClient({
    phrase,
    network: Network.Testnet,
    config:{
      host: "ar-test.h4s.dojima.network",
      protocol: "https",
      timeout: 100000,
    }
  })
  let address = arClient.getAddress()
  try {
      await arClient.mintArTokens(address)
        const balance = await arClient.getBalance(address)
      console.log(`Address: ${address} with balance ${balance}`)

    } catch (error) {
      console.log(`Caught: ${error} `)
    }
}
```

### Transfer ar using ArweaveClient

- Create new ArweaveClient instance
- Build transaction
- Returns txHash as string

```ts
const transferAr = async () => {
  // First initiate ArweaveClient
  let amountToTransfer = 0.001
  let recipient = 'insert address'
  console.log("Building transaction")
  try {
    const txid = await arClient.transfer({ 
      recipient,
      amount: amountToTransfer
    })
    console.log(`Transaction sent: ${txid}`)
    return txid
  } catch (error) {
    console.log(`Caught: ${error} `)
  }
}
```

## Get transaction Data & transaction History

- Create new ArweaveClient instance
- Call getTransactionData(hash) returns hash-details
- Call getTransactionsHistory(address) returns list of transactions (if any)

```ts
// Retrieve transaction data for a particular hash
const transactionData = async () => {
  let hash = "insert hash"
  let Address = arClient.getAddress()
  try {
    const txData = await arClient.getTransactionData(
      hash
    )
    console.log(`Transaction data ${txData}`)
  } catch (error) {
    console.log(`Caught: ${error} `)
  }
}

// Retrieve transaction history for a particular address
const transactionHistory = async () => {
  let Address = arClient.getAddress()
  try {
    const txHistory = await arClient.getTransactionsHistory({
      address: Address
    })
    console.log(`Found ${txHistory.total.toString()}`)
    txHistory.txs.forEach(tx => console.log(tx))
  } catch (error) {
    console.log(`Caught: ${error} `)
  }
}
```

### Get gas fee for transaction

- Retrieve gas fee for transaction from build tx

```ts
const fee = async () => {
  let amountToTransfer = 0.001
  let recipient = 'insert address'
  try {
    const rawTx = await arClient.createTransaction(
        recipient, 
       amountToTransfer
    )
    const fees = arClient.getFees(rawTx)
    console.log(`Fees Fast: ${fees.average} Fastest: ${fees.fast} Average: ${fees.slow}`)
  } catch (error) {
    console.log(`Caught ${error}`)
  }
}
```

### Get Arweave Inbound address

- Get Arweave Inbound address from hermes chain
- Can be used in adding liquidity pool and swapping

```ts
const inboundAddr = async () => {
  try {
    const inboundAddress = await arClient.getArweaveInboundAddress()
    console.log('Inbound Address :: ', inboundAddress)
  } catch (error) {
    console.log(`Caught ${error}`)
  }
}
```

### Get default liquidity pool gas fee

- Get Arweave default liquidity pool gas fee from hermes chain

```ts
const defaultLPGasFee = async () => {
  try {
    const LPDefaultGasFee = await arClient.getDefaultLiquidityPoolGasFee()
    console.log('Liquidity pool default gas fee :: ', LPDefaultGasFee)
  } catch (error) {
    console.log(`Caught ${error}`)
  }
}
```

### Add AR token into liquidity pool

- Add AR tokens into liquidity pool
- Get Arweave Inbound address from hermes chain

```ts
const addARToLiquidityPool = async () => {
  let amountToTransfer = 0.001
  const inboundAddress = await arClient.getArweaveInboundAddress()
  try {
    const liquidityPoolHash = await arClient.addLiquidityPool(
      amountToTransfer,
      inboundAddress,
      dojAddress,           // optional dojima address
    )
    console.log('Liquidity pool hash : ', liquidityPoolHash)
  } catch (error) {
    console.log(`Caught ${error}`)
  }
}
```

### Swap AR tokens

- Swap AR tokens to required token using receiver address
- Get Arweave Inbound address from hermes chain
- Supported tokens for swapping - 'DOT', 'DOJ', 'ETH', 'SOL'

```ts
import {SwapAssetList} from '@d11k-ts/utils'

const swapAR = async () => {
  let amountToTransfer = 0.001
  const inboundAddress = await arClient.getArweaveInboundAddress()
  try {
    const swapHash = await arClient.swap(
       amountToTransfer,
      SwapAssetList,
      inboundAddress,
      reciepient                // Respective receiver SwapAssetList token address
    )
    console.log('Swap tx hash : ', swapHash)
  } catch (error) {
    console.log(`Caught ${error}`)
  }
}
```

### Example Code

For sample code check out example test case in [`Arweeave`](https://github.com/dojimanetwork/d11k-ts/blob/main/packages/d11k-arweave/examples/test.ts)