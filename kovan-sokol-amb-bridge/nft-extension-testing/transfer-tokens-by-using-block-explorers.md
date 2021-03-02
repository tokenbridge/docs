---
description: >-
  Step by step instructions how to transfer tokens using features provided by
  Etherscan and BlockScout
---

# Transfer tokens by using block explorers

The instructions below use the Etherscan UI and the Blockscout UI to demonstrate the token transfer process. 

## Kovan -&gt; Sokol

The process to transfer a non-fungible token from the Kovan testnet to the Sokol testnet consists of two steps:

1. Approve the NFT OmniBridge mediator contract on the Kovan side to operate with a non-fungible token.
2. Initiate a request to transfer the token through the bridge on the OmniBridge mediator contract located on Kovan.

{% hint style="warning" %}
Make sure that the token contract is verified in Etherscan. Token contracts deployed as part of the NFT OmniBridge mediator operations are not verified automatically, so if the token does not allow read and write in the block explorer, follow the steps to verify the contract before starting.
{% endhint %}

#### Step 1: Approve the mediator contract to transfer tokens

The NFT OmniBridge mediator contract uses `transferFrom` functionality of the ERC721 token contract to pick the token from the owner; it must be explicitly approved to perform this operation.

Go to the token contract page in Etherscan and click on the "Write Contract"/"Write as Proxy" tab

![](../../.gitbook/assets/image%20%28135%29.png)

Go to the `approve` method and enter the following:

* to \(address\) field:  the mediator contract address on the Kovan chain \(`0x63be59CF177cA9bb317DE8C4aa965Ddda93CB9d7`\) 
* tokenId \(uint256\):  the id of the token to transfer

![](../../.gitbook/assets/image%20%28138%29.png)

Press the "Write" button to send the transaction.

#### Step 2: Initiate the transfer request

Open the mediator contract \([`0x63be59CF177cA9bb317DE8C4aa965Ddda93CB9d7`](https://kovan.etherscan.io/address/0x63be59CF177cA9bb317DE8C4aa965Ddda93CB9d7#writeProxyContract)\)  in Etherscan and go to the "Write as Proxy" tab.

![](../../.gitbook/assets/image%20%28141%29.png)

Scroll to the `relayToken` method. Enter the following:

* token \(address\) field: the ERC721 token contract address the NFT is belongs to.
* tokenId \(uint256\) field: the id of the token to transfer

![](../../.gitbook/assets/image%20%28133%29.png)

Press Write to send the transaction.

The Arbitrary Message Bridge oracles will send their confirmations to the Sokol chain. As soon as enough confirmations received, the transfer will be automatically executed.

You can monitor this process using [the AMB Live Monitoring tool](https://docs.tokenbridge.net/about-tokenbridge/components/amb-live-monitoring-application): [https://alm-test-amb.herokuapp.com/](https://alm-test-amb.herokuapp.com/).

Specify the hash \(tx id\) of the transaction used to call `relayToken` in the ALM entry page and it will check the status of the AMB request initiated by this transaction in real time:

![](../../.gitbook/assets/image%20%28132%29.png)

The link in "Executed by" section can be used to get more details about the terminating transaction: 

![](../../.gitbook/assets/image%20%28131%29.png)

The token can be observed by clicking on the Token Id in the "Token Transfer" tile:

![](../../.gitbook/assets/image%20%28137%29.png)

![](../../.gitbook/assets/image%20%28134%29.png)

## Sokol -&gt; Kovan

The procedure to transfer ERC721 tokens from Sokol to Kovan differs from the transferring NFTs from Kovan to Sokol. It consists of three steps:

1. Approve the NFT OmniBridge mediator contract to operate with a non-fungible token.
2. Initiate a request to transfer the token through the bridge on the OmniBridge mediator contract.
3. Finalze the request by collecting the oracles' confirmations and transferring the Arbitreary Message Bridge contract on the Kovan side.

{% hint style="warning" %}
Make sure that the token contract is verified in BlockScout. Token contracts deployed as part of the NFT OmniBridge mediator operations are not verified automatically, so if the token does not allow read and write in the block explorer, follow the steps to verify the contract before starting.
{% endhint %}

#### Step 1: Approve the mediator contract to transfer tokens

The NFT OmniBridge mediator contract uses `transferFrom` functionality of the ERC721 token contract to pick the token from the owner; it must be explicitly approved to perform this operation.

Go to the token contract page in BlockScout and click on the "Write Contract"/"Write as Proxy" tab and go to the `approve` method. Enter the following:

* to \(address\) field:  the mediator contract address on the Sokol chain \(`0x3ecEe2667f80fc0858437119621b820efc6b0Ede`\) 
* tokenId \(uint256\):  the id of the token to transfer

![](../../.gitbook/assets/image%20%28142%29.png)

Press the "Write" button to send the transaction.

#### Step 2: Initiate the transfer request

Open the mediator contract \([`0x3ecEe2667f80fc0858437119621b820efc6b0Ede`](https://blockscout.com/poa/sokol/address/0x3ecEe2667f80fc0858437119621b820efc6b0Ede/write-proxy)\)  in BlockScout and go to the "Write Proxy" tab.

![](../../.gitbook/assets/image%20%28139%29.png)

Scroll to the `relayToken` method. Enter the following:

* token \(address\) field: the ERC721 token contract address the NFT is belongs to.
* tokenId \(uint256\) field: the id of the token to transfer

![](../../.gitbook/assets/image%20%28136%29.png)

Press Write to send the transaction.

#### Step 3: Finalize the token transfer 

The Arbitrary Message Bridge oracles will use the Sokol chain to collect confirmations of the NFT token transfer. As soon as the confirmations collected, it is necessary to relay the confirmations to the Kovan testnet to finalize the token transfer.

You can monitor this process using [the AMB Live Monitoring tool](https://docs.tokenbridge.net/about-tokenbridge/components/amb-live-monitoring-application): [https://alm-test-amb.herokuapp.com/](https://alm-test-amb.herokuapp.com/).

Specify the hash \(tx id\) of the transaction used to call `relayToken` in the ALM entry page and it will check the status of the AMB request initiated by this transaction in real time:

![](../../.gitbook/assets/image%20%28130%29.png)

Change the chain in MetaMask/NiftyWallet to the Kovan chain and press Execute to send transaction to the Arbitrary Message Bridge contract with collected confirmations of the AMB oracles.

{% hint style="info" %}
An alternative way to manually deliver confirmations to the AMB contracts on the Kovan side is to [use the AMB Helper contract](https://docs.tokenbridge.net/kovan-sokol-amb-bridge/about-the-kovan-sokol-amb/submit-confirmations-manually).
{% endhint %}

As soon as the transaction is verified and included in a block, the token will be transferred to the account that called the \`relayTokens\` method of the NFT OmniBridge mediator.

![](../../.gitbook/assets/image%20%28140%29.png)



