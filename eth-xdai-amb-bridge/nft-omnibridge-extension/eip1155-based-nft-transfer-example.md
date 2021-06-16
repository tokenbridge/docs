---
description: >-
  Use the NFT OmniBridge extension to transfer EIP1155 NFTs between xDai and
  Ethereum
---

# EIP1155-based NFT Transfer Example

The NFT extension is operational, and a UI to transfer ERC721 NFTs is currently in development. For now, users can access and write to contracts using BlockScout and Etherscan. In the following example, we will bridge an NFT from xDai to Ethereum and back using methods accessed through these block explorers.

{% hint style="warning" %}
The NFT Extension is in Beta and transfers are performed at your own risk. NFT transfers can be very expensive and are not reversible once you initiate a transfer. Keep this in mind when deciding whether or not to bridge NFTs between xDai and Ethereum.
{% endhint %}

## -&gt; xDai to Ethereum

NFTs can be minted on xDai very inexpensively. These NFTs can then be bridged to Ethereum using the NFT OmniBridge extension. The EIP1155 standard support batching transfer, so several tokens can be transferred in one bridge operation if these tokens are in the same contract.

The process consists of several steps.

1. Locate your NFT contract and tokenID\(s\).
2. Initiate a request to transfer.
3. Finalize the transfer request on Ethereum.

{% hint style="info" %}
Token contracts must be verified in BlockScout to access write operations. If your token contract is not yet verified, [follow these steps for BlockScout](https://docs.blockscout.com/for-users/smart-contract-interaction/verifying-a-smart-contract).
{% endhint %}

## 1\) Locate your NFT 

You will need the contract and token ID\(s\) for your EIP1155 NFT\(s\) to start. If you have trouble locating, you can enter your wallet address in the [BlockScout search bar](https://blockscout.com/poa/xdai) and unroll the tokens list in the Balance tile. Here you will see your EIP1155s. Find one which you need to bridge, note its **TokenID**:

![](../../.gitbook/assets/image%20%28162%29.png)

Click on a NFT to get eventually to the EIP1155 token contract page:

![](../../.gitbook/assets/image%20%28156%29.png)

On the token contract page go to the **Write Contract** / **Write Proxy** tab:

![](../../.gitbook/assets/image%20%28150%29.png)

## 2\) Initiate the Transfer

Depending on amount of tokens belonging to the same contract it is required to bridge two methods should be used:

### Transfer one token

1. Press the **Connect to MetaMask** button to connect the address that holds the NFT
2. In the `safeTransferFrom` method, add the following:
   1. from \(address\): the address that holds the NFT
   2. to \(address\): `0x2c0bF58cC87763783e35a625ff6a3e50d9E05337`

      _This is the xDai mediator contract._

   3. id \(uint256\): TokenID for your EIP1155
   4. value \(uint256\): amount of this TokenID entities it is required to bridge, in most cases - `1`
   5. data \(bytes\): `0x`
3. Click the **Write** button and confirm in MetaMask.

![](../../.gitbook/assets/image%20%28165%29.png)

### Transfer several tokens

1. Press the **Connect to MetaMask** button to connect the address that holds the NFT
2. In the `safeBatchTransferFrom` method, add the following:
   1. from \(address\): the address that holds the NFT
   2. to \(address\): `0x2c0bF58cC87763783e35a625ff6a3e50d9E05337`

      _This is the xDai mediator contract._

   3. ids \(uint256\[\]\): list of TokenIDs for your EIP1155 in square brackets delimited by commas
   4. values \(uint256\[\]\): amount of this TokenID entities it is required to bridge, in most cases - `1`, in square brackets delimited by commas, number of values must correspond to number of TokenIDs
   5. data \(bytes\): `0x`
3. Click the **Write** button and confirm in MetaMask.

![](../../.gitbook/assets/image%20%28159%29.png)

## 3\) Finalize the Transfer on Ethereum

The Arbitrary Message Bridge oracles will use the xDai chain to collect confirmations of the NFT token\(s\) transfer. As soon as the confirmations are collected, they will be relayed to Ethereum for finalization.

1\) Find and copy the transaction hash id of the previous transaction \(`safeTransferFrom` or `safeBatchTransferFrom`\). You can find this in your MetaMask wallet in the Activity section. Click on the Contract Interaction and the Details icon to copy the tx hash.

![](../../.gitbook/assets/image%20%28163%29.png)

2\) Go to the the ALM Monitoring tool here: [https://alm-xdai.herokuapp.com/](https://alm-xdai.herokuapp.com/) and paste in the tx hash.

![](../../.gitbook/assets/nftalm1.png)

You can follow the status on the monitor. Once 4 validators are successful you can execute the transaction.

![](../../.gitbook/assets/image%20%28152%29.png)

3\) Switch to **Ethereum Mainnet in MetaMask** and press the **Execute** button**.** Confirm the transaction in MetaMask**.**This will send the transaction to the Arbitrary Message Bridge contract with collected confirmations of the AMB oracles.

![](../../.gitbook/assets/image%20%28154%29.png)

{% hint style="info" %}
Gas fee estimates to transfer may be prohibitively expensive. Note:

* Fees will likely be significantly lower than the estimate.
* You can try return later when fees are lower and execute then. There is no time limit for the transfer. 
{% endhint %}

Once the transaction is verified and included in a block, the token will be transferred to the same account on Ethereum that called the `safeTransferFrom`/`safeBatchTransferFrom`method.

## -&gt; Ethereum to xDai

The following process is similar to the above using Etherscan rather than BlockScout to write transactions. You will not need to manually execute on the xDai side, it is automated when bridging NFTs from Ethereum to xDai.

## 1\) Locate your NFT 

Etherscan does not provide simple way to discover EIP1155 tokens owned by a particular account. So, you either need to know an address of the token contract initially deployed on the Mainnet or, in case of bridged tokens, could use the NFT OmniBridge to discover the address of the bridged token contract.

1. Open the **Read as Proxy** tab of the NFT OmniBridge contract: [https://etherscan.io/address/0x6C8d0AFDDBD29a0954feEB73904923fC8f73C480\#readProxyContract](https://etherscan.io/address/0x6C8d0AFDDBD29a0954feEB73904923fC8f73C480#readProxyContract). 
2. Having the address of the token contract on the xDai chain it is possible to call the method `bridgedTokenAddress` and enter the address of the token contract on the xDai chain there
3. Press the **Query** button
4. Press to the appeared address of the bridged token contract and go to the **Write Contract** / **Write as Proxy** tab in the **Contract** section.

![](../../.gitbook/assets/image%20%28151%29.png)

![](../../.gitbook/assets/image%20%28161%29.png)

![](../../.gitbook/assets/image%20%28167%29.png)

## 2\) Initiate the Transfer

Depending on amount of tokens belonging to the same contract it is required to bridge two methods should be used:

### Transfer one token

1. Press the **Connect to Web3** button to connect the address that holds the NFT
2. In the `safeTransferFrom` method, add the following:
   1. from \(address\): the address that holds the NFT
   2. to \(address\): `0x6C8d0AFDDBD29a0954feEB73904923fC8f73C480`

      _This is the Ethereum Mainnet mediator contract._

   3. id \(uint256\): TokenID for your EIP1155
   4. amount \(uint256\): amount of this TokenID entities it is required to bridge, in most cases - `1`
   5. data \(bytes\): `0x`
3. Click the **Write** button and confirm in MetaMask.

![](../../.gitbook/assets/image%20%28149%29.png)

### Transfer several tokens

1. Press the **Connect to Web3** button to connect the address that holds the NFT
2. In the `safeBatchTransferFrom` method, add the following:
   1. from \(address\): the address that holds the NFT
   2. to \(address\): `0x2c0bF58cC87763783e35a625ff6a3e50d9E05337`

      _This is the Ethereum Mainnet mediator contract._

   3. ids \(uint256\[\]\): list of TokenIDs for your EIP1155 in square brackets delimited by commas \(without spaces\)
   4. amounts \(uint256\[\]\): amount of this TokenID entities it is required to bridge, in most cases - `1`, in square brackets delimited by commas \(without spaces\), number of values must correspond to number of TokenIDs
   5. data \(bytes\): `0x`
3. Click the **Write** button and confirm in MetaMask.

![](../../.gitbook/assets/image%20%28164%29.png)

## 4\) Monitor progress and view in BlockScout when complete <a id="4-monitor-progress-and-view-in-blockscout-when-complete"></a>

The Arbitrary Message Bridge oracles will send confirmations to the xDai chain. As soon as enough confirmations received, the transfer is executed automatically \(does not need manual execution as opposed to xDai -&gt; Eth transfers\).

You can monitor this progress with the ALM tool at [https://alm-xdai.herokuapp.com/](https://alm-xdai.herokuapp.com/). Paste in the tx hash from the contract interaction in MetaMask to monitor.

![Copy and paste the hash into https://alm-xdai.herokuapp.com/](../../.gitbook/assets/image%20%28168%29.png)

Once the transaction is complete, click on the "Executed By" link in the [ALM](https://alm-xdai.herokuapp.com/) to view more information about the transfer in BlockScout.

![Click to view more info](../../.gitbook/assets/image%20%28160%29.png)

In BlockScout, click on the TokenID to see information more information on the token.

![](../../.gitbook/assets/image%20%28166%29.png)

