---
description: >-
  Step by step instructions how to transfer tokens by using features provided by
  Etherscan and BlockScout
---

# How to transfer tokens

The instructions below will use the Etherscan UI and the Blockscout UI to demonstrate the process of the tokens transfer. For sure, some applications would like to introduce a more convenient UI. So, in this case the application will need to call the methods of the multi-token mediators contracts described in this manual.

## General case

The general case consider a transfer of "pure" ERC20 token. For the tokens compatible with ERC677 and ERC827 token standards the steps could be simplified - see the separate section below.

### Ethereum Mainnet -&gt; xDai chain

The steps below assume that the account performing the actions owns some amount of an ERC20 tokens on the Ethereum Mainnet. Also, the account must be funded with some ether to cover gas fees.

Also, the MetaMask/NiftyWallet must be unlocked and rights to access the account must be granted for Etherscan.

For the demonstration purposes the Sai token is chosen to be transferred:

![](../../.gitbook/assets/image%20%2880%29.png)

#### Step 1: approve the mediator contract to transfer tokens

The mediator contract will use `transferFrom` functionality of the ERC20 token contract to lock the tokens, that's why it must be explicitly approved to perform this operation.

![](../../.gitbook/assets/image%20%2870%29.png)

First of all, it is required to connect the Web3 provider \(MetaMask/NiftyWallet\). Then, the mediator contract address on the Ethereum Mainnet \(`0x88ad09518695c6c3712AC10a214bE5109a655671`\) and the amount of tokens that is going to be transferred must be entered in the text field belonging to the `approve` method.

![](../../.gitbook/assets/image%20%2865%29.png)

The button "Write" must be pressed after that to send the transaction.

![](../../.gitbook/assets/image%20%2864%29.png)

The window of the MetaMask/NiftyWallet will appear. The gas price could be adjusted there in order to speed up the transaction verification. As soon as the transaction is confirmed in the MetaMask/NiftyWallet, it is necessary to wait for the verification by the block miners. Depending on the gas price specified and traffic congestions it could take from several seconds till several minutes.

#### Step 2: initiating the transfer request

Before the next action, the token contract address needs to be copied.

![](../../.gitbook/assets/image%20%2882%29.png)

Then the mediator contract \([`0x88ad09518695c6c3712AC10a214bE5109a655671`](https://etherscan.io/address/0x88ad09518695c6c3712AC10a214bE5109a655671)\) should be opened in Etherscan.

![](../../.gitbook/assets/image%20%2861%29.png)

The mediator contract is a proxy contract, so in order to call a method of the implementation contract the "Write as proxy" tab must be used.

![](../../.gitbook/assets/image%20%2858%29.png)

Since it is a new contract opened in Etherscan, it is required to connect the Web3 provider \(MetaMask/NiftyWallet\) again. Then, the token contract address and the amount of tokens that is going to be transferred must be entered in the text field belonging to the `relayTokens` method.

![](../../.gitbook/assets/image%20%2879%29.png)

The button "Write" must be pressed after that to send the transaction.

![](../../.gitbook/assets/image%20%2871%29.png)

The window of the MetaMask/NiftyWallet will appear. The gas price could be adjusted there in order to speed up the transaction verification. As soon as the transaction is confirmed in the MetaMask/NiftyWallet, it is necessary to wait for the verification by the block miners. Depending on the gas price specified and traffic congestions it could take from several seconds till several minutes.

When the transaction is included in a block, the Arbitrary Message Bridge validators will wait for 8 blocks. After that, they will send confirmations to the xDai chain that the multi-token mediator contract must be invoked to complete the transfer of the tokens.

It is possible to monitor the process of the confirmation sending and the the AMB request execution by [the AMB Live Monitoring tool](https://docs.tokenbridge.net/about-tokenbridge/components/amb-live-monitoring-application): [https://alm-xdai.herokuapp.com/](https://alm-xdai.herokuapp.com/). The hash \(tx id\) of the transaction used to call `relayTokens` should be specified in the ALM entry page and it will check the status of the AMB request initiated by this transaction in real time

![The ALM entry page with the transaction id specifed](../../.gitbook/assets/image%20%2875%29.png)

![The example of ALM response in case of successful execution of the AMB request](../../.gitbook/assets/image%20%2868%29.png)

If the AMB request is executed successfully the following will happen:

* If no transactions for this token contract to transfer assets through the AMB happened before, a new ERC677 token contract will be deployed in the xDai chain. The token contract will be initialized with the same symbol and decimals as for the original token in the Ethereum Mainnet. The name of the new token will be extended with the letters "on xDai" \(e.g. "Dai Stablecoin v1.0 on xDai"\). At the end, the requested amount of tokens will be minted and sent to the account that called `relayTokens`.
* If the ERC677 token has already been registered by the mediator for the original ERC20 token, obviously, deployment of the contract will be skipped but the requested amount of tokens will be minted and sent to the account that called `relayTokens`.

So, eventually it is possible to find the token contract on the xDai chain \(in the current example, Sai tokens has the symbol "DAI", that's why it is being used to discover the new token contract\)

![](../../.gitbook/assets/image%20%2881%29.png)

The link that is available on the token name will lead to the token view in the BlockScout:

![](../../.gitbook/assets/image%20%2866%29.png)

![](../../.gitbook/assets/image%20%2873%29.png)

The token view will allow to see that the amount of tokens transferred from the Ethereum Mainnet chain was minted successfully \(the sender is the address `0x0000000...000000`\). 

{% hint style="info" %}
This view also contains the information that this token was bridged and a link to the original token.
{% endhint %}

After that the token can be added to the MetaMask/NiftyWallet by the address. Thus, the usual operations to transfer tokens to another EOA or contracts are available.

### xDai chain -&gt; Ethereum Mainnet

The steps below assume that the account performing the actions must be funded with some xDai to cover gas fees.

Also, the MetaMask/NiftyWallet must be unlocked and rights to access the account must be granted for BlockScout.

{% hint style="warning" %}
Make sure that the token contract is verified in BlockScout. The token contracts deployed as part of the multi-token mediator operations are not verified automatically, so if the token does not allow read and write in the block explorer, the steps to verify the contract are required to be performed.
{% endhint %}

#### Step: transferAndCall invokation to transfer tokens

The token contract deployed by the mutli-token mediator supports ERC677 standard and that's why, instead of calling `approve` and `relayTokens`, one method `transferAndCall` can be used to transfer tokens to the mediator contract and notify it about this action at the same time.

The required method is available on the tab "Write Proxy" of the token contract in BlockScout:

![](../../.gitbook/assets/image%20%2872%29.png)

![](../../.gitbook/assets/image%20%2878%29.png)

The text fields should be filled with the multi-token mediator contract address on the xDai chain \(`0xf6A78083ca3e2a662D6dd1703c939c8aCE2e268d`\), amount of tokens to transfer and "0x" in the `_data` field. To send the transaction the button "Write" must be pressed.

![](../../.gitbook/assets/image%20%2860%29.png)

The window of the MetaMask/NiftyWallet will appear. The gas price should be 1 GWei. As soon as the transaction is confirmed in the MetaMask/NiftyWallet, it is necessary to wait for the verification by the xDai chain authorities. Usually, it takes few seconds.

When the transaction is included in a block, the Arbitrary Message Bridge validators will wait for one more block. After that, they will collect confirmations in the xDai chain and transfer them to the Ethereum Mainnet. The transaction sent by a validator to the Ethereum Mainnet will execute the request to unlock the tokens.

Here is also possible to monitor the process of the confirmation sending and the the AMB request execution by [the AMB Live Monitoring tool](https://docs.tokenbridge.net/about-tokenbridge/components/amb-live-monitoring-application): [https://alm-xdai.herokuapp.com/](https://alm-xdai.herokuapp.com/). The hash \(tx id\) of the transaction used to call `transferAndCall` should be specified in the ALM entry page and it will check the status of the AMB request initiated by this transaction in real time:

![](../../.gitbook/assets/image%20%2863%29.png)

As the result, the requested amount of tokens reduced by the fee amount will be unlocked on the Ethereum Mainnet.

## Simplification for ERC677/ERC827 tokens

If the token on the Ethereum Mainnet side is ERC677 or ERC827 compatible it is possible to omit the call of the `approve` method and call only the `transferAndCall` method in the token contract.

Below is example with the STAKE token contract:

![](../../.gitbook/assets/image%20%2874%29.png)

The mutli-token mediator contract address on the Ethereum Mainnet \(`0x88ad09518695c6c3712AC10a214bE5109a655671`\) must be specified as the recipient of the tokens, amount of tokens is filled in the "value" field, the field "data" contains "0x".

![](../../.gitbook/assets/image%20%2877%29.png)

## Simplification for the token on the xDai side

The token contact deployed on the xDai chain is a customized version of ERC677 standard. It contains [the changes](https://github.com/poanetwork/tokenbridge-contracts/blob/e09bd71bb67cf2ebce3cd7a4ec7130beea733018/contracts/ERC677BridgeToken.sol#L58-L62) that allows to use the `transfer` method to withdraw tokens from the xDai chain instead of `transferAndCall`. So, it is enough to specify the multi-token mediator contract address on the xDai chain \(`0xf6A78083ca3e2a662D6dd1703c939c8aCE2e268d`\) as the recipient and amount of tokens to initiate request to transfer tokens back to the Ethereum Mainnet.

