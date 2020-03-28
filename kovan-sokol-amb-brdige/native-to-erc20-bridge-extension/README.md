---
description: >-
  Description of the AMB bridge extension to test native tokens relay to ERC20
  tokens
---

# native-to-ERC20 bridge extension

The native-to-ERC20 bridge extension of the Kovan-Sokol Arbitrary Message Bridge is a pair of mediator contracts allowing to test transfers of native tokens to another chain in form of ERC20-compatible tokens.

The initial goals to deploy this extension were:

* investigate the ability to transfer native tokens to another chain through AMB; these experiments will be used to migrate existing bridges such as the POA-POA20 bridge and WETC bridge to the Arbitrary Message Bridge platform
* demonstrate of collecting fees on AMB contracts with Gas Token
* test a new Burner Wallet plugin to transfer assets through AMB

The contract addresses:

* The bridgeable token at Kovan Testnet:
  * [`0xff94183659f549D6273349696d73686Ee1d2AC83`](https://kovan.etherscan.io/address/0xff94183659f549d6273349696d73686ee1d2ac83)
* Mediator contract at Kovan Testnet:
  * [`0x99FB1a25caeB9c3a5Bf132686E2fe5e27BC0e2dd`](https://kovan.etherscan.io/address/0x99fb1a25caeb9c3a5bf132686e2fe5e27bc0e2dd)
* Mediator contract at POA Sokol Testnet:
  * [`0x867949C3F2f66D827Ed40847FaA7B3a369370e13`](https://blockscout.com/poa/sokol/address/0x867949C3F2f66D827Ed40847FaA7B3a369370e13)

Anyone who owns SPOA native tokens can use the bridge - SPOAs are locked in the bridge mediator contract and the same amount of KSPOA tokens are minted on the Kovan testnet. The reverse operation burns KSPOA bridgeable tokens on the Kovan testnet and unlock SPOA native tokens on the Sokol testnet.

