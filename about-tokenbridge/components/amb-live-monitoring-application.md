---
description: Information about AMB Live Monitoring application
---

# AMB Live Monitoring application

An AMB Live Monitor is currently available for **xDai &lt;-&gt; Rinkeby** Monitoring and is located at [https://alm-rinkeby.herokuapp.com/](https://alm-rinkeby.herokuapp.com/)

The Monitor shows confirmations and tx status for each bridge validator, and can monitor transactions in both directions \(when initiating a transaction from the "Home" or Foreign" chain\). In the xDai &lt;-&gt; Rinkeby bridge, xDai is the Home network with fast and inexpensive operations, and Rinkeby is the Foreign network.

![AMB Live Monitor](../../.gitbook/assets/alm-monitor1.png)

## Foreign -&gt; Home \(Rinkeby -&gt; xDai\) State Transitions

Note that txs must use the Arbitrary Message Bridge to be monitored \(transactions using a different bridge mode, such as the current xDai &lt;-&gt; Dai bridge are not monitored\). 

Foreign -&gt; Home transactions may require two transactions. The first approves the mediator to transfer tokens, and the second to confirm the transaction. In this case the 2nd transaction should be entered into the interface.

### Example transaction hash

[0xf2fbc1b9caf77f7f66ee8ad58ef6b5f49819f2972d68b89d6c9b28eb3cd00ac6](https://rinkeby.etherscan.io/tx/0xf2fbc1b9caf77f7f66ee8ad58ef6b5f49819f2972d68b89d6c9b28eb3cd00ac6)

1\) After completing an AMB bridge transaction \([we transfer MOONs on Rinkeby to xMOONs on xDai using the moon-exchange UI](https://moon-exchange.herokuapp.com/)\), go to the MetaMask Activity tab and select the 2nd transaction \(Contract Interaction\). 

![](../../.gitbook/assets/mm-1.png)

2\) Select the transaction and copy the tx hash. This can be done at any time during or after a transaction.  Paste this hash into the ALM monitor to view tx status.

![](../../.gitbook/assets/mm-2.png)

### State Transition Messages

| Status | Message | Reason |
| :--- | :--- | :--- |
| Error | Transaction not found.  1. Check that the transaction hash is correct.  2. Wait several blocks for the transaction to be mined, gas price effects mining speed. | The transaction specified by the user not found. |
| Waiting | The specified transaction was included in a block. Validators are waiting for chain finalization before sending their confirmations. | The transaction specified by the user was included in a block but no transactions from any validator have been found yet. |
| Waiting | The specified transaction was included in a block. Some validators have sent confirmations, others are waiting for chain finalization. | The transaction specified by the user was included in a block but less than “requiredSignatures” of validators sent the transactions with confirmation. |
| Pending | The specified transaction was included in a block. A majority of validators sent confirmations which have not yet been added to a block. | ”requiredSignatures” or more validators sent confirmations but most of them have  not been mined yet. |
| Failed | The specified transaction was included in a block, but confirmations sent by a majority of validators failed. The cross-chain relay request will not be processed. | The number of failed confirmations does not allow the tx to reach the required number of the signatures. |
| Success | Success | Confirmations of ”requiredSignatures” or more validators were successfully included into blocks. |

### Screenshots

The ALM will auto-update as the transaction progresses through different states. 

#### Waiting for a transaction

![](../../.gitbook/assets/waiting-1.png)

#### Success

Click on an age metric to view the transaction details in Etherscan.

![](../../.gitbook/assets/success-1.png)

## Home -&gt; Foreign \(xDai -&gt; Rinkeby\) State Transitions

### Example transaction hash

[0x03c11c1b7510e4e07290634783e73914ffe6b7db60e36e0cb36011863ff66fda](https://blockscout.com/poa/xdai/tx/0x03c11c1b7510e4e07290634783e73914ffe6b7db60e36e0cb36011863ff66fda/token_transfers)

1\) After completing an AMB bridge transaction \([we transfer xMOONs on xDai to MOONs on Rinkeby using the moon-exchange UI](https://moon-exchange.herokuapp.com/)\), go to the MetaMask Activity tab and select the transaction \(Transfer & Call\).

![](../../.gitbook/assets/mm-10.png)

2\) Select the transaction and copy the tx hash. This can be done at any time during or after a transaction.  Paste this hash into the ALM monitor to view tx status.

![](../../.gitbook/assets/mm11.png)

### State Transition Messages

In Home -&gt; Foreign transactions there are waiting/pending states for confirmation as well as for execution.

| Status | Message | Reason |
| :--- | :--- | :--- |
| Error | Transaction not found.  1. Check that the transaction hash is correct.  2. Wait several blocks for the transaction to be mined, gas price effects mining speed. | The transaction specified by the user not found |
| Confirmation Waiting | The specified transaction was included in a block. Validators are waiting for chain finalization before sending their signatures. | The transaction specified by the user was included in a block but no transactions from any validator were found |
| Confirmation Waiting | The specified transaction was included in a block. Some validators have sent signatures, others are waiting for chain finalization. | The transaction specified by the user was included in a block but less than “requiredSignatures” of validators sent the transactions with confirmation |
| Confirmation Pending | The specified transaction was included in a block. A majority of validators sent signatures which have not yet been added to a block. | ”requiredSignatures” or more validators sent confirmations but most of them were not mined yet |
| Confirmation Failed | The specified transaction was included in a block, but transactions sent by a majority of validators failed. The cross-chain relay request will not be processed. | Confirmations of ”requiredSignatures” or more validators were successfully included into blocks |
| Execution Waiting | The specified transaction was included in a block and the validators collected signatures. Either  1. One of the validators is waiting for chain finalization.  2. A validator skipped its duty to relay signatures. Check status again after a few blocks. | Signatures were collected in the Home chain but the transaction from the validator to forward signatures was not yet found on the Foreign side. |
| Execution Pending | The specified transaction was included in a block and the validators collected signatures. The validator’s transaction with collected signatures was sent but is not yet added to a block. | The transaction from the validator to forward signatures was discovered in the transaction pool on the Foreign side but not mined yet. |
| Execution Failed | The specified transaction was included in a block and the validators collected signatures. The validator’s transaction with collected signatures was sent but did not succeed. | The transaction with collected signatures was included in the block on the Foreign side but its status is “failed”. |
| Success | Success | The transaction with the collected signatures was applied successfully to the Foreign chain. It does not matter if it is sent by a validator or by another account. |

###  Screenshots

The ALM will auto-update as the transaction progresses through different states. 

#### Waiting for Execution

![](../../.gitbook/assets/2020-08-03_13-06-02.png)

#### Success

Click on an age metric to view the transaction details in BlockScout.

![](../../.gitbook/assets/execution-success.png)





