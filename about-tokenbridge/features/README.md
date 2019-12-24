---
description: TokenBridge is an interoperability solution for EVM chains
---

# Features, Definitions and Modes

### Chain and Network Definitions

A bridge is created between 2 networks, referred to as a Native \(or Home\) Network and a Foreign network.

* **Native \(Home\)**: A network with fast and inexpensive operations. All bridge operations to collect validator confirmations are performed on this side of the bridge.
* **Foreign**: Can be any chain, but generally refers to the Ethereum mainnet.
* **ERC20**: Refers to an [ERC20](https://theethereum.wiki/w/index.php/ERC20_Token_Standard) token created during the bridge process. In the ERC20-ERC20 bridge, ERC677 represent ERC20 tokens on one side of the bridge and are minted and burned accordingly.

### Bridge Modes

A bridge can be configured for several different network configurations. This currently includes a Native-to-ERC20 Bridge, an ERC20-to-ERC20 bridge, an ERC20-to-Native Bridge, and the AMB bridge.

* **Native to ERC20**: An EVM sidechain coin is converted to an ERC20 compatible token \(ERC677 token\) on the Ethereum network. When a bridge transfer is initiated from the Native side, coins are locked on the Native sidechain and minted on the Ethereum network. When bridged in the opposite direction, tokens are burned on the Foreign side and unlocked in the Native network. The POA to POA20 Bridge uses this mode.
* **ERC20 to ERC20**: ERC20 compatible tokens are locked on the Foreign network and minted as ERC20 compatible tokens \(ERC677 tokens\) on the Native network. When transferred from Native to Foreign, the ERC677 tokens are burned and the ERC20 tokens are unlocked. Usage of ERC677 tokens on the Foreign network will increase the bridge security.
* **ERC20 to Native**: Coins are locked in the Foreign Network and ERC20 tokens are minted in the Native network \(the Native network must support [Parity BlockReward](https://wiki.parity.io/Block-Reward-Contract) functionality\). The xDai chain uses this bridge mode.
* **AMB Bridge:** Transfer arbitrary data between two networks - data is interpreted as an arbitrary contract method invocation. This allows transfer operations with NFT tokens and their metadata.

### Bridge Components

The bridge consists of several components, including smart contracts, an event handler, and an optional UI. All components except for the Bridge Smart Contracts are located in the [https://github.com/poanetwork/tokenbridge](https://github.com/poanetwork/tokenbridge) repository. 

* **TokenBridge**. Listens to events and sends transactions to authorize asset transfers. 
* **Bridge UI Application**. A DApp GUI to transfer tokens and coins between chains. 
* **Bridge Monitor**. A tool for checking balances and unprocessed events in bridged networks. 
* **Bridge Deployment Playbooks**. Optional playbook which can manage token-bridge configuration instructions for remote deployments. 
* **Bridge Smart Contracts**. Manages bridge validators, collects signatures, and confirms asset relay and disposal.  Located at: [https://github.com/poanetwork/poa-bridge-contracts](https://github.com/poanetwork/poa-bridge-contracts)

{% hint style="success" %}
Content moved from the POA forum: [https://forum.poa.network/t/bridge-definitions-networks-and-components/1824](https://forum.poa.network/t/bridge-definitions-networks-and-components/1824)
{% endhint %}

