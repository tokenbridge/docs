---
description: How to transfer tokens manually through the BSC-xDai OmniBridge
---

# Manual tokens transfer

The OmniBridge is a decentralized application. It means that the tokens can be transferred through the extension without using a dedicated UI. 

{% hint style="warning" %}
Manual transfer of tokens through the OmniBridge extension assumes deep understanding of what exactly is being performed in every operation. A person performing these operations must take possible risks of loosing funds in case of incorrect actions.
{% endhint %}

## Transfer from the Binance Smart Chain

{% hint style="info" %}
The instructions below uses [MyEtherWallet](https://www.myetherwallet.com/) to interaction with the token contract. This is because some tokens contract cannot be verified by [BscScan](https://bscscan.com/) due to its limitations that's why it is not possible to interact with the tokens contracts there.   
  
_One could find more convenient ways to interact with the token contracts._
{% endhint %}

1. Login to [MyEtherWallet](https://www.myetherwallet.com/) by one of suitable ways. If MetaMask is used to login, the Binance Smart Chain must be [added to the MetaMask](https://docs.binance.org/smart-chain/wallet/metamask.html) first.

![](../../.gitbook/assets/image%20%28123%29.png)

2. Choose "Interact with Contract" in the main menu

![](../../.gitbook/assets/image%20%28114%29.png)

3. Enter the address of the token contract \([_Wrapped BNB_](https://bscscan.com/token/0xbb4CdB9CBd36B01bD1cBaEBF2De08d9173bc095c) _is used in the example_\) in the Binance Smart Chain and the following ABI JSON to the form and press "Continue".

```javascript
[
  {
    "constant":false,
    "inputs":[
      {
        "name":"spender",
        "type":"address"
      },
      {
        "name":"value",
        "type":"uint256"
      }
    ],
    "name":"approve",
    "outputs":[
      {
        "name":"",
        "type":"bool"
      }
    ],
    "payable":false,
    "stateMutability":"nonpayable",
    "type":"function"
  }
]
```

![](../../.gitbook/assets/image%20%28109%29.png)

4. Choose the `approve` method from the dropdown list and fill data in the form where "Spender" is the OmniBridge mediator contract [`0xF0b456250DC9990662a6F25808cC74A6d1131Ea9`](https://bscscan.com/address/0xF0b456250DC9990662a6F25808cC74A6d1131Ea9) and "Value" is the amount of tokens that is going to be transferred through the bridge. The value is specified in Wei and must be [within the limits on the bridge operations](https://docs.tokenbridge.net/bsc-xdai-amb/omnibridge-extension#transfer-limits). Finally, press the "Write" button and confirm the transaction sending in your wallet. Wait until the transaction is included in a block.

![](../../.gitbook/assets/image%20%28120%29.png)

5. Use the BscScan site to access to the OmniBridge mediator on the Binance Smart Chain and go to "Write as Proxy" tab: [https://bscscan.com/address/0xF0b456250DC9990662a6F25808cC74A6d1131Ea9\#writeProxyContract](https://bscscan.com/address/0xF0b456250DC9990662a6F25808cC74A6d1131Ea9#writeProxyContract).

6. Connect to Web3 wallet to the BscScan app to be able to invoke the contract's method:

![](../../.gitbook/assets/image%20%28117%29.png)

7. Scroll till the `relayTokens` method and fill the token contract address and the value which is going to be sent through the bridge \(it must be the same or lesser than the value specified in the `approve` method\). Press the "Write" button, confirm the transaction in the wallet. Wait for the transaction inclusion into the blockchain.

![](../../.gitbook/assets/image%20%28110%29.png)

8. Press to the "View your transaction" button to get the hash of the transaction. And use this hash on [the AMB Live Monitoring \(ALM\) app](https://alm-bsc-xdai.herokuapp.com/) to look for the bridging process status.

9. Press to the link in the "Executed by" section of ALM to refer to the transaction that causes the token transfer  finalization.

![](../../.gitbook/assets/image%20%28108%29.png)

There will be a tile In the "Tokens Transfers" clarifying amount of tokens transferred through the bridge and receiver of the tokens.

{% hint style="warning" %}
Depending on the tokens origin it could be two possible operations mentioned in the tile: if the token's origin is the Binance Smart chain it will be "Token Minting"; if the token's origin is the xDai chain it will be "Token Transfer".
{% endhint %}

![](../../.gitbook/assets/image%20%28118%29.png)

10. Press on the token symbol to get the address of the bridged token to add it in your wallet if it is necessary. 

![](../../.gitbook/assets/image%20%28115%29.png)

![](../../.gitbook/assets/image%20%28119%29.png)

## Transfer from the xDai chain

{% hint style="warning" %}
The token transfer process from the xDai chain to the Binance Smart Chain requires  a user to send transactions on both chains. That is why the xDai native tokens and the BNB native tokens are required to pay for gas fees for these transactions.
{% endhint %}

1. Choose the xDai chain in MetaMask. If such network is not configured in the MetaMask follow [these instructions](https://www.xdaichain.com/for-users/wallets/metamask/metamask-setup) to set it up.

2. Use [the BlockScout site](https://blockscout.com/poa/xdai) to find the token that needs to be bridge.

![](../../.gitbook/assets/image%20%28122%29.png)

3. Go to the "Write Proxy" tab on the token contract page

![](../../.gitbook/assets/image%20%28111%29.png)

4. Scroll till the "approve" method and fill data in the form where "spender" is the OmniBridge mediator contract [`0x59447362798334d3485c64D1e4870Fde2DDC0d75`](https://blockscout.com/poa/xdai/address/0x59447362798334d3485c64D1e4870Fde2DDC0d75) and "value" is the amount of tokens that is going to be transferred through the bridge. The value is specified in Wei and must be [within the limits on the bridge operations](https://docs.tokenbridge.net/bsc-xdai-amb/omnibridge-extension#transfer-limits). Finally, press the "Write" button and confirm the transaction sending in your wallet. Wait until the transaction is included in a block.

![](../../.gitbook/assets/image%20%28105%29.png)

5. Switch to the OmniBridge mediator in the BlockScout and go to "Write as Proxy" tab: [https://blockscout.com/poa/xdai/address/0x59447362798334d3485c64D1e4870Fde2DDC0d75/write-proxy](https://blockscout.com/poa/xdai/address/0x59447362798334d3485c64D1e4870Fde2DDC0d75/write-proxy)

6. Scroll till the `relayTokens` method and fill the token contract address and the value which is going to be sent through the bridge \(it must be the same or lesser than the value specified in the `approve` method\). Press the "Write" button, confirm the transaction in the wallet. Wait for the transaction inclusion into the blockchain.

![](../../.gitbook/assets/image%20%28107%29.png)

7. When the modal window reporting about the successful operation appears press the transaction link to get its hash. Use this hash on [the AMB Live Monitoring \(ALM\) app](https://alm-bsc-xdai.herokuapp.com/) to look for the bridging process status.

![](../../.gitbook/assets/image%20%28112%29.png)

8. Switch the chain to the Binance Smart Chain in MetaMask and press the "Execute" button to finialize the tokens transfer. This action collects the Arbitrary Message Bridge oracles confirmations and deliver them to BSC. BNB native tokens are required to pay for gas fees to finalize the transfer.

![](../../.gitbook/assets/image%20%28124%29.png)

As soon as the submitted transaction is included in the block the "Executed by" section of ALM will contain the link on the transaction performed the tokens transfer.

![](../../.gitbook/assets/image%20%28113%29.png)

9. Press to the link in the "Executed by" section to see transfer details.

![](../../.gitbook/assets/image%20%28103%29.png)

10. Press on the token name to get the address of the bridged token to add it in your wallet if it is necessary. 

![](../../.gitbook/assets/image%20%28106%29.png)

