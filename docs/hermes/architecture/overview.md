---
sidebar_position: 1
---
# Overview

### Dojima Architecture

![medium](https://dojima-images.s3.ap-south-1.amazonaws.com/dojima-docs/img/dojimainfrastructure.jpg)
Dojima Network is built on a multi-layer architecture comprising two blockchains that collaboratively interact with other blockchains.
This design enables liquidity access and serves as a cross-chain development platform for creating cross-chain applications. These layers include the Hermes layer and the DojimaChain.

- The Hermes layer is built on top of the Cosmos SDK and tendermint. It is the buffer layer that is connected to various independent blockchains.

- DojimaChain operates as the intermediate layer where developers deploy applications and access the Hermes layer to establish connections with all chains.


In simple terms, we will create a buffer layer on top of Cosmos SDK and Tendermint, establishing connections with major blockchains while maintaining liquidity pools for the Dojima native token(DOJ) and other tokens of prominent blockchain platforms.
Liquidity data will be available and verified by all validators at the end of each block and supplied to contracts on the intermediate layer, Dojima chain.
This data can be accessed by smart contracts developed by cross-chain DApp creators.

Some of the features that Dojima Network offers include:

1. Universal Liquidity Access: This enables developers to access the liquidity of all blockchains directly from their protocols.

2. Cross-Chain Execution and Transfer: This enables users to execute contract code on multiple platforms and also enables cross-chain data transfer to communicate with custom smart contracts.

3. Cross-Chain Liquidity Pools: This feature enables developers and users to access cross-chain liquidity pools for executing various custom cross-chain actions
