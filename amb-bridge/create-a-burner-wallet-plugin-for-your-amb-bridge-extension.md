# Create a burner wallet plugin for your AMB bridge extension

The [TokenBridge burner wallet plugin](https://www.npmjs.com/package/@poanet/tokenbridge-bw-exchange) allows the burner wallet to exchange assets interacting with AMB mediators. You can use the definitions it provides to create your own assets or exchange pairs so user can operate with them easily.

### Introduction

The [Burner Wallet 2.0](https://github.com/burner-wallet/burner-wallet-2) is a modular, extendable and customizable web application.

It provides a set of packages and plugins that allow you to extend the basic functionality. Here we will focus on the Assets package and the Exchange Plugin.

**Assets**

You can add any native or ERC20 token to track its balance and send transactions. For example you can define a new ERC20 and add it to the wallet:

```javascript
import { xdai, dai, eth, ERC20Asset } from '@burner-wallet/assets';

const test = new ERC20Asset({
  id: 'tst', // The internal ID used by the wallet.
  name: 'Test Token', // The display name that will be displayed to the user.
  network: '1', // The chain ID of the chain the token is deployed to.
  address: '0x52ad726d80dbb4A9D4430d03657467B99843406b' // Address where the token contract is deployed
});

const core = new BurnerCore({
  assets: [test, xdai, dai, eth],
});
```

The `ERC20Asset` class extends from the `Asset` class. The `Asset` class provides several methods to allow the wallet interact with the token. The following are the most important to pay attention and that could be overridden if your token behaves differently.

* `getBalance`: Indicates how to get the balance of your asset.
* `startWatchingAddress`: Indicates how to listen to value transfers incoming into your account.
* `_send`: Indicates how to send value to another account.

**Gateways**

Gateways can be thought of as “wrapped RPC providers”, as they transmit data from the wallet to endpoints such as Infura. Gateways use the `network` id from the assets to select the correct endpoints.

The `@burner-wallet/core` module contains some standard gateways:

* InfuraGateway
* XDaiGateway 
* InjectedGateway \(which transmits messages through an injected Web3 provider such as Metamask\).

**Exchange Plugin**

The `@burner-wallet/exchange` package is an extendable plugin for implementing asset exchanges and bridges. The exchange module accepts an array of trading pairs.

```text
const exchange = new Exchange({
  pairs: [new Pair1(), new Pair2()]
})
```

`Pair` is an abstract class that defines the interface for trading pairs. If you would like to add custom trading functionality, you can extend this class and implement it's methods:

* `estimateAtoB`: Indicates how to estimate the B Asset the user will receive for the amount of A Asset. For example Fees could be considered here. This method returns the amount to be received, and a custom message to display in UI.
* `estimateBtoA`: Indicates how to estimate the A Asset the user will receive for the amount of B Asset. For example Fees could be considered here. This method returns the amount to be received, and a custom message to display in UI.
* `exchangeAtoB`: Indicates how to send A Asset to be exchanged for B Asset. Here you can add logic to detect exchange finalization for example for a more complex exchange operation like bridges.
* `exchangeBtoA`: Indicates how to send B Asset to be exchanged for A Asset. Here you can add logic to detect exchange finalization for example for a more complex exchange operation like bridges.

Exchange pairs examples:

* [XDAIBridge](https://github.com/burner-wallet/burner-wallet-2/blob/develop/packages/exchange/src/pairs/XDaiBridge.ts): It allows the user to exchange the pair DAI &lt;&gt; xDAI. Since validators need to verify the transaction, and release the tokens on the other network, this pair detects the exchange finalization by listening to events on the bridge contracts.
* [Uniswap](https://github.com/burner-wallet/burner-wallet-2/blob/develop/packages/exchange/src/pairs/Uniswap.ts): It allows the user to exchange the pair DAI &lt;&gt; ETH by using Uniswap. In this case, `exchangeAtoB` is extended for converting DAI to ETH, since it requires performing two transactions. First calling `approve` on the token contract and then calling the method from the Uniswap contract.     

**TokenBridge Plugin**

The [TokenBridge Burner Wallet 2 Plugin](https://github.com/poanetwork/tokenbridge/tree/develop/burner-wallet-plugin/tokenbridge-bw-exchange) provides some generic resources that can be used and extended:

* `ERC677Asset` - A representation of an Erc677 token
* `NativeMediatorAsset` - Represents a native token that interacts with a Mediator extension.
* `Mediator` Pair - Represents an Exchange Pair that interacts with mediators extensions.
* `TokenBridgeGateway` - A gateway to operate with ETC, POA Sokol and POA Core networks.

The asset `ERC677Asset` extends from `ERC20Asset` and overrides some methods:

* `_send`: In this case the method `transferAndCall` is used instead of the `transfer` method.
* `startWatchingAddress`: Add logic to correctly track the transfer events related to the wallet account.
* `getTx`: Overrides the logic to return the stored information about a transfer transaction to avoid errors on the information displayed.

The asset `NativeMediatorAsset` extends from the `NativeAsset` of the burner wallet core. It extends the functionality with the following method:

* `scanMediatorEvents`: Add logic to watch transfer from mediator contracts to the wallet account to display it in the activity list.
* `getTx`: Overrides the logic to return the stored information about a transfer transaction to avoid errors on the information displayed.

The pair `Mediator` extend from some other classes that has `Pair` as base. It implements the previous mentioned methods to estimate and exchange the assets. It also implements some methods to detect the exchange finalization. Here are some details of the implemented methods:

* `estimateAtoB`: Gets the fee, calculates the amount of B Asset the user will receive and sets a custom message to be displayed mentioning the fee charges.
* `estimateBtoA`: Gets the fee, calculates the amount of A Asset the user will receive and sets a custom message to be displayed mentioning the fee charges.
* `exchangeAtoB`: Sends A Asset to the mediator contract. Then it calls `detectExchangeAToBFinished`.
* `exchangeBtoA`: Sends B Asset to the mediator contract. Then it calls `detectExchangeBToAFinished`.
* `detectExchangeAToBFinished`: Wait for events emitted by the mediator contract to detect the exchange finalization.
* `detectExchangeBToAFinished`: Wait for events emitted by the mediator contract to detect the exchange finalization.

The gateway `TokenBridgeGateway` extends from the `Gateway` class of the burner wallet core. It provides access from the wallet to the following networks:

* ETC
* POA Sokol
* POA Core

#### Project structure

There are three main folders in the project:

* `wallet` - is a burner wallet instance ready to test your plugin
* `test-wallet` - is a burner wallet instance ready to test your plugin and resources in testnets
* `my-plugin` - is the folder where the plugin code is located. To change the name of the plugin it is necessary to update the folder name `my-plugin` and all mentions to `my-plugin` to the new name of your plugin.

Inside `my-plugin` you can find the files that defines the resources to be exposed by the plugin to be used by the burner wallet in order to interact with the ERC677 to ERC677 bridge extension:

* `Stake` - extends from `ERC677Asset` defined in `@poanet/tokenbridge-bw-exchange`
* `xStake` - extends from `ERC677Asset` defined in `@poanet/tokenbridge-bw-exchange`
* `StakeBridge` - extends from `Mediator` defined in `@poanet/tokenbridge-bw-exchange`

In this repo example case, the class `StakeBridge` extends the `Mediator` class but has some differences on how to estimate the values and calculate the transfers fees. That's why it overrides the methods:

* `estimateAtoB`: To add specific logic to get the fee from the A to B exchange and estimate the value that will be received.
* `estimateBtoA`: To avoid fee calculations since there are no fees for B to A exchange.

You can extend or replace these resources based on your use case.

Inside the `wallet` folder, the file `wallet/src/index.tsx` integrates the plugin into the wallet by importing the resources in the following line:

```text
import { Stake, xStake, StakeBridge } from 'my-plugin'
```

To be able to use and to display the balances for `Stake` and `xStake` it is necessary to list them in the list of assets as follow:

```text
const core = new BurnerCore({
    ...
  assets: [Stake, xStake]
})
```

This is how the main Burner Wallet page will looks like:

![](https://i.imgur.com/YRjpvFo.png)

Then, in order to perform exchange operations between the assets it is needed that the defined pair is included in the Exchange plugin as follows:

```text
const exchange = new Exchange({
  pairs: [new StakeBridge()]
})
```

This is how the exchange section will look like:

![](https://i.imgur.com/rkLbNye.png)

#### Clone the sample repo

Clone the [sample repo](https://github.com/poanetwork/tokenbridge-burner-wallet-plugin) to create a plugin project that uses the TokenBridge plugin. This sample repo contains a ready to publish plugin for a ERC677 to ERC677 bridge extension, but you can later modify it to define your own resources.

#### Install dependencies

Run `yarn install`. This repo uses Lerna and Yarn Workspaces, so `yarn install` will install all dependencies and link modules in the repo.

#### Build

To build the plugin package, from the root folder of project, you need to run the following command:

```text
yarn build
```

#### Test plugin and resources in testnets

The project includes a burner wallet instance where you can test the implementation of the plugin in testnet. For that, you have to make sure that the build step was performed and that the resources you modified are correctly imported and used in the `src/index.tsx` file of the `test-wallet` folder.

First create an `.env` file in `test-wallet` folder from `.env.example` and set the required parameters for the ERC677 to ERC677 bridge extension:

```text
REACT_APP_INFURA_KEY=<your key from infura.com>
REACT_APP_HOME_NETWORK=
REACT_APP_HOME_TOKEN_NAME=
REACT_APP_HOME_TOKEN_ADDRESS=
REACT_APP_HOME_MEDIATOR_ADDRESS=

REACT_APP_FOREIGN_NETWORK=
REACT_APP_FOREIGN_TOKEN_NAME=
REACT_APP_FOREIGN_TOKEN_ADDRESS=
REACT_APP_FOREIGN_MEDIATOR_ADDRESS=
```

To start the burner wallet instance run:

```text
yarn start-test-wallet
```

#### Run plugin in Mainnet

The project includes a burner wallet instance where you can use the implementation of the plugin. For that, you have to make sure that the build step was performed and that the plugin resources you modified are correctly imported and used in the `src/index.tsx` file of the `wallet` folder.

First create an `.env` file in `wallet` folder and set:

```text
REACT_APP_INFURA_KEY=<your key from infura.com>
```

To start the burner wallet instance run:

```text
yarn start-wallet
```

#### Publish to npm

In order to make the plugin accessible for other projects it needs to be published in the npm registry. For that, you can follow these steps:

1. Create account in [https://www.npmjs.com/](https://www.npmjs.com/)
2. Go to `my-plugin` folder
3. Run `yarn build`. Make sure it generates the `dist` folder
4. Update `version` in `my-plugin/package.json`
5. Run `yarn publish` and fill login information if required. The prompt will ask for the new version, complete it with the version from `my-plugin/package.json`

More information in [https://classic.yarnpkg.com/en/docs/publishing-a-package/](https://classic.yarnpkg.com/en/docs/publishing-a-package/)

