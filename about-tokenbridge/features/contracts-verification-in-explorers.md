---
description: >-
  How to enable automatic contract verification feature in bridge contracts
  deployment script
---

# Contracts verification in explorers

The instructions below show how to configure the variables to enable the automatic contract verification in block explorers when using the [bridge contracts deployment script](https://github.com/poanetwork/tokenbridge-contracts/blob/master/deploy/README.md). This feature only supports Blockscout and Etherscan block explorers.

In the example we are going to deploy a bridge between Sokol and Kovan testnets, and we are going to automatically verify the contracts on [Blockscout](https://blockscout.com/poa/sokol/) for the contracts deployed in Sokol and [Etherscan](https://kovan.etherscan.io) for the contracts deployed in Kovan.&#x20;

It is worth to mention that the home and foreign side of the bridge are not limited to a specific explorer and they can be used in any of the sides. For example, in this case, we could also use the [Kovan Blockscout](https://blockscout.com/eth/kovan) version to verify the contracts in Kovan.

While Blockscout does not require authentication, Etherscan requires to create an user and an API-KEY.

### Create an etherscan API-KEY token

1. First create an account on [https://etherscan.io/register](https://etherscan.io/register)
2. Sign in into your account &#x20;

![Sign in into your etherscan account](<../../.gitbook/assets/scrnli\_12\_30\_2019\_3-26-19 PM.png>)

&#x20;   3\. Select the `API-KEYs` option from the menu

![Select API-KEYs](<../../.gitbook/assets/scrnli\_12\_30\_2019\_3-30-27 PM.png>)

&#x20;   4\. Click on the button `Create a new API-KEY token`&#x20;

![Button to create a new API-KEY token](<../../.gitbook/assets/scrnli\_12\_30\_2019\_3-31-23 PM.png>)

&#x20;   5\. Add an optional name to the `API-KEY` and click on the button `Continue`

![Add a name and click on continue](<../../.gitbook/assets/scrnli\_12\_30\_2019\_3-32-40 PM.png>)

&#x20;   6\. The created `API-KEY` will be displayed in the list.

![List of API-KEYs](<../../.gitbook/assets/scrnli\_12\_30\_2019\_3-33-19 PM.png>)

### Variable configuration for deployment script

At the moment of setting the variable for the configuration of the bridge deployment the following should be completed:

* **HOME\_EXPLORER\_URL**: The api url of Blockscout explorer to verify all the deployed contracts in Home network.
* **HOME\_EXPLORER\_API\_KEY**:  The api key of the explorer api, if required, used to verify all the deployed contracts in Home network. In this case it is not needed because Blockscout does not require an api key.
* **FOREIGN\_EXPLORER\_URL**: The api url of Etherscan explorer to verify all the deployed contracts in Foreign network.
* **FOREIGN\_EXPLORER\_API\_KEY**: The api key of Etherscan explorer api, used to verify all the deployed contracts in Foreign network that we generated in the previous step.

This is how the configuration should look like:

```
...
HOME_EXPLORER_URL=https://blockscout.com/poa/sokol/api

FOREIGN_EXPLORER_URL=https://api-kovan.etherscan.io/api
FOREIGN_EXPLORER_API_KEY=Z1MREJ9P8TTCRGF59GK5M5YBC43WHIWF2X
...
```

After running the deployment script, if we search for the bridge addresses on the explorers, they should be verified showing the compilation data and the source code of the contracts.

Here is an example of how a verified contract looks in Blockscout

![Verified contract in Blockscout](<../../.gitbook/assets/scrnli\_12\_30\_2019\_4-27-01 PM.png>)



Here is an example of how a verified contract looks in Etherscan

![Verified contract in Etherscan](<../../.gitbook/assets/scrnli\_12\_30\_2019\_4-27-23 PM.png>)
