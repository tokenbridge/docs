---
description: Find the analogous token address for tokens bridged on Ethereum and xDai
---

# Corresponding token contract addresses (ETH - XDAI)

There are several approaches to discover the token contract on the Ethereum Mainnet that corresponds to the token contract on the xDai chain.

## Approach #1: BlockScout

BlockScout allows you to see if a token was bridged using the multi-token extension.

![](<../../.gitbook/assets/image (67).png>)

The link available on the token name leads to the token view in the BlockScout:

![](<../../.gitbook/assets/image (68).png>)

This view contains information that this token was bridged and a link to the original token.

![](<../../.gitbook/assets/image (84).png>)

BlockScout also distinguishes bridged tokens at the _Top of the tokens_ page by specifying the bridged property. A worker which fetches this property checks new unprocessed tokens every 1 minute and updates bridged status and it is bridged, adds a link to the original token.

![](<../../.gitbook/assets/image (2) (1).png>)

## Approach #2: Mediator storage

The multi-token mediator on the xDai chain ([`0xf6A78083ca3e2a662D6dd1703c939c8aCE2e268d`](https://blockscout.com/xdai/mainnet/address/0xf6A78083ca3e2a662D6dd1703c939c8aCE2e268d)) provides methods for viewing correspondence of bridgeable tokens:

* `foreignTokenAddress` - returns the address of the token contract on the Ethereum Mainnet by specifying the address the token contract on the xDai chain.
* `homeTokenAddress` - returns the address of the token contract on the xDai chain by specifying the address of the token contract on the Ethereum chain.

![The contract page in the BlockScout allows to read the contract's data](<../../.gitbook/assets/image (85).png>)

![The method to get correspondence for the token contract on the xDai](<../../.gitbook/assets/image (86).png>)

![The method returns the address of the token contract on the Ethereum Mainnet](<../../.gitbook/assets/image (87).png>)
