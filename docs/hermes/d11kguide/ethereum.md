---
title : Ethereum

---


# `@d11k-ts/ethereum`

## Modules

- `client` - Custom client for communicating with Ethereum by using [`ethers`](https://github.com/ethers-io/ethers.js)

## Installation

```
yarn add @d11k-ts/ethereum
```

Following dependencies have to be installed into your project. These are not included in `@d11k-ts/ethereum`.

```
yarn add axios ethers
```

## Service Providers

This package uses the following service providers:

| Function                  | Service   | Notes                                                                          |
| ------------------------- | --------- | ------------------------------------------------------------------------------ |
| ETH balances              | Etherscan | https://etherscan.io/apis#accounts (module=`account`, action=`balance`)        |
| Token balances            | Etherscan | https://etherscan.io/apis#tokens (module=`account`, action=`tokenbalance`)     |
| ETH transaction history   | Etherscan | https://etherscan.io/apis#accounts (module=`account`, action=`txlistinternal`) |
| Token transaction history | Etherscan | https://etherscan.io/apis#accounts (module=`account`, action=`tokentx`)        |
| Transaction fees          | Etherscan | https://etherscan.io/apis#gastracker (module=`gastracker`, action=`gasoracle`) |
| Transaction broadcast     | Etherscan | https://sebs.github.io/etherscan-api/#eth_sendrawtransaction                   |
| Explorer                  | Etherscan | https://etherscan.io/                                                          |

Etherscan API rate limits: https://info.etherscan.com/api-return-errors/

- Testnet API - [https://api-goerli.etherscan.io/](https://api-goerli.etherscan.io/) , Explorer - [https://goerli.etherscan.io/](https://goerli.etherscan.io/)

- This package uses `etherjs` library, by default it uses several providers. (`https://docs.ethers.io/v5/api-keys/`)

## Documentation : Basic usage examples

### Connect wallet to new EthereumClient

- Create new EthereumChain client
- Network default is `Mainnet`

```ts
// Imports
import {Network} from '@d11k-ts/client'
import {ETH_DECIMAL, EthereumClient} from '@d11k-ts/ethereum'
import {assetAmount, assetToBase, baseToAsset} from '@d11k-ts/utils'

//Connect wallet, validate address and check balance 
const connectWallet = async () => {
  let phrase = "phrase"
  // Mainnet
  const ethClient = new EthereumClient({phrase})
  // testnet
  // const bnbClient = new EthereumClient({ 
  //    phrase, 
  //    network: Network.Testnet,
  //    etherscanApiKey: 'get-etherscan-api-key',
  //    ethplorerApiKey: 'get-ethplorer-api-key',
  //  })
  let address = ethClient.getAddress()
  let isValid = ethClient.validateAddress(address)
  console.log(address)
  if (isValid === true) {
    try {
      const balance = await ethClient.getBalance(address)
      let assetAmount = (baseToAsset(balance[0].amount)).amount()
      console.log(`Adress: ${address} with balance ${assetAmount}`)

    } catch (error) {
      console.log(`Caught: ${error} `)
    }
  } else {
    console.log(`Address: ${address} is invalid`)
  }
}

```

### Transfer eth using EthereumClient

- Create new EthereumClient instance
- Convert amount to transfer to base amount
- Build transaction
- Returns txHash as string

```ts
// Transfer ethereum other TxParams > feeOptionKey?, gasLimit?, gasPrice? 
const transferEth = async () => {
  // First initiate EthereumClient
  let amountToTransfer = 0.001
  let recipient = 'insert address'
  let amount = assetToBase(assetAmount(amountToTransfer, ETH_DECIMAL))
  console.log("Building transaction")
  try {
    const txid = await ethClient.transfer({
      amount,
      recipient,
      "memo": "memo",               // optional
      "walletIndex": 0,             // optional (default)
      "asset": AssetETH,            // optional (default)
    })
    console.log(`Transaction sent: ${txid}`)
    return txid
  } catch (error) {
    console.log(`Caught: ${error} `)
  }
}

```

### Get transaction Data & transaction History

- Create new EthereumClient instance
- Call getTransactionData(hash) returns hash-details
- Call getTransactions(address) returns list of transactions (if any)

```ts
// Retrieve transaction data for a particular hash
const transactionData = async () => {
  let hash = "insert hash"
  let Address = ethClient.getAddress()
  try {
    const txData = await ethClient.getTransactionData(
      hash,
      Address         // optional
    )
    console.log(`Transaction data ${txData}`)
  } catch (error) {
    console.log(`Caught: ${error} `)
  }
}

// Retrieve transaction history for a particular address
const transactionHistory = async () => {
  let Address = ethClient.getAddress()
  try {
    const txHistory = await ethClient.getTransactions({address: Address})
    console.log(`Found ${txHistory.total.toString()}`)
    txHistory.txs.forEach(tx => console.log(tx))
  } catch (error) {
    console.log(`Caught: ${error} `)
  }
}

```

### Get transfer Fees estimations

- Retrieve estimated gas prices and gas limits from ethereum client

```ts
// Retrieve fee estimations from transaction parameters
const feeEstimations = async () => {
  let amountToTransfer = 0.001
  let amount = assetToBase(assetAmount(amountToTransfer, ETH_DECIMAL))
  let recipient = "insert address"
  try {
    const fees = await ethClient.estimateFeesWithGasPricesAndLimits({
      "amount": amount,
      "recipient": recipient
    })
    console.log(`Fees average : ${baseToAsset(fees.fees.average).amount()}, gas limits: ${fees.gasLimit}, gas prices average: ${baseToAsset(fees.gasPrices.average).amount()}`)

  } catch (error) {
    console.log(`Caught: ${error} `)
  }
}

```

### Example Code

For sample code check out example test case in [`Ethereum`](https://github.com/dojimanetwork/d11k-ts/blob/main/packages/d11k-ethereum/examples/test.ts)