---
description: >-
  Instructions how to submit the oracles' confirmation to the Kovan side
  manually
---

# Submit confirmations manually

It is required to submit the oracles' confirmations collected on the Sokol side to the AMB contract on the Kovan chain manually in several cases:

* The bridge oracles are configured to not transfer the messages confirmations. This is the default mode how the messages directed from Sokol to Kovan are being handled starting from the middle of November 2020. 
* The bridge oracles by some reason skipped their duty to transfer collected confirmations.

If it is discovered that the message was not passed to the Kovan chain \(e.g. in [AMB Live Monitoring app](https://alm-test-amb.herokuapp.com/)\) the following steps could be performed.

1. Take the transaction initiated the message passing through the AMB bridge and discover the logs generated during the transaction execution. The `encodedData` argument emitted with the `UserRequestForSignature` event is exactly what will be used on further steps.

![](../../.gitbook/assets/image%20%2897%29.png)

2. Go to [the AMB helper contract](https://blockscout.com/poa/sokol/address/0x40F0606f7dbA8BF0863773052DE49489F6ca6E19/read-contract) and call `getSignatures` there with the encoded data from the `UserRequestForSignature` event. It will produce a blob with signatures.

![](../../.gitbook/assets/image%20%2896%29.png)

3. Pass the encoded data and the signatures to the AMB Bridge contract \([0xfe446bef1dbf7afe24e81e05bc8b271c1ba9a560](https://kovan.etherscan.io/address/0xfe446bef1dbf7afe24e81e05bc8b271c1ba9a560#writeProxyContract)\) on the Kovan side and press the "Write" button to send the transaction.

![](../../.gitbook/assets/image%20%2898%29.png)

