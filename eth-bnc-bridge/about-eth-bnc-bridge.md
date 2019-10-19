---
description: >-
  Experimental bridge to relay ERC20 tokens from an EVM-based chain to the
  Binance chain
---

# About ETH-BNC bridge

The TokenBridge solution suggests for users functionality to transfer digital assets between two EVM based chains. The bridge operations are served by the TokenBridge oracles \(Validators\) - nodes that listen user's relay requests. A user sends funds to a specific \(bridge\) account in one chain and formulate the relay request. Every node votes for the relay operation for the request. As soon as enough votes collected the relay request finalized and the corresponding amount of assets is unlocked.

The [Binance Chain](https://docs.binance.org/) does not support any kind of multisig wallets that is why the functionality to vote for the request can be implemented with [Threshold Signature Scheme](https://zengo.com/implementing-open-source-tss-to-binance-coin-bnb/) - a system utilizing Multiparty Computation to generate a digital signature of a message in a trustless manner involving subset of validators.

The ETH-to-BNC bridge combine the TokenBridge approach with the Threshold Signature Scheme to swap assets from an Ethereum Virtual Machine based chain to the Binance Chain and back with applying the voting mechanics by authorities.

