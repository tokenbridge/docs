---
description: >-
  A guide on using block explorers to transfer Wrapped BNB from the xDai chain
  to the Binance Smart Chain in the form of BNB native tokens.
---

# Transfer WBNB on xDai to BNB on BSC

## Background

BNB is the native token for the Binance Smart Chain (BSC), and all operations on BSC require this token to pay for gas fees. There is also a BEP-20 version of this token [Wrapped BNB/WBNB](https://bscscan.com/address/0xbb4CdB9CBd36B01bD1cBaEBF2De08d9173bc095c) -- it is used mostly in cases when unified token operations are required (for example, on AMM platforms).

When the BSC-xDai OmniBridge first started, wrapped BNB was bridged to the xDai chain in form of ERC677 token: [Wrapped BNB from BSC](https://blockscout.com/xdai/mainnet/address/0xCa8d20f3e0144a72C6B5d576e9Bd3Fd8557E2B04/transactions).

Although the bridged token can be transferred back to BSC,  it is still be in form of the BEP-20 token, and it cannot be used in transactions to pay for gas fees. In this case, if a user has no BNB, it is impossible for them to unwrap these BNB tokens.

This set of instructions demonstrates how the Wrapped BNB can be bridged from the xDai chain directly to BNB tokens using a new `relay-and-call` feature implemented recently in the OmniBridge contracts. In the last section of the manual there is also an instruction on how to transfer BNB to WBNB on the xDai chain using a single operation. This may not be used often but some users may find it handy.

This instruction assumes that you have access to [BlockScout](https://blockscout.com/poa/xdai) and [BSCScan](https://bscscan.com). You also must have a bit of xDai to pay for gas fees for a bridge transaction on the xDai chain.&#x20;

## Bridge WBNB on xDai to BNB

1\. Change the chain to xDai in MetaMask/NiftyWallet.&#x20;

2\. Find the Wrapped BNB token in [BlockScout](https://blockscout.com/poa/xdai):

![](<../../.gitbook/assets/image (136).png>)

WBNB token in the xDai chain: [`0xCa8d20f3e0144a72C6B5d576e9Bd3Fd8557E2B04`](https://blockscout.com/poa/xdai/address/0xCa8d20f3e0144a72C6B5d576e9Bd3Fd8557E2B04)

3\. Go to the [Write Proxy](https://blockscout.com/poa/xdai/address/0xCa8d20f3e0144a72C6B5d576e9Bd3Fd8557E2B04/write-proxy) tab

![](<../../.gitbook/assets/image (140).png>)

4\. Scroll to the `transferAndCall` method.

![](<../../.gitbook/assets/image (141).png>)

Enter the following information to the fields:

* `_to` (address) the address of the OmniBridge contract on the xDai chain: `0x59447362798334d3485c64D1e4870Fde2DDC0d75`
* `_value` (uint256) with amount of WBNB to be bridged (bridge fees will be subtracted from this value)
*   `_data` (bytes) with two pieces concatenated:

    * the address of the WBNB OmniBridge helper contract on Binance Smart Chain (`0xefc33f8b2c4d51005585962be7ea20518ea9fd0d`)
    * the address of the BNB recipient without `0x`.

    E.g. for the recipient `0xbf3d6f830ce263cae987193982192cd990442b53` the value in `_data` field is`0xefc33f8b2c4d51005585962be7ea20518ea9fd0dbf3d6f830ce263cae987193982192cd990442b53`

Press **Write** to send the transaction.&#x20;

5\. As soon as the transaction is included in the block, click on the transaction link to get the transaction details:

![](<../../.gitbook/assets/image (142).png>)

6\. Use "**View in ALM App**" link on the page with transaction details to track status of the transfer and finalize the bridging operation if required.

![](<../../.gitbook/assets/image (143).png>)

7\. Eventually, a transaction in the Binance Smart Chain will process unlocking the corresponding amount of WBNB and unwrapping them into BNB native tokens:

![](<../../.gitbook/assets/image (144).png>)

## Bridge BNB to the xDai chain

1\. Visit the WBNB OmniBridge helper contract on [BSCScan](https://bscscan.com): [`0xefc33f8b2c4d51005585962be7ea20518ea9fd0d`](https://bscscan.com/address/0xefc33f8b2c4d51005585962be7ea20518ea9fd0d)

2\. Go to the [Write Contract](https://bscscan.com/address/0xefc33f8b2c4d51005585962be7ea20518ea9fd0d#writeContract) tab:

![](<../../.gitbook/assets/image (137).png>)

and connect your wallet.

3\. Scroll to the `wrapAndRelayTokens` method and enter the amount of BNB to bridge to the xDai chain:

![](<../../.gitbook/assets/image (138).png>)

Press **Write** to send the transaction.

4\. As soon as the transaction is included in the block, press the "View you transaction" button to get the transaction hash which can be used in [the AMB Live Monitoring app](https://alm-bsc-xdai.herokuapp.com) to track the status of the transaction.

![](<../../.gitbook/assets/image (139).png>)
