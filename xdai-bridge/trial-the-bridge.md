---
description: Technical information about a test erc20-to-native bridge instance
---

# Trial bridge

The bridge is functioning between Kovan and Sokol chains. The main purpose is for testing the xDai TokenBridge UI and differs from the production version of the bridge. Key differences:

* A generic ERC20 token is used on the Kovan chain rather than a clone of the original DAI token.
* Native tokens (SPOA) are minted on the Sokol side by the bridge directly without involving the `BlockReward` functionality.

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

To get ERC20 tokens for testing, first send SPOA native tokens first to the bridge contract. The corresponding amount of ERC20 tokens will be released in a few minutes on the other side of the bridge.
