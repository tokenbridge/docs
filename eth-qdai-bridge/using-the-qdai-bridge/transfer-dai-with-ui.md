---
description: Exchange tokens by using a UI based on BurnerWallet 2
---

# Transfer DAI with UI

{% hint style="info" %}
This manual assumes that [the MetaMask extension](https://metamask.io) is set up in the browser and initialized with an account funded with Dai and Ether in the Ethereum Mainnet. The qDai JSON RPC URL is added to the network list supported by the MetaMask.
{% endhint %}

Go to the UI app by the following URL: [https://qdai-app.herokuapp.com/](https://qdai-app.herokuapp.com). It may take some time to load. If an error appears, reload the page. A page similar to this will appear.

![The main window of the UI based on the BurnerWallet2](<../../.gitbook/assets/image (34).png>)

Press the "Exchange" button.

![The exchange page](<../../.gitbook/assets/image (35).png>)

## Exchanging DAI to qDai

{% hint style="warning" %}
Use the Main Ethereum Network in Metamask. You will sign 2 transactions, the first to approve the transfer and the second to transfer the tokens.
{% endhint %}

1\. Choose Dai in the "From" dropdown list:

![The "From" field specifies the token that will be exchanged](<../../.gitbook/assets/image (36).png>)

2\. Enter some amount of tokes to exchange in the left field and press the "Exchange" button on the bottom of the app.

![The left field specifies amount of tokens to be exchanged ](<../../.gitbook/assets/image (37).png>)

3\.  A MetaMask window to sign a transaction that approves the token transfer will pop up. Press the "Confirm" button.&#x20;

![The MetaMask window to approve the token transfer](<../../.gitbook/assets/image (38).png>)

{% hint style="warning" %}
Adjustments to the gas price may be required. Press the "Edit" button to adjust.
{% endhint %}

4\. Once this transaction is verified and included in a block, another MetaMask window will appear to confirm the second transaction. This transaction  transfers tokens to the mediator account and sends the relay request through the Arbitrary Message Bridge. Press the "Confirm" button.

![The MetaMask window to initiate the transfer through the bridge](<../../.gitbook/assets/image (39).png>)

{% hint style="warning" %}
Adjustments to the gas price may be required. Press the "Edit" button to adjust.
{% endhint %}

5\. Wait for the second transaction verification. After that the bridge validators will wait for chain finalization (usually 8 blocks) and confirm the relay request on the other side of the bridge. During transaction processing the wallet window will display the "Exchanging assets..." message.

![A message to wait during operations to sign transactions and during period of the chain finalization](<../../.gitbook/assets/image (40).png>)

6\. When complete, the  balance in both fields of the exchange form will update.

![New values of balances in the exchange form](<../../.gitbook/assets/image (41).png>)

7\. Close the exchange form with the X button in the top right corner, and the new balance of tokens will be displayed on the corresponding tiles. The "Recent activity" list is updated with deposit transactions: the receiver of the first transaction is the mediator contract on the Ethereum Mainnet side, the second transaction reflects minting new tokens for the recipient account in the qDai chain.

![Tiles with balances updated on the main wallet page after the token exchange.](<../../.gitbook/assets/image (42).png>)

## Exchanging qDai to DAI

{% hint style="info" %}
&#x20;We assume the wallet is open to the exchange page.
{% endhint %}

{% hint style="warning" %}
The qDai chain is chosen in the MetaMask
{% endhint %}

1\. Double check that  qDai native tokens are chosen in the "From" dropdown list:

![This state of elements means that qDai will be exchanged to Dai](<../../.gitbook/assets/image (43).png>)

2\. Enter an amount of native tokes to exchange in the left field. The message about bridge fees related to this transaction appears. The amount of tokens received after the exchange is displayed on the right side. Press the "Exchange" button on the bottom of the app.

![The exchange form displays estimated fees for bridge operations](<../../.gitbook/assets/image (44).png>)

3\. The MetaMask window to confirm the operation to bridge qDai token will appear. The qDai chain allows for transaction without gas fees so the gas price is 0 for transaction sent within this network. Press the "Confirm" button.

![Transaction to the qDai chain must be sent with 0 gas price](<../../.gitbook/assets/image (45).png>)

4\. The chain finalization period is very short on the qDai chain since it uses the Istanbul BFT consensus with instant finality. The waiting period is due to validator signatures pending on the Ethereum Mainnet side. As soon as this transaction is included in a block the wallet window is updated with the actual balance. Close the exchange page to return back to the main wallet window.&#x20;
