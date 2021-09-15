---
description: Instructions on relaying DAOstack tokens through the GEN-xGEN bridge extension
---

# Transfer GEN between the ETH Mainnet and the xDai Chain

{% hint style="warning" %}
This manual is not intended as an official protocol to transfer GEN tokens through the AMB extension. The actions described below provide an idea about how to automate operations involving the Arbitrary Message Bridge, and demonstrate the transfer process.
{% endhint %}

{% hint style="info" %}
It is assumed that accounts executing operations below have a small amount of Ether and xDai for gas fees as well as an amount of GENs to transfer. GEN tokens can be obtained through [Uniswap](https://uniswap.exchange/) or other exchanges.
{% endhint %}

For demonstration purposes we use [MyEtherWallet \(MEW\)](https://www.myetherwallet.com/access-my-wallet) to move assets from the Ethereum Mainnet to the xDai chain. These actions may be applied to any other wallet with similar capabilities.

## Deposit GEN tokens to the xDai chain

1. GEN is a ERC827-compatible token. If the account that receives tokens is a contract, it is possible to call a method of this contract. The `onTokenTransfer` method of the mediator contract will be used to notify the mediator contract that some amount of tokens has been sent. We can build the method invocation with [https://abi.hashex.org/](https://abi.hashex.org/)
2. 1\) Add the following JSON in the input field:

```javascript
[{"constant":false,"inputs":[{"name":"_from","type":"address"},
{"name":"_value","type":"uint256"},{"name":"_data","type":"bytes"}],
"name":"onTokenTransfer","outputs":[{"name":"","type":"bool"}],
"payable":false,"stateMutability":"nonpayable","type":"function"}]
```

![](../../../.gitbook/assets/image%20%282%29.png)

* 2\) Click **Parse**
* 3\) Choose _onTokenTransfer_ in the **Function type** dropdown
* 4\) Enter the **\_from** address. It is the account that will send the GEN tokens.
* 5\) Enter the **\_value** - the amount of tokens \(in Wei\) to transfer.
* 6\) Leave the **\_data** field empty.
* 7\) Click **Copy** to copy the content of the **ABI-encoded output** text field and store it somewhere.

![](../../../.gitbook/assets/image%20%2812%29.png)

1. Activate and open a web3 wallet \(like MetaMask or Nifty Wallet\) and select the Ethereum Mainnet chain. Choose the account that will send the tokens \(the same as it was used on the step 1.4\). Go to [MyEtherWallet \(MEW\)](https://www.myetherwallet.com/access-my-wallet) and select the option to login with a web3 wallet. Next:
2. 1\) Select the **Interact with Contract** item from the sidebar menu
3. 2\) Initialize the GEN token contract interface by entering the DAOstack token contract address in the **Contract Address** field: `0x543ff227f64aa17ea132bf9886cab5db55dcaddf`.
4. 3\) Add the following JSON in the **`ABI/JSON Interface`** field:

```javascript
[{"constant":false,"inputs":[{"name":"_to","type":"address"},
{"name":"_value","type":"uint256"},{"name":"_data","type":"bytes"}],
"name":"transfer","outputs":[{"name":"","type":"bool"}],
"payable":false,"stateMutability":"nonpayable","type":"function"}]
```

* 4\) Click **Continue**

![](../../../.gitbook/assets/image%20%2825%29%20%281%29.png)

1. Fill the parameters to execute the `transfer` method:
2. 1\) Select `transfer` from the **Select an Item** dropdown
3. 2\) Enter the **\_to** address `0x6eA6C65E14661C0BcaB5bc862fE5E7D3B5630C2F`. This is the mediator contract serving the bridge extension on the Ethereum Mainnet
4. 3\) Enter the **\_value** - the amount of tokens \(in Wei\) to transfer. It must be the same as the value specified in the step 1.5.
5. 4\) Enter the **\_data** with the hexadecimal string copied in step 1.7. Prepend the string by `0x` symbols.
6. 5\) Press **Write** to send the tokens.

![](../../../.gitbook/assets/image%20%2821%29%20%281%29%20%281%29.png)

1. Check that the Gas price is not set too high, then **Submit** the transaction with a web3 wallet \(like MetaMask or Nifty wallet\). Wait to proceed until it is included in the chain.
2. The AMB bridge requires a short amount time to relay the deposit request to the xDai chain. After some time the xGEN balance of the account that sent the tokens will increase. The result of the relay operation can be monitored [in Blockscout](https://blockscout.com/xdai/mainnet/tokens/0x3e12081dd66a3600fc0a2e6cc9e6b5b3b8f037f6/token_transfers) \(input the final token contract to monitor\).

## Withdraw GEN tokens from the xDai chain \(the interim token\)

1. Choose the xDai chain in the browser wallet extension and login to [MyEtherWallet \(MEW\)](https://www.myetherwallet.com/access-my-wallet). Select the **Interact with Contract** item in the side navigation menu. \(_note: you must have xGEN tokens in your wallet on the xDai chain to proceed_\)
2. Initialize the xGEN bridgeable token contract interface:
3. 1\) Add the token **Contract Address** `0x3E12081DD66A3600FC0A2E6cc9e6b5B3b8f037f6`.
4. 2\) Add the following JSON in the **`ABI/JSON Interface`** field:

```javascript
[{"type":"function","stateMutability":"nonpayable","payable":false,
"outputs":[{"type":"bool","name":""}],"name":"transferAndCall",
"inputs":[{"type":"address","name":"_to"},
{"type":"uint256","name":"_value"},{"type":"bytes","name":"_data"}],
"constant":false}]
```

* 3\) Click **Continue.**

![](../../../.gitbook/assets/image%20%2831%29.png)

1. Transfer the xGEN tokens to the mediator contract:
2. 1\) Select _transferAndCall_ from the the **Select an Item** dropdown
3. 2\) Enter in the **\_to** address: `0xe47097ceF3B0bcbb0095A21523714bF0022E2DB8`. This is the  mediator contract serving the bridge extension in the xDai chain.
4. 3\) Enter the **\_value** to transfer in Wei in the `_value` field.
5. 4\) Enter `0x` symbols to the **\_data** field.
6. 5\) Click **Write.**

![](../../../.gitbook/assets/image%20%2820%29.png)

1. Check the gas price, then **Submit** the transaction through the web3 wallet extension and wait until it is included in the chain.
2. It will require the AMB bridge some time to transfer tokens to the Ethereum Mainnet. After several minutes, the GEN balance of the account that sent the tokens will increase. The result of the relay operation can be monitored [in Etherscan](https://etherscan.io/token/0x543ff227f64aa17ea132bf9886cab5db55dcaddf?a=0x6eA6C65E14661C0BcaB5bc862fE5E7D3B5630C2F), and should be viewable in your web3 wallet connected to the Ethereum Mainnet.

## Withdraw GEN tokens from the xDai chain \(the DAOstack token\)

{% hint style="warning" %}
These actions are valid only when the xGEN token is represented by DAOstack-developed contract. In this case there are plans to substitute the interim token with a DAOstack contract after some trial period. Until that time the actions below are not applicable - use [the way specified for the interim token](https://docs.tokenbridge.net/eth-xdai-amb-bridge/gen-xgen-bridge-extension/transfer-gen-between-the-eth-mainnet-and-the-xdai-chain#withdraw-gen-tokens-from-the-xdai-chain-the-interim-token).
{% endhint %}

{% hint style="warning" %}
It is assumed that the address of the DAOstack-developed token will be `0x543ff227f64aa17ea132bf9886cab5db55dcaddf.`
{% endhint %}

1. Prepare the encoded call of the method `onTokenTransfer` by the same way as it is described by the first step in [the section _Deposit GEN tokens to the xDai chain_](https://docs.tokenbridge.net/eth-xdai-amb-bridge/gen-xgen-bridge-extension/transfer-gen-between-the-eth-mainnet-and-the-xdai-chain#deposit-gen-tokens-to-the-xdai-chain)_._
2. Choose the xDai chain in the browser wallet extension and login to [MyEtherWallet \(MEW\)](https://www.myetherwallet.com/access-my-wallet). The account that will send the tokens must be the same as the `account _from` used to encode the mediator contract's method in the previous step. \(the same as in step 1.4\). Go to [MyEtherWallet \(MEW\)](https://www.myetherwallet.com/access-my-wallet) and select the option to login with a web3 wallet. Next:
3. 1\) Select the **Interact with Contract** item from the sidebar menu
4. 2\) Initialize the xGEN token contract interface by entering the DAOstack token contract address in the **Contract Address** field: `0x543ff227f64aa17ea132bf9886cab5db55dcaddf`.
5. 3\) Add the following JSON in the **`ABI/JSON Interface`** field:

```javascript
[{"constant":false,"inputs":[{"name":"_to","type":"address"},
{"name":"_value","type":"uint256"},{"name":"_data","type":"bytes"}],
"name":"transfer","outputs":[{"name":"","type":"bool"}],
"payable":false,"stateMutability":"nonpayable","type":"function"}]
```

* 4\) Click **Continue**

![](../../../.gitbook/assets/image%20%2825%29%20%281%29%20%281%29.png)

1. Fill the parameters to execute the `transfer` method:
2. 1\) Select `transfer` from the **Select an Item** dropdown
3. 2\) Enter the **\_to** address `0xe47097ceF3B0bcbb0095A21523714bF0022E2DB8`. This is the mediator contract serving the bridge extension on the xDai chain.
4. 3\) Enter the **\_value** - the amount of tokens \(in Wei\) to transfer. It must be the same as the value encoded in the call of _onTokenTransfer_.
5. 4\) Enter the **\_data** with the hexadecimal string - encoded value of `onTokenTransfer` call. Prepend the string by `0x` symbols.
6. 5\) Press **Write** to send the tokens.

![](../../../.gitbook/assets/contract-interact-xdai.png)

1. Check that the Gas price is not set too high, then **Submit** the transaction with a web3 wallet \(like MetaMask or Nifty wallet\). Wait to proceed until it is included in the chain.
2. It will require the AMB bridge some time to transfer tokens to the Ethereum Mainnet. After several minutes, the GEN balance of the account that sent the tokens will increase. The result of the relay operation can be monitored [in Etherscan](https://etherscan.io/token/0x543ff227f64aa17ea132bf9886cab5db55dcaddf?a=0x6eA6C65E14661C0BcaB5bc862fE5E7D3B5630C2F), and should be viewable in your web3 wallet connected to the Ethereum Mainnet.

