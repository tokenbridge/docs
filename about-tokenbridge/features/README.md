---
description: TokenBridge is an interoperability solution for EVM chains
---

# Features, Definitions and Modes

{% hint style="success" %}
TokenBridge MonoRepository: [https://github.com/poanetwork/tokenbridge](https://github.com/poanetwork/tokenbridge)
{% endhint %}

### Chain and Network Definitions

A bridge is created between 2 networks, referred to as a Native (or Home) Network and a Foreign network.

* **Native (Home)**: A network with fast and inexpensive operations. All bridge operations to collect validator confirmations are performed on this side of the bridge.
* **Foreign**: Can be any chain, but generally refers to the Ethereum mainnet.
* **ERC20**: Refers to an [ERC20](https://theethereum.wiki/w/index.php/ERC20\_Token\_Standard) token created during the bridge process. In the ERC20-ERC20 bridge, ERC677 represent ERC20 tokens on one side of the bridge and are minted and burned accordingly.

### Bridge Modes

A bridge can be configured for several different network configurations. This currently includes a Native-to-ERC20 Bridge, an ERC20-to-ERC20 bridge, an ERC20-to-Native Bridge, and the AMB bridge.

* **ERC20 to ERC20**: ERC20 compatible tokens are locked on the Foreign network and minted as ERC20 compatible tokens (ERC677 tokens) on the Native network. When transferred from Native to Foreign, the ERC677 tokens are burned and the ERC20 tokens are unlocked. Usage of ERC677 tokens on the Foreign network will increase the bridge security.
* **ERC20 to Native**: Coins are locked in the Foreign Network and ERC20 tokens are minted in the Native network (the Native network must support [OpenEthereum BlockReward](https://openethereum.github.io/Block-Reward-Contract.html) functionality). The xDai chain uses this bridge mode.
* **AMB Bridge:** Transfer arbitrary data between two networks - data is interpreted as an arbitrary contract method invocation.  For example, this allows for transfer operations with NFT tokens and their metadata.

### Bridge Components

The bridge consists of several components, including smart contracts, an event handler, and an optional UI. All components except for the Bridge Smart Contracts are located in the [https://github.com/poanetwork/tokenbridge](https://github.com/poanetwork/tokenbridge) repository.&#x20;

* **TokenBridge**. Listens to events and sends transactions to authorize asset transfers.&#x20;
* **Bridge UI Application**. A DApp GUI to transfer tokens and coins between chains.&#x20;
* **Bridge Monitor**. A tool for checking balances and unprocessed events in bridged networks.&#x20;
* **Bridge Deployment Playbooks**. Optional playbook which can manage token-bridge configuration instructions for remote deployments.&#x20;
* **Bridge Smart Contracts**. Manages bridge validators, collects signatures, and confirms asset relay and disposal.  Located at: [https://github.com/poanetwork/tokenbridge-contracts](https://github.com/poanetwork/tokenbridge-contracts)

{% hint style="success" %}
Content moved from the POA forum: [https://forum.poa.network/t/bridge-definitions-networks-and-components/1824](https://forum.poa.network/t/bridge-definitions-networks-and-components/1824)
{% endhint %}
