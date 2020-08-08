---
description: Kovan-Sokol Arbitrary Message Bridge information
---

# About the Kovan-Sokol AMB

An Arbitrary Message Bridge \(AMB\) between the Kovan Testnet and the POA Sokol Testnet allows Dapps developers to test cross-chain applications.

In order to organize the cross-chain communication the corresponding application can [implement its own AMB extension](https://docs.tokenbridge.net/amb-bridge/how-to-develop-xchain-apps-by-amb). This is represented by two mediator contracts so that either assets or arbitrary data can be transferred between chains. The deployed mediator contracts **do not** require a set of oracles to be setup, allowing an application to rapidly test functionality without spending resources on entire infrastructure setup.

The mediator contracts rely on the following information about the Kovan-Sokol Arbitrary Message Bridge:

* **Kovan Testnet**:
  * AMB contract: [`0xFe446bEF1DbF7AFE24E81e05BC8B271C1BA9a560`](https://kovan.etherscan.io/address/0xfe446bef1dbf7afe24e81e05bc8b271c1ba9a560#code)\`\`
  * Gas limit to call method in the POA Network: `2000000`
  * Fee: `0.05` [Gas Tokens](https://docs.tokenbridge.net/amb-bridge/gas-token-minting)
  * Finalization rate: `1` blocks
* **Sokol Testnet**:
  * AMB contract: [`0xFe446bEF1DbF7AFE24E81e05BC8B271C1BA9a560`](https://blockscout.com/poa/sokol/address/0xFe446bEF1DbF7AFE24E81e05BC8B271C1BA9a560/contracts)\`\`
  * Gas limit to call method in the Ethereum Mainnet: `2000000`
  * Fee: none
  * Finalization rate: `1` block

It is possible to get an AMB transaction status by using [the Live Monitoring app](https://docs.tokenbridge.net/about-tokenbridge/components/amb-live-monitoring-application): [https://alm-test-amb.herokuapp.com/](https://alm-test-amb.herokuapp.com/).

