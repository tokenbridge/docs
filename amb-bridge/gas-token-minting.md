---
description: >-
  Gas tokens can be minted in the foreign network as possible compensation for
  bridging messages
---

# Gas Token Minting

## Conceptual Abstract 

Ethereum Mainnet gas policy and gas refund mechanisms allow the possibility of gas tokenization. GasToken \([https://gastoken.io](https://gastoken.io)\) technology leverages these mechanisms to enable gas savings.

At the moment there is no fee managing logic inside the AMB bridge; tokens are generally not transferred when using the message bridge. Thus, the AMB bridge works in subsidized mode by default.

Automatic gas token minting can be used as an alternative for fee collection. For every message pass request - when someone is calling `requireToPassMessage` on the Foreign AMB bridge contract - the configured amount of gas tokens is generated and transferred to the configured receiver address.

{% hint style="info" %}
Note: the process of minting gas tokens is an expensive operation in terms of gas usage, the exact transaction gas usage will depend on the configured minting parameter in the contract. 
{% endhint %}

## GST2 token

The Foreign AMB bridge uses the GST2 ERC-20 token on the Ethereum Mainnet: [0x0000000000b3F879cb30FE243b4Dfee438691c04](https://etherscan.io/token/0x0000000000b3F879cb30FE243b4Dfee438691c04).  
This is a regular ERC-20 token, which creates stub contracts when minting gas tokens, and calls `selfdestruct` on them when burning tokens.

## Possible scenarios

There are four possible scenarios for an end-user or contract when interacting with a new version of the Foreign AMB bridge. The best configuration approach can be guided by these questions: 

* Who is responsible for minting GST tokens?
* Are GST tokens going to be minted in the same or separate transaction?
* How much gas will a transaction eventually consume?

### 1\) Automatic minting on the bridge side

The simplest way is to fully rely on the bridge contract. This approach requires zero initial preparation before calling `requireToPassMessage` on the ForeignAMB bridge contract. After that, during a call to `requireToPassMessage`, the bridge will mint a configured amount of gas tokens and transfer them to the specified receiver.

This variant is the cheapest \(in terms of the total spent gas\) and generally the preferred method.

### 2\) Using GST from the allowance

This case applies when your account which directly interacts with the bridge already contains an amount of gas tokens. If you don't want to spend additional gas to mint unnecessary gas tokens, you can allow the bridge contract to spend gas tokens from your interactor address by calling the `approve` method on the GST2 contract.

First, if the current configured minting parameter is `X`, make sure that your account has at least `X` gas token on its balance, and the current allowance to the bridge account is at least `X` as well. During the call, the bridge will withdraw the configured amount of tokens from your account rather than minting them. This approach results in the gas savings needed for an end call to the bridge contract - the bridge does not spend any gas on minting tokens.

This approach is recommended for environments with tight gas limit restrictions and accounts with another external gas token source.

### 3\) Hybrid approach

Approaches 1 & 2  can be used by the bridge simultaneously. The bridge will use both strategies when the provided allowance is less than the target amount of gas tokens. First, the bridge will withdraw all approved tokens from the sender account, then it will mint the remaining amount of gas tokens. \(Note: make sure that your gas token allowance to the bridge contract does not exceed your real gas token balance\)

This interaction method is recommended when you need a compromise between other strategies. The spent gas for this case will fall in between the gas amount for full minting and full allowance approaches.

### 4\) Interaction through the mediator contract

It is also possible that the following situation exists: your account has some GST2 tokens on balance which you want to pay as a fee. Your account interacts with a third-party contract which internally initiates a call to the bridge.

Although your initial transaction sender \(`tx.origin`\) has an active gas tokens balance, the final bridge caller \(`msg.sender`\) is a mediator contract, which has a zero gas tokens balance.

In this case, the recommendation is to include additional logic into the mediator contract. For example:

```text
function pass(bytes memory _data, uint256 _gas) external {
  transferFrom(tx.origin, address(this), 50);
  approve(address(bridge()), 50);
  bridge().requireToPassMessage(address(this), _data, _gas);
}
```

For this type of mediator, you will first need to approve gas tokens to the mediator account, then call a corresponding method of the mediator contract as usual. The mediator will withdraw tokens from your account and redirect them to the bridge address, which will result in gas tokens spent from your balance.

This may also make sense in other circumstances. For example, instead of approving tokens to the mediator address, you can transfer them to the mediator account which supports this type of interaction. In this case, the mediator will also serve as a temporary owner of gas tokens in a slightly different manner.

This variant is recommended for complex scenarios when the initial gas tokens owner interacts with the Foreign bridge through other third-party contracts.

