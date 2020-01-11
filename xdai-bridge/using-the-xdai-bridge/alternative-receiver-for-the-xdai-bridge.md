---
description: Instructions how to use the Alternative receiver feature with the xDai bridge
---

# Alternative receiver for the xDai bridge

The new feature _Alternative Receiver_ has integrated in the contracts of the xDai bridge as part of [the recent contracts upgrade](https://forum.poa.network/t/migration-of-the-xdai-tokenbridge-completed/3212). With this feature it becomes possible to transfer tokens through the bridge to any account by very simple actions. It means that Alice can send Dai or Sai to Bob’s account on the xDai chain in one transaction, and Bob can send xDai to Clare’s account on the Ethereum Mainnet in one transaction too.

Due to different nature of tokens on two sides of the xDai bridge the operations to transfer assets to an alternative receiver from one chain to another differ as well.

{% hint style="danger" %}
The following instructions are for illustrative purposes only. MyEtherWallet is not totally compatible with xDai for these types of contract calls.  Alternate receiver is designed for use by Multisig wallets and other contracts.
{% endhint %}

### Sai/Dai to xDai

1. Choose the Ethereum Mainnet in the MetaMask extension and login to [MyEtherWallet \(MEW\)](https://www.myetherwallet.com/access-my-wallet).

2. Initialize the Sai token contract interface by putting the Sai token contract address `0x89d24a6b4ccb1b6faa2625fe562bdd9a23260359` and the following JSON in the **`ABI/JSON Interface`** field: 

```javascript
[{"constant":false,"inputs":[{"name":"guy","type":"address"},
{"name":"wad","type":"uint256"}],"name":"approve",
"outputs":[{"name":"","type":"bool"}],"payable":false,
"stateMutability":"nonpayable","type":"function"}]
```

![](../../.gitbook/assets/image%20%289%29.png)

3. Approve the bridge contract to perform operations with tokens:

![](../../.gitbook/assets/image%20%281%29.png)

where

* `Guy` -- the address of the xDai bridge contract in the Ethereum Mainnet
* `Wad` -- the amount of tokens \(in Wei\) that is going to be sent through the bridge

4. Submit the transaction in the MetaMask and wait when it is included in the chain.

5. Initialize the xDai bridge contract interface by putting the bridge contract address `0x4aa42145Aa6Ebf72e164C9bBC74fbD3788045016` and the following JSON in the **`ABI/JSON Interface`** field:

```javascript
[{"constant":false,"inputs":[{"name":"_receiver",
"type":"address"},{"name":"_amount","type":"uint256"}],
"name":"relayTokens","outputs":[],"payable":false,
"stateMutability":"nonpayable","type":"function"},
{"constant":false,"inputs":[{"name":"_from","type":"address"},
{"name":"_receiver","type":"address"},{"name":"_amount",
"type":"uint256"},{"name":"_token","type":"address"}],
"name":"relayTokens","outputs":[],"payable":false,
"stateMutability":"nonpayable","type":"function"},
{"constant":false,"inputs":[{"name":"_from","type":"address"},
{"name":"_receiver","type":"address"},{"name":"_amount",
"type":"uint256"}],"name":"relayTokens","outputs":[],
"payable":false,"stateMutability":"nonpayable",
"type":"function"},{"constant":false,
"inputs":[{"name":"_receiver","type":"address"},
{"name":"_amount","type":"uint256"},{"name":"_token",
"type":"address"}],"name":"relayTokens","outputs":[],
"payable":false,"stateMutability":"nonpayable","type":"function"}]
```

![](../../.gitbook/assets/image%20%286%29.png)

6. Choose an appropriate `relayTokens` method. There are four methods there:

* `relayTokens(address _receiver, uint256 _amount)`-- can be used to specify an alternative receiver to transfer the Dai tokens 
* `relayTokens(address _from, address _receiver, uint256 _amount)` -- intended to be invoked in scenarios when the Dai tokens deposit is performed by another contract on behalf of a user account \(e.g. by a DEX\)
* `relayTokens(address _receiver, uint256 _amount, address _token)` -- can be used to specify an alternative receiver to transfer the Sai tokens
* `relayTokens(address _from, address _receiver, uint256 _amount, address _token)` -- intended to be invoked in scenarios when the Sai tokens deposit is performed by another contract on behalf of a user account \(e.g. by a DEX\)

![](../../.gitbook/assets/image%20%2811%29.png)

where

* `_receiver` -- the account that will get native tokens on the xDai chain
* `_amount` -- the amount of tokens \(in Wei\) to transfer; it should be less or equal amount of tokens approved for the bridge operations
* `_token` -- the address of Sai token contract

7. Submit the transaction in the MetaMask and wait when it is included in the chain.

8. It will require the xDai bridge some time to relay the deposit request to the xDai chain. Eventually the balance of the account that was specified as `_receiver` in the `relayTokens` method call will be increased. 

### xDai to Dai

1. Choose the xDai chain in the browser wallet extension and login to [MyEtherWallet \(MEW\)](https://www.myetherwallet.com/access-my-wallet). 

2. Initialize the xDai bridge contract interface by putting the bridge contract address `0x7301CFA0e1756B71869E93d4e4Dca5c7d0eb0AA6` and the following JSON in the **`ABI/JSON Interface`** field:

```javascript
[{"type":"function","stateMutability":"payable","payable":true,
"outputs":[],"name":"relayTokens","inputs":[{"type":"address",
"name":"_receiver"}],"constant":false}]
```

![](../../.gitbook/assets/image%20%284%29.png)

3. Prepare the call of `relayTokens` method:

![](../../.gitbook/assets/image%20%287%29.png)

where

* `_receiver` -- the account that will get Dai tokens on the Ethereum Mainnet
* `Value in ETH` -- the amount of native tokens \(in ether\) to transfer

4. Submit the transaction in the MetaMask and wait when it is included in the chain.

5. It will require the xDai bridge some time to relay the withdrawal request to the Ethereum Mainnet. Eventually the balance of the receiver account in the Dai token contract will be increased.

