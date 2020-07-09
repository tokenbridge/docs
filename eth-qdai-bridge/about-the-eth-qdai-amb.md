---
description: ETH-qDai Arbitrary Message Bridge information
---

# About the ETH-qDai AMB

An Arbitrary Message Bridge \(AMB\) between the Ethereum Mainnet and the qDai chain demonstrates the ability to transfer data between a public network and an enterprise chain built using Quorum technology.

Any application can [build its own AMB extension](https://docs.tokenbridge.net/amb-bridge/how-to-develop-xchain-apps-by-amb). This is represented by two mediator contracts so that either assets or arbitrary data can be transferred between chains. The deployed mediator contracts **do not** require a set of oracles to be setup, allowing an application to launch quickly and reducing the cost of application ownership.

The mediator contracts rely on the following information about the ETH-qDai Arbitrary Message Bridge:

* **Ethereum Mainnet**:
  * AMB contract: [`0xcEb06eCea3F588Cb60e39BD4DB7869013C6f65a5`](https://etherscan.io/address/0xceb06ecea3f588cb60e39bd4db7869013c6f65a5)
  * Gas limit to call method in the xDai chain: `2000000`
  * Finalization rate: `8` blocks
* **xDai Chain**:
  * AMB contract: [`0xD4075FB57fCf038bFc702c915Ef9592534bED5c1`](https://blockscout.com/poa/qdai/address/0xD4075FB57fCf038bFc702c915Ef9592534bED5c1/transactions)
  * Gas limit to call method in the Ethereum Mainnet: `2000000`
  * Finalization rate: `1` block

