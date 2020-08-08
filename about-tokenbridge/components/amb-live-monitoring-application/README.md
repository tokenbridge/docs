---
description: Information about AMB Live Monitoring application
---

# AMB Live Monitoring application

The monitoring application shows confirmations and the transaction status for each [Arbitrary Message Bridge](https://docs.tokenbridge.net/amb-bridge/about-amb-bridge) validator, and can monitor transactions in both directions \(when initiating a transaction from the "Home" or Foreign" chain\). Usually, the Home chain \(a.k.a. the Home side of the bridge\) is a chain with fast and inexpensive operations, whereas the chain is slow transactions and high gas fees is the Foreign chain \(a.k.a. the Foreign side of the bridge\).

The main aim of the application is to track the status of requests the users are sending through AMB mediators and help to understand the reason why a particular request is not processed yet.

{% hint style="warning" %}
Transactions must use the Arbitrary Message Bridge contracts to be monitored. Transactions using a vanilla TokenBridge contracts \(e.g. POA-POA20 or Dai-xDai\) bridge are discoverable by the ALM app. 
{% endhint %}

![AMB Live Monitoring application](../../../.gitbook/assets/alm-monitor1.png)

## Existing ALM instances

Currently there are several ALM apps available dedicated for particular Arbitrary Message Bridges:

* [https://alm-xdai.herokuapp.com/](https://alm-xdai.herokuapp.com/) - for the AMB between the Ethereum Mainnet and the xDai chain
* [https://alm-rinkeby.herokuapp.com/](https://alm-rinkeby.herokuapp.com/) - for the AMB between the Rinkeby testnet and the xDai chain
* [https://alm-etc.herokuapp.com/](https://alm-etc.herokuapp.com/) - for the AMB between the Ethereum Mainnet and the Ethereum Classic
* [https://alm-test-amb.herokuapp.com/](https://alm-test-amb.herokuapp.com/) - for the AMB between the Kovan testnet and the Sokol testnet

