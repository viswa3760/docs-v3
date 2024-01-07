---
title: Verifying A Smart Contract
---

Once verified, a smart contract or token contract's source code becomes publicly available and verifiable. This creates transparency and trust. Plus, it's easy to do! Verification is available for Solidity.

## Smart Contract Verification with Blockscout

1)  You will be given an address to check a pending transaction after the contract is created. If it doesn't take you to [https://doj-bex-test.dojima.network/](https://doj-bex-test.dojima.network/), go to Dojima Chain block explorer, make sure you're on the chain where the contract was set up, then type the address of the contract into the search field. Your contract details should come up.
![medium](https://dojima-images.s3.ap-south-1.amazonaws.com/dojima-docs/img/contract_deploying_1.png)
![medium](https://dojima-images.s3.ap-south-1.amazonaws.com/dojima-docs/img/contract_deploying_2.png)
![medium](https://dojima-images.s3.ap-south-1.amazonaws.com/dojima-docs/img/contract_deploying_3.png)

2) To view the bytecode, select the Code tab and press the Verify and Publish button. Several options for verification will be available to you. Please select the "via flattened source code" (solidity) option.

![medium](https://dojima-images.s3.ap-south-1.amazonaws.com/dojima-docs/img/contract_deploying_4.png)

### Via Flattened Source Code

![medium](https://dojima-images.s3.ap-south-1.amazonaws.com/dojima-docs/img/contract_deploying_5.png)

1. **Contract Address**: The 0x address entered when the contract was created
2. **Contract Name:** The name of the class that was mentioned in the.sol files. In the `contract MyContract {..` **MyContract** , for example, the contract's name is MyContract.
3. **Include Nightly Builds:** If you wish to display nightly builds, then yes.
4. **Compiler:** Taken from the first line of the `X.X.X. contract's pragma solidity`. Use the appropriate compiler instead of the nightly build.
5. **EVM Version:** [See EVM version details](https://docs.blockscout.com/for-developers/evm-version-information).
6. **Optimization:** Check yes if you made optimization available during compilation.
7. **Optimization Runs:** The default value for the Solidity Compiler is 200. change only if you modified this value during compilation.
8. **Enter the Solidity Contract Code:** If your solidity code uses a library or inherits dependencies from another contract, you might need to flatten it. The [POA solidity flattener](https://github.com/poanetwork/solidity-flattener) or [the truffle flattener](https://www.npmjs.com/package/truffle-flattener) are our recommendations.
9. **Try to fetch constructor arguments automatically:** Similar contracts might be offered if they exist.
10. **ABI-encoded Constructor Arguments:** [See this page for more info](https://docs.blockscout.com/for-users/abi-encoded-constructor-arguments).
11. **Add Contract Libraries:** For any necessary libraries that must be called in the .sol file, enter their name and 0x address.
Choose `"Verify and Publish"` from the menu.
If everything is going well, you should notice a tick next to Code in the code tab and a new tab labelled `"Read Contract." `Any transactions related to your contract will now be listed in BlockScout with the contract name.
