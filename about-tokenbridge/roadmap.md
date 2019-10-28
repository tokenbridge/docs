# Roadmap

### Q4 2019 - AMB between ETH-POA and ETH-xDAI

**Target date: Q4 2019**

The bridges currently deployed between the Ethereum Mainnet, POA Network and xDai Chain only transfer fungible tokens. However, several projects have requested the ability to transfer other types of digital assets, for example non-fungible tokens. 

First, the AMB will be set up between the Ethereum Mainnet and the xDai Chain. Next, it will be deployed between the Mainnet and POA Network. Once AMB bridges are available,  the same set of validator nodes will be able to transfer data between bridged chains for dozens of different applications. No reconfiguration will be required to facilitate these transfers.

### Upgrade xDAI bridge to support alternative receiver and relative withdrawal limits

**Target date: Q4 2019**

* **Alternative receiver:** Any contract in one chain will have the ability to send tokens cross-chain to any external address or contract. This feature will benefit owners of multsig wallets - they will be able to exchange Dai to xDai and vice versa. 
* **Relative withdrawal limits**: The current daily withdrawal limit is absolute, creating a potential security issue if all funds are withdrawn. The new configuration will base withdrawal limits on the total bridge balance. For example, a 6% relative limit will restrict daily withdrawal operations to 6% of the overall bridge balance.

### Staking token bridge on top of AMB

**Target date: Q2 2020**

The arbitrary message bridge generalizes bridge operations and creates the opportunity for the same set of validators nodes to relay any data from one chain to another without any reconfiguration. This will allow for a smooth transition when the xDai chain is upgraded to [POSDAO](https://www.xdaichain.com/for-validators/posdao-whitepaper); the staking token transfer will be handled by the existing AMB infrastructure. Token exchange will be possible as soon as [the mediator contract](https://docs.tokenbridge.net/amb-bridge/how-to-develop-xchain-apps-by-amb) responsible for handling new asset transfers is deployed.



