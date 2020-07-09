---
description: the qDai chain information
---

# About the qDai chain

The qDai chain is an experimental chain built on top of [the Quorum blockchain platform. ](https://www.goquorum.com/)[A special patch was applied](https://github.com/poanetwork/quorum/commit/0e922bd8412b2c2019624c82a2b129f5f580d8c2) to the Quorum go-client to support [a Block Reward contract](https://openethereum.github.io/wiki/Block-Reward-Contract). This feature initially appeared in the Parity Ethereum client, and allows flexible token minting.

Key properties of the qDai chain:

* Blocks are produced every 1 second
* [Istanbul BFT](https://docs.goquorum.com/en/latest/Consensus/ibft/ibft/) consensus
* Block limit is `74'000'000` gas
* Gas price is `0`
* No block reward
* new native tokens are minted as part Dai tokens deposit \(similar to [the xDai chain](https://www.xdaichain.com/)\)

The JSON RPC endpoint for the chain: [https://quorum-rpc.tokenbridge.net](https://quorum-rpc.tokenbridge.net).

The block explorer instance is available at [https://blockscout.com/poa/qdai/](https://blockscout.com/poa/qdai/).

