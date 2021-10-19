---
description: A demonstration of Arbitrary Message Bridging using CryptoKitties
---

# 😸 CryptoKitties AMB bridge extension Demo

{% hint style="info" %}
**An AMB bridge extension** is a pair of mediator contracts associated with a specific pair of Arbitrary Message Bridge contracts.
{% endhint %}

The CryptoKitties bridge extension allows users to transfer a NFT representing a cat from one chain to another. It demonstrates the ability to perform operations with NFTs through the Arbitrary Message Bridge (AMB), which is part of [the TokenBridge project](https://github.com/poanetwork/tokenbridge).

In the demos, we deploy contracts and then transfer an NFT between 2 testnets, **Sokol** and **Kovan**.&#x20;

* **Deployed on Kovan**:&#x20;
  * CryptoKitties contract (KittyCore) similar to the original [CryptoKitties](https://github.com/cryptocopycats/awesome-cryptokitties/)&#x20;
  * A mediator contract (ForeignMediator). Kovan is called the foreign bridge in this scenario&#x20;
* **Deployed on Sokol**:&#x20;
  * A modified version of [CryptoKitties](https://github.com/cryptocopycats/awesome-cryptokitties/) which can mint a new cat with the same specified metadata (SimpleBridgeKitty)
  * A mediator contract (HomeMediator). Sokol is called the home bridge. Only the mediator contract communicating with the AMB is allowed to mint a cat.

{% hint style="info" %}
It is possible to deploy the contracts in the opposite direction as well (where KittyCore & ForeignMediator are deployed on Sokol & SimpleBridgeKitty & HomeMediator on Kovan). For demo purposes, we arbitrarily chose Kovan as the foreign network.
{% endhint %}

![A test cat deployed on Kovan](../../.gitbook/assets/pretty\_kitty.png)

## Getting Started

{% hint style="warning" %}
In the following example we deploy contracts enable test CryptoKitty creation. If you choose to deploy your own contracts, you can also create additional test cats using this instruction.

If you would like to try bridging **without creating your own test cat**, please contact us on [Discord](https://discord.gg/mPJ9zkq) or the [TokenBridge forum ](https://forum.poa.network/c/tokenbridge/)with your wallet address, and we will send you a kitty to play with :heart\_eyes\_cat:.  With a test cat, you can start from step 4 below.
{% endhint %}

### Example Instructions

1. [Deploy CryptoKitty Contracts on both networks](deploy-cryptokitty-contracts.md)
2. [Verify Contracts in BlockScout](verify-contracts-in-blockscout.md)
3. [View Kitties in BlockScout (optional)](view-in-blockscout.md)
4. Use one of these methods to initiate and complete an NFT transfer between networks:
   1. [NiftyWallet Transfer](niftywallet-transfer.md)
   2. [MyEtherWallet Transfer](myetherwallet-mew-transfer.md)

## Additional Information

### Example Contracts in the Kovan (foreign) testnet:

* [KittyCore](https://blockscout.com/eth/kovan/tokens/0x13AC5C6338796a31A39e74D70B0153C1bE5f53B4): ERC721 Token Contract for CryptoKitties (approximate replica of original CryptoKitty contract). Includes all functions that create a Kitty with unique attributes including ID, ownership, and metadata.
* [ForeignMediator](https://blockscout.com/eth/kovan/address/0x7dB6493D9B6D99D9A240a6914AdAd5e0E8E8BE40/transactions): Token management contract that confirms transaction correctness, locks/unlocks transferred Kitties, and sends requests to mint Kitties on Sokol side.

### Example Contracts in the Sokol (home) testnet:

* [HomeMediator](https://blockscout.com/poa/sokol/address/0x5EeC77239398FE328791E28700CAFddB2990ea97/transactions): Token management contract that confirms transaction accuracy, processes and sends token mint and burn requests, and sends requests to unlock cats on Kovan side.
* [SimpleBridgeKitty](https://blockscout.com/poa/sokol/address/0xc6a592ED792de33e6CBBF7ce04Dd9D3884B46B9A): Contract that creates a cat with identical attributes (id, ownership, & metadata) to the cat locked in the Kovan mediator contract. Cats can only be minted through a request from the Sokol mediator contract.

### Contracts source:

* [https://github.com/poanetwork/cryptokitties-xdai-demo](https://github.com/poanetwork/cryptokitties-xdai-demo)

### Deployed AMB bridge contracts:

* on [Kovan](https://blockscout.com/eth/kovan/address/0xfe446bef1dbf7afe24e81e05bc8b271c1ba9a560/contracts) testnet
* on [Sokol](https://blockscout.com/poa/sokol/address/0xfe446bef1dbf7afe24e81e05bc8b271c1ba9a560/contracts) testnet

