---
description: Description of the AMB bridge extension allowing for MOON tokens transfer
---

# MOON bridge extension

The MOON bridge extension of the Rinkeby-xDai Arbitrary Message Bridge allows a user to transfer [Moon tokens](https://rinkeby.etherscan.io/address/0xdf82c9014f127243ce1305dfe54151647d74b27a), [a new method](https://www.reddit.com/r/CryptoCurrency/comments/gj96lb/introducing_rcryptocurrency_moons/) by which the [r/CryptoCurrency](https://www.reddit.com/r/CryptoCurrency/) subreddit's contributors are rewarded. The transfer may happen from the Rinkeby Testnet to the xDai chain as well as in the opposite direction.

* Mediator contract at Rinkeby Mainnet:[`0xFEaB457D95D9990b7eb6c943c839258245541754`](https://rinkeby.etherscan.io/address/0xFEaB457D95D9990b7eb6c943c839258245541754)\`\`
* Mediator contract at xDai chain:[`0x1E0507046130c31DEb20EC2f870ad070Ff266079`](https://blockscout.com/poa/xdai/address/0x1E0507046130c31DEb20EC2f870ad070Ff266079)
* Moon tokens on Rinkeby [`0xDF82c9014F127243CE1305DFE54151647d74B27A`](https://rinkeby.etherscan.io/address/0xdf82c9014f127243ce1305dfe54151647d74b27a)\`\`
* xMoon tokens on xDai [`0x1e16aa4Df73d29C029d94CeDa3e3114EC191E25A`](https://blockscout.com/poa/xdai/tokens/0x1e16aa4Df73d29C029d94CeDa3e3114EC191E25A) 

Anyone who owns [MOON tokens](https://rinkeby.etherscan.io/address/0xdf82c9014f127243ce1305dfe54151647d74b27a) on Rinkeby can use the bridge. MOONs are locked in the mediator contract and the same amount of [xMOON bridgeable tokens](https://blockscout.com/poa/xdai/address/0xC5C35D01B20f8d5cb65C60f02113EF6cd8e79910) are minted on the xDai chain. The reverse operation burns xMOON bridgeable tokens on the xDai chain and unlocks MOON tokens on the Rinkeby Testnet.

