# Create a burner wallet plugin for your AMB bridge extension

The [TokenBridge burner wallet plugin](https://www.npmjs.com/package/@poanet/tokenbridge-bw-exchange) allows the burner wallet to exchange assets interacting with AMB mediators. You can use the definitions it provides to create your own assets or exchange pairs so user can operate with them easily.

In this example we are going to show a plugin to interact with a ERC677 to ERC677 bridge extension that works on top of AMB bridge. It can be used as a starting point to develop your own plugin.

#### Clone the sample repo

Clone the [sample repo](https://github.com/poanetwork/tokenbridge-burner-wallet-plugin) to create a plugin project that uses the TokenBridge plugin. This sample repo contains a ready to publish plugin for a ERC677 to ERC677 bridge extension, but you can later modify it to define your own resources.

#### Project structure

There are three main folders in the project:

* `wallet` - is a burner wallet instance ready to test your plugin
* `test-wallet` - is a burner wallet instance ready to test your plugin and resources in testnets
* `my-plugin` - is the folder where the plugin code is located. To change the name of the plugin it is necessary to update the folder name `my-plugin` and all mentions to `my-plugin` to the new name of your plugin.

Inside `my-plugin` you can find the files that defines the resources to be exposed by the plugin to be used by the burner wallet in order to interact with the ERC677 to ERC677 bridge extension:

* `Stake` - extends from `ERC677Asset` defined in `@poanet/tokenbridge-bw-exchange`
* `xStake` - extends from `ERC677Asset` defined in `@poanet/tokenbridge-bw-exchange`
* `StakeBridge` - extends from `Mediator` defined in `@poanet/tokenbridge-bw-exchange`

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

