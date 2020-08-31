---
description: Following a withdrawal from xDai to Dai
---

# Withdrawal Authorization Flow

1. User sends a transaction to the bridge contract on xDai to initiate a withdrawal.  
2. The `UserRequestForSignature` method is called. Example tx: [https://blockscout.com/poa/xdai/tx/0x8e23cf0ab01476c2df5b71a72603f2c229d3d9a63ad6ca71ce164798f3733826/internal\_transactions](https://blockscout.com/poa/xdai/tx/0x8e23cf0ab01476c2df5b71a72603f2c229d3d9a63ad6ca71ce164798f3733826/internal_transactions)
3. The request generates an event on the xDai side.
4. Bridge validator nodes catch this event and send confirmation \(signatures\) to the contract on the xDai side.
5. Once enough signatures are collected \(currently 3 of 4\), one of the bridge validators sends the signatures to Ethereum.
6. The bridge contract on Ethereum checks that the signatures are valid. If they are,  the requested Dai is unlocked for the user.  _Note: This final step can be delayed if Ethereum mainnet is congested._

To track the relay we locate the originating transaction, find the corresponding transactions from confirmed validators, then find the transaction with signatures on Ethereum. 

* Code that checks the signatures and unblocks funds on Ethereum \(starting from`executeSignatures`  \(line 752\)\) [https://etherscan.io/address/0x7e7669bdff02f2ee75b68b91fb81c2b38f9228c2\#code](https://etherscan.io/address/0x7e7669bdff02f2ee75b68b91fb81c2b38f9228c2#code)
* Example transaction that makes this call: [https://etherscan.io/tx/0x74efc3302beeaa14fda51e03cfedd03693961db41b1b9b6069c576431f844c91](https://etherscan.io/tx/0x74efc3302beeaa14fda51e03cfedd03693961db41b1b9b6069c576431f844c91)

