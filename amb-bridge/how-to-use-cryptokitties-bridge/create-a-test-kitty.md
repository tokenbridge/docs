# Create a Test Cat

{% hint style="warning" %}
 If you would like to try to the bridge feature **without creating your own test cat**, please contact us on [Discord](https://discord.gg/mPJ9zkq) or the [TokenBridge forum ](https://forum.poa.network/c/tokenbridge/)with your wallet address, and we will send you a test cat to play with 😻.  With a test cat, you can proceed from [NiftyWallet Transfer](niftywallet-transfer.md) or [MEW transfer](myetherwallet-mew-transfer.md) instructions.
{% endhint %}

## Test Cat Creation Instruction

If you deployed your own contracts and have access to the ownership address, you can also create a test cat using the **createPromoKitty** method in the **KittyCore** contract.

### Nifty Wallet

1\) Open the KittyCore contract from [step 3 in the NiftyWallet Transfer](niftywallet-transfer.md#3-add-kittycore-contract) instructions. Click on **Execute Methods**.

![Execute methods in the KittyCore contract](../../.gitbook/assets/2kitty1.png)

2\) Enter the following information and click **Next**:

* Select method: **createPromoKitty**
* \_genes: **uint256 integer**
* \_owner: **0x address of contract owner**. The `HOME_MEDIATOR_OWNER` parameter from the [Deploy CryptoKitty Contracts](deploy-cryptokitty-contracts.md) instruction.

![Enter method parameters and click Next](../../.gitbook/assets/2kitty2.png)

3\) Select the wallet account that will execute the transaction. **This must be sent with the same ownership account.** Click **Next.**

![Select the ownership account ](../../.gitbook/assets/2kitty3.png)

4\) Submit the transaction. ****It should process successfully. See the [View Cats in BlockScout page](view-in-blockscout.md) to see your newly created cat. 

\*\*\*\*





