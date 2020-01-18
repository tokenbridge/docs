---
description: Description of the AMB bridge extension allowing transfer sUSD tokens
---

# sUSD bridge extension

sUSD bridge extension of ETH-xDai Arbitrary Message Bridge is the pair of mediator contracts \(similar to used [here](https://docs.tokenbridge.net/amb-bridge/erc677-to-erc677-bridge-on-top-of-amb)\) allowing to transfer [Synth sUSD](https://etherscan.io/token/0x57ab1e02fee23774580c119740129eac7081e9d3) from the Ethereum Mainnet to the xDai chain and back.

* Mediator contract at Ethereum Mainnet:
  * [`0x71F12d03E1711cb96E11E1A5c12Da7466699Db8D`](https://etherscan.io/address/0x71F12d03E1711cb96E11E1A5c12Da7466699Db8D)
* Mediator contract at xDai chain:
  * [`0xD9a3039cfC70aF84AC9E566A2526fD3b683B995B`](https://blockscout.com/poa/xdai/address/0xd9a3039cfc70af84ac9e566a2526fd3b683b995b/transactions)

This extension is mostly was deployed to demonstrate work of the ETH-xDai AMB. Anyone who owns sUSD tokens could deposit few of them in the xDai chain as so the same amount of [sUSD bridgeable tokens](https://blockscout.com/poa/xdai/address/0x4c36d2919e407f0cc2ee3c993ccf8ac26d9ce64e) will be minted there. The reverse operation will burn sUSD bridgeable tokens in xDai chain and unlock Synth sUSD tokens in the Ethereum Mainnet.

The step by step instructions could be used to [Transfer sUSD through the bridge extension](https://docs.tokenbridge.net/eth-xdai-amb-bridge/susd-bridge-extension/transfer-susd-through-the-bridge-extension).

