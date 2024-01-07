---
title: Polkadot
---


# `@d11k-ts/polkadot`

## Modules

- `client` - Custom client for communicating with polkadot by using [@polkadot/api](https://github.com/polkadot-js/api)

## Installation

```
yarn add @d11k-ts/polkadot
```

## Documentation : Basic usage examples

### Connect wallet to new PolkadotClient

- Create new Polkadot client
- Network default is `Mainnet`

```ts
// Imports
import { Network } from '@d11k-ts/client'
import { PolkadotClient } from '@d11k-ts/polkadot'

//Connect wallet, get address and check balance 
const connectWallet = async () => {
  let phrase = "phrase"
  // Mainnet
  const polkaClient = new PolkadotClient({phrase})
  // testnet
  // const polkaClient = new PolkadotClient({ 
  //    phrase, 
  //    network: Network.Testnet 
  //    provider: 'wss://dotws-test.h4s.dojima.network:9944'
  // })
  let address = polkaClient.getAddress()
  try {
      const balance = await polkaClient.getBalance(address)
      console.log(`Adress: ${address} with balance ${balance}`)

    } catch (error) {
      console.log(`Caught: ${error} `)
    }
  process.exit()
}
```

### Transfer dot using PolkadotClient

- Create new PolkadotClient instance
- Build transaction
- Returns txHash as string

```ts
const transferDot = async () => {
  // First initiate PolkadotClient
  let amountToTransfer = 0.001
  let recipient = 'insert address'
  console.log("Building transaction")
  try {
    const txid = await polkaClient.transfer({ 
      recipient,
      amount: amountToTransfer
    })
    console.log(`Transaction sent: ${txid}`)
    return txid
  } catch (error) {
    console.log(`Caught: ${error} `)
  }
  process.exit()
}
```

### Get transaction Data & transaction History

- No code for retrieving tx data and history in @d11k-ts/polkadot.
- View tx details in explorer
- Mainnet : [polkadot-subscan](https://polkadot.subscan.io/)

### Get gas fee for transaction

- Retrieve gas fee for transaction from build tx

```ts
const fee = async () => {
  let amountToTransfer = 0.001
  let recipient = 'insert address'
  try {
    const fees = polkaClient.getFees({
      recipient,
      amount: amountToTransfer
    })
    console.log(`Fees Fast: ${fees.average} Fastest: ${fees.fast} Average: ${fees.slow}`)
  } catch (error) {
    console.log(`Caught ${error}`)
  }
  process.exit()
}
```

### Get Polkadot Inbound address

- Get Polkadot Inbound address from hermes chain
- Can be used in adding liquidity pool and swapping

```ts
const inboundAddr = async () => {
  try {
    const inboundAddress = await polkaClient.getPolkadotInboundAddress()
    console.log('Inbound Address :: ', inboundAddress)
  } catch (error) {
    console.log(`Caught ${error}`)
  }
  process.exit()
}
```

### Get default liquidity pool gas fee

- Get Polkadot default liquidity pool gas fee from hermes chain

```ts
const defaultLPGasFee = async () => {
  try {
    const LPDefaultGasFee = await polkaClient.getDefaultLiquidityPoolGasFee()
    console.log('Liquidity pool default gas fee :: ', LPDefaultGasFee)
  } catch (error) {
    console.log(`Caught ${error}`)
  }
  process.exit()
}
```

### Add DOT token into liquidity pool

- Add DOT tokens into liquidity pool
- Get Polkadot Inbound address from hermes chain

```ts
const addDotToLiquidityPool = async () => {
  let amountToTransfer = 0.001
  const inboundAddress = await polkaClient.getPolkadotInboundAddress()
  try {
    const liquidityPoolHash = await polkaClient.addLiquidityPool(
      amountToTransfer,
      inboundAddress,
      dojAddress,           // optional dojima address
    )
    console.log('Liquidity pool hash : ', liquidityPoolHash)
  } catch (error) {
    console.log(`Caught ${error}`)
  }
  process.exit()
}
```

### Swap DOT tokens

- Swap DOT tokens to required token using receiver address
- Get Polkadot Inbound address from hermes chain
- Supported tokens for swapping - 'AR', 'DOJ', 'ETH', 'SOL'

```ts
import {SwapAssetList} from '@d11k-ts/utils'

const swapDOT = async () => {
  let amountToTransfer = 0.001
  const inboundAddress = await polkaClient.getPolkadotInboundAddress()
  try {
    const swapHash = await polkaClient.swap(
       amountToTransfer,
      SwapAssetList,
      inboundAddress,
      reciepient                // Respective receiver SwapAssetList token address
    )
    console.log('Swap tx hash : ', swapHash)
  } catch (error) {
    console.log(`Caught ${error}`)
  }
  process.exit()
}
```

### Example Code

For sample code check out example test case in [`Polkadot`](https://github.com/dojimanetwork/d11k-ts/blob/main/packages/d11k-polkadot/examples/test.ts)