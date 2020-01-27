---
description: The AMB can be used to relay any data between chains
---

# About the AMB

The Arbitrary Message Bridge \(AMB\) is designed to relay **any data** between two EVM-based chains. The originating contract encodes data in the form of an arbitrary method call, which can also include or exclude parameters. This information, along with the target contract address, is passed to the AMB contracts. As soon as data are relayed from chain A to chain B by the Arbitrary Message Bridge oracles, the bridge contract on side B passes the ABI-encoded method to the target contract.

**AMB usage examples:**

* transfer NFTs between two chains
* trigger a method in one chain after some contract invocation in another chain
* propagate tokens prices to another chain
* transfer digital asset \(native or ERC20 tokens\) ownership similar to the generic TokenBridge
* synchronize contracts states between two chains

AMB's universality means it can be used as a base layer for bridge and application construction. Once the bridge contracts are deployed and the corresponding validators are running the oracles, other applications can use them without the need to deploy their own infrastructure.

{% hint style="success" %}
Check out the [ETH-xDai AMB ](../eth-xdai-amb-bridge/about-the-eth-xdai-amb.md)section to view and try some live extensions.
{% endhint %}

