# About the AMB

Intention of the Arbitrary Message Bridge is to relay any data between two EVM-based chains. The originating contract encode data that need to be transferred in form of arbitrary method call together with parameters or without them. It passes them and the target contract address to the AMB contracts. As soon as the data are relayed to the another side by the Arbitrary Message Bridge oracles, the bridge contract on that side will pass the ABI-encoded method to the target contract.

AMB can be used:

* to transfer NFTs between two chains
* to trigger a method in one chain after some contract invocation in another chain
* to propagate tokens prices to another chain
* to transfer digital assets \(native or ERC20 tokens\) ownership similar to generic TokenBridge bridge
* to synchronize contracts states between two chains
* etc.

Universality of AMB allows to consider it as a low level protocol that can be used to build different type of bridges on top. Once the bridge contracts are deployed and the corresponding validators run the oracles other applications could use them without necessity to deploy their own infrastructure.

