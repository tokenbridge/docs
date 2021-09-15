---
description: Token transfer limits are the way to secure the bridge operations
---

# Transfer Limits

The transfer limits are applicable for those bridge modes where ERC20 or native tokens are involved in operations: `native-to-erc20`, `erc20-to-native` and `erc20-to-erc20`.

The intention to introduce transfer limits was to achieve the following aims:

* avoid drying out the validators accounts by relaying requests with low value
* secure the bridge for the case when the bridge contract on one side was compromised by rejecting transactions with very high value
* avoid malicious actions from the validators by rejecting their confirmations for requests with very high value

## Transfer limits for deposits

There are two cases how the limits are applied when tokens are deposited to another chain through the bridge.

**Actively controlled deposit**

This case is applicable for the `native-to-erc20` mode and for the mode `erc20-to-erc20` when tokens supporting ERC677 \(`transferAndCall`\) are used on both sides of the bridge.

![Actively controlled deposit for the native-to-erc20 bridge mode](../../.gitbook/assets/image%20%2817%29.png)

![Actively controlled deposit for the erc677-to-erc677 bridge mode](../../.gitbook/assets/image%20%288%29.png)

The first set of checks whether the value of the transaction is within the limits happens on step 1 for the`native-to-erc20` mode or on step 2 for the mode `erc20-to-erc20` after invocation of the`onTokenTransfer` method:

* the transferred value must be greater or equal than minimum allowable value per transaction
* the transferred value must be less or equal than maximum allowable value per transaction
* the accumulated value of all transfers sent in this day in this direction must be less or equal than maximum allowable accumulated values per day

The second set of checks occurs on step 3 for `native-to-erc20` and on step 4 for `erc20-to-erc20`:

* the value of the transfer confirmed by the validator must be less or equal than minimum allowable value per transaction
* the accumulated value of all confirmed transfers sent in this day in this direction must be less or equal than maximum allowable accumulated values per day

The checks on the Home side of the bridge are intended to limit bridge operations in case of malicious actions of validators.

Although so far the limits are not synchronized automatically on both side of the bridge, the bridge owners must make sure that maximum allowable deposit value per transaction must be the same on both sides of the bridge. Similar rule is for the maximum allowable accumulated deposits value per day.

**Passive perception of deposit**

The checks described here happen during tokens transfers in the `erc20-to-native` mode and in the mode `erc20-to-erc20` when generic ERC20 tokens are used on the Foreign side of the bridge.

![Passive perception of deposit for the erc20-to-native bridge mode](../../.gitbook/assets/image%20%2832%29.png)

Since the bridge contract on the Foreign side is not involved in the transfer operation no checks occur on this side. That's why in these bridge modes it is not possible to check minimal allowable value per transaction.

The checks are only applied on step 3:

* the value of the transfer confirmed by the validator must be less or equal than minimum allowable value per transaction
* the accumulated value of all confirmed transfers sent in this day in this direction must be less or equal than maximum allowable values per day

## Transfer limits for withdrawals

It is assumed that the tokens participating in withdrawals are controlled by the bridge \(or bridge owners\) that is why the transfer limits behave similarly in all bridge modes.

![Withdrawal for the erc20-to-native bridge mode](../../.gitbook/assets/image%20%2810%29.png)

![Withdrawal for the natvie-to-erc20 and erc20-to-erc20 bridge modes](../../.gitbook/assets/image%20%2827%29.png)

The first set of checks for detection whether the withdrawal is within the limits happens on step 1 for the `erc20-to-native` mode and on step 2 for the modes `native-to-erc20` and `erc20-to-erc20`. It makes sure that:

* the transferred value is greater or equal than minimum allowable value per transaction
* the transferred value is less or equal than maximum allowable value per transaction
* the accumulated value of all transfers sent in this day in this direction is less or equal than maximum allowable accumulated values per day

The checks are applied in the second time when one oracle sends all collected confirmations to the bridge contract on the Foreign side of the bridge \(on step 5 in the case of the `erc20-to-native` mode and on step 6 in other modes\):

* the value of the transfer confirmed by the validator must be less or equal than minimum allowable value per transaction
* the accumulated value of all confirmed transfers sent in this day in this direction must be less or equal than maximum allowable values per day

Again, the bridge owners are responsible for synchronization of the maximum allowable withdrawal per transaction value and the maximum allowable accumulated withdrawals per day value between two sides of the bridge.

