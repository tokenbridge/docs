---
description: >-
  Instructions how to submit the oracles' confirmation to the Ethereum side
  manually
---

# Submit confirmations manually

Since the Arbitrary Message Bridge between the Ethereum Mainnet and the xDai chain was switched to [the require-and-claim scheme to transfer data from the xDai chain](https://forum.poa.network/t/request-and-claim-to-transfer-assets-from-xdai-chain/4495), some users and application will find useful to use a manual process to gather the oracles confirmations and send them to the AMB contracts on the Mainnet side.

{% hint style="info" %}
This approach is an equivalent of set of actions performing by [the OmniBridge UI](https://www.xdaichain.com/for-users/omnibridge) after pressing the "Claim" button or by the [AMB Live Monitoring app](https://alm-xdai.herokuapp.com/) after pressing the "Execute" button.
{% endhint %}

So, below is the list of actions that can be executed in the BlockScout and Etherscan, or, if you are familiar with the contract interaction through Web3 provider, it can be done by importing contract's ABI to your application.

1. Take the transaction initiated the message passing through the AMB bridge and discover the logs generated during the transaction execution. The `encodedData` argument emitted with the `UserRequestForSignature` event is exactly what will be used on further steps.

![](../../.gitbook/assets/image%20%28102%29.png)

2. Go to [the AMB helper contract](https://blockscout.com/poa/xdai/address/0x7d94ece17e81355326e3359115D4B02411825EdD/read-contract) and call `getSignatures` there with the encoded data from the `UserRequestForSignature` event. It will produce a blob with signatures.

![](../../.gitbook/assets/image%20%28100%29.png)

3. Pass the encoded data and the signatures to the Arbitrary Message Bridge contract \([`0x4C36d2919e407f0Cc2Ee3c993ccF8ac26d9CE64e`](https://etherscan.io/address/0x4C36d2919e407f0Cc2Ee3c993ccF8ac26d9CE64e#writeProxyContract)\) on the Ethereum Mainnet and press the "Write" button to send the transaction.

![](../../.gitbook/assets/image%20%2899%29.png)

{% hint style="warning" %}
The MetaMask will show high gas estimate for this transaction. In fact, in the most cases the final gas consumption will be lower. Please refer to [the OmniBridge UI FAQ](https://www.xdaichain.com/about-xdai/faqs/bridges-xdai-bridge-and-omnibridge#metamask-is-showing-very-high-fees-to-claim-a-transaction-on-ethereum-tokens-bridged-from-xdai-to-ethereum-is-this-estimate-accurate) to learn more.
{% endhint %}



