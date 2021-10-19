---
description: Full duplex bridge for ERC20-based tokens between POA Network and xDai
---

# OmniBridge Extension

The OmniBridge multi-token extension for the Arbitrary Message Bridge between the POA Network and the xDai chain is the simplest way to transfer **ANY** ERC20/ERC677/ERC827 token to and from the xDai chain.

By using this extension any user (not only the token contract owner) can transfer tokens in both directions: from POA to xDai and from the xDai chain to POA Network with fast, inexpensive transactions and without deploying any additional contracts.&#x20;

The specified token amount is locked in the mediator contract, a new token contract is deployed automatically on the POA/xDai chain, and the requested token amount is minted on the xDai/POA chain. The reverse operation burns bridged tokens on the xDai/POA chain and unlocks the tokens from the token contract on another side of the bridge.

Note that tokens are appended with the name of the originating chain "from POA" or "from xDai" when bridging.

## OmniBridge technical information and extension parameters

* Mediator contract on POA Network: [`0x8134470b7CF6f57Faee2076adf8F7301fD5865a5`](https://blockscout.com/poa/core/address/0x8134470b7CF6f57Faee2076adf8F7301fD5865a5)
* Mediator contract on the xDai chain: [`0x63be59CF177cA9bb317DE8C4aa965Ddda93CB9d7`](https://blockscout.com/xdai/mainnet/address/0x63be59CF177cA9bb317DE8C4aa965Ddda93CB9d7)

### Transfer limits&#x20;

Transfer limits are configured per a particular pair of tokens.&#x20;

**Default limits:**

Default limits to transfer assets **from POA Network to the xDai chain**:

* Daily limit: 10'000'000'001 tokens
* Maximum per transaction: 10'000'000'000 tokens
* Minimum per transaction: 0.00001 token

Default limits to transfer assets **from the xDai chain to POA Network **

* Daily limit: 10'000'000'001 tokens
* Maximum per transaction: 10'000'000'000 tokens
* Minimum per transaction: 0.00001 token

### Bridge operation fees

Fees are also configurable per a particular pair of tokens.

**Default fees:**

* There are no fees (**except gas fees** for the originating transaction) to transfer assets from the POA Network to the xDai chain.
* The fee to transfer assets (besides gas fees for the originating transaction) from the xDai chain to POA Network is **0.1%**.
