---
description: Rinkeby-xDai Arbitrary Message Bridge information
---

# About the Rinkeby-xDai AMB



The main use case of the Arbitrary Message Bridge \(AMB\) between the Rinkeby Testnet and the xDai chain is to relay tokens emitted by Reddit \(e.g. Moons and Bricks\) to a chain with a real value \(xDai\) through the AMB extensions.

DApp developers may also consider this pair of chains useful for their cross-chain applications. In order to organize cross-chain communication applications can [implement their own AMB extension](https://docs.tokenbridge.net/amb-bridge/how-to-develop-xchain-apps-by-amb). This is represented by two mediator contracts so that either assets or arbitrary data can be transferred between chains. The deployed mediator contracts **do not** require a set of oracles to be setup, allowing the application to rapidly provide the main functionality to end users without spending resources on setting up the entire infrastructure.

Here are the technical details about the Rinkeby-xDai chain Arbitrary Message Bridge:

* **Rinkeby Testnet**:
  * AMB contract: [`0xD4075FB57fCf038bFc702c915Ef9592534bED5c1`](https://rinkeby.etherscan.io/address/0xD4075FB57fCf038bFc702c915Ef9592534bED5c1)\`\`
  * Gas limit to call method in the Rinkeby Testnet: `3000000` 
  * Fee: none
  * Finalization rate: `1` blocks
* **xDai chain**:
  * AMB contract: [`0xc38D4991c951fE8BCE1a12bEef2046eF36b0FA4A`](https://blockscout.com/poa/xdai/address/0xc38D4991c951fE8BCE1a12bEef2046eF36b0FA4A)\`\`
  * Gas limit to call method in the xDai chain: `3000000`
  * Fee: none
  * Finalization rate: `1` block

