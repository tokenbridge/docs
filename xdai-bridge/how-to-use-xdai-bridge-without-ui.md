# How to use xDai Bridge without UI

There is no need to use the Bridge UI if you want transfer your DAI through the bridge. You can use the instruction below and the bridge will relay your asset to another network.

### Transfer  Dai from the Ethereum Mainnet to the xDai Chain

* Make a usual transfer of DAI tokens \(`0x89d24A6b4CcB1B6fAA2625fE562bDD9a23260359`\) on the ETH Mainnet by any software that is able to do ERC20 transfers \(e.g. [NiftyWallet ](https://chrome.google.com/webstore/detail/nifty-wallet/jbdaocneiiinmjbjlgalhcelgbejmnid?hl=en), [MyEtherWallet.com](http://myetherwallet.com/), [TrustWallet](https://trustwallet.com/)\). Use the Token Bridge address `0x4aa42145Aa6Ebf72e164C9bBC74fbD3788045016` as the recipient of the payment.
* Wait for the transaction confirmation in the ETH Mainnet \(depends on the gas price you setup for the transfer transaction and the network throughput\).
* Wait for the relay confirmation by the bridge validators \(depends on the number of blocks that the bridge validators wait for to consider the chain finalized, for now it is `8`\).
* Check your balance on the xDai chain

![Sending Dai to xDai on Ethereum](../.gitbook/assets/screenshot_20191009-095817.jpg)

### Transfer xDai from the xDai chain to the Ethereum Mainnet

* Send xDai coins to the Token Bridge address `0x7301CFA0e1756B71869E93d4e4Dca5c7d0eb0AA6` on the xDai Сhain by any wallet software.
* Wait for the transaction confirmation in the xDai chain \(5 seconds\).
* Wait for relay confirmation by the bridge validators \(depends on number of validators and the ETH Mainnet network throughput\)
* Check your balance on the ETH Mainnet

![Sending xDai to Dai in AlphaWallet](../.gitbook/assets/untitled.png)

{% hint style="success" %}
Instruction is migrated from the POA forum [https://forum.poa.network/t/how-to-relay-dai-stablecoins-without-usage-of-the-bridge-ui/1876](https://forum.poa.network/t/how-to-relay-dai-stablecoins-without-usage-of-the-bridge-ui/1876)
{% endhint %}

