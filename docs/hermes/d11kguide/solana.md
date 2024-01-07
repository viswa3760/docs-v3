---
title: Solana
---
# `@d11k-ts/solana`

## Modules

- `client` - Custom client for communicating with solana by
  using [`@solana/web3.js`](https://github.com/solana-labs/solana-web3.js)

## Installation

```
yarn add @d11k-ts/solana
```

Following dependencies have to be installed into your project. These are not included in `@d11k-ts/solana`.

```
yarn add axios
```

## Documentation : Basic usage examples

### Connect wallet to new SolanaClient

- Create new Solana client
- Network default is `Mainnet`

```ts
// Imports
import {SolanaClient} from '@d11k-ts/solana'
import {Network} from "@d11k-ts/client";

//Connect wallet, get address and check balance 
const connectWallet = async () => {
  let phrase = "phrase"
  // Mainnet
  const solClient = new SolanaClient({phrase})
  // devnet
  // const solClient = new SolanaClient({
  //    phrase, 
  //    network: Network.Stagenet
  //    endpoint: 'https://sol-test.h4s.dojima.network:8899'
  // })
  let address = solClient.getAddress()
  try {
    const balance = await solClient.getBalance(address)
    console.log(`Adress: ${address} with balance ${balance}`)

  } catch (error) {
    console.log(`Caught: ${error} `)
  }
}
```

### Request airdrop - testnet 'sol' tokens using SolanaClient

- Create new Solana client
- Network is set to `devnet`
- By default `2 SOL` tokens were added to address on every call
- `Note: Devnet tokens are not useful in Mainnet`

```ts
// Imports
import {SolanaClient} from '@d11k-ts/solana'
import {Network} from "@d11k-ts/client";

//Connect wallet, get address, request sol tokens and check balance 
const connectWallet = async () => {
  let phrase = "phrase"
  // Mainnet
  const solClient = new SolanaClient({phrase})
  // devnet
  // const solClient = new SolanaClient({
  //    phrase, 
  //    network: Network.Stagenet
  //    endpoint: 'https://sol-test.h4s.dojima.network:8899'
  // })
  let address = solClient.getAddress()
  try {
    await solClient.requestSolTokens(address)
    const balance = await solClient.getBalance(address)
    console.log(`Address: ${address} with balance ${balance}`)

  } catch (error) {
    console.log(`Caught: ${error} `)
  }
}
```

### Transfer sol using SolanaClient

- Create new SolanaClient instance
- Build transaction
- Returns txHash as string

```ts
const transferSol = async () => {
  // First initiate SolanaClient
  let amountToTransfer = 0.001
  let recipient = 'insert address'
  console.log("Building transaction")
  try {
    const txid = await solClient.transfer({
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

### Get transaction Data & transaction History

- Create new SolanaClient instance
- Call getTransactionData(hash) returns hash-details
- Call getTransactionsHistory(address) returns list of transactions (if any)

```ts
// Retrieve transaction data for a particular hash
const transactionData = async () => {
  let hash = "insert hash"
  let Address = solClient.getAddress()
  try {
    const txData = await solClient.getTransactionData(
      hash
    )
    console.log(`Transaction data ${txData}`)
  } catch (error) {
    console.log(`Caught: ${error} `)
  }
}

// Retrieve transaction history for a particular address
const transactionHistory = async () => {
  let Address = solClient.getAddress()
  try {
    const txHistory = await solClient.getTransactionsHistory({
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

- Solana has fixed fee client, average, fast and fastest return the same value

```ts
const fee = async () => {
  try {
    const fees = solClient.getFees()
    console.log(`Fees Fast: ${fees.average} Fastest: ${fees.fast} Average: ${fees.slow}`)
  } catch (error) {
    console.log(`Caught ${error}`)
  }
}
```

### Get Solana Inbound address

- Get Solana Inbound address from hermes chain

- Can be used in adding liquidity pool and swapping

```ts
const inboundAddr = async () => {
  try {
    const inboundAddress = await solClient.getSolanaInboundAddress()
    console.log('Inbound Address :: ', inboundAddress)
  } catch (error) {
    console.log(`Caught ${error}`)
  }
}
```

### Get default liquidity pool gas fee

- Get Solana default liquidity pool gas fee from hermes chain

```ts
const defaultLPGasFee = async () => {
  try {
    const LPDefaultGasFee = await solClient.getDefaultLiquidityPoolGasFee()
    console.log('Liquidity pool default gas fee :: ', LPDefaultGasFee)
  } catch (error) {
    console.log(`Caught ${error}`)
  }
}
```

### Add SOL token into liquidity pool

- Add SOL tokens into liquidity pool
- Get Solana Inbound address from hermes chain

```ts
const addSOLToLiquidityPool = async () => {
  let amountToTransfer = 0.001
  const inboundAddress = await solClient.getSolanaInboundAddress()
  try {
    const liquidityPoolHash = await solClient.addLiquidityPool(
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

### Swap SOL tokens

- Swap SOL tokens to required token using receiver address
- Get Solana Inbound address from hermes chain
- Supported tokens for swapping - 'DOT', 'DOJ', 'ETH', 'AR'

```ts
import {SwapAssetList} from '@d11k-ts/utils'
const swapSOL = async () => {
  let amountToTransfer = 0.001
  const inboundAddress = await solClient.getSolanaInboundAddress()
  try {
    const swapHash = await solClient.swap(
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

For sample code check out example test case in [`Solana`](https://github.com/dojimanetwork/d11k-ts/blob/main/packages/d11k-solana/examples/test.ts)