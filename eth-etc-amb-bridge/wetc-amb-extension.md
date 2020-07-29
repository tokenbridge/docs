---
description: >-
  Description of the AMB bridge extension allowing for ETC native tokens
  exchange to Wrapped ETC ERC20 token
---

# WETC AMB extension

{% hint style="info" %}
The WETC extension was born after upgrade the old vanilla TokenBridge contracts \(WETC bridge\) to the AMB mediators.
{% endhint %}

The WETC bridge extension of the ETH-ETC Arbitrary Message Bridge allows a user to transfer ETC native tokens from the Ethereum Classic to the Ethereum Mainnet in form of ERC20 tokens. The transfer may happen both direction.

* Mediator contract at Ethereum Mainnet: [`0x0cB781EE62F815bdD9CD4c2210aE8600d43e7040`](https://etherscan.io/address/0x0cB781EE62F815bdD9CD4c2210aE8600d43e7040)
* Mediator contract at Ethereum Classic: [`0x073081832B4Ecdce79d4D6753565c85Ba4b3BeA9`](https://blockscout.com/etc/mainnet/address/0x073081832B4Ecdce79d4D6753565c85Ba4b3BeA9)
* Wrapped ETC tokens at Ethereum Classic: [`0x86aaBCc646f290b9Fc9Bd05CE17C3858d1511Da1`](https://etherscan.io/address/0x86aabcc646f290b9fc9bd05ce17c3858d1511da1) 

Anyone who owns ETCs on Ethereum Classic can use the bridge. ETCs are locked in the mediator contract and the same amount of [Wrapped ETC bridgeable tokens](https://etherscan.io/token/0x86aabcc646f290b9fc9bd05ce17c3858d1511da1) are minted on the Ethereum Mainnet side. The reverse operation burns WETC bridgeable tokens on the Ethereum Mainnet and unlocks ETC native tokens on the Ethereum Classic.

For the demonstration purposes, an application based on Burner Wallet 2 technology can be used as an UI to transfer tokens from one chain to another: [https://wetc-app.herokuapp.com/](https://wetc-app.herokuapp.com/).

![The main window of the WETC exchange app](../.gitbook/assets/image%20%2853%29.png)

![The exchange window of the WETC exchange app](../.gitbook/assets/image%20%2854%29.png)

