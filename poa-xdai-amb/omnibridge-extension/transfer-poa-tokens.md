---
description: >-
  A guide on using block explorers to transfer POA native tokens to and from the
  xDai chain.
---

# Transfer POA tokens

## Background

POA is the native token for the POA Network, and all operations on POA require this token to pay for gas fees. There is also a ERC-20 version of this token [Wrapped POA/WPOA](https://blockscout.com/poa/core/address/0xD2CFBCDbDF02c42951ad269dcfFa27c02151Cebd) - it is used mostly in cases when unified token operations are required \(for example, on AMM platforms\).

When the POA-xDai OmniBridge first started, the wrapped POA was bridged to the xDai chain in form of ERC677 token: [Wrapped POA from POA](https://blockscout.com/xdai/mainnet/address/0x9fe3864F9Ae7cfb5668Dae90C0e20c4C3D437664).

Although the bridged token can be transferred back to POA,  it is still be in form of the ERC-20 token, and it cannot be used in transactions to pay for gas fees. In this case, if a user has no POA, it is impossible for them to unwrap these POA tokens.

This set of instructions demonstrates how the Wrapped POA can be bridged from the xDai chain directly to POA tokens. In the last section of the manual there are also instructions on how to transfer POA to WPOA on the xDai chain using a single operation. This may not be used often but some users may find it handy.

This instruction assumes that you have access to [BlockScout for xDai](https://blockscout.com/xdai/mainnet) and [BlockScout for POA](https://blockscout.com/poa/core). You also must have a bit of xDai to pay for gas fees for a bridge transaction on the xDai chain. 

## Bridge ERC20 WPOA on xDai to POA native token

1. Change the chain to xDai in MetaMask/NiftyWallet.

2. Find the Wrapped BNB token in [BlockScout](https://blockscout.com/poa/xdai):

![](../../.gitbook/assets/image%20%28172%29.png)

WPOA ERC20 token in the xDai chain: [`0x9fe3864F9Ae7cfb5668Dae90C0e20c4C3D437664`](https://blockscout.com/xdai/mainnet/address/0x9fe3864F9Ae7cfb5668Dae90C0e20c4C3D437664)

3. Go to the [Write Proxy tab](https://blockscout.com/xdai/mainnet/address/0x9fe3864F9Ae7cfb5668Dae90C0e20c4C3D437664/write-proxy)

![](../../.gitbook/assets/image%20%28129%29.png)

4. Scroll to the `transferAndCall` method.

![](../../.gitbook/assets/image%20%286%29.png)

Enter the following information to the fields:

* `_to` \(address\) the address of the OmniBridge contract on the xDai chain: `0x63be59CF177cA9bb317DE8C4aa965Ddda93CB9d7`
* `_value` \(uint256\) with amount of WPOA to be bridged \(bridge fees will be subtracted from this value\)
* `_data` \(bytes\) with two pieces concatenated:

  * the address of the WPOA OmniBridge helper contract on the POA Network \(`0x38D54E770b172934dd0e2D6Ae71f2c981b364e08`\)
  * the address of a POA recipient without `0x`.

  E.g. for the recipient `0xbf3d6f830ce263cae987193982192cd990442b53` the value in `_data` field is `0x38D54E770b172934dd0e2D6Ae71f2c981b364e08bf3d6f830ce263cae987193982192cd990442b53`

Press **Write** to send the transaction. 

5. As soon as the transaction is included in the block, click on the transaction link to get the transaction details:

![](../../.gitbook/assets/image%20%28101%29.png)

6. Use "**View in ALM App**" link on the page with transaction details to track status of the transfer and finalize the bridging operation if required \(it also can be done by using the block explorer\).

![](../../.gitbook/assets/image%20%28154%29.png)

7. Eventually, a transaction in the POA Network will process unlocking the corresponding amount of ERC20 WPOA:

![](../../.gitbook/assets/image%20%28171%29.png)

and unwrapping them into POA native tokens \(the last tiles in "Internal Transactions"\):

![](../../.gitbook/assets/image%20%2834%29.png)

## Bridge POA native tokens to the xDai chain

1. Visit the WPOA OmniBridge helper contract on [BlockScout](https://blockscout.com/poa/core): [`0xF6a1Ad94d29679388e533B63bfE1Fd6f1680D23B`](https://blockscout.com/poa/core/address/0xF6a1Ad94d29679388e533B63bfE1Fd6f1680D23B)

2. Go to [the Write Contract tab](https://blockscout.com/poa/core/address/0xF6a1Ad94d29679388e533B63bfE1Fd6f1680D23B/write-contract):

![](../../.gitbook/assets/image%20%2830%29.png)

3. Scroll to the `wrapAndRelayTokens` method and enter the amount of POA native tokens to bridge to the xDai chain:

![](../../.gitbook/assets/image%20%2821%29.png)

Press **Write** to send the transaction.

4. As soon as the transaction is included in the block, click on the transaction link to get the transaction details. Use "**View in ALM App**" link on the page with transaction details to track status of the transfer.

