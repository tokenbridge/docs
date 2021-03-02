---
description: Description of the AMB bridge extension allowing for BRICK tokens transfer
---

# BRICK bridge extension

The MOON bridge extension of the Rinkeby-xDai Arbitrary Message Bridge allows a user to transfer [BRICK tokens](https://rinkeby.etherscan.io/token/0xe0d8d7b8273de14e628d2f2a4a10f719f898450a), [a new method](https://www.reddit.com/r/FortNiteBR/comments/gj8tm1/introducing_rfortnitebr_bricks/) by which the [r/FortNiteBR](https://www.reddit.com/r/FortNiteBR/) subreddit's contributors are rewarded. The transfer may happen from the Rinkeby Testnet to the xDai chain as well as in the opposite direction.

* Mediator contract at Rinkeby Mainnet: [`0xD925002f88279776dEB4907bA7F8dC173e2EA7a7`](https://rinkeby.etherscan.io/address/0xD925002f88279776dEB4907bA7F8dC173e2EA7a7)
* Mediator contract at xDai chain: [`0xf85b17E64Bc788D0CB1A8c8C87c0d74e520c2A54`](https://blockscout.com/xdai/mainnet/address/0xf85b17E64Bc788D0CB1A8c8C87c0d74e520c2A54)
* BRICK tokens on Rinkeby [`0xe0d8d7b8273de14e628d2f2a4a10f719f898450a`](https://rinkeby.etherscan.io/address/0xe0d8d7b8273de14e628d2f2a4a10f719f898450a)
* xBRICK tokens on xDai [`0x2f9ceBf5De3bc25E0643D0E66134E5bf5c48e191`](https://blockscout.com/xdai/mainnet/address/0x2f9ceBf5De3bc25E0643D0E66134E5bf5c48e191) 

Anyone who owns [BRICK tokens](https://rinkeby.etherscan.io/token/0xe0d8d7b8273de14e628d2f2a4a10f719f898450a) on Rinkeby can use the bridge. BRICKs are locked in the mediator contract and the same amount of [xBRICK bridgeable tokens](https://blockscout.com/xdai/mainnet/address/0x2f9ceBf5De3bc25E0643D0E66134E5bf5c48e191) are minted on the xDai chain. The reverse operation burns xBRICK bridgeable tokens on the xDai chain and unlocks BRICK tokens on the Rinkeby Testnet.

