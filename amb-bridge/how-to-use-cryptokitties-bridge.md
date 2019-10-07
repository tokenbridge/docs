# How to use Cryptokitties Bridge

The CryptoKitties bridge allows to transfer a NFT presenting a Kitty from one chain to another. It is used to demonstrate ability to perform operations with NFTs through Arbitrary Message Bridge \(AMB\) which is part of [the TokenBridge project](https://github.com/poanetwork/tokenbridge).

This demo assumes that the CryptoKitties contract similar to the original [CryptoKitties](https://github.com/cryptocopycats/awesome-cryptokitties/) is deployed on the Kovan testnet. The Sokol testnet contains a modified version of [CryptoKitties](https://github.com/cryptocopycats/awesome-cryptokitties/) - it allows to mint new Kitty with a specified metadata and only the mediator contract communicating with AMB is allowed to do so.

Contracts in Sokol testnet:

* [Mediator](https://blockscout.com/poa/sokol/address/0x5EeC77239398FE328791E28700CAFddB2990ea97)
* [SimpleBridgeKitty](https://blockscout.com/poa/sokol/address/0xc6a592ED792de33e6CBBF7ce04Dd9D3884B46B9A)

Contracts in Kovan testnet:

* [Mediator](https://blockscout.com/eth/kovan/address/0x7dB6493D9B6D99D9A240a6914AdAd5e0E8E8BE40)
* [KittyCore](https://blockscout.com/eth/kovan/tokens/0x13AC5C6338796a31A39e74D70B0153C1bE5f53B4)

Contracts sources: [https://github.com/poanetwork/cryptokitties-xdai-demo](https://github.com/poanetwork/cryptokitties-xdai-demo)

Deployed AMB bridges contracts can be found [here](https://forum.poa.network/t/using-arbitrary-message-bridging/2710/8).



#### Display Kitties

You can use Blockscout to display your kitties:

* In the [Inventory](https://blockscout.com/eth/kovan/tokens/0x13ac5c6338796a31a39e74d70b0153c1be5f53b4/inventory) section, all kitties and its owner are displayed

![](https://i.imgur.com/Bd6lwxQ.png)

* In the [Read Contract](https://blockscout.com/eth/kovan/tokens/0x13ac5c6338796a31a39e74d70b0153c1be5f53b4/read_contract) section, you can call the method `getKitty` with the Id of the Kitty to get the metadata

![](https://i.imgur.com/tbToaFL.png)

Below two approaches to transfer NFTs from the Kovan testnet to Sokol testnet \(and in opposite direction\) are considered:

* by using [MyEtherWallet](https://www.myetherwallet.com/) \(MEW\)
* by using [Nifty wallet chrome extension](https://chrome.google.com/webstore/detail/nifty-wallet/jbdaocneiiinmjbjlgalhcelgbejmnid)

#### Transfer CryptoKitties with MEW

**Transfer Kitty from Kovan to Sokol**

1. Login to [MyEtherWallet](https://www.myetherwallet.com/) and make sure that you are on the Kovan network.
2. Approve the token to be transferred by the bridge:

* Visit in another browser tab [the Kitties contract in Blockscout](https://blockscout.com/eth/kovan/address/0x13ac5c6338796a31a39e74d70b0153c1be5f53b4/contracts), go to the "Code" tile and copy ABI there.
* Add the contract to MEW by using the address `0x13ac5c6338796a31a39e74d70b0153c1be5f53b4` and copied ABI.

![](https://i.imgur.com/21XfFuD.png)

* Make a transaction to execute the `approve` method: on `_to` parameter paste the mediator contract address `0x7dB6493D9B6D99D9A240a6914AdAd5e0E8E8BE40`, in `_tokenId` parameter insert the Id of the token you want to transfer. Press `Write` and confirm the transaction confirmation.

![](https://i.imgur.com/bC4Yvoo.png)

* Press "Back" in the MEW interface.

   3. Initiate the token transfer:

* Visit in another browser tab [the Mediator contract in Blockscout](https://blockscout.com/eth/kovan/address/0x7db6493d9b6d99d9a240a6914adad5e0e8e8be40/read_contract), go to the "Read Contract" tile and click to the address in the `implementation` field:   

![](https://i.imgur.com/DuyKKde.png)

* Go to the "Code" tile of the implementation of the mediator contract and copy ABI there.
* Add the contract to MEW by using the address `0x7db6493d9b6d99d9a240a6914adad5e0e8e8be40` and copied ABI.

![](https://i.imgur.com/nZnGAm3.png)



* Make a transaction to execute the `transferToken` method: on `_from` parameter paste the address of your account that will receive the token on the other network, in `_tokenId` parameter insert the Id of the token you want to transfer. Press `Write` and confirm the transaction confirmation.

![](https://i.imgur.com/dMnwDXF.png)

As soon as the transaction confirmed the token will be locked in the Mediator contract in Kovan: 

![](https://i.imgur.com/gRwDC0O.png)

After waiting a couple of seconds to allow the AMB bridge perform their operations, check the [token contract on Sokol](https://blockscout.com/poa/sokol/tokens/0xc6a592ED792de33e6CBBF7ce04Dd9D3884B46B9A/inventory) and see that the token bridged is now Minted with the same Id: 

![](https://i.imgur.com/fgSUaYd.png)

and metadata

![](https://i.imgur.com/sVkIZSZ.png)

**Transfer Kitty from Sokol to Kovan**

No difference for the transferring a NFT in this direction except another contract addresses.

1. Make sure that you are on the Sokol network in MEW
2. Approve the token to be transferred by the bridge:
   * Visit [the Kitties contract in Blockscout](https://blockscout.com/poa/sokol/address/0xc6a592ED792de33e6CBBF7ce04Dd9D3884B46B9A/contracts), go to the "Code" tile and copy ABI there.
   * Add the contract to MEW by using the address `0xc6a592ED792de33e6CBBF7ce04Dd9D3884B46B9A` and copied ABI.
   * Make a transaction to execute the `approve` method: on `_to` parameter paste the mediator contract address `0x7dB6493D9B6D99D9A240a6914AdAd5e0E8E8BE40`, in `_tokenId` parameter insert the Id of the token you want to transfer. Press `Write` and confirm the transaction confirmation.
3. Initiate the token transfer:
   * Visit in another browser tab [the Mediator contract in Blockscout](https://blockscout.com/poa/sokol/address/0x5EeC77239398FE328791E28700CAFddB2990ea97/read_contract), go to the "Read Contract" tile and click to the address in the `implementation` field:
   * Go to the "Code" tile of the implementation of the mediator contract and copy ABI there.
   * Add the contract to MEW by using the address `0x5EeC77239398FE328791E28700CAFddB2990ea97` and copied ABI.
   * Make a transaction to execute the `transferToken` method: on `_from` parameter paste the address of your account that will receive the token on the other network, in `_tokenId` parameter insert the Id of the token you want to transfer. Press `Write` and confirm the transaction confirmation.

When the token is transferred in the opposite direction, it is burned in Sokol and unlocked on Kovan. After waiting a couple of seconds to allow the AMB bridge perform their operations, check the [token contract on Kovan](https://blockscout.com/eth/kovan/tokens/0x13AC5C6338796a31A39e74D70B0153C1bE5f53B4/inventory) and see that the token bridged is now owned by your account again with the same Id and metadata as before.

#### Transfer CryptoKitties with NiftyWallet

**Transfer Kitty from Kovan to Sokol**

1. First you need to log into your wallet through the [Nifty wallet chrome extension](https://chrome.google.com/webstore/detail/nifty-wallet/jbdaocneiiinmjbjlgalhcelgbejmnid)
2. Select Kovan Test Network
3. Add KittyCore contract:
   * Copy the contract address: `0x13AC5C6338796a31A39e74D70B0153C1bE5f53B4`
   * On Nifty Wallet click on `Import Account` menu
   * Select `Contract` as type and paste the address of the contract. The ABI will be fetched automatically from blockscout.

     ![](https://i.imgur.com/Mvl3TiQ.png)

   * Click on Import button.
   * It is useful to edit the name of the imported contract to for example `KittyCore`
4. Add Mediator contract:
   * Copy the contract address: `0x7dB6493D9B6D99D9A240a6914AdAd5e0E8E8BE40`
   * Enter `Import Account` section
   * Select `Proxy` as type and paste the address of the contract
   * After ABI is loaded, click on Import button.

Now that we have the token and mediator contracts available, to transfer a token to the other Network we need to perform 2 transactions. First call `approve` method of the token contract and then call `transferToken` of mediator contract.

To call `approve` we need to follow these steps:

1. Select KittyCore contract on Nifty Wallet                                  **** ![](https://i.imgur.com/vYlNJ96.png)
2. Click on `Execute Methods` button
3. Select `approve` method, on `_to` parameter paste mediator contract address `0x7dB6493D9B6D99D9A240a6914AdAd5e0E8E8BE40`, in `_tokenId` parameter insert the Id of the token you want to transfer 

   ![](https://i.imgur.com/uWHauR5.png)

4. Click next
5. Select the account that will send the transaction
6. Submit the transaction and wait until it is mined.

Now let's call `transferToken` to make the transfer and bridge the token.

1. Select Mediator contract on Nifty Wallet
2. Click on Execute Methods button
3. Select `transferToken` method, on `_from` parameter paste the address of your account that will receive the token on the other network, in `_tokenId` parameter insert the Id of the token you want to transfer. 

   ![](https://i.imgur.com/8YnckjR.png)

4. Click next
5. Select the account that will send the transaction
6. Submit the transaction and wait until it is mined.

Now the token is locked in the Mediator contract in Kovan and after waiting a couple of seconds to allow the AMB bridge perform their operations we can check the [token contract on Sokol](https://blockscout.com/poa/sokol/tokens/0xc6a592ED792de33e6CBBF7ce04Dd9D3884B46B9A/inventory) and see that the token bridged is now Minted with the same Id and metadata 

![](https://i.imgur.com/wYw1pPT.png)

 

![](https://i.imgur.com/hGP7ZNT.png)

**Transfer Kitty from Sokol to Kovan**

To transfer the Kitty from Sokol back to Kovan, the procedure is pretty similar.

1. Select Sokol Test Network on Nifty Wallet
2. Add SimpleBridgeKitty contract: 

* Copy the contract address: `0xc6a592ED792de33e6CBBF7ce04Dd9D3884B46B9A`
* On Nifty Wallet click on `Import Account` menu
* Select `Contract` as type and paste the address of the contract. The ABI will be fetched automatically from blockscout.
* Click on Import button.
* It is useful to edit the name of the imported contract to for example `SimpleBridgeKitty`

     3. Add Mediator contract:

* Copy the contract address: `0x5EeC77239398FE328791E28700CAFddB2990ea97`
* Enter `Import Account` section
* Select `Proxy` as type and paste the address of the contract
* After ABI is loaded, click on Import button.

Again, two transactions are needed to bridge the token back to Kovan

      4.  Follow the explained steps to call `approve` method of the token contract. On `_to` parameter paste  mediator contract address `0x5EeC77239398FE328791E28700CAFddB2990ea97`, in `_tokenId` parameter insert the Id of the token you want to transfer

      5. Follow the explained steps to call `transferToken` of mediator contract. On `_from` parameter paste the address of your account that will receive the token on the other network, in `_tokenId` parameter insert the Id of the token you want to transfer.

In this case the token is burned in Sokol and after waiting a couple of seconds to allow the AMB bridge perform their operations we can check the [token contract on Kovan](https://blockscout.com/eth/kovan/tokens/0x13AC5C6338796a31A39e74D70B0153C1bE5f53B4/inventory) and see that the token bridged is now owned by your account again with the same Id and metadata as before.



