---
description: the qDai chain information
---

# About the qDai chain

The qDai chain is an experimental chain built on top of [the Quorum technologies](https://www.goquorum.com/). [A special patch was applied](https://github.com/poanetwork/quorum/commit/0e922bd8412b2c2019624c82a2b129f5f580d8c2) to the Quorum go-client to introduce the support of [a Block Reward contract](https://openethereum.github.io/wiki/Block-Reward-Contract) the feature initially appeared in Parity Ethereum client, allowing to perform flexible minting of new tokens.

Here is the key properties of the qDai chain:

* the blocks are being produced every 1 second
* [Istanbul BFT](https://docs.goquorum.com/en/latest/Consensus/ibft/ibft/) consensus is being used
* the block limit is `74'000'000` gas
* the gas price is `0`
* there is no block reward
* new native tokens are minted as part Dai tokens deposit \(similar to [the xDai chain](https://www.xdaichain.com/)\)

The JSON RPC endpoint for the chain: [https://quorum-rpc.tokenbridge.net](https://quorum-rpc.tokenbridge.net).

The block explorer instance is available by [https://blockscout.com/poa/qdai/](https://blockscout.com/poa/qdai/).

