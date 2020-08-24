---
description: The AMB can be used to relay any data between chains
---

# About the AMB

The Arbitrary Message Bridge \(AMB\) is designed to relay **any data** between two EVM-based chains. The originating contract encodes data in the form of an arbitrary method call, which can also include or exclude parameters. This information, along with the target contract address, is passed to the AMB contracts. As soon as data are relayed from chain A to chain B by the Arbitrary Message Bridge oracles, the bridge contract on side B passes the ABI-encoded method to the target contract.

## **AMB usage examples:**

* transfer NFTs between two chains
* trigger a method in one chain after some contract invocation in another chain
* propagate tokens prices to another chain
* transfer digital asset \(native or ERC20 tokens\) ownership similar to the generic TokenBridge
* synchronize contracts states between two chains

AMB's universality means it can be used as a base layer for bridge and application construction. Once the bridge contracts are deployed and the corresponding validators are running the oracles, other applications can use them without the need to deploy their own infrastructure.

{% hint style="success" %}
* Check out the [ETH-xDai AMB ](../eth-xdai-amb/about-the-eth-xdai-amb.md)section to view and try some live extensions.
* Learn about our new [multi-token extension,](../eth-xdai-amb/multi-token-extension/) where an ERC20 on Ethereum is bridged and automatically created on xDai!
{% endhint %}

## Existing AMB extensions

We have developed several AMB extensions. A brief description and links to the Github repos are below.

* [native-to-erc20](https://github.com/poanetwork/tokenbridge-contracts/tree/master/contracts/upgradeable_contracts/amb_native_to_erc20) - an extension that allows a user to transfer native tokens on one chain to ERC677 tokens on another chain. It works similarly to the POA20 bridge.
* [CryptoKitties NFTs](https://github.com/poanetwork/cryptokitties-xdai-demo) - an extension prepared for demonstration purposes. It allows users to transfer CryptoKitties ERC721 tokens from the Ethereum Mainnet to the xDai chain.
* [erc20-to-erc20](https://github.com/poanetwork/tokenbridge-contracts/tree/master/contracts/upgradeable_contracts/amb_erc677_to_erc677) - an extension to transfer an ERC20 token linked with the extension to an ERC677 token on another chain. 
* [erc20-to-native](https://github.com/poanetwork/tokenbridge-contracts/tree/master/contracts/upgradeable_contracts/amb_erc20_to_native) - an extension to transfer an ERC20 token on one chain to a native token on another chain. It works similarly to the xDai bridge.
* [mutli-erc20-to-erc677](https://github.com/poanetwork/tokenbridge-contracts/tree/master/contracts/upgradeable_contracts/multi_amb_erc20_to_erc677) - an extension that allows users to transfer **any** ERC20 token to an ERC677 token on another chain. This is also known as as multi-token bridging.

## Video Explainers

### AMB Overview with Igor Barinov - EthCC 2020

{% embed url="https://youtu.be/ybnf2tR9sZQ" %}

### AMB cross-chain transfers with Alex Kolotov - [NonCon 2020](https://noncon.org/)

{% embed url="https://www.youtube.com/watch?v=3-2deK21Q14" %}

### AMB multi-token extension presentation at EDCON 2020

{% embed url="https://youtu.be/WMubACRjS\_4" %}

### AMB presentation at Waves online Meetup \(Russian presentation\)

На онлайн-митапе эксперты обсудят современные тенденции развития технологии, а также поделятся практическими решениями.

Александр Колотов, руководитель группы разработки в проекте TokenBridge, преподаватель Университета Иннополис

{% embed url="https://youtu.be/8qSnHB9g8K8?t=282" %}



