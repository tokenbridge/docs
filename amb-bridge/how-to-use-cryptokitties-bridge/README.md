---
description: A demonstration of Arbitrary Message Bridging using CryptoKitties
---

# Demo: CryptoKitties Bridge

The CryptoKitties bridge allows users to transfer a NFT representing a Kitty from one chain to another. It demonstrates the ability to perform operations with NFTs through the Arbitrary Message Bridge \(AMB\), which is part of [the TokenBridge project](https://github.com/poanetwork/tokenbridge).

In the demos, we will transfer an NFT between 2 testnest, **Sokol** and **Kovan**. We assume that the CryptoKitties contract similar to the original [CryptoKitties](https://github.com/cryptocopycats/awesome-cryptokitties/) is deployed on the Kovan testnet. The Sokol testnet contains a modified version of [CryptoKitties](https://github.com/cryptocopycats/awesome-cryptokitties/) - it can mint a new Kitty with a specified metadata - only the mediator contract communicating with AMB is allowed to do so.

Demos are available for [NiftyWallet](niftywallet-transfer.md) and [MyEtherWallet](myetherwallet-mew-transfer.md). 

### Contracts in the Kovan testnet:

* [KittyCore](https://blockscout.com/eth/kovan/tokens/0x13AC5C6338796a31A39e74D70B0153C1bE5f53B4): ERC721 Token Contract for CryptoKitties \(approximate replica of original CryptoKitty contract\). Includes all functions that create a Kitty with unique attributes including ID, ownership, and metadata.
* [Mediator](https://blockscout.com/eth/kovan/address/0x7dB6493D9B6D99D9A240a6914AdAd5e0E8E8BE40): Token management contract that confirms transaction correctness, locks/unlocks transferred Kitties, and sends requests to mint Kitties on Sokol side.

### Contracts in the Sokol testnet:

* [Mediator](https://blockscout.com/poa/sokol/address/0x5EeC77239398FE328791E28700CAFddB2990ea97): Token management contract that confirms transaction accuracy, processes and sends token mint and burn requests, and sends requests to unlock Kitties on Kovan side.
* [SimpleBridgeKitty](https://blockscout.com/poa/sokol/address/0xc6a592ED792de33e6CBBF7ce04Dd9D3884B46B9A): Contract that creates a Kitty with identical attributes \(id, ownership, & metadata\) to the Kitty locked in the Kovan mediator contract. Kitties can only be minted through a request from the Sokol mediator contract.

### Contracts sources:

* [https://github.com/poanetwork/cryptokitties-xdai-demo](https://github.com/poanetwork/cryptokitties-xdai-demo)

### Deployed AMB bridge contracts:

* on [Kovan](https://blockscout.com/eth/kovan/address/0xfe446bef1dbf7afe24e81e05bc8b271c1ba9a560/contracts) testnet
* on [Sokol](https://blockscout.com/poa/sokol/address/0xfe446bef1dbf7afe24e81e05bc8b271c1ba9a560/contracts) testnet



