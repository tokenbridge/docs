---
description: Useful documents helping to use the multi-token AMB extension
---

# Multi-token extension

The multi-token extension for the Arbitrary Message Bridge between the Ethereum Mainnet and the xDai chain is the simplest way to transfer **ANY** ERC20/ERC677/ERC827 token to the xDai chain.

{% hint style="info" %}
An AMB bridge extension is a pair of mediator contracts associated with a specific pair of Arbitrary Message Bridge contracts.
{% endhint %}

By using this extension any user \(not only the token contract owner\) is able to transfer tokens from the Ethereum Mainnet to the chain with cheap and fast transactions without necessity to deploy any additional contracts. The specified amount tokens is locked in the mediator contract, a new token contract is deployed automatically on the xDai chain and the required amount tokens is minted on the xDai chain. The reverse operation burns bridgeable tokens on the xDai chain and unlocks the tokens on the required token contract in the Ethereum Mainnet.

{% hint style="info" %}
More details for the operations to deposit and withdraw tokens are available here.
{% endhint %}

## Technical information and parameters of the extension

The mediator contract on the Ethereum Mainnet: [`0x88ad09518695c6c3712AC10a214bE5109a655671`](https://etherscan.io/address/0x88ad09518695c6c3712AC10a214bE5109a655671)

The mediator contract on the xDai chain: [`0xf6A78083ca3e2a662D6dd1703c939c8aCE2e268d`](https://blockscout.com/poa/xdai/address/0xf6A78083ca3e2a662D6dd1703c939c8aCE2e268d)

### Transfer limits 

Transfer limits are configured per a particular pair of tokens.

Default limits to transfer assets **from the Ethereum Mainnet to the xDai chain**:

* Daily limit: 1'000'000 tokens
* Maximum per transaction: 100'000 tokens
* Minimum per transaction: 1 token

Default limits to transfer assets **from the xDai chain to the Ethereum Mainnet**:

* Daily limit: 10'000 tokens
* Maximum per transaction: 3'000 tokens
* Minimum per transaction: 1 token

### Bridge operations fees

There are no fees \(except gas fees for the originating transaction\) to transfer assets from the Ethereum Mainnet to the xDai chain.

The fee to transfer assets\(besides gas fees for the originating transaction\) from the xDai chain to the Ethereum Mainnet is **0.5%**.

The fees are also configured per a particular pair of tokens.



