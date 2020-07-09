---
description: Exchange tokens by using a UI based on BurnerWallet 2
---

# Transfer DAI with UI

{% hint style="info" %}
This manual assumes that [the MetaMask extension](https://metamask.io/) is set up in the browser and initialized with the account that funded with Dai and Ether in the Ethereum Mainnet. The qDai JSON RPC URL is added to the network list supported by the MetaMask.
{% endhint %}

Go to the UI app by the following URL: [https://qdai-app.herokuapp.com/](https://qdai-app.herokuapp.com/). It could take some time for loading. If any error appears after that try to reload the page one more time. Eventually the page like this must appear:

![The main window of the UI based on the BurnerWallet2](../../../.gitbook/assets/image%20%2845%29.png)

Press "Exchange" button.

![The exchange page](../../../.gitbook/assets/image%20%2842%29.png)

## Exchanging DAI to qDai

{% hint style="warning" %}
The Ethereum Mainnet is chosen in the MetaMask
{% endhint %}

1. Choose Dai in the "From" dropdown list:

![The &quot;From&quot; field specifies the token that will be exchanged](../../../.gitbook/assets/image%20%2848%29.png)

2. Enter some amount of tokes to exchange in the left field and press the "Exchange" button on the bottom of the app.

![The left field specifies amount of tokens to be exchanged ](../../../.gitbook/assets/image%20%2849%29.png)

3.  The MetaMask window for the first transaction to approve the token transfer will appear to be signed. Press the "Confirm" button. 

![The MetaMask window to approve the token transfer](../../../.gitbook/assets/image%20%2839%29.png)

{% hint style="warning" %}
The adjustments of the gas price could be required. Press the "Edit" button for this.
{% endhint %}

4. As soon as the first transaction is verified and included in a block, another MetaMask window will appear to confirm the second transaction signing. This transaction perform actual transfer of tokens to the mediator account and sends the relay request through the Arbitrary Message Bridge. Press the "Confirm" button.

![The MetaMask window to initiate the transfer through the bridge](../../../.gitbook/assets/image%20%2837%29.png)

{% hint style="warning" %}
The adjustments of the gas price could be required. Press the "Edit" button for this.
{% endhint %}

5. Wait for the second transaction verification. After that the bridge validators will wait for the chain finalization \(usually 8 blocks\) and confirm the relay request on another side of the bridge. During this period the wallet window will inform about "Exchanging assets...":

![A message to wait during operations to sign transactions and during period of the chain finalization](../../../.gitbook/assets/image%20%2846%29.png)

6. Finally the balance in both fields of the exchange form will be updated:

![New values of balances in the exchange form](../../../.gitbook/assets/image%20%2840%29.png)

7. If the exchange form is closed with the cross button in the top right corner, new balance of tokens will be displayed on the corresponding tiles. The "Recent activity" list is updated with deposit transactions: the receiver of the first transaction is the mediator contract on the Ethereum Mainnet side, the second transaction reflects minting new tokens for the recipient account in the qDai chain.

![Tiles with balances updated on the main wallet page after the token exchange.](../../../.gitbook/assets/image%20%2843%29.png)

## Exchanging qDai to DAI

{% hint style="info" %}
It is assumed that the wallet is opened on the exchange page.
{% endhint %}

{% hint style="warning" %}
The qDai chain is chosen in the MetaMask
{% endhint %}

1. Double check that the qDai native tokens are chosen in the "From" dropdown list:

![This state of elements means that qDai will be exchanged to Dai](../../../.gitbook/assets/image%20%2847%29.png)

2. Enter some amount of native tokes to exchange in the left field. The message about bridging fees taken for this transaction appears. The amount of tokens that will be received after exchange displayed on the right side. Press the "Exchange" button on the bottom of the app.

![The exchange form is able to display amount of fees for bridging operation](../../../.gitbook/assets/image%20%2841%29.png)

3. The MetaMask window to confirm the operation to bridge qDai token will appear. The qDai chain allows transaction without fees so the gas price is 0 for transaction sent within this network. Press the "Confirm" button.

![Transaction to the qDai chain must be sent with 0 gas price](../../../.gitbook/assets/image%20%2850%29.png)

4. The chain finalization period is very short on the qDai chain since it uses the Istanbul BFT consensus with instant finality. The main period to wait for finish the bridging operation is the time the transaction with the validators signatures will be in pending state on the Ethereum Mainnet side. As soon as this transaction is included in a block the wallet window will be update with the actual balance. Close the exchange page to return back to the main wallet window. 

