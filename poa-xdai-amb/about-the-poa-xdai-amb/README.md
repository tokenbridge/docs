---
description: POA-xDai Arbitrary Message Bridge information
---

# About the POA-xDai AMB

The main goal of the Arbitrary Message Bridge between the POA Network and the xDai chain is to provide a platform for the OmniBridge connecting both chains.

Similar to other AMBs deployed between other chains, anyone is able to develop and deploy a pair of contracts - mediators to implement their own logic of interchain communication. Read more about the AMB mediators [here](https://docs.tokenbridge.net/amb-bridge/how-to-develop-xchain-apps-by-amb).

The mediator contracts rely on the following information about the POA-xDai Arbitrary Message Bridge:

* **POA Network**:
  * AMB contract: [`0xB2218bdEbe8e90f80D04286772B0968ead666942`](https://blockscout.com/poa/core/address/0xB2218bdEbe8e90f80D04286772B0968ead666942) 
  * Gas limit to call method in the xDai chain: `2000000`
  * Finalization rate: `12` blocks
* **xDai Chain**:
  * AMB contract: [`0xc2d77d118326c33BBe36EbeAbf4F7ED6BC2dda5c`](https://blockscout.com/xdai/mainnet/address/0xc2d77d118326c33BBe36EbeAbf4F7ED6BC2dda5c) 
  * Gas limit to call method in the POA Network: `2000000`
  * Finalization rate: `12` blocks

### Transactions

It is possible to get the status of an AMB transaction using [the Live Monitoring app](https://docs.tokenbridge.net/about-tokenbridge/components/amb-live-monitoring-application): [https://alm-poa-xdai.herokuapp.com/](https://alm-poa-xdai.herokuapp.com/). Transactions require a multi-sig \(for bridge validators, not users\) for a successful transfer. Current validators can be viewed with the live monitoring application. 

For transactions from the xDai chain the [manual execution](https://docs.tokenbridge.net/poa-xdai-amb/about-the-poa-xdai-amb/submit-confirmations-manually) is required. This action delivers the validator confirmations gathered on the xDai chain to the POA Network and triggers the transferred message handling. The Live Monitoring app simplifies the way how to execute the transfer - a special button will allow to finalize the delivery of the message to POA Network.

