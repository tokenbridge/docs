---
description: >-
  Instructions how to manually submit the oracles' confirmation to the POA
  Network side
---

# Submit confirmations manually

The Arbitrary Message Bridge between the POA Network and the xDai chain requires a request-and-claim scheme to transfer data from the xDai chain. This scheme requires at least two transactions to pass the message from the xDai chain: one transaction to initiate the message transfer and a second to forward collected oracles' confirmations for the message transfer request to the contracts on the POA Network.

Some users and applications may want to use a manual process to gather the oracles confirmations and send them to the AMB contracts on the POA Network side.

{% hint style="info" %}
This approach is the equivalent of the set of actions performing by the [AMB Live Monitoring app](https://alm-poa-xdai.herokuapp.com) after pressing the "Execute" button.
{% endhint %}

Below is the list of actions that can be executed in the BlockScout, or, if you are familiar with the contract interaction through a Web3 provider, it can be done by importing the contract's ABI to your application.

1\. Find a transaction in [the BlockScout application](https://blockscout.com/xdai/mainnet)  which initiated message passing through the AMB bridge and go to the logs generated during the transaction execution. The `encodedData` argument emitted with the `UserRequestForSignature` event will be used in the next steps.&#x20;

![](<../../.gitbook/assets/image (166).png>)

2\. Go to [the AMB helper contract](https://blockscout.com/xdai/mainnet/address/0x68C69307a0975D2636fA9772c7633204648788A8/read-contract) and call `getSignatures` there with the encoded data from the `UserRequestForSignature` event. It will produce a blob with signatures.

![](<../../.gitbook/assets/image (167).png>)

3\. Pass the encoded data and the signatures to the method `safeExecuteSignaturesWithAutoGasLimit` of the Arbitrary Message Bridge contract ([`0xB2218bdEbe8e90f80D04286772B0968ead666942`](https://blockscout.com/poa/core/address/0xB2218bdEbe8e90f80D04286772B0968ead666942/write-proxy)) on the POA Network and press the "Write" button to send the transaction.&#x20;

![](<../../.gitbook/assets/image (168).png>)

{% hint style="warning" %}
MetaMask will show a high gas estimate for this transaction. In most cases the final gas consumption will be significantly lower.
{% endhint %}
