---
description: >-
  This guide describes how to use the block explorers to transfer Wrapped BNB
  from the xDai chain to Binance Smart Chain in form of BNB native tokens
---

# Transfer WBNB on xDai to BNB on BSC

## Background

Since BNB is a native token for the Binance Smart Chain it is obvious that all operations in BSC  require to use this token to pay for gas fees. There is also a BEP-20 version of this token [Wrapped BNB/WBNB](https://bscscan.com/address/0xbb4CdB9CBd36B01bD1cBaEBF2De08d9173bc095c) -- it is used mostly in case when unified operations with tokens are required \(for example, on AMM platforms\).

As soon as the BSC-xDai OmniBridge has been run, the wrapped BNB was bridged to the xDai chain in form of ERC677 token: [Wrapped BNB on xDai](https://blockscout.com/poa/xdai/address/0xCa8d20f3e0144a72C6B5d576e9Bd3Fd8557E2B04).

But even the bridged token can be transferred back to BSC it still be in form of the BEP-20 token, that is why it cannot be used in transactions to pay for gas fees. But if a user has no BNB it will be impossible to him/her to unwrap the BNB tokens.

This set of instructions demonstrates how the Wrapped BNB can be bridged from the xDai chain directly to BNB tokens with usage of a new feature relay-and-call implemented recently in the OmniBridge contracts. In the last section of the manual there is also the instruction how to transfer BNBs to WBNB on the xDai chain by one operation -- although this ability will not be used often some users could find it handy.

The manual assumes that you have access to [BlockScout](https://blockscout.com/poa/xdai) and [BSCScan](https://bscscan.com/). You also must have a bit xDai to pay for gas fees for a bridging transaction in the xDai chain. 

## Bridge WBNB on xDai to BNB

1. Change the chain to xDai in MetaMask/NiftyWallet. 

2. Find the Wrapped BNB token in [BlockScout](https://blockscout.com/poa/xdai):

![](../../.gitbook/assets/image%20%281%29.png)

WBNB token in the xDai chain: [`0xCa8d20f3e0144a72C6B5d576e9Bd3Fd8557E2B04`](https://blockscout.com/poa/xdai/address/0xCa8d20f3e0144a72C6B5d576e9Bd3Fd8557E2B04)

3. Go to the [Write Proxy](https://blockscout.com/poa/xdai/address/0xCa8d20f3e0144a72C6B5d576e9Bd3Fd8557E2B04/write-proxy) tab

![](../../.gitbook/assets/image%20%28148%29.png)

4. Scroll to the `transferAndCall` method.

![](../../.gitbook/assets/image%20%28144%29.png)

Enter the following information to the fields:

* `_to` \(address\) with the address of the OmniBridge contract on the xDai chain: `0x59447362798334d3485c64D1e4870Fde2DDC0d75`
* `_value` \(uint256\) with amount of WBNB which is going to be bridged \(bridge fees will be subtracted from this value\)
* `_data` \(bytes\) with two pieces concatenated:

  * the address of the WBNB OmniBridge helper contract on Binance Smart Chain \(`0xefc33f8b2c4d51005585962be7ea20518ea9fd0d`\)
  * the address of the BNB recipient without `0x`.

  E.g. for the recipient `0xbf3d6f830ce263cae987193982192cd990442b53` the eventual value to enter in the `_data` field will be `0xefc33f8b2c4d51005585962be7ea20518ea9fd0dbf3d6f830ce263cae987193982192cd990442b53`

Press Write to send the transaction. 

5. As soon as the transaction is included in the block, click on the transaction link to get the transaction details:

![](../../.gitbook/assets/image%20%28101%29.png)

6. Use "View in ALM App" link on the page with transaction details to track status of the transfer and finalize the bridging operation.

![](../../.gitbook/assets/image%20%28143%29.png)

7. Eventually, it will be a transaction in the Binance Smart Chain unlocking corresponding amount of WBNB and unwrapping them into BNB native tokens:

![](../../.gitbook/assets/image%20%2813%29.png)

## Bridge BNB to the xDai chain

1. Visit the WBNB OmniBridge helper contract on [BSCScan](https://bscscan.com/): [`0xefc33f8b2c4d51005585962be7ea20518ea9fd0d`](https://bscscan.com/address/0xefc33f8b2c4d51005585962be7ea20518ea9fd0d)

2. Go to the [Write Contract](https://bscscan.com/address/0xefc33f8b2c4d51005585962be7ea20518ea9fd0d#writeContract) tab:

![](../../.gitbook/assets/image%20%28145%29.png)

and connect the wallet.

3. Scroll to the `wrapAndRelayTokens` method and enter amount of BNB to bridge to the xDai chain:

![](../../.gitbook/assets/image%20%28147%29.png)

Press Write to send the transaction.

4. As soon as the transaction is included in the block, press to the "View you transaction" button to get the transaction hash which can be used in [the AMB Live Monitoring app](https://alm-bsc-xdai.herokuapp.com/) to track the status of the transaction.

![](../../.gitbook/assets/image%20%28146%29.png)

