---
description: ETH-BSC Arbitrary Message Bridge information
---

# About the ETH-BSC AMB

The Arbitrary Message Bridge between the Ethereum Mainnet and the Binance Smart Chain is mostly setup as an experiment.

{% hint style="warning" %}
Due to high gas prices in both chains it is hard to maintain this bridge: upgrade of the contracts with new fixes and improvements is being performed with lower priority, there could be also lack of funds on the bridge oracles.
{% endhint %}

The mediator contracts could use the following information about the ETH-BSC Arbitrary Message Bridge:

* **Ethereum Mainnet**:
  * AMB contract: [`0x07955be2967B655Cf52751fCE7ccC8c61EA594e2`](https://etherscan.io/address/0x07955be2967B655Cf52751fCE7ccC8c61EA594e2)
  * Gas limit to call method in the Binance Smart Chain: `1000000`
  * Finalization rate: `8` blocks
* **Binance Smart Chain**:
  * AMB contract: [`0x6943a218d58135793f1fe619414ed476c37ad65a`](https://bscscan.com/address/0x6943a218d58135793f1fe619414ed476c37ad65a)
  * Gas limit to call method in the Ethereum Mainnet: `1000000`
  * Finalization rate: `8` blocks

### Transactions

It is possible to get the status of an AMB transaction using [the Live Monitoring app](https://docs.tokenbridge.net/about-tokenbridge/components/amb-live-monitoring-application): [http://alm-bsc.herokuapp.com/](http://alm-bsc.herokuapp.com/). Transactions require a multi-sig \(for bridge validators, not users\) for a successful transfer. Current validators can be viewed with the live monitoring application.

### Bridge Oracles

For transactions from BSC manual execution is required. This action delivers the validator confirmations gathered on BSC to the Mainnet and triggers the transferred message handling. Since the bridge oracles does not operate with the Ethereum Mainnet directly they do not need to have a positive balance on this chain.

At the same time, the process of the confirmation delivery to BSC requires from the bridge oracles to have BNB for gas fees. If it is found that some bridge oracle does not send transactions, consider to top up its account on BSC. The list of oracles is available by using the method `validatorList` of the validator set contract: [`0xc7b4618d03a756f8345bd1bf1cccbe3681f823ef`](https://bscscan.com/address/0xc7b4618d03a756f8345bd1bf1cccbe3681f823ef#readProxyContract)

