# View Kitties in BlockScout

## Display Kitties

1\) Go to BlockScout on Kovan and enter in the contract address:  
[https://blockscout.com/eth/kovan/address/0x13ac5c6338796a31a39e74d70b0153c1be5f53b4](https://blockscout.com/eth/kovan/address/0x13ac5c6338796a31a39e74d70b0153c1be5f53b4)

2\) To view all kitties and their owners, go to the [Inventory](https://blockscout.com/eth/kovan/tokens/0x13ac5c6338796a31a39e74d70b0153c1be5f53b4/inventory) section. You can access by clicking the shortened token hex next to **KittyCore**, then navigating to the Inventory tab.

![Click on 0x13ac to access the token attributes](../../.gitbook/assets/crytpo_kitties_1.png)

![Inventory Tab shows each unique kitties token including Token ID and Owner Address.](../../.gitbook/assets/inventory.png)

3\) Select the [Read Contract](https://blockscout.com/eth/kovan/tokens/0x13ac5c6338796a31a39e74d70b0153c1be5f53b4/read_contract)  section to call different methods. Call the `getKitty` method with the Token ID to get metadata for that kitty.

![Read Contract tab displays contract methods and allows for queries](../../.gitbook/assets/readcontract2.png)

![Enter the token ID in the getKitty method to display metadata](../../.gitbook/assets/getkitty2.png)

