---
description: >-
  Technical details about the NFT OmniBridge AMB extension deployed on top of
  AMB between the Rinkeby testnet and the xDai chain
---

# NFT OmniBridge extension

This is a beta version of the NFT OmniBridge AMB extension. The extension allows users to transfer any non-fungible tokens implemented through ERC721 and EIP1155 compatible token contracts from one chain to another.

{% hint style="info" %}
The main idea of this bridge is to allow owners of NFTs on the xDai chain to test compatibility of the tokens on test version of [the market place OpenSea](https://testnets.opensea.io/get-listed/step-two).
{% endhint %}

## Technical details <a href="technical-details" id="technical-details"></a>

The extension works with tokens originally deployed on either side of the bridge. It uses the mirroring concept:

1. A non-fungible token is locked on one side of the bridge - the OmniBridge mediator contract becomes the owner of the token. For EIP1155 tokens it is possible to send several tokens at once.
2. The new token is minted on the other side of the bridge with the same Token ID and TokenURI. The owner of the new token is by default set to the same account that sent the token to the bridge in the originating transaction (an alternative receiver feature can be used to specify another token owner). **The only thing that can be changed in the bridged token is the owner. No other data like the Token URI can be updated on chain.**
3. If the token is bridged back, it is burned and the token with the corresponding Token ID is unlocked on that side of the bridge where the token originated.

A bridged NFTs uniqueness is provided by making a correspondence between the originating token contract and the contact which appears during the transfer of the first token from this contract. An example:

* Consider an ERC721 contract _A_ that has an NFT with ID 1. The bridging of this token causes the deployment of a new contract _A\*_ and minting of an NFT with ID 1. If later the token with the ID 1 of another ERC721 contract _B_ is transferred through the bridge, a contract _B\*_ will be deployed so the token 1 of the contract _A\*_ and the token 1 of the contract _B\*_ maintain their uniqueness.

## Deployment information <a href="deployment-information" id="deployment-information"></a>

* Mediator contract on the Rinkeby Testnet: [`0xEc05e3f4D845f0E39e33146395aCE5D35c01Fcc0`](https://rinkeby.etherscan.io/address/0xEc05e3f4D845f0E39e33146395aCE5D35c01Fcc0)
* Mediator contract on the xDai chain: [`0x2c0bF58cC87763783e35a625ff6a3e50d9E05337`](https://blockscout.com/poa/xdai/address/0x2c0bF58cC87763783e35a625ff6a3e50d9E05337)
