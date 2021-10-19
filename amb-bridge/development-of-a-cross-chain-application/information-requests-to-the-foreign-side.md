---
description: Getting information from the Foreign side with a contract call
---

# Information requests to the Foreign side

Recent versions (`6.0.0`+) of the AMB contracts allow any contract deployed on the Home chain to request and receive information from the Foreign chain asynchronously. For example, a contract on the Sokol chain can request data from the Kovan chain through the Kovan-Sokol AMB bridge, or a contract from the xDai chain can request information from Rinkeby or BSC.

### Information Types

Everything that can be returned by the following JSON RPC API calls can be requested from the Foreign chain:

* `eth_call`
* `eth_getStorageAt`
* `eth_getBalance`
* `eth_getBlockByNumber`
* `eth_getBlockByHash`
* `eth_getTransactionReceipt`
* `eth_getTransactionByHash`

### Process

1.  T contract that receives the information should invoke the following method of the AMB contract:

    ```
     function requireToGetInformation(bytes32 _requestSelector, 
                                      bytes calldata _data) external returns (bytes32);
    ```

    where `_requestSelector` is one of the following identifiers:

    * `0x88b6c755140efe88bff94bfafa4a7fdffe226d27d92bd45385bb0cfa90986650` for `eth_call`
    * `0xed99ae50430a72b5fd8de83256893be815884aa6e59d3e25e754c5269620e964` for `eth_getBalance`
    * `0x771ca5f7250ac7deadb5ecd3a00e0d901edb92aff583f55c8db58ced9a140926` for `eth_getStorageAt`
    * `0x21bed3a725245055f5aa932a62078981ec55f2464167839ea001f45c839c8808` for `eth_getBlockByNumber`
    * `0x31deda753ce7d0fdf0af4d4d03a69913616c4b1377be882d407fbed7cd5a7a98` for `eth_getBlockByHash`
    * `0x0f47e1863d0e05e42b4a2aeee1322f349562a50b6166c14622210ade49a0b274` for `eth_getTransactionReceipt`
    * `0x05c2b13240a3dff2b14abb3b793a0a5763a11c190af35bd2b5279c5bac8f2a94` for `eth_getTransactionByHash`

    and `_data` is an ABI encoded set of arguments for the corresponding call:

    * `eth_call`: `(address _to, bytes _calldata)`
    * `eth_getBalance`: `(address _account)`
    * `eth_getStorageAt`: `(address _contract, bytes32 _slot)`
    * `eth_getBlockByNumber`: `(uint256 _number)`
    * `eth_getBlockByHash`: `(bytes32 _hash)`
    * `eth_getTransactionReceipt`: `(bytes32 _txhash)`
    * `eth_getTransactionByHash`: `(bytes32 _txhash)`

    The method `requireToGetInformation` returns a message id assigned by the AMB contract for this information request.
2. The AMB contract generates a message for the bridge oracles.
3. Based on the timestamp of the Home chain's block with the transaction for the information request, the oracles calculates a block number (for `eth_call`, `eth_getBalance` and `eth_getStorageAt`) to access the blockchain state.
4. The oracles call the target RPC API and receive the result of the API method execution.
5.  The oracles sends a transaction to the AMB contract with the `confirmInformation` invocation.

    ```
     function confirmInformation(bytes32 _messageId, 
                                 bool _status, 
                                 bytes _result) external;
    ```
6.  The AMB contract invokes `onInformationReceived` of the contract which originates the information request from step 1.

    ```
     function onInformationReceived(bytes32 messageId, 
                                    bool status, 
                                    bytes calldata result) external;
    ```

    where

    * `messageId` is the message id associated with the request which the information is received for
    * `status` is the status of the request execution
    * `result` is ABI-encoded response of the JSON RPC node on the information request.

### Available Bridges

Currently the cross-chain information requests are available on the following bridges:

* xDai-ETH, requests from xDai to the Ethereum Mainnet (will be available after the current security audit)
* [Kovan-Sokol AMB](https://docs.tokenbridge.net/kovan-sokol-amb-bridge/about-the-kovan-sokol-amb), requests from Sokol to Kovan
* [Rinkeby-xDai AMB](https://docs.tokenbridge.net/rinkeby-xdai-amb-bridge/about-the-rinkeby-xdai-amb), requests from xDai to Rinkeby
* [BSC-xDai AMB](https://docs.tokenbridge.net/bsc-xdai-amb/about-the-bsc-xdai-amb), requests from xDai to Binance Smart Chain
* [ETH-BSC AMB](https://docs.tokenbridge.net/eth-etc-amb-bridge/about-the-eth-etc-amb), requests from Binance Smart Chain to the Ethereum Mainnet

### Examples

The following examples use contracts deployed on the Sokol chain. The Kovan-Sokol AMB is used to demonstrate how information can be received from Kovan with transactions initiated on Sokol.

{% tabs %}
{% tab title="eth_call" %}
The contract [`0x958671816193729054B7732c2741d93A2641138e`](https://blockscout.com/poa/sokol/address/0x958671816193729054B7732c2741d93A2641138e) shows how to get the total supply of a token contract located on the Kovan chain.

1. Use the token contract address for the method `requestTotalSupply`
2. Discover the message id for the information request in the method `lastMessageId`
3. Wait for one minute (depends of number of block the oracles wait for the chain finalization)
4. Use the message id to check the status (it must be `2`) of the response by calling `status`
5. Use the message id to get the total supply of the token by calling `response`
{% endtab %}

{% tab title="eth_getBalance" %}
The contract [`0x790C7BF6e3F74d64BE78278a26A701efE80109ee`](https://blockscout.com/poa/sokol/address/0x790C7BF6e3F74d64BE78278a26A701efE80109ee) shows how to get the balance of KETH for an account on the Kovan chain.

1. Use an account address for the method `requestBalance`
2. Discover the message id for the information request in the method `lastMessageId`
3. Wait for one minute (depends of number of block the oracles wait for the chain finalization)
4. Use the message id to check the status (it must be `2`) of the response by calling `status`
5. Use the message id to get the balance of the requested account by calling `response`
{% endtab %}

{% tab title="eth_getStorageAt" %}
The contract [`0x3b7e229686159a38956e7974F6603a2b23677097`](https://blockscout.com/poa/sokol/address/0x3b7e229686159a38956e7974F6603a2b23677097) shows how to get a storage slot value associated with a contract on the Kovan chain.

1. Use a contract address and a slot index in the hexadecimal form for the method `requestEthGetStorageAt`
2. Discover the message id for the information request in the method `lastMessageId`
3. Wait for one minute (depends of number of block the oracles wait for the chain finalization)
4. Use the message id to check the status (it must be `2`) of the response by calling `status`
5. Use the message id to get the slot value by calling `response`
{% endtab %}

{% tab title="eth_getBlockBy*" %}
The contract [`0xF606BA8bD4066d73a5F350adB8605F3CD02aFe55`](https://blockscout.com/poa/sokol/address/0xF606BA8bD4066d73a5F350adB8605F3CD02aFe55) shows how to get a block header from the Kovan chain.

The data structure that keeps a block header can be defined as follows:

```
struct Block {
    uint256 blockNumber;
    bytes32 blockHash;
    address miner;
    uint256 gasUsed;
    uint256 gasLimit;
    bytes32 parentHash;
    bytes32 receiptRoot;
    bytes32 stateRoot;
    bytes32 transactionRoot;
    uint256 timestamp;
    uint256 difficulty;
    uint256 totalDifficulty;
}
```

1. Use a block number or hash for the method `requestEthGetBlockByNumber` or `requestEthGetBlockByHash`.
2. Discover the message id for the information request in the method `lastMessageId`
3. Wait for one minute (depends of number of block the oracles wait for the chain finalization)
4. Use the message id to check the status (it must be `2`) of the response by calling `status`
5. Use the block number or hash to get the deserialized block header by calling `getBlockByNumber` or `getBlockByHash`
{% endtab %}

{% tab title="eth_getTransactionReceipt" %}
The contract [`0x90f2B33cBC8E8d29763997f780b7C2589D9e17d3`](https://blockscout.com/poa/sokol/address/0x90f2B33cBC8E8d29763997f780b7C2589D9e17d3) shows how to get a receipt of a transaction from the Kovan chain.

The data structures that keep the transactions receipts can be defined as follows:

```
struct Log {
    address from;
    bytes32[] topics;
    bytes data;
}
    
struct TransactionReceipt {
    bytes32 txHash;
    uint256 blockNumber;
    bytes32 blockHash;
    uint256 transactionIndex;
    address from;
    address to;
    uint256 gasUsed;
    bool status;
    Log[] logs;
}
```

1. Use a transaction hash for the method `requestEthGetTransactionReceipt`
2. Discover the message id for the information request in the method `lastMessageId`
3. Wait for one minute (depends of number of block the oracles wait for the chain finalization)
4. Use the message id to check the status (it must be `2`) of the response by calling `status`
5. Use the transaction hash to get the deserialized receipt by calling `getReceipt`
{% endtab %}

{% tab title="eth_getTransactionByHash" %}
The contract [`0x2D95548B66f5528383B0FC95a26311f92C4AcdcE`](https://blockscout.com/poa/sokol/address/0x2D95548B66f5528383B0FC95a26311f92C4AcdcE) shows how to get a transaction from the Kovan chain.

The data structure that keeps the transactions can be defined as follows:

```
struct Transaction {
    bytes32 txHash;
    uint256 blockNumber;
    bytes32 blockHash;
    uint256 transactionIndex;
    address from;
    address to;
    uint256 value;
    uint256 nonce;
    uint256 gas;
    uint256 gasPrice;
    bytes input;
}
```

1. Use a transaction hash for the method `requestEthGetTransactionByHash`
2. Discover the message id for the information request in the method `lastMessageId`
3. Wait for one minute (depends of number of block the oracles wait for the chain finalization)
4. Use the message id to check the status (it must be `2`) of the response by calling `status`
5. Use the transaction hash to get the deserialized receipt by calling `transactions`
{% endtab %}
{% endtabs %}
