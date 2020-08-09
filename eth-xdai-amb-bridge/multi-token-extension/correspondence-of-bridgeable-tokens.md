---
description: >-
  The manual to find the correspondence between tokens linked with the
  multi-token mediator
---

# Correspondence of bridgeable tokens

Some users that own tokens transferred by the multi-token mediator would find useful to see ways how to discover which token contract in the Ethereum Mainnet corresponds to the token in the xDai chain.

It can be achieved by two approaches presented below.

#### Approach \#1: the BlockScout feature

The BlockScout provides an ability to see if some token was bridged through the multi-token extension.

![](../../.gitbook/assets/image%20%2890%29.png)

The link that is available on the token name will lead to the token view in the BlockScout:

![](../../.gitbook/assets/image%20%2870%29.png)

This view contains the information that this token was bridged and a link to the original token.

![](../../.gitbook/assets/image%20%2858%29.png)

#### Approach \#2: the mediator storage

The multi-token mediator on the xDai chain \([`0xf6A78083ca3e2a662D6dd1703c939c8aCE2e268d`](https://blockscout.com/poa/xdai/address/0xf6A78083ca3e2a662D6dd1703c939c8aCE2e268d)\) provides methods that allow to see correspondence of bridgeable tokens:

* `foreignTokenAddress` - returns an address of the token contract on the Ethereum Mainnet by specifying the address of the token contract on the xDai chain.
* `homeTokenAddress` - returns an address of the token contract on the xDai chain by specifying the address of the token contract on the Ethereum Mainnet chain.

![The contract page in the BlockScout allows to read the contract&apos;s data](../../.gitbook/assets/image%20%2892%29.png)

![The method to get correspondence for the token contract on the xDai](../../.gitbook/assets/image%20%2862%29.png)

![The method returns the address of the token contract on the Ethereum Mainnet](../../.gitbook/assets/image%20%2864%29.png)

