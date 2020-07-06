---
description: ETH-xDai Arbitrary Message Bridge information
---

# About the ETH-xDai AMB

An Arbitrary Message Bridge \(AMB\) between the Ethereum Mainnet and the xDai chain extends the number of the applications that can leverage cross-chain communications.

Any application can [build its own AMB extension](https://docs.tokenbridge.net/amb-bridge/how-to-develop-xchain-apps-by-amb). This is represented by two mediator contracts so that either assets or arbitrary data can be transferred between chains. The deployed mediator contracts **do not** require a set of oracles to be setup, allowing an application to launch quickly and reducing the cost of application ownership.

The mediator contracts rely on the following information about the ETH-xDai Arbitrary Message Bridge:

* **Ethereum Mainnet**:
  * AMB contract: [`0x4C36d2919e407f0Cc2Ee3c993ccF8ac26d9CE64e`](https://etherscan.io/address/0x4C36d2919e407f0Cc2Ee3c993ccF8ac26d9CE64e)
  * Gas limit to call method in the xDai chain: `2000000`
  * Finalization rate: `8` blocks
* **xDai Chain**:
  * AMB contract: [`0x75Df5AF045d91108662D8080fD1FEFAd6aA0bb59`](https://blockscout.com/poa/xdai/address/0x75df5af045d91108662d8080fd1fefad6aa0bb59/transactions)
  * Gas limit to call method in the Ethereum Mainnet: `2000000`
  * Finalization rate: `1` block

{% hint style="success" %}
A detailed description of the AMB and examples of AMB extensions are available here: [Arbitrary Message Bridge \(AMB\)](https://docs.tokenbridge.net/amb-bridge/about-amb-bridge).
{% endhint %}

It is possible to get an AMB transaction status by using the Live Monitoring app: [https://alm-xdai.herokuapp.com/](https://alm-xdai.herokuapp.com/).

