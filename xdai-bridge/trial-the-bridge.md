---
description: Technical information about a test erc20-to-native bridge instance
---

# Trial the bridge

The bridge is functioning between Kovan and Sokol chains. The main purpose of it is to test the xDai TokenBridge UI that's why it does not repeat the production version of the bridge in the full manner. Here is a list of differences:

* A generic ERC20 token is used on the Kovan chain rather than a clone of the original DAI token.
* The native tokens \(SPOA\) are minted on the Sokol side by the bridge directly without involvement of the BlockReward functionality.

### Contracts information

{% tabs %}
{% tab title="Kovan" %}
* Bridge contract: [`0xEa7F8C8d2c55eE242f2F22c11F43421E459229b8`](https://kovan.etherscan.io/address/0xEa7F8C8d2c55eE242f2F22c11F43421E459229b8)
* ERC20 Token contract: [`0x40a81c34f36ebe2d98bac578d66d3ee952a48f24`](https://kovan.etherscan.io/address/0x40a81c34f36ebe2d98bac578d66d3ee952a48f24)
{% endtab %}

{% tab title="Sokol" %}
* Bridge contract: [`0xed47976103eBcCF7685e8aF185deD9EcF57E146A`](https://blockscout.com/poa/sokol/address/0xed47976103eBcCF7685e8aF185deD9EcF57E146A)
{% endtab %}
{% endtabs %}

### Getting tokens for testing

In order to get ERC20 tokens for testing, it is necessary to send SPOA native tokens first to the bridge contract. The corresponding amount of ERC20 tokens will be released in few minutes on another side of the bridge.

