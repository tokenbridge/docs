---
description: Instructions on relaying MOON tokens through the MOON AMB bridge extension
---

# Transfer Moons between Rinkeby and xDai Chain using the MOON bridge extension

{% hint style="warning" %}
The instructions below use MyEtherWallet to transfer tokens. This method is not very intuitive. We expect a DApp \(e.g. Burner Wallet 2\) will adopt these instructions to provide a better user experience.
{% endhint %}

We use [MyEtherWallet \(MEW\)](https://www.myetherwallet.com/access-my-wallet)  to transfer MOON tokens through the bridge extension. MEW may be used for both types of operations: to deposit tokens to the xDai chain and to withdraw tokens from the xDai chain.

{% hint style="info" %}
You will need a small amount of Rinkeby Testnet ether for gas fees and an amount of Moons to transfer for this tutorial.
{% endhint %}

## Deposit MOON tokens to the xDai chain

1. Activate and open a web3 wallet \(like MetaMask or Nifty Wallet\) and select the Rinkeby Testnet. Go to [MyEtherWallet \(MEW\)](https://www.myetherwallet.com/access-my-wallet) and select the option to **login with MewCX \(MetaMask or other web3 wallet\)**. Use a wallet that contains some amount of Moon tokens. Next:

* 1\) Select the **Interact with Contract** item from the sidebar menu
* 2\) Initialize the MOON token contract interface by entering the Moon token contract address in the **Contract Address** field: `0xdf82c9014f127243ce1305dfe54151647d74b27a` 
* 3\) Add the following JSON in the **`ABI/JSON Interface`** field: 

```javascript
[{"constant":false,"inputs":[{"name":"spender","type":"address"},
{"name":"value","type":"uint256"}],"name":"approve",
"outputs":[{"name":"","type":"bool"}],"payable":false,
"stateMutability":"nonpayable","type":"function"}]
```

* 4\) Click **Continue.**

![Interact with a contract using MEW](../../.gitbook/assets/mew1%20%281%29.png)

2. Approve the mediator contract to perform operations with tokens:

* 1\) Select `approve` from the **Select an Item** dropdown
* 2\) Enter the **Spender** address `0xFEaB457D95D9990b7eb6c943c839258245541754`. This is the mediator contract serving the bridge extension on the Rinkeby Testnet.
* 3\) Enter the **Value** - the amount of tokens \(in Wei\) you approve to transfer from this address. Leave Value in ETH field blank.
* 4\) Press **Write** to initiate the approval.

{% hint style="warning" %}
Note that minimum and maximum transaction amounts for deposit are embedded into the extension. 

* **Min** per transaction: **1 MOON** \(_the MOON's decimals is 0, 1 Moon = 1,000,000,000,000,000,000_\)
* **Max** per transaction: **100,000,000,000,000,000,000,000 \(100,000 MOON\)**
* Transaction limit **max per day**: **6,000,000,000,000,000,000,000,000 \(6M MOON\)**
{% endhint %}

3. Check that the Gas price - 1 Gwei is enough, then **Submit** the transaction using your web3 wallet \(like MetaMask or Nifty wallet\). Wait to proceed until it is included in the chain.

4. Press the **Back** button. You will now initialize the mediator contract interface from the Interact with Contract interface:

* 1\) Enter the mediator contract address: `0xFEaB457D95D9990b7eb6c943c839258245541754` 
* 2\) Enter the following JSON in the **`ABI/JSON Interface`** field:

```javascript
[{"constant":false,"inputs":[{"name":"_receiver","type":"address"},
{"name":"_value","type":"uint256"}],"name":"relayTokens","outputs":[],
"payable":false,"stateMutability":"nonpayable","type":"function"},
{"constant":false,"inputs":[{"name":"_from","type":"address"},
{"name":"_receiver","type":"address"},{"name":"_value",
"type":"uint256"}],"name":"relayTokens","outputs":[],"payable":false,
"stateMutability":"nonpayable","type":"function"}]
```

* 3\) Press **Continue**.

5\) Choose an appropriate `relayTokens` method. There are two possible methods:

1. `relayTokens(address _receiver, uint256 _amount)`- Used to transfer MOON tokens to a recipient in the xDai chain.
2. `relayTokens(address _from, address _receiver, uint256 _amount)` - Used in scenarios when the MOON tokens deposit is performed by another contract on behalf of a user account \(e.g. a wallet contract\).

* 1\) Select the **first** relayTokens method.
* 2\) `_receiver` - Enter the account that will receive the MOON tokens on the xDai chain. Typically we assume the same account that deposits the token also receives the token, so enter the address \(from your web3wallet & shown in MEW\) you are initiating the transfer from. However, you can enter another address if you prefer.
* 3\)`_amount` -- the amount of tokens \(in Wei\) to transfer; it must be less or equal to the amount of tokens approved for the bridge operations in step 2.3.
* 4\) Press **Write**.

7. Check the gas price, then Submit the transaction your web3 wallet and wait until it is included in the chain.

8. It will require the AMB bridge a short \(20-40 seconds\) amount of time to relay the deposit request to the xDai chain. After some time the balance of the account specified as `_receiver` in the `relayTokens` method call will increase. The result of the relay operation can be monitored in [Blockscout](https://blockscout.com/poa/xdai/tokens/0xC5C35D01B20f8d5cb65C60f02113EF6cd8e79910/token_transfers).

## Withdraw MOON tokens from the xDai chain

No special operations are required to transfer MOON tokens back to the Rinkeby Testnet. Just send MOON tokens in the xDai chain to the mediator `0x1E0507046130c31DEb20EC2f870ad070Ff266079`. They will be sent to the same wallet address. You will need a very small amount of xDai to process.

If you want to specify an alternative receiver of the tokens \(a different address\) in the Rinkeby Testnet, the  `relayTokens` method from the mediator contract can be used.

## Viewing your MOON Tokens

You will need to add the Moon contract addresses to your wallet to view, and be sure you are connected to the correct chain.  For instructions on adding custom tokens, [see the sUSD tutorial](../../eth-xdai-amb-bridge/susd-bridge-extension/transfer-susd-through-the-bridge-extension.md#view-balances). Add 18 decimals of precision to view accurate balance.

* Moon tokens on Rinkby [`0xDF82c9014F127243CE1305DFE54151647d74B27A`](https://rinkeby.etherscan.io/address/0xdf82c9014f127243ce1305dfe54151647d74b27a)\`\`
* xMoon tokens on xDai [`0xC5C35D01B20f8d5cb65C60f02113EF6cd8e79910`](https://blockscout.com/poa/xdai/address/0xC5C35D01B20f8d5cb65C60f02113EF6cd8e79910/transactions)



