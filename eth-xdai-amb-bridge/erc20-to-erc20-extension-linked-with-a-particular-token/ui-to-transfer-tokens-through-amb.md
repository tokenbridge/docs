---
description: How to develop a web-application to transfer tokens through AMB
---

# UI to transfer tokens through AMB

This manual describes how to rapidly develop a web-application to transfer tokens using the Arbitrary Message Bridge between the Ethereum Mainnet and the xDai chain. It assumes that an `erc-to-erc` extension was deployed [using these steps](deploy-erc20-erc677-erc827-to-erc677-amb-bridge-extension.md).

{% hint style="info" %}
The application is based on [the Burner Wallet 2 interface](https://github.com/burner-wallet/burner-wallet-2). Quick launch of a new application is possible with [the TokenBridge plugin developed for the Arbitrary Message Bridge mediators](https://github.com/poanetwork/tokenbridge/tree/master/burner-wallet-plugin).
{% endhint %}

![The main page of the BW2-based application to transfer tokens through AMB](<../../.gitbook/assets/image (46).png>)

## Prerequisites

Before developing the application developing, the following must be prepared:

* the AMB mediator address responsible for working with the bridgeable tokens
* the ERC20/ERC677/ERC827 token contract address in the Ethereum Mainnet
* the ERC677 token contract address deployed together with the mediators

{% hint style="warning" %}
For demonstration purposes, data for [the sUSD AMB extension](susd-bridge-extension/) will be used below.
{% endhint %}

## Instructions

1\. Clone the repo with the application template

```
git clone https://github.com/poanetwork/tokenbridge-burner-wallet-plugin.git
cd tokenbridge-burner-wallet-plugin bw-plugin
```

2\. Add the assets to bridge by creating two files:

* `my-plugin/src/assets/sUSD.ts` is for the asset on the Ethereum Mainnet;
* `my-plugin/src/assets/xsUSD.ts` is for the ERC677 token created by the `erc-to-erc` AMB extension deployment process.

{% tabs %}
{% tab title="my-plugin/src/assets/sUSD.ts" %}
```javascript
import { BridgeableERC20Asset } from '@poanet/tokenbridge-bw-exchange'

export default new BridgeableERC20Asset({
  id: 'susd',    //internal id of the asset
  name: 'sUSD',  //displayed name of the asset
  network: '1',  //chain id (ethereum mainnet)
  address: '0x57ab1e02fee23774580c119740129eac7081e9d3', //token contract address
  bridgeModes: ['erc-to-erc-amb']
})
```
{% endtab %}

{% tab title="my-plugin/src/assets/xsUSD.ts" %}
```javascript
import { ERC677Asset } from '@poanet/tokenbridge-bw-exchange'

export default new ERC677Asset({
  id: 'xsusd',    //internal id of the asset
  name: 'xsUSD',  //displayed name of the asset
  network: '100', //chain id (xdai chain)
  address: '0x4C36d2919e407f0Cc2Ee3c993ccF8ac26d9CE64e' //token contract address
})
```
{% endtab %}
{% endtabs %}

3\. Rename `my-plugin/src/pairs/StakeBridge.ts` to `my-plugin/src/pairs/sUSDBridge.ts` and replace its contents as follows:

{% code title="my-plugin/src/pairs/sUSDBridge.ts" %}
```javascript
import { Mediator } from '@poanet/tokenbridge-bw-exchange'
import { sUSD, xsUSD } from '../index'

// Mediator contract address at the xDai chain
const homeMediatorAddress = '0xD9a3039cfC70aF84AC9E566A2526fD3b683B995B'
// Mediator contract at the Ethereum Mainnet
const foreignMediatorAddress = '0x71F12d03E1711cb96E11E1A5c12Da7466699Db8D'

export default class sUSDBridge extends Mediator {
  constructor() {
    super({
      assetA: sUSD.id,
      assetABridge: foreignMediatorAddress,
      assetB: xsUSD.id,
      assetBBridge: homeMediatorAddress
    })
  }
}
```
{% endcode %}

4\. Modify `my-plugin/src/index.ts` to export new assets and the bridgeable pair.

{% code title="my-plugin/src/index.ts" %}
```javascript
export { default as sUSD } from './assets/sUSD'
export { default as xsUSD } from './assets/xsUSD'
export { default as sUSDBridge } from './pairs/sUSDBridge'
```
{% endcode %}

5\. Modify `wallet/src/index.tsx` to operate with new objects:

*   line 10 contains:

    ```
    import { sUSD, xsUSD, sUSDBridge } from 'my-plugin'
    ```
*   line 15 contains:&#x20;

    ```
    assets: [sUSD, xsUSD]
    ```
*   line 19 contains:

    ```
    pairs: [new sUSDBridge()]
    ```

6\. Build the docker image with the wallet.&#x20;

```
docker-compose build wallet
```

7\. Run the container locally with the wallet application by specifying the port to listen to and [an Infura Project ID](https://infura.io/docs) which will be used by the application to connect to an Infura JSON RPC node:

```
docker run -ti -p 8080:8080 -e PORT=8080 \
  -e REACT_APP_INFURA_KEY=YOUR-PROJECT-ID --rm bw-plugin_wallet:latest
```

8\. Wait for the application server to start. The URL address to connect to the wallet application will display:

```
wallet:   Local:            http://localhost:8080/
```

9\. Run a browser and paste the URL in the terminal (`http://localhost:8080/`). The browser must have [the MetaMask extension](https://metamask.io) installed. [The xDai RPC endpoint must be added](https://www.xdaichain.com/for-users/wallets/metamask/metamask-setup) to MetaMask. Press the "Exchange" button to test a transfer of bridgeable tokens through the AMB.

![The exchange page allows to bridge tokens through AMB](<../../.gitbook/assets/image (47).png>)

10\. After testing the application, it can either be deployed to a platform like Heroku or the developed pluging can be published as [a NPM library](https://www.npmjs.com) and integrated into the [Burner Factory](http://burnerfactory.com): [https://github.com/burner-factory/verified-plugins](https://github.com/burner-factory/verified-plugins).
