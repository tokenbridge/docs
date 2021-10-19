---
description: ETH-POA Arbitrary Message Bridge information
---

# About the ETH-POA AMB

An Arbitrary Message Bridge (AMB) between the Ethereum Mainnet and the POA Network extends the number of the applications that can leverage cross-chain communications.

Any application can [build its own AMB extension](https://docs.tokenbridge.net/amb-bridge/how-to-develop-xchain-apps-by-amb). This is represented by two mediator contracts so that either assets or arbitrary data can be transferred between chains. The deployed mediator contracts **do not** require a set of oracles to be setup, allowing an application to launch quickly and reducing the cost of application ownership.

The mediator contracts rely on the following information about the ETH-POA Arbitrary Message Bridge:

* **Ethereum Mainnet**:
  * AMB contract: [`0x2140ECDC45c89ca112523637824513baE72C8671`](https://etherscan.io/address/0x2140ECDC45c89ca112523637824513baE72C8671)``
  * Gas limit to call method in the POA Network: `2000000`
  * Finalization rate: `8` blocks
* **POA Network**:
  * AMB contract: [`0xD9a3039cfC70aF84AC9E566A2526fD3b683B995B`](https://blockscout.com/poa/core/address/0xd9a3039cfc70af84ac9e566a2526fd3b683b995b/transactions)``
  * Gas limit to call method in the Ethereum Mainnet: `2000000`
  * Finalization rate: `1` block

{% hint style="success" %}
A detailed description of the AMB and examples of AMB extensions are available here: [Arbitrary Message Bridge (AMB)](https://docs.tokenbridge.net/amb-bridge/about-amb-bridge).
{% endhint %}
