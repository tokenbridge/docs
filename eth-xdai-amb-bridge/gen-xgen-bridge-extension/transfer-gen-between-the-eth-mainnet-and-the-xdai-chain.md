---
description: Instructions on relaying DAOstack tokens through the GEN-xGEN bridge extension
---

# Transfer GEN between the ETH Mainnet and the xDai Chain

{% hint style="warning" %}
This manual is not intended as an official protocol to transfer GEN tokens through the AMB extension. The actions described below provide an idea about how to automate operations involving the Arbitrary Message Bridge, and demonstrate the transfer process.
{% endhint %}

{% hint style="info" %}
It is assumed that accounts executing operations below have a small amount of Ether and xDai for gas fees as well as an amount of GENs to transfer. GEN can be obtained through [Uniswap](https://uniswap.exchange/) or other exchanges.
{% endhint %}

For demonstration purposes we use [MyEtherWallet \(MEW\)](https://www.myetherwallet.com/access-my-wallet)  to move assets from the Ethereum Mainnet to the xDai chain. These actions may be applied to any other wallet with similar capabilities.

## Deposit GEN tokens to the xDai chain

1. GEN is a ERC827-compatible token. If the account that receives tokens is a contract, it is possible to call a method of this contract. The `onTokenTransfer` method of the mediator contract will be used to notify the mediator contract that some amount of tokens has been sent. We can build the method invocation with [https://abi.hashex.org/](https://abi.hashex.org/) 

* 1\) Add the following JSON in the input field:

```javascript
[{"constant":false,"inputs":[{"name":"_from","type":"address"},
{"name":"_value","type":"uint256"},{"name":"_data","type":"bytes"}],
"name":"onTokenTransfer","outputs":[{"name":"","type":"bool"}],
"payable":false,"stateMutability":"nonpayable","type":"function"}]
```

![](../../.gitbook/assets/image%20%282%29.png)

* 2\) Click **Parse**
* 3\) Choose _onTokenTransfer_ in the **Function type** dropdown
* 4\) Enter the **\_from** address. It is the account that will send the GEN tokens.
* 5\) Enter the **\_value** - the amount of tokens \(in Wei\) to transfer.
* 6\) Leave the **\_data** field empty.
* 7\) Click **Copy** to copy the content of the **ABI-encoded output** text field and store it somewhere.

![](../../.gitbook/assets/image%20%288%29.png)

2. Activate and open a web3 wallet \(like MetaMask or Nifty Wallet\) and select the Ethereum Mainnet chain. Chose the account that will send the tokens \(the same as it was used on the step 1.4\). Go to [MyEtherWallet \(MEW\)](https://www.myetherwallet.com/access-my-wallet) and select the option to login with a web3 wallet. Next:

* 1\) Select the **Interact with Contract** item from the sidebar menu
* 2\) Initialize the GEN token contract interface by entering the DAOstack token contract address in the **Contract Address** field: `0x543ff227f64aa17ea132bf9886cab5db55dcaddf`.
* 3\) Add the following JSON in the **`ABI/JSON Interface`** field:

```javascript
[{"constant":false,"inputs":[{"name":"_to","type":"address"},
{"name":"_value","type":"uint256"},{"name":"_data","type":"bytes"}],
"name":"transfer","outputs":[{"name":"","type":"bool"}],
"payable":false,"stateMutability":"nonpayable","type":"function"}]
```

* 4\) Click **Continue**

![](../../.gitbook/assets/image%20%2815%29.png)

3. Fill the parameters to execute the `transfer` method:

* 1\) Select `transfer` from the **Select an Item** dropdown
* 2\) Enter the **\_to** address `0x6eA6C65E14661C0BcaB5bc862fE5E7D3B5630C2F`. This is the mediator contract serving the bridge extension on the Ethereum Mainnet
* 3\) Enter the **\_value** - the amount of tokens \(in Wei\) to transfer. It must be the same as the value specified in the step 1.5.
* 4\) Enter the **\_data** with the hexadecimal string copied in the step 1.7. Prepend the string by `0x` symbols.
* 5\) Press **Write** to send the tokens.

![](../../.gitbook/assets/image%20%2820%29.png)

4. Check that the Gas price is not set too high, then **Submit** the transaction with a web3 wallet \(like MetaMask or Nifty wallet\). Wait to proceed until it is included in the chain.

5. The AMB bridge requires a short amount time to relay the deposit request to the xDai chain. After some time the xGEN balance of the account that sent the tokens will increase. The result of the relay operation can be monitored [in Blockscout](https://blockscout.com/poa/xdai/tokens/0x3e12081dd66a3600fc0a2e6cc9e6b5b3b8f037f6/token_transfers) \(input the final token contract to monitor\). 

