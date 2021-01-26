---
description: TokenBridge provides data and token transfer capabilities across EVM chains
---

# Welcome

The TokenBridge allows users to transfer data \(e.g. digital asset ownership information\) between two chains in the Ethereum ecosystem. Cross-chain bridges provide fast and secure connections between blockchains, creating scalability and connection - interoperability - between Ethereum networks. 

## Navigating the docs

TokenBridge docs are organized in the sidebar menu.

1. [**About TokenBridge**](about-tokenbridge/features/): General info and details about the implementation, including a link to the monorepo at [https://github.com/poanetwork/tokenbridge](https://github.com/poanetwork/tokenbridge)
2. \*\*\*\*[**Arbitrary Message Bridge \(AMB\)**](amb-bridge/arbitrary-message-bridge-deployment/): A bridge designed for universal cross-chain data transfer. Includes parameters, how-tos and examples.
3. Bridge-by-bridge details. Each section includes technical and connection details as well as links to examples and use-cases.
   1. \*\*\*\*[**xDai Bridge**](xdai-bridge/about.md): ERC20-to-Native TokenBridge implementation
   2. \*\*\*\*[**ETH-xDai AMB**](eth-xdai-amb-bridge/about-the-eth-xdai-amb.md): AMB between Ethereum and xDai, includes the Multi-token bridge extension.
   3. \*\*\*\*[**Rinkeby-xDai AMB**](rinkeby-xdai-amb-bridge/about-the-rinkeby-xdai-amb.md): AMB between Rinkeby testnet and xDai. Used for xMOON projects.
   4. \*\*\*\*[**Kovan-Sokol AMB**](kovan-sokol-amb-bridge/about-the-kovan-sokol-amb/): Useful for testing applications and extensions.
   5. \*\*\*\*[**ETH-POA AMB**](eth-poa-amb-bridge/about-the-eth-poa-amb.md): AMB between Ethereum mainnet and POA Network.
   6. \*\*\*\*[**ETH-ETC AMB**](eth-etc-amb-bridge/about-the-eth-etc-amb.md):  AMB between Ethereum Mainnet and Ethereum Classic. Used to create WETC on Ethereum.
   7. \*\*\*\*[**ETH-qDai AMB**](eth-qdai-bridge/about-the-eth-qdai-amb.md): Bridge between the experimental Quorum chain and the Ethereum Mainnet.
   8. \*\*\*\*[**ETH-BNC Bridge**](eth-bnc-bridge/about-eth-bnc-bridge.md):  combines the TokenBridge + a Threshold Signature Scheme approach to bridge between Ethereum and Binance Chain. 

## **Production asset-transfer bridges**

The following bridges are fully-functional in production environments:

* \*\*\*\*[**POA Bridge**](https://bridge.poa.net/) \(POA network to Eth Mainnet\):The POA Bridge was the first EVM cross-chain production bridge in existence.
* \*\*\*\*[**xDai Bridge**](https://dai-bridge.poa.network/) \(Eth Mainnet to xDai Network\): The xDai chain uses the ERC20-to-Native TokenBridge functionality to provide fast, inexpensive and stable transactions.
* \*\*\*\*[**Eth Classic Bridge**](https://wetc-app.herokuapp.com/) \(Eth Classic to Eth Mainnet\): The Eth Classic Bridge connects ETC to ETH, where ETC is available as WETC.

![POA Bridge UI](.gitbook/assets/poa-bridge.png)

![xDai Bridge UI](.gitbook/assets/bridge1.jpg)

## \*\*\*\*

