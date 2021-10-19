---
description: >-
  Instructions on relaying SPOA native tokens through the native-to-ERC20 bridge
  extension
---

# Transfer SPOA through native-to-ERC20 extension without UI

In order to test transferring SPOA tokens through the bridge extension [MyEtherWallet (MEW)](https://www.myetherwallet.com/access-my-wallet) can be used. MEW may be used for both types of operations: to swap native tokens to the ERC20 compatible tokens and to swap ERC20 tokens to the native tokens.

## Swap SPOA native tokens to ERC20 tokens

1\. Activate and open a web3 wallet (like MetaMask or Nifty Wallet) and select the Sokol Testnet. Go to [MyEtherWallet (MEW)](https://www.myetherwallet.com/access-my-wallet) and select the option to login with a web3 wallet.

2\. Send native tokens to the mediator contract:

* 1\) specify the amount of tokens (in `ether`) and enter the recipient address `0x867949C3F2f66D827Ed40847FaA7B3a369370e13`. This is the mediator contract serving the bridge extension in the Sokol testnet.

{% hint style="warning" %}
Note that minimum and maximum transaction amounts are embedded into the bridge.&#x20;

* **Min** per transaction: **0.001 SPOA**
* **Max** per transaction: **100 SPOA**
* Transaction limit **max per day**: **1,000.00 SPOA**
{% endhint %}

![](<../../.gitbook/assets/image (28).png>)

* 2\) scroll down the page and press **Send Transaction**

3\. Check in a web3 wallet (like MetaMask or Nifty wallet) that the Gas price is not set too high, then **Submit** the transaction. Wait to proceed until it is included in the chain.

4\. It will require the AMB bridge a short amount time to relay the deposit request to the Kovan Testnet. After some time the balance of the same account that sent SPOA tokens will increase. The result of the relay operation can be monitored in [Etherscan](https://kovan.etherscan.io/token/0xff94183659f549d6273349696d73686ee1d2ac83#balances).

## Swap ERC20 tokens to SPOA native tokens

1\. Choose the Kovan Testnet in the browser wallet extension and login to [MyEtherWallet (MEW)](https://www.myetherwallet.com/access-my-wallet). Select to the **Interact with Contract** item in the side navigation menu.

2\. Initialize the ERC20 bridgeable token contract interface:

* 1\) Add the token **Contract Address** `0xff94183659f549D6273349696d73686Ee1d2AC83`.
* 2\) Add the following JSON in the **`ABI/JSON Interface`** field:

```javascript
[{"constant":false,"inputs":[{"name":"_to","type":"address"},
{"name":"_value","type":"uint256"}],"name":"transfer",
"outputs":[{"name":"","type":"bool"}],"payable":false,
"stateMutability":"nonpayable","type":"function"}]
```

* 3\) Click **Continue.**

![](<../../.gitbook/assets/image (29).png>)

3\. Transfer the ERC20 bridgeable tokens to the mediator contract:

* 1\) Select **transfer** from the the **Select an Item** dropdown
* 2\) Enter in the `_to` address: `0x99FB1a25caeB9c3a5Bf132686E2fe5e27BC0e2dd`. This is the mediator contract serving the bridge extension in the Kovan testnet.
* 3\) Enter the value to transfer in Wei in the `_value` field.
* 4\) Click **Write.**

{% hint style="warning" %}
Note that minimum and maximum transaction amounts are embedded into the bridge.&#x20;

* **Min** per transaction: **0.001 KSPOA**
* **Max** per transaction: **100.00 KSPOA**
* Transaction limit **max per day**: **1,000.00 KSPOA**
{% endhint %}

![](<../../.gitbook/assets/image (30).png>)

{% hint style="info" %}
The `transfer` method of the bridgeable token contract will automatically notify the mediator contract about the new amount of tokens transferred to the mediator contract account. For this reason, no other action is required from the user side to finish the swap request.
{% endhint %}

4\. Check the gas price, then **Submit** the transaction through the web3 wallet extension and wait until it is included in the chain.

5\. It will require the AMB bridge some time to transfer tokens to the Sokol Testnet. After few seconds, the balance of the account specified as `_to` in the `transfer` method call will increase. The result of the relay operation can be monitored in [Blockscout](https://blockscout.com/poa/sokol/address/0x867949C3F2f66D827Ed40847FaA7B3a369370e13/coin-balances), and should be viewable in your web3 wallet connected to the Sokol Testnet.
