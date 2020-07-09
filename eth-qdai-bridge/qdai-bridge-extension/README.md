---
description: Description of the AMB bridge extension allowing for DAI token transfer
---

# qDai bridge extension

The qDai bridge extension of the ETH-qDai Arbitrary Message Bridge is a pair of mediator contracts allowing the user to transfer [DAI stable tokens](https://makerdao.com/en/) from the Ethereum Mainnet to the qDai chain and back.

This extension allows users to transform DAI \(an ERC20 stable token\) on the mainnet into qDai on an EVM-compatible chain. qDai native tokens can then be sent quickly and with 0 cost on the qDai network.

* Mediator contract at Ethereum Mainnet:
  * [`0xf6edFA16926f30b0520099028A145F4E06FD54ed`](https://etherscan.io/address/0xf6edFA16926f30b0520099028A145F4E06FD54ed)
* Mediator contract at qDai chain:
  * [`0xFEaB457D95D9990b7eb6c943c839258245541754`](https://blockscout.com/poa/qdai/address/0xFEaB457D95D9990b7eb6c943c839258245541754/transactions)

This extension was deployed to demonstrate an ability to transfer assets from a public chain to an enterprise chain. Anyone who owns [DAI tokens](https://etherscan.io/token/0x6b175474e89094c44da98b954eedeac495271d0f) can use the bridge - DAIs are locked in the bridge contract and the same amount of qDai native tokens are minted on the qDai chain. The reverse operation burns qDai tokens on the qDai chain and unlocks DAI tokens on the Ethereum Mainnet.

{% hint style="info" %}
The code of the mediators implementing this extension can be found [here](https://github.com/poanetwork/tokenbridge-contracts/tree/master/contracts/upgradeable_contracts/amb_erc20_to_native).
{% endhint %}

