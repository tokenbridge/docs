---
description: >-
  New cats can be created by the contract owner. Cats can be sent from one
  address to another with the transfer method.
---

# Create/Transfer a Test Cat

{% hint style="warning" %}
 If you would like to try to the bridge feature **without creating your own test cat**, please contact us on [Discord](https://discord.gg/mPJ9zkq) or the [TokenBridge forum ](https://forum.poa.network/c/tokenbridge/)with your wallet address, and we will send you a test cat to play with 😻.  With a test cat, you can proceed from [NiftyWallet Transfer](niftywallet-transfer.md) or [MEW transfer](myetherwallet-mew-transfer.md) instructions.
{% endhint %}

## Test Cat Creation Instruction

If you deployed your own contracts and have access to the ownership address, you can also create a test cat using the **createPromoKitty** method in the **KittyCore** contract.

## Nifty Wallet

1\) Open the KittyCore contract from [step 3 in the NiftyWallet Transfer](niftywallet-transfer.md#3-add-kittycore-contract) instructions. Click on **Execute Methods**.

![Execute methods in the KittyCore contract](../../.gitbook/assets/2kitty1.png)

2\) Enter the following information and click **Next**:

{% hint style="info" %}
The genes parameter is a secret CryptoKitty formula. To copy an existing cat, go to [https://etherscan.io/address/0x06012c8cf97bead5deae237070f9587f8e7a266d\#readContract](https://etherscan.io/address/0x06012c8cf97bead5deae237070f9587f8e7a266d#readContract), call `getKitty` with a random Id, copy the `genes`attribute, and paste into the \_genes field.
{% endhint %}

* Select method: **createPromoKitty**
* \_genes: **uint256 integer**
* \_owner: **0x address of contract owner**. The `HOME_MEDIATOR_OWNER` parameter from the [Deploy CryptoKitty Contracts](deploy-cryptokitty-contracts.md) instruction.

![Enter method parameters and click Next](../../.gitbook/assets/2kitty2.png)

3\) Select the wallet account that will execute the transaction. **This must be sent with the same ownership account.** Click **Next.**

![Select the ownership account ](../../.gitbook/assets/2kitty3.png)

4\) Submit the transaction. ****It should process successfully. See the [View Cats in BlockScout page](view-in-blockscout.md) to see your newly created cat. 

### **Transfer a Test Cat to Another Address \(Nifty\)**

You can transfer a cat to another address using the `transfer` method in the KittyCore contract.

1\) Go to the KittyCore contract and click **Execute methods**.

2\) Enter the following and click **Next**:

* method: **transfer**
* \_to: **0x address** where you are **sending** the cat
* \_tokenId: Make sure this is the **correct ID** of your cat. You can check your tokens with the [view cats in BlockScout](view-in-blockscout.md) instruction.

![](../../.gitbook/assets/3kitty.png)

3\) Select the wallet account to execute the transaction. **This must be the token holders account.**

![Execute using the token holders account](../../.gitbook/assets/2kitty3.png)

4\) After the transaction is submitted, check the account on BlockScout \(search by account and click the Tokens tab\) to make sure the cat has been successfully transferred.

### MyEtherWallet \(MEW\)

1\) Follow steps 1 & 2 in MyEtherWallet transfer to connect to the Kovan network with the contract owner address in MetaMask. Paste in the deployed KittyCore address and ABI from BlockScout.

2\) In the Read/Write Contract Interface:

{% hint style="info" %}
The genes parameter is a secret CryptoKitty formula. To copy an existing cat, go to [https://etherscan.io/address/0x06012c8cf97bead5deae237070f9587f8e7a266d\#readContract](https://etherscan.io/address/0x06012c8cf97bead5deae237070f9587f8e7a266d#readContract), call `getKitty` with a random Id, copy the `genes`attribute, and paste into the \_genes field.
{% endhint %}

* 1\) choose the `createPromoKitty` method from the **Select an Item** dropdown menu.
* 2\) ****\_genes: **uint256 integer**
* 3\) \_owner: Your 0x address from MetaMask. The `HOME_MEDIATOR_OWNER` parameter from the [Deploy CryptoKitty Contracts](deploy-cryptokitty-contracts.md) instruction.
* 4\) **Value in Eth:** Keep at 0
* 5\) Press `Write`

![Use createPromoKitty method to create a new cat](../../.gitbook/assets/mew1.png)

3\) Submit the transaction. ****On success, see the [View Cats in BlockScout page](view-in-blockscout.md) to see your newly created cat. 

### **Transfer a Test Cat to Another Address \(MEW\)**

You can transfer a cat to another address using the `transfer` method in the KittyCore contract.

1\) Follow steps 1 & 2 in MyEtherWallet transfer to connect to the Kovan network. You can connect with **any address that owns a test cat**.  Paste in the deployed KittyCore address and ABI from BlockScout.

2\) In the Read/Write Contract Interface enter the following:

* 1\) choose the `transfer` method from the **Select an Item** dropdown menu.
* 2\) ****\_to\(address\): any 0x address where you want to transfer the cat.
* 3\) \_tokenId: Make sure this is the **correct ID** of your cat. You can check your tokens with the [view cats in BlockScout](view-in-blockscout.md) instruction.
* 4\) **Value in Eth:** Keep at 0
* 5\) Press `Write`

![Transfer a cat to another address with the transfer method](../../.gitbook/assets/mew2.png)

4\) After the transaction is submitted, check the account on BlockScout \(search by account and click the Tokens tab\) to make sure the cat has been successfully transferred.

