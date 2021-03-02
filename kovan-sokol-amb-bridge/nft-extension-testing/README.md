---
description: >-
  Technical details about the NFT OmniBridge AMB extension deployed for testing
  purposes
---

# NFT extension \(testing\)

This is a test version of the NFT OmniBridge AMB extension. The extension provides an ability to transfer any non-fungible tokens implemented through ERC721 compatible token contracts from one chain to another. 

## Technical details

The extension works with tokens originally deployed on either side of the bridge. It uses the concept of mirroring:

1. A non-fungible token is locked on one side of the bridge - the OmniBridge mediator contract becomes the owner of the token.
2. The new token is minted on the other side of the bridge with the same Token ID and TokenURI. The owner of the new token is set to the same account that sent the token to the bridge as part of the originating transaction \(an alternative receiver feature can be used to specify another token owner\). **The only thing that can be changed in the bridged token is the owner. No other data like the Token URI can be updated on chain.** 
3. If the token is bridged back, it is burned and the token with the corresponding Token ID is unlocked on that side of the bridge which is the origin of the token.

Uniqueness of the bridged NFTs is provided through making a correspondence between the originating token contract and the contact which appears during the transfer of the first token from this contract. It is better to explain this in an example:

* Consider an ERC721 contract _A_ that has an NFT with ID 1. The bridging of this token causes the deployment of a new contract _A\*_ and minting of an NFT with ID 1. If later the token with the ID 1 of another ERC721 contract _B_ is transferred through the bridge, a contract _B\*_ will be deployed so the token 1 of the contract _A\*_ and the token 1 of the contract _B\*_ maintain their uniqueness. 

## Deployment information

* Mediator contract on the Kovan testnet: [`0x63be59CF177cA9bb317DE8C4aa965Ddda93CB9d7`](https://kovan.etherscan.io/address/0x63be59cf177ca9bb317de8c4aa965ddda93cb9d7#code)
* Mediator contract on the Sokol chain: [`0x3ecEe2667f80fc0858437119621b820efc6b0Ede`](https://blockscout.com/poa/sokol/address/0x3ecEe2667f80fc0858437119621b820efc6b0Ede/contracts)



