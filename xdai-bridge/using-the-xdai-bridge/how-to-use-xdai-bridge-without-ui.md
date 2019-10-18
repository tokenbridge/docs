---
description: 'Transfer Dai to xDai and back again, without the UI'
---

# How to use the xDai Bridge without the UI

{% hint style="success" %}
There is no need to use the Bridge UI if you want transfer your DAI to xDai or xDai to DAI. The instructions below show how to relay your assets without the UI. 
{% endhint %}

## Transfer Dai from the Ethereum Mainnet to the xDai Chain

* Make a usual transfer of DAI tokens \(`0x89d24A6b4CcB1B6fAA2625fE562bDD9a23260359`\) on the ETH Mainnet with any wallet software designed for ERC20 transfers \(e.g. [NiftyWallet ](https://chrome.google.com/webstore/detail/nifty-wallet/jbdaocneiiinmjbjlgalhcelgbejmnid?hl=en), [MyEtherWallet.com](http://myetherwallet.com/), [TrustWallet](https://trustwallet.com/)\). 
  * Use the Token Bridge address `0x4aa42145Aa6Ebf72e164C9bBC74fbD3788045016` as the recipient of the payment.
* Wait for transaction confirmation in the ETH Mainnet \(transaction time depends on the gas price you setup for the transfer transaction and the network throughput\).
* Wait for the relay confirmation by the bridge validators \(time depends on the number of blocks \ the bridge validators wait for to consider the chain finalized, currently set at  `8`\).
* Check your balance on the xDai chain.

![Sending Dai to xDai on Ethereum](../../.gitbook/assets/screenshot_20191009-095817.jpg)

### Transfer xDai from the xDai chain to the Ethereum Mainnet

* Send xDai coins to the Token Bridge address `0x7301CFA0e1756B71869E93d4e4Dca5c7d0eb0AA6` on the xDai Сhain using any wallet software.
* Wait for the transaction confirmation in the xDai chain \(5 seconds\).
* Wait for relay confirmation by the bridge validators \(depends on number of validators and the ETH Mainnet network throughput\)
* Check your balance on the ETH Mainnet

![Sending xDai to Dai in AlphaWallet](../../.gitbook/assets/untitled.png)

{% hint style="success" %}
Instructions migrated from the POA forum [https://forum.poa.network/t/how-to-relay-dai-stablecoins-without-usage-of-the-bridge-ui/1876](https://forum.poa.network/t/how-to-relay-dai-stablecoins-without-usage-of-the-bridge-ui/1876)
{% endhint %}

