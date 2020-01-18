# About the ETH-xDai AMB

The goal of Arbitrary Message Bridge \(AMB\) between the Ethereum Mainnet and the xDai chain is to extend the number of the applications that use cross-chain communications.

Every application could [build its own AMB extension](https://docs.tokenbridge.net/amb-bridge/how-to-develop-xchain-apps-by-amb) which is represented in form of two mediators contracts as so either assets or arbitrary data will be transferred between chains.

The mediator contracts must rely on the following information about the ETH-xDai Arbitrary Message Bridge:

* Ethereum Mainnet:
  * AMB contract: [`0x4C36d2919e407f0Cc2Ee3c993ccF8ac26d9CE64e`](https://etherscan.io/address/0x4C36d2919e407f0Cc2Ee3c993ccF8ac26d9CE64e)
  * Gas limit to call method in the xDai chain: `2000000`
* xDai chain:
  * AMB contract: [`0x75Df5AF045d91108662D8080fD1FEFAd6aA0bb59`](https://blockscout.com/poa/xdai/address/0x75df5af045d91108662d8080fd1fefad6aa0bb59/transactions)
  * Gas limit to call method in the Ethereum Mainnet: `2000000`

Detailed description what is AMB and examples of AMB extensions are available in separate section of the TokenBridge documentation: [Arbitrary Message Bridge \(AMB\)](https://docs.tokenbridge.net/amb-bridge/about-amb-bridge).

