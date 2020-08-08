---
description: Instructions to setup the ALM application locally
---

# Local deployment

For testing purposes or in case if [the existing instances of ALM](https://docs.tokenbridge.net/about-tokenbridge/components/amb-live-monitoring-application#existing-alm-instances) are not available the application can be deployed locally in the containerised environment.

## Build and run

### 1. Clone the repo

```bash
git clone --recursive https://github.com/poanetwork/tokenbridge.git
cd tokenbridge/alm
```

### 2. Prepare a configuration file

Copy the configuration file template

```bash
cp .env.example .env
```

an open it in your favourite text editor:

```bash
# Addresses of the AMB contracts.
COMMON_HOME_BRIDGE_ADDRESS=0x...
COMMON_FOREIGN_BRIDGE_ADDRESS=0x...

# URLs to the JSON RPC nodes.
# Infura URLs must be specified togehter with a project id.
COMMON_HOME_RPC_URL=https://link.to.rpc.node.at.home
COMMON_FOREIGN_RPC_URL=https://link.to.rpc.node.at.foreign

# Short name of the chains ALM will work with. The name will
# be available for users in the top right corner of the app.
ALM_HOME_NETWORK_NAME=Some name 
ALM_FOREIGN_NETWORK_NAME=Another name

# URLs to the block explorers to refer to a transaction if a user
# would like to get more details. The template sequence %s is used
# for the tx hash.
# For example, https://blockscout.com/poa/sokol/tx/%s or
# https://kovan.etherscan.io/tx/%s
ALM_HOME_EXPLORER_TX_TEMPLATE=https://some.url/hash/%s
ALM_FOREIGN_EXPLORER_TX_TEMPLATE=https://another.url/tx/%s

# URLs to the explorers APIs that are used by ALM to discover pending
# or failed transactions
# Examples of API URLs for widely used exploreres:
# - https://blockscout.com/poa/sokol/api
# - https://api-kovan.etherscan.io/api?apikey=YourApiKeyToken
ALM_HOME_EXPLORER_API=https://some.explorer.url/api
ALM_FOREIGN_EXPLORER_API=https://another.explorer.url/api

# Port where the application will listen to. This port will be also
# by the docker-compose tool when the application starts
PORT=8080
```

### 3. Build the docker image

```bash
docker-compose build
```

### 4. Run the application

```bash
docker-compose up -d
```

Use a browser to get into [http://localhost:8080](http://localhost:8080/) \(if another value was configured for the parameter `PORT` use it instead of 8080.

The main window of the application will look like the following:

![](../../../.gitbook/assets/image%20%2856%29.png)

## Examples of existing AMBs configs

Since there are several deployed instances for existing Arbitrary Message Bridges, it is worth to share their configs as so anyone could have an opportunity to run the AMB Live Monitoring tool locally.

{% hint style="warning" %}
Replace `PROJECT-ID` and `ETHERSCAN-API-KEY` in the configurations files with your data.
{% endhint %}

### Ethereum Mainnet to xDai

```bash
PORT=8080

COMMON_HOME_BRIDGE_ADDRESS=0x75Df5AF045d91108662D8080fD1FEFAd6aA0bb59
COMMON_FOREIGN_BRIDGE_ADDRESS=0x4C36d2919e407f0Cc2Ee3c993ccF8ac26d9CE64e

COMMON_HOME_RPC_URL=https://xdai.poanetwork.dev/
COMMON_FOREIGN_RPC_URL=https://mainnet.infura.io/v3/PROJECT-ID

ALM_HOME_NETWORK_NAME=xDai chain
ALM_FOREIGN_NETWORK_NAME=Ethereum Mainnet

ALM_HOME_EXPLORER_TX_TEMPLATE=https://blockscout.com/poa/xdai/tx/%s
ALM_FOREIGN_EXPLORER_TX_TEMPLATE=https://etherscan.io/tx/%s

ALM_HOME_EXPLORER_API=https://blockscout.com/poa/xdai/api
ALM_FOREIGN_EXPLORER_API=https://api.etherscan.io/api?apikey=ETHERSCAN-API-KEY
```

### Rinkeby to xDai

```bash
PORT=8080

COMMON_HOME_BRIDGE_ADDRESS=0xc38D4991c951fE8BCE1a12bEef2046eF36b0FA4A
COMMON_FOREIGN_BRIDGE_ADDRESS=0xD4075FB57fCf038bFc702c915Ef9592534bED5c1

COMMON_HOME_RPC_URL=https://xdai.poanetwork.dev/
COMMON_FOREIGN_RPC_URL=https://rinkeby.infura.io/v3/PROJECT-ID

ALM_HOME_NETWORK_NAME=xDai chain
ALM_FOREIGN_NETWORK_NAME=Rinkeby Testnet

ALM_HOME_EXPLORER_TX_TEMPLATE=https://blockscout.com/poa/xdai/tx/%s
ALM_FOREIGN_EXPLORER_TX_TEMPLATE=https://rinkeby.etherscan.io/tx/%s

ALM_HOME_EXPLORER_API=https://blockscout.com/poa/xdai/api
ALM_FOREIGN_EXPLORER_API=https://api-rinkeby.etherscan.io/api?apikey=ETHERSCAN-API-KEY
```

### Ethereum Mainnet to Ethereum Classic

```bash
PORT=8080

COMMON_HOME_BRIDGE_ADDRESS=0xA126c73d1bDf3a3D5F719A8D38a4692186e7503F
COMMON_FOREIGN_BRIDGE_ADDRESS=0x5a91B345244d3A285b30287b4c63c154eCBD2b7e

COMMON_HOME_RPC_URL=https://www.ethercluster.com/etc
COMMON_FOREIGN_RPC_URL=https://mainnet.infura.io/v3/PROJECT-ID

ALM_HOME_NETWORK_NAME=Ethereum Classic
ALM_FOREIGN_NETWORK_NAME=Ethereum Mainnet

ALM_HOME_EXPLORER_TX_TEMPLATE=https://blockscout.com/etc/mainnet/tx/%s
ALM_FOREIGN_EXPLORER_TX_TEMPLATE=https://etherscan.io/tx/%s

ALM_HOME_EXPLORER_API=https://blockscout.com/etc/mainnet/api
ALM_FOREIGN_EXPLORER_API=https://api.etherscan.io/api?apikey=ETHERSCAN-API-KEY
```

### Kovan to Sokol \(test bridge\)

```bash
PORT=8080

COMMON_HOME_BRIDGE_ADDRESS=0xFe446bEF1DbF7AFE24E81e05BC8B271C1BA9a560
COMMON_FOREIGN_BRIDGE_ADDRESS=0xFe446bEF1DbF7AFE24E81e05BC8B271C1BA9a560

COMMON_HOME_RPC_URL=https://sokol.poa.network
COMMON_FOREIGN_RPC_URL=https://kovan.infura.io/v3/PROJECT-ID

ALM_HOME_NETWORK_NAME=Sokol testnet
ALM_FOREIGN_NETWORK_NAME=Kovan testnet

ALM_HOME_EXPLORER_TX_TEMPLATE=https://blockscout.com/poa/sokol/tx/%s
ALM_FOREIGN_EXPLORER_TX_TEMPLATE=https://kovan.etherscan.io/tx/%s

ALM_HOME_EXPLORER_API=https://blockscout.com/poa/sokol/api
ALM_FOREIGN_EXPLORER_API=https://api-kovan.etherscan.io/api?apikey=ETHERSCAN-API-KEY
```

