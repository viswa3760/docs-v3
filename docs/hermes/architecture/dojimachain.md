---
title: Dojima Chain
---
[//]: # (---)

[//]: # (## Dojima Chain)

![medium](../../img/hermes/seamless-deployment.svg)


### Introduction

The **Dojima Chain** is a critical component of the Dojima Network ecosystem, serving as a foundational layer for the seamless integration of assets, NFTs, and decentralized finance (DeFi) applications from various interconnected blockchains. Designed with security, interoperability, and scalability in mind, the Dojima Chain is powered by a decentralized network of Proof-of-Stake (PoS) validators.

### Key Features

#### 1. **Interoperability:**
The Dojima Chain is designed to bridge the divide between multiple layer 1 and layer 2 blockchains. It acts as a pivotal middle-ground where assets and data from diverse blockchain ecosystems converge, fostering cross-chain compatibility.

#### 2. **Validator Network:**
Security is paramount, and the Dojima Chain relies on a network of validators to ensure the integrity and trustworthiness of transactions and data. Validators within the Dojima Network ecosystem play multifaceted roles, including running full nodes, block production, transaction validation, consensus participation, relayer and oracle services, and checkpoint commitment.

#### 3. **Ethereum Virtual Machine (EVM) Compatibility:**
The Dojima Chain seamlessly integrates with the Ethereum Virtual Machine (EVM), enabling developers to deploy and execute smart contracts using familiar languages such as Solidity. This compatibility empowers developers to leverage existing Ethereum-based applications and tools within the Dojima ecosystem.

#### 4. **Dojima Token (DOJ):**
Transactions within the Dojima Chain are facilitated using the native token, Dojima (DOJ). DOJ operates both as an ERC-20 token and as the native token for the Dojima network. This dual functionality allows users to pay gas fees, participate in staking, and transfer value within the ecosystem.

#### 5. **Block Producer Selection:**
The Dojima Chain employs a committee of Block Producers, selected from the validator pool, to ensure efficient block generation and validation. The selection process is based on the validators' staked tokens, with regular shuffling to maintain fairness and security.

### Block Producer Selection Process

The Block Producer selection process in the Dojima Chain is designed to ensure fairness and security. Here's a simplified example of how it works:

[//]: # (- Validators are allocated slots based on the number of staked tokens. For instance, UserA with 100 staked DOJ tokens receives 5 slots, while UserB and UserC with 40 staked DOJ tokens each receive 2 slots.)

[//]: # (- These slots are shuffled using historical block data as a seed, ensuring randomness and fairness.)

[//]: # (- The producer set for the next span is determined based on governance-defined producer counts. For example, if 5 producers need to be selected, the producer set may include [A: 3, B: 1, C: 1].)

[//]: # (- Validators in the producer set serve as Block Producers for the upcoming span, with selection facilitated by Tendermint's proposer selection algorithm.)

[//]: # (Imagine a validator pool with 4 validators: Validator1, Validator2, Validator3, and Validator4. Each validator has staked a different amount of DOJ tokens. Validator1 has staked 200 DOJ tokens, Validator2 has staked 150 DOJ tokens, Validator3 has staked 100 DOJ tokens, and Validator4 has staked 50 DOJ tokens.)

[//]: # ()
[//]: # (Validators are assigned slots proportionally to their stake. The total number of slots allocated is 10. Here's the distribution of slots:)

[//]: # ()
[//]: # (- Validator1: 4 slots)

[//]: # (- Validator2: 3 slots)

[//]: # (- Validator3: 2 slots)

[//]: # (- Validator4: 1 slot)

[//]: # ()
[//]: # ()
[//]: # (Now, let's shuffle the slots using a random seed. After shuffling, we get the following sequence: [Validator3, Validator1, Validator2, Validator2, Validator4, Validator1, Validator3, Validator1, Validator2, Validator3].)

[//]: # ()
[//]: # (Next, based on the number of producers to be selected &#40;let's say we need to select 3 producers&#41;, we pick validators from the top of the shuffled list. In this case, the producer set for the next span is defined as:)

[//]: # ()
[//]: # (Producer1: Validator3)

[//]: # (Producer2: Validator1)

[//]: # (Producer3: Validator2)

[//]: # (These selected validators will take on the role of Block Producers for the next span in the DojimaChain network. This illustrates the producer selection process in the DojimaChain ecosystem.)
[//]: # (## DojimaChain Producer Selection Process)

Imagine a validator pool with 4 validators: Validator1, Validator2, Validator3, and Validator4. Each validator has staked a different amount of DOJ tokens. Validator1 has staked 200 DOJ tokens, Validator2 has staked 150 DOJ tokens, Validator3 has staked 100 DOJ tokens, and Validator4 has staked 50 DOJ tokens.

Validators are assigned slots proportionally to their stake. The total number of slots allocated is 10. Here's the distribution of slots:

- Validator1: 4 slots
- Validator2: 3 slots
- Validator3: 2 slots
- Validator4: 1 slot

Now, let's shuffle the slots using a random seed. After shuffling, we get the following sequence: [Validator3, Validator1, Validator2, Validator2, Validator4, Validator1, Validator3, Validator1, Validator2, Validator3].

Next, based on the number of producers to be selected (let's say we need to select 3 producers), we pick validators from the top of the shuffled list. In this case, the producer set for the next span is defined as:

- Producer1: Validator3
- Producer2: Validator1
- Producer3: Validator2

These selected validators will take on the role of Block Producers for the next span in the DojimaChain network. This illustrates the producer selection process in the DojimaChain ecosystem.


### System Call Interface

Within the Dojima Chain's EVM, the System Call Interface plays a vital role. It serves as an internal operator address, enabling the maintenance of Block Producer states at specified block intervals. System Calls trigger requests for updated Block Producer lists, ensuring the network's smooth operation.

### State Syncing

The Dojima Chain maintains synchronization with different blockchains through the Hermes Chain. This synchronization process ensures that state data from various native chains is securely integrated into the Dojima ecosystem. Validators validate the data using a Threshold Signature Scheme before it is stored in the Hermes Chain.

### Conclusion

The Dojima Chain is at the core of the Dojima Network's mission to provide developers with a powerful, secure, and interoperable platform for building cross-chain applications. With EVM compatibility, robust validator networks, and advanced features, it stands as a key element in the evolution of the blockchain and Web3 space.

[//]: # (---)

[//]: # (# Dojima Chain)

[//]: # (![medium]&#40;img/Dojima_3d.png&#41;)

[//]: # (The dojima chain layer is where assets, NFT’s and Defi dapps from all the connected chains meet. The Dojima chain layer is powered by Decentralised network of Proof-of-Stake &#40;PoS&#41; validators. )

[//]: # (Dojima Network relies on a set of validators to secure the network. The role of validators is to run a full node, produce blocks, validate, participate in consensus and commit checkpoints.)

[//]: # ()
[//]: # (### EVM Compatible VM)

[//]: # ()
[//]: # (The Ethereum Virtual Machine &#40;EVM&#41; is a powerful, sandboxed virtual stack embedded within every full Dojima node, responsible for executing contract bytecode. )

[//]: # (Contracts are typically written in higher level languages, like Solidity, then compiled to EVM bytecode.)

[//]: # ()
[//]: # (### DojimaChain Fee Model:)

[//]: # ()
[//]: # (In the context of normal transaction, fees are collected in the form of Dojima tokens and subsequently distributed to block producers, mirroring the transaction fee mechanism in Ethereum.)

[//]: # (Dojima features its native token, Dojima &#40;DOJ&#41;, which serves a dual purpose. It operates both as an ERC20 token for gas payments &#40;transaction fees&#41; and for staking within the network.)

[//]: # (An important thing to note is that on the Dojima chain, Dojima tokens function simultaneously as both ERC20 tokens and the native token.)

[//]: # (Consequently, users have the flexibility to utilize DOJ for paying transaction fees &#40;gas&#41; as well as for transferring assets to other accounts.)

[//]: # (For genesis-contracts, gasPrice and gasLimit works same as Ethereum, but during the execution it won't deduct the fees from sender's account.)

[//]: # (Genesis transactions from current validators are executed with gasPrice = 0.)

[//]: # (Validators have to send following types of transaction like State proposals like deposits & Span proposals on Dojima Chain.)

[//]: # ()
[//]: # (### Proposers and Producers Selection)

[//]: # ()
[//]: # (Block Producers for the DojimaChain layer are a committee selected from the Validator pool on the basis of their stake,)

[//]: # (This selection process occurs at regular intervals and involves periodic shuffling. The frequency of these intervals is )

[//]: # (determined by the governance framework established by the Validators, taking into account considerations related to dynasty and network stability)

[//]: # (A validators ratio of Stake/Staking power specifies the probability to be selected as a member of the block producer committee.)

[//]: # ()
[//]: # (### Selection Procedure)

[//]: # ()
[//]: # (Let's suppose we have 3 validators in pool, and they are UserA,UserB and UserC. UserA staked 100 DOJ tokens whereas UserB and UserC staked 40 DOJ tokens.)

[//]: # (Validator slots are allocated in proportion to the amount staked, with UserA receiving a total of 5 slots, and UserB and UserC each receiving 2 slots.)

[//]: # (All the validators are given these slots [ A, A, A, A, A, B, B, C, C ].)

[//]: # ()
[//]: # (Using historical block data as seed, we shuffle this array. After shuffling the slots using the seed, say we get this array [ A, B, A, A, C, B, A, A, C].)

[//]: # (Depending on Producer count&#40;maintained by validator's governance&#41;,  we extract validators from the top of the shuffled array. )

[//]: # (For e.g. if we want to select 5 producers we get the producer set as [ A, B, A, A, C]. Hence, the producer set for the next span is defined as [ A: 3, B:1, C:1 ].)

[//]: # ()
[//]: # (Using this validator set and tendermint's proposer selection algorithm we choose a producer for every sprint on DojimaChain.)

[//]: # ()
[//]: # (### SystemCall Interface)

[//]: # ()
[//]: # (System call is an internal operator address which is under EVM. This helps to maintain the state for Block Producers for every few blocks.)

[//]: # (A System Call is triggered for every few blocks and a request is made for the new list of Block Producers. )

[//]: # (Once the state is updated, changes are received after block generation on DojimaChain  to all the Validators.)

[//]: # ()
[//]: # (### State syncing)

[//]: # ()
[//]: # (Dojima Chain retrieves the state of different blockchains from the Hermes Chain. The state stored on Hermes is sourced from native chain events and undergoes validation by all participating validators.)

[//]: # (This validation occurs in a secure manner using the Threshold Signature Scheme. Hermes pulls data from respective native chains using chain clients and validators validate this data,)

[//]: # (which is then stored in hermes chain. Since all the participating chains may have different underlying architectures, )

[//]: # (the validation logic has been tailored to accommodate these differences before data integration into the system.".)