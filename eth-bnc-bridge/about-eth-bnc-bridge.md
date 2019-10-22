---
description: >-
  Experimental bridge to relay ERC20 tokens from an EVM-based chain to the
  Binance chain
---

# About ETH-BNC bridge

The TokenBridge solution allows digital asset transfer between two Ethereum Virtual Machine \(EVM\) based chains. Bridge operations are served by the TokenBridge oracles \(Validators\) - nodes that listen to user's relay requests. A user sends funds to a specific \(bridge\) account in one chain and formulates the relay request. Then, each validator node votes to approve the requested relay operation using a multisig wallet. As soon as enough votes are collected, the relay request is finalized and the corresponding asset amount is unlocked.

The [Binance Chain](https://docs.binance.org/) does not support multisig wallets. However, the same voting functionality described above can be implemented with a [Threshold Signature Scheme](https://zengo.com/implementing-open-source-tss-to-binance-coin-bnb/) \(TSS\). A TSS uses Multiparty Computation to generate a digital signature of a message in a trustless manner, using a subset of validators.

The ETH-to-BNC bridge combines the TokenBridge approach with a TSS to approve relay operations and facilitate asset transfer between an EVM chain and the Binance chain. 

