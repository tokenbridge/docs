---
description: ETH-ETC Arbitrary Message Bridge information
---

# About the ETH-ETC AMB

An Arbitrary Message Bridge \(AMB\) between the Ethereum Mainnet and the Ethereum Classic extends the number of the applications that can leverage cross-chain communications. It was mainly deployed as an experiment to migrate the vanilla TokenBridge serving exchange ETC to [WETC](https://etherscan.io/token/0x86aabcc646f290b9fc9bd05ce17c3858d1511da1) to the AMB protocol. 

Any application can [build its own AMB extension](https://docs.tokenbridge.net/amb-bridge/how-to-develop-xchain-apps-by-amb). This is represented by two mediator contracts so that either assets or arbitrary data can be transferred between chains. The deployed mediator contracts **do not** require a set of oracles to be setup, allowing an application to launch quickly and reducing the cost of application ownership.

The mediator contracts rely on the following information about the ETH-ETC Arbitrary Message Bridge:

* **Ethereum Mainnet**:
  * AMB contract: [`0x5a91B345244d3A285b30287b4c63c154eCBD2b7e`](https://etherscan.io/address/0x5a91B345244d3A285b30287b4c63c154eCBD2b7e)
  * Gas limit to call method in the xDai chain: `2000000`
  * Finalization rate: `8` blocks
* **Ethereum Classic**:
  * AMB contract: [`0xA126c73d1bDf3a3D5F719A8D38a4692186e7503F`](https://blockscout.com/etc/mainnet/address/0xA126c73d1bDf3a3D5F719A8D38a4692186e7503F)
  * Gas limit to call method in the Ethereum Mainnet: `2000000`
  * Finalization rate: `8` block

It is possible to get an AMB transaction status by using [the Live Monitoring app](https://docs.tokenbridge.net/about-tokenbridge/components/amb-live-monitoring-application): [https://alm-etc.herokuapp.com/](https://alm-etc.herokuapp.com/).

{% hint style="success" %}
A detailed description of the AMB and examples of AMB extensions are available here: [Arbitrary Message Bridge \(AMB\)](https://docs.tokenbridge.net/amb-bridge/about-amb-bridge).
{% endhint %}

