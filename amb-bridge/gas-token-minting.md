---
description: >-
  Gas tokens can be minted in foreign network as a possible compensation for
  bridging messages
---

# Gas token minting

## Abstract idea behind

Ethereum Mainnet gas policy and gas refund mechanism allow a possibility of gas tokenization. This idea is used in GasToken \([https://gastoken.io](https://gastoken.io)\) technology.

For now, there is no any fee managing logic inside AMB bridge, since no tokens are generally transferred as a part of message bridging. Thus, the AMB bridge by default works in subsidized mode.

The automatic gas token minting can be used as an alternative for fee collection. For every message pass request, when someone is calling `requireToPassMessage` on the Foreign AMB bridge contract, the configured amount of gas tokens will be generated and transferred to the configured receiver address.

## GST2 token

The Foreign AMB bridge uses GST2 ERC-20 token in the Ethereum Mainnet: [0x0000000000b3F879cb30FE243b4Dfee438691c04](https://etherscan.io/token/0x0000000000b3F879cb30FE243b4Dfee438691c04).  
This is a regular ERC-20 token, which creates stub contracts when minting gas tokens, and calls `selfdestruct` on them when burning tokens.

## Possible scenarios

There are four possible scenarios for an end-user or contract in interacting with a new version of Foreign AMB bridge. The difference between them is in the answers to the following questions:

* Who is responsible for minting GST tokens?
* Are GST tokens are going to be minted in the same or separate transaction?
* How much gas will a transaction eventually consume?

### Automatic minting on the bridge side

The simplest way is to fully rely on thhe bridge contract. This approach requires zero initial preparation before calling `requireToPassMessage` on the ForeignAMB bridge contract. After that, during a call to `requireToPassMessage`, the bridge will mint a configured amount of gas tokens and transfer them to the specified receiver.

This variant is also the cheapest one \(in terms of the total spent gas\) and should be generally preferred among the others.

### Using GST from the allowance

This case is applicable when your account, which directly interacts with the bridge, already have some gas tokens. If you don't want to spend additional gas for minting unnecessary gas tokens, you can allow bridge contract to spend gas tokens from your interactor address by calling `approve` method on GST2 contract.

The bridge will withdraw a configured amount of tokens from your account, instead of minting them. This approach results in the sufficient gas savings needed for an end call to the bridge contract, since the bridge won't spend any gas on minting tokens.

This approach is recommended for environments with tight gas limit restrictions and accounts with other external gas tokens source.

### Hybrid approach

Previously mentioned approaches can be used by the bridge simultaneously. The bridge will use both strategies when the provided allowance less than the target amount of gas tokens. The bridge will withdraw all approved tokens from sender account, then it will mint the remaining amount of gas tokens.

This way if an interaction is recommended when you need some kind of compromise between other strategies. The spent gas for such case will be also somewhere in the middle between the gas amount for full minting and full allowance approaches.

### Interaction through mediator contract

It is also possible, that the following situation exists: your account has some GST2 tokens on balance which you want to pay as a fee. Your account interacts with some third-party contract, which internally initiates a call to the bridge.

Although your initial transaction sender \(`tx.origin`\) had some active gas tokens balance. The final bridge caller \(`msg.sender`\) will be a mediator contract, which has empty gas tokens balance.

For such case, the recommendation is to include an additional logic into the mediator contract. As an example, it can look like this:

```text
function pass(bytes memory _data, uint256 _gas) external {
  transferFrom(tx.origin, address(this), 50);
  approve(address(bridge()), 50);
  bridge().requireToPassMessage(address(this), _data, _gas);
}
```

For such kind of mediator, you will first need to approve gas tokens to the mediator account, then call a correspondent method of mediator contract as usual. The mediator will withdraw tokens from your account and redirect them to the bridge address, which will finally result in spending gas tokens from your balance.

Other possibilities also exist. For example, instead of approving tokens to the mediator address, you can transfer them to the mediator account which supports such kind of interaction. In this case, the mediator will also play as a temporary owner of gas tokens, but in a slightly different manner.

This variant is recommended for complex scenarios when the initial owner of gas tokens interacts with the Foreign bridge through other third-party contracts.

