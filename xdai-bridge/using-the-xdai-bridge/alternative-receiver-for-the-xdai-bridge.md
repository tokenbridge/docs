---
description: Instructions how to use the Alternative receiver feature with the xDai bridge
---

# Alternative receiver for the xDai bridge

The new feature _Alternative Receiver_ has integrated in the contracts of the xDai bridge as part of [the recent contracts upgrade](https://forum.poa.network/t/migration-of-the-xdai-tokenbridge-completed/3212). With this feature it becomes possible to transfer tokens through the bridge to any account by very simple actions. It means that Alice can send Dai to Bob’s account on the xDai chain in one transaction, and Bob can send xDai to Clare’s account on the Ethereum Mainnet in one transaction too.

Due to different nature of tokens on two sides of the xDai bridge the operations to transfer assets to an alternative receiver from one chain to another differ as well.

## Dai to xDai

1. Open MetaMask and choose the Ethereum Mainnet.

2. Go to the Dai Token Contract -&gt; Write Contract functionality in Etherscan.  
[https://etherscan.io/address/0x6b175474e89094c44da98b954eedeac495271d0f\#writeContract](https://etherscan.io/address/0x6b175474e89094c44da98b954eedeac495271d0f#writeContract)

3. Connect to your Web3Wallet \(MetaMask\).

![](../../.gitbook/assets/1-etherscan.png)

4. Approve the bridge contract to perform operations with tokens:

* `usr(address)` -- the address of the xDai bridge contract in the Ethereum Mainnet: `0x4aa42145Aa6Ebf72e164C9bBC74fbD3788045016`
* `wad(uint256)` -- the amount of tokens \(in Wei\) approved to send through the bridge \(in this case 2 Dai\): `2000000000000000000`
* Click **Write**

![](../../.gitbook/assets/2-etherscanwrite.png)

4. Confirm the transaction in the MetaMask and wait until it is included in the chain.

![](../../.gitbook/assets/etherscan-3.png)

5. Initialize the xDai bridge contract interface in Etherscan. Here you will write to the proxy contract. [https://etherscan.io/address/0x4aa42145aa6ebf72e164c9bbc74fbd3788045016\#writeProxyContract](https://etherscan.io/address/0x4aa42145aa6ebf72e164c9bbc74fbd3788045016#writeProxyContract)

6. You will see several  `relayTokens` methods. Use Method \(1\) to send to an alternate address. You can also use a second method \(14\) if the Dai deposit is performed by another contract of behalf of the user account \(like a DEX\). There are also 2 other relayToken methods \(4\), \(22\) that specify a `_token(address)`. These are not in use.

**relayTokens Method \(1\)**

* `_receiver (address)` - address of the alternate receiver, the account that will be sent native tokens on the xDai chain
* `_amount (uint256)` - the amount of tokens \(in Wei\) to transfer; must be less or equal amount of tokens approved for the bridge operations
* Click **Write**

**relayTokens Method\(14\)**

* `_sender (address)` - optional. Use when the Dai deposit is performed by another contract on behalf of a user account \(e.g. by a DEX\)
* `_receiver (address)` - address of the alternate receiver, the account that will be sent native tokens on the xDai chain
* `_amount (uint256)` - the amount of tokens \(in Wei\) to transfer; must be less or equal amount of tokens approved for the bridge operations
* Click **Write**

![Here we send .5 Dai. We can send any amount up to the amount approved in step 4.](../../.gitbook/assets/4-etherscan.png)

7. Submit the transaction in the MetaMask and wait until it is included in the chain.

8. The xDai bridge will take some time to relay the deposit request to the xDai chain. Once complete, the balance of the `_receiver`account will increase with the corresponding amount of xDai.

### xDai to Dai

{% hint style="info" %}
Since Etherscan does not currently support xDai, we use MyEtherWallet for this example. You can also use Nifty Wallet.
{% endhint %}

1. Choose the xDai chain in the browser wallet extension and login to [MyEtherWallet \(MEW\)](https://www.myetherwallet.com/access-my-wallet). 

2. Initialize the xDai bridge contract interface by putting the bridge contract address `0x7301CFA0e1756B71869E93d4e4Dca5c7d0eb0AA6` and the following JSON in the **`ABI/JSON Interface`** field:

```javascript
[{"type":"function","stateMutability":"payable","payable":true,
"outputs":[],"name":"relayTokens","inputs":[{"type":"address",
"name":"_receiver"}],"constant":false}]
```

![](../../.gitbook/assets/image%20%2811%29.png)

3. Prepare the call for the  `relayTokens` method:

![](../../.gitbook/assets/image%20%2819%29.png)

where

* `_receiver` -- Account to receive Dai tokens on the Ethereum Mainnet
* `Value in ETH` -- the amount of native tokens \(in ether\) to transfer

4. Submit the transaction in the MetaMask and wait when it is included in the chain.

5. It will require the xDai bridge some time to relay the withdrawal request to the Ethereum Mainnet. Eventually the balance of the receiver account in the Dai token contract will be increased.

