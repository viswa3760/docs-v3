---
title: Ethereum State Sender Contract
---

## Introduction

  Ethereum, a pioneering decentralized platform, empowers developers to create and deploy smart contracts. These self-executing pieces of code automate intricate processes and agreements, akin to digital agreements that trigger automatically when predefined conditions are met.

  However, Ethereum's significance transcends its technological prowess. It has cultivated a vibrant ecosystem where global developers converge to craft decentralized applications (dApps). Leveraging Ethereum's smart contracts, these dApps provide a wide array of services. These range from decentralized finance (DeFi) and non-fungible tokens (NFTs) to decentralized governance and beyond.

## The State Sender Contract

  The State Sender Contract is a smart contract designed to facilitate Ethereum (dApp) developers in sending tokens and payloads to the **Dojima Chain**.  
  
  To utilize the State Sender Contract, follow these straightforward steps:
### Step 1: Copy the State Sender Contract from GitHub

  * Access the State Sender Contract Interface and Contract on the GitHub repository [here](https://github.com/dojimanetwork/dojima-evm-contracts/blob/dojima-contracts/contracts/interfaces/IStateSender.sol) and [here](https://github.com/dojimanetwork/dojima-evm-contracts/blob/dojima-contracts/contracts/StateSender.sol) respectively.
  * Copy both the Interface and Contract into their corresponding folders, typically located in **'. /contracts/'**, **'. /interfaces/'** or as per your project structure.

### Step 2: Obtain the State Sender Contract Address

  * Retrieve the State Sender Contract address from the Dojima Chain Explorer.

  **Note: The State Sender Contract address may vary for different chains. 
    Ensure that you select the Ethereum chain and the appropriate mainnet or testnet.** 

### Step 3: Initialize the State Sender Contract

  * Initialize the State Sender Contract in your dapp by passing the State Sender Contract address as a parameter.

```solidity
// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.19;

// Import the interface from the GitHub repository
import { IStateSender } from './interfaces/IStateSender.sol';

contract App {
    // Declare a variable to hold the address of the StateSender contract
    address public stateSender;

    constructor(address _stateSender) {
        stateSender = _stateSender;
    }
  
    /**
    * @dev Function to call the tokenTransferWithPayload function from the StateSender contract
    * @param destinationChain The chain to which the tokens and payload are to be sent.
    * @param destinationContract The contract to which the tokens and payload are to be sent.
    * @param asset The address of the token to be sent.
    * @param tokenAmount The amount of tokens to be sent.
    * @param payload The abi encoded contract call to be sent.
    * @notice destinationChain and destinationContract should be registered with the state sender contract before sending the tokens and payload.
    */
    function sendState(
        bytes32 destinationChain,
        address destinationContract,
        address asset,
        uint256 tokenAmount,
        bytes calldata payload
    ) public {
        // Create an instance of the IStateSender interface using the StateSender address
        IStateSender stateSenderInstance = IStateSender(stateSender);

        // Call the tokenTransferWithPayload function
        stateSenderInstance.tokenTransferWithPayload(
            destinationChain,
            destinationContract,
            asset,
            tokenAmount,
            payload
        );
    }
}
```

### Step 4: Event emitted by the State Sender Contract TokenTransferWithPayload
  * Once the State Sender Contract executes the TokenTransferWithPayload function, it emits an event called TokenTransfer. This event plays a vital role in the interaction with **Narada**.
  * The TokenTransfer event furnishes essential information in its parameters:
    * **depositID** - This identifier uniquely identifies deposits on the Dojima chain. It is relevant only when the destinationChain is **Dojima**.
    * **destinationChain** -  This denotes the specific chain to which the tokens and payload have been dispatched.
    * **destinationContract** - It signifies the target contract to which the tokens and payload are delivered.
    * **asset** - This parameter contains the address of the token that was sent.
    * **tokenAmount** - The amount of tokens sent.
    * **payload** - This field holds the ABI-encoded contract call that was transmitted.
      Step 4: Processing the Event Emitted by the State Sender Contract - TokenTransferWithPayload
      Once the State Sender Contract executes the TokenTransferWithPayload function, it emits an event called TokenTransfer. This event plays a vital role in the interaction with Narada.