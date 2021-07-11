---
description: Getting information from the Foreign side by a contract call
---

# Information requests to the Foreign side

The recent version \(`6.0.0` and greater\) of the AMB contracts support a new functionality which allows to any contract deployed on the Home chain to request and receive information from the Foreign chain in asynchronous manner. For example, a contract on the Sokol chain can request some data from the Kovan chain through the Kovan-Sokol AMB bridge, or a contract from the xDai chain can request information from Rinkeby or BSC.

### What information can be requested?

Everything that can be returned by the following JSON RPC API calls can be requested from the Foreign chain:

* `eth_call`
* `eth_getStorageAt`
* `eth_getBalance`
* `eth_getTransactionReceipt`

### What is the process to get information?



1. A contract that requires to get the information invoke the following method of the AMB contract:

   ```text
    function requireToGetInformation(bytes32 _requestSelector, 
                                     bytes calldata _data) external returns (bytes32);
   ```

   where `_requestSelector` is one of the following identifiers:

   * `0x88b6c755140efe88bff94bfafa4a7fdffe226d27d92bd45385bb0cfa90986650` for `eth_call`
   * `0xed99ae50430a72b5fd8de83256893be815884aa6e59d3e25e754c5269620e964` for `eth_getBalance`
   * `0x771ca5f7250ac7deadb5ecd3a00e0d901edb92aff583f55c8db58ced9a140926` for `eth_getStorageAt`
   * `0x0f47e1863d0e05e42b4a2aeee1322f349562a50b6166c14622210ade49a0b274` for `eth_getTransactionReceipt`

   and `_data` is ABI encoded set of arguments for the corresponding call:

   * `eth_call`: `(address _to, bytes _calldata)`
   * `eth_getBalance`: `(address _account)`
   * `eth_getStorageAt`: `(address _contract, bytes32 _slot)`
   * `eth_getTransactionReceipt`: `(bytes32 _txhash)`

   The method `requireToGetInformation` returns a message id assigned by the AMB contract for this information request.

2. The AMB contract generates a message for the bridge oracles.
3. Based on the timestamp of the Home chain's block where the transaction with the information requests is included into, the oracles calculates a block number \(for `eth_call`, `eth_getBalance` and `eth_getStorageAt`\) to access the blockchain state.
4. The oracles call the target RPC API and receive the result of the API method execution.
5. The oracles sends a transaction to AMB contract with the `confirmInformation` invocation.

   ```text
    function confirmInformation(bytes32 _messageId, 
                                bool _status, 
                                bytes _result) external;
   ```

6. The AMB contract invokes `onInformationReceived` of the contract which originates the information request on the step 1.

   ```text
    function onInformationReceived(bytes32 messageId, 
                                   bool status, 
                                   bytes calldata result) external;
   ```

   where

   * `messageId` is the message id associated with the request which the information is received for
   * `status` is the status of the request execution
   * `result` is ABI-encoded response of the JSON RPC node on the information request.

### Where to use?

Currently the cross-chain information requests are available on the following bridges:

* [Kovan-Sokol AMB](https://docs.tokenbridge.net/kovan-sokol-amb-bridge/about-the-kovan-sokol-amb), requests from Sokol to Kovan
* [Rinkeby-xDai AMB](https://docs.tokenbridge.net/rinkeby-xdai-amb-bridge/about-the-rinkeby-xdai-amb), requests from xDai to Rinkeby
* [BSC-xDai AMB](https://docs.tokenbridge.net/bsc-xdai-amb/about-the-bsc-xdai-amb), requests from xDai to Binance Smart Chain
* [ETH-BSC AMB](https://docs.tokenbridge.net/eth-etc-amb-bridge/about-the-eth-etc-amb), requests from Binance Smart Chain to the Ethereum Mainnet

### Examples

There are few contracts deployed on the Sokol chain and interacting with the Kovan-Sokol AMB to demonstrate how the information can be received from the Kovan testnet by originating transactions from the Sokol chain.

{% tabs %}
{% tab title="eth\_call" %}
The contract [`0x119A4D67a918669482783a9AC4e382C208bcD892`](https://blockscout.com/poa/sokol/address/0x119A4D67a918669482783a9AC4e382C208bcD892/contracts) shows how to get the total supply of a token contract located on the Kovan chain.

1. Use the token contract address for the method `requestTotalSupply`
2. Discover the message id for the information request in the method `lastMessageId`
3. Wait for one minute \(depends of number of block the oracles wait for the chain finalization\)
4. Use the message id to check the status \(it must be `2`\) of the response by calling `status`
5. Use the message id to get the total supply of the token by calling `response`
{% endtab %}

{% tab title="eth\_getBalance" %}
The contract [`0x0543776EbD97D8f846d65c62AA052D41acF78ec6`](https://blockscout.com/poa/sokol/address/0x0543776EbD97D8f846d65c62AA052D41acF78ec6/contracts) shows how to get the balance of KETH for an account on the Kovan chain.

1. Use an account address for the method `requestBalance`
2. Discover the message id for the information request in the method `lastMessageId`
3. Wait for one minute \(depends of number of block the oracles wait for the chain finalization\)
4. Use the message id to check the status \(it must be `2`\) of the response by calling `status`
5. Use the message id to get the balance of the requested account by calling `response`
{% endtab %}

{% tab title="eth\_getStorageAt" %}
The contract [`0xEB0A870038560019310d869f4f8467b8b65A2eE4`](https://blockscout.com/poa/sokol/address/0xEB0A870038560019310d869f4f8467b8b65A2eE4/contracts) shows how to get a storage slot value associated with a contract on the Kovan chain.

1. Use a contract address and a slot index in the hexadecimal form for the method `requestEthGetStorageAt`
2. Discover the message id for the information request in the method `lastMessageId`
3. Wait for one minute \(depends of number of block the oracles wait for the chain finalization\)
4. Use the message id to check the status \(it must be `2`\) of the response by calling `status`
5. Use the message id to get the slot value by calling `response`
{% endtab %}

{% tab title="eth\_getTransactionReceipt" %}
The contract [`0x418FDA4cB55fde2cd2ceD855d16C4fCe6045F2B3`](https://blockscout.com/poa/sokol/address/0x418FDA4cB55fde2cd2ceD855d16C4fCe6045F2B3/contracts) shows how to get a receipt of a transaction from the Kovan chain.

The data structures that keep the transactions receipts can be described as follows:

```text
struct Log {
    address from;
    bytes32[] topics;
    bytes data;
}
    
struct Receipt {
    bytes32 txHash;
    uint256 blockNumber;
    bool status;
    Log[] logs;
}
```

1. Use a transaction hash for the method `requestEthGetTransactionReceipt`
2. Discover the message id for the information request in the method `lastMessageId`
3. Wait for one minute \(depends of number of block the oracles wait for the chain finalization\)
4. Use the message id to check the status \(it must be `2`\) of the response by calling `status`
5. Use the transaction hash to get the deserialized receipt by calling `getReceipt`
{% endtab %}
{% endtabs %}

