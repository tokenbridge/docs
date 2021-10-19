# Table of contents

* [Welcome](README.md)

## About TokenBridge

* [Features, Definitions and Modes](about-tokenbridge/features/README.md)
  * [TokenBridge Roles](about-tokenbridge/features/tokenbridge-roles/README.md)
    * [Administrative Groups and Roles](about-tokenbridge/features/tokenbridge-roles/administrative-groups-and-roles.md)
    * [Validator Roles](about-tokenbridge/features/tokenbridge-roles/validator-roles.md)
    * [User Roles](about-tokenbridge/features/tokenbridge-roles/user-roles.md)
  * [Transfer Limits](about-tokenbridge/features/transfer-limits.md)
  * [Contracts verification in explorers](about-tokenbridge/features/contracts-verification-in-explorers.md)
* [Components](about-tokenbridge/components/README.md)
  * [Monitor](about-tokenbridge/components/monitor/README.md)
    * [Monitor deployment for existing bridges](about-tokenbridge/components/monitor/monitor-deployment-for-existing-bridges.md)
  * [AMB Live Monitoring application](about-tokenbridge/components/amb-live-monitoring-application/README.md)
    * [Local deployment](about-tokenbridge/components/amb-live-monitoring-application/local-deployment.md)
    * [ALM transition states](about-tokenbridge/components/amb-live-monitoring-application/alm-transition-states.md)
* [Use Cases](about-tokenbridge/use-cases/README.md)
  * [Mainnet Participation](about-tokenbridge/use-cases/mainnet-participation.md)
  * [Cross-Chain Project Highlights](about-tokenbridge/use-cases/cross-chain-project-highlights.md)
  * [Reduce Computation Costs](about-tokenbridge/use-cases/reduce-computation-costs.md)
* [Security Audits](about-tokenbridge/security-audits.md)
* [Roadmap](about-tokenbridge/roadmap.md)

## Arbitrary Message Bridge (AMB) <a href="amb-bridge" id="amb-bridge"></a>

* [About the AMB](amb-bridge/about-amb-bridge.md)
* [Arbitrary Message Bridge Deployment](amb-bridge/arbitrary-message-bridge-deployment/README.md)
  * [1) AMB contracts deployment](amb-bridge/arbitrary-message-bridge-deployment/1-amb-contracts-deployment.md)
  * [2) TokenBridge oracle instances](amb-bridge/arbitrary-message-bridge-deployment/2-tokenbridge-oracle-instance.md)
  * [Add-on: xDai and AMB bridge oracles on the same node](amb-bridge/arbitrary-message-bridge-deployment/add-on-xdai-and-amb-bridge-oracles-one-the-same-node.md)
* [Development of a cross-chain application](amb-bridge/development-of-a-cross-chain-application/README.md)
  * [Transacting via the bridge](amb-bridge/development-of-a-cross-chain-application/how-to-develop-xchain-apps-by-amb.md)
  * [Information requests to the Foreign side](amb-bridge/development-of-a-cross-chain-application/information-requests-to-the-foreign-side.md)
* [ERC677 to ERC677 AMB bridge extension](amb-bridge/erc677-to-erc677-bridge-on-top-of-amb.md)
* [😸 CryptoKitties AMB bridge extension Demo](amb-bridge/how-to-use-cryptokitties-bridge/README.md)
  * [Deploy CryptoKitty Contracts](amb-bridge/how-to-use-cryptokitties-bridge/deploy-cryptokitty-contracts.md)
  * [Verify Contracts in BlockScout](amb-bridge/how-to-use-cryptokitties-bridge/verify-contracts-in-blockscout.md)
  * [View Cats in BlockScout](amb-bridge/how-to-use-cryptokitties-bridge/view-in-blockscout.md)
  * [NiftyWallet Transfer](amb-bridge/how-to-use-cryptokitties-bridge/niftywallet-transfer.md)
  * [MyEtherWallet (MEW) Transfer](amb-bridge/how-to-use-cryptokitties-bridge/myetherwallet-mew-transfer.md)
  * [Create/Transfer a Test Cat](amb-bridge/how-to-use-cryptokitties-bridge/create-a-test-kitty.md)
* [Create a Burner Wallet plugin for your AMB bridge extension](amb-bridge/create-a-burner-wallet-plugin-for-your-amb-bridge-extension.md)

## xDai Bridge

* [About the xDai Bridge](xdai-bridge/about.md)
* [Using the xDai Bridge](xdai-bridge/using-the-xdai-bridge/README.md)
  * [How to use the xDai Bridge without the UI](xdai-bridge/using-the-xdai-bridge/how-to-use-xdai-bridge-without-ui.md)
  * [Alternative receiver for the xDai bridge](xdai-bridge/using-the-xdai-bridge/alternative-receiver-for-the-xdai-bridge.md)
  * [Withdrawal Authorization Flow](xdai-bridge/using-the-xdai-bridge/withdrawal-authorization-flow.md)
* [xDai Bridge Contracts Management](xdai-bridge/xdai-bridge-contracts-management/README.md)
  * [Upgrade Contracts - Instructions](xdai-bridge/xdai-bridge-contracts-management/upgrade-contracts.md)
  * [Configuration](xdai-bridge/xdai-bridge-contracts-management/configuration.md)
  * [Admin Privileges Management](xdai-bridge/xdai-bridge-contracts-management/admin-privileges-management.md)
  * [ERC20 Tokens Release](xdai-bridge/xdai-bridge-contracts-management/erc20-tokens-release.md)
  * [xDai Bridge Management API](xdai-bridge/xdai-bridge-contracts-management/xdai-bridge-management-api.md)
* [xDai Bridge oracle maintenance](xdai-bridge/xdai-bridge-oracle-maintenance/README.md)
  * [Oracle migration to a new server](xdai-bridge/xdai-bridge-oracle-maintenance/oracle-migration-to-a-new-server.md)
* [Trial bridge](xdai-bridge/trial-the-bridge.md)

## ETH-XDAI AMB <a href="eth-xdai-amb-bridge" id="eth-xdai-amb-bridge"></a>

* [About the ETH-xDai AMB](eth-xdai-amb-bridge/about-the-eth-xdai-amb/README.md)
  * [Submit confirmations manually](eth-xdai-amb-bridge/about-the-eth-xdai-amb/submit-confirmations-manually.md)
* [🌉 OmniBridge Extension](eth-xdai-amb-bridge/multi-token-extension/README.md)
  * [OmniBridge UI](eth-xdai-amb-bridge/multi-token-extension/ui-to-transfer-tokens/README.md)
    * [Transfer any ERC20 from Ethereum to xDai](eth-xdai-amb-bridge/multi-token-extension/ui-to-transfer-tokens/transfer-erc20.md)
  * [Transfer tokens manually](eth-xdai-amb-bridge/multi-token-extension/how-to-transfer-tokens.md)
  * [Transfer WETH from xDai to ETH on Mainnet](eth-xdai-amb-bridge/multi-token-extension/transfer-weth-from-xdai-to-eth-on-mainnet.md)
  * [New token contract verification in BlockScout](eth-xdai-amb-bridge/multi-token-extension/new-token-contract-verification-in-blockscout.md)
  * [Corresponding token contract addresses (ETH - XDAI)](eth-xdai-amb-bridge/multi-token-extension/correspondence-of-bridgeable-tokens.md)
  * [Get status of the OmniBridge deposit](eth-xdai-amb-bridge/multi-token-extension/get-status-of-the-omnibridge-deposit.md)
  * [OmniBridge Extension internals & diagrams](eth-xdai-amb-bridge/multi-token-extension/extension-internals.md)
  * [🌱 Bridged Tokens List](eth-xdai-amb-bridge/multi-token-extension/the-bridged-tokens-list/README.md)
    * [Token list compilation](eth-xdai-amb-bridge/multi-token-extension/the-bridged-tokens-list/token-list-compilation.md)
* [NFT OmniBridge extension](eth-xdai-amb-bridge/nft-omnibridge-extension/README.md)
  * [UI Beta](eth-xdai-amb-bridge/nft-omnibridge-extension/ui-beta.md)
  * [ERC721-based NFT Transfer Example](eth-xdai-amb-bridge/nft-omnibridge-extension/nft-transfer-example.md)
  * [EIP1155-based NFT Transfer Example](eth-xdai-amb-bridge/nft-omnibridge-extension/eip1155-based-nft-transfer-example.md)
* [ERC20-to-ERC20 extension linked with a particular token](eth-xdai-amb-bridge/erc20-to-erc20-extension-linked-with-a-particular-token/README.md)
  * [Deploy ERC20 to ERC677 AMB bridge extension](eth-xdai-amb-bridge/erc20-to-erc20-extension-linked-with-a-particular-token/deploy-erc20-erc677-erc827-to-erc677-amb-bridge-extension.md)
  * [UI to transfer tokens through AMB](eth-xdai-amb-bridge/erc20-to-erc20-extension-linked-with-a-particular-token/ui-to-transfer-tokens-through-amb.md)
  * [xMOON-MOON bridge extension](eth-xdai-amb-bridge/erc20-to-erc20-extension-linked-with-a-particular-token/xmoon-moon-bridge-extension.md)
  * [GEN-xGEN bridge extension](eth-xdai-amb-bridge/erc20-to-erc20-extension-linked-with-a-particular-token/gen-xgen-bridge-extension/README.md)
    * [Transfer GEN between the ETH Mainnet and the xDai Chain](eth-xdai-amb-bridge/erc20-to-erc20-extension-linked-with-a-particular-token/gen-xgen-bridge-extension/transfer-gen-between-the-eth-mainnet-and-the-xdai-chain.md)
    * [Change the token contract on the xDai chain](eth-xdai-amb-bridge/erc20-to-erc20-extension-linked-with-a-particular-token/gen-xgen-bridge-extension/change-the-token-contract-on-the-xdai-chain.md)
  * [sUSD bridge extension](eth-xdai-amb-bridge/erc20-to-erc20-extension-linked-with-a-particular-token/susd-bridge-extension/README.md)
    * [Transfer sUSD between the ETH Mainnet and the xDai Chain using the sUSD bridge extension](eth-xdai-amb-bridge/erc20-to-erc20-extension-linked-with-a-particular-token/susd-bridge-extension/transfer-susd-through-the-bridge-extension.md)
    * [Send sUSD between two wallets on xDai](eth-xdai-amb-bridge/erc20-to-erc20-extension-linked-with-a-particular-token/susd-bridge-extension/send-susd-between-two-wallets-on-xdai.md)

## BSC-xDai AMB

* [About the BSC-xDai AMB](bsc-xdai-amb/about-the-bsc-xdai-amb/README.md)
  * [Submit confirmations manually](bsc-xdai-amb/about-the-bsc-xdai-amb/submit-confirmations-manually.md)
* [OmniBridge Extension](bsc-xdai-amb/omnibridge-extension/README.md)
  * [Manual tokens transfer (No UI)](bsc-xdai-amb/omnibridge-extension/manual-tokens-transfer.md)
  * [Transfer WBNB on xDai to BNB on BSC](bsc-xdai-amb/omnibridge-extension/transfer-wbnb-on-xdai-to-bnb-on-bsc.md)

## RINKEBY-XDAI AMB <a href="rinkeby-xdai-amb-bridge" id="rinkeby-xdai-amb-bridge"></a>

* [About the Rinkeby-xDai AMB](rinkeby-xdai-amb-bridge/about-the-rinkeby-xdai-amb.md)
* [AMB Live Monitoring application](rinkeby-xdai-amb-bridge/amb-live-monitoring-application.md)
* [MOON bridge extension](rinkeby-xdai-amb-bridge/moon-bridge-extension/README.md)
  * [Transfer Moons between Rinkeby and xDai Chain using the MOON bridge extension](rinkeby-xdai-amb-bridge/moon-bridge-extension/transfer-moons-between-rinkeby-and-xdai-chain-using-the-moon-bridge-extension.md)
* [BRICK bridge extension](rinkeby-xdai-amb-bridge/brick-bridge-extension.md)
* [NFT OmniBridge extension](rinkeby-xdai-amb-bridge/nft-omnibridge-extension.md)

## POA-XDAI AMB

* [About the POA-xDai AMB](poa-xdai-amb/about-the-poa-xdai-amb/README.md)
  * [Submit confirmations manually](poa-xdai-amb/about-the-poa-xdai-amb/submit-confirmations-manually.md)
* [OmniBridge Extension](poa-xdai-amb/omnibridge-extension/README.md)
  * [Transfer POA tokens](poa-xdai-amb/omnibridge-extension/transfer-poa-tokens.md)

## Kovan-Sokol AMB <a href="kovan-sokol-amb-bridge" id="kovan-sokol-amb-bridge"></a>

* [About the Kovan-Sokol AMB](kovan-sokol-amb-bridge/about-the-kovan-sokol-amb/README.md)
  * [Submit confirmations manually](kovan-sokol-amb-bridge/about-the-kovan-sokol-amb/submit-confirmations-manually.md)
* [OmniBridge extension (testing)](kovan-sokol-amb-bridge/multi-token-extension-testing.md)
* [NFT extension (testing)](kovan-sokol-amb-bridge/nft-extension-testing/README.md)
  * [Transfer tokens by using block explorers](kovan-sokol-amb-bridge/nft-extension-testing/transfer-tokens-by-using-block-explorers.md)
* [Native-to-ERC20 bridge extension](kovan-sokol-amb-bridge/native-to-erc20-bridge-extension/README.md)
  * [Transfer SPOA through native-to-ERC20 extension without UI](kovan-sokol-amb-bridge/native-to-erc20-bridge-extension/transfer-spoa-through-native-to-erc20-extension-without-ui.md)

## ETH-BSC AMB

* [About the ETH-BSC AMB](eth-bsc-amb/about-the-eth-bsc-amb.md)
* [OmniBridge Extension](eth-bsc-amb/omnibridge-extension.md)

## ETH-POA AMB <a href="eth-poa-amb-bridge" id="eth-poa-amb-bridge"></a>

* [About the ETH-POA AMB](eth-poa-amb-bridge/about-the-eth-poa-amb.md)

## ETH-ETC AMB <a href="eth-etc-amb-bridge" id="eth-etc-amb-bridge"></a>

* [About the ETH-ETC AMB](eth-etc-amb-bridge/about-the-eth-etc-amb.md)
* [WETC AMB extension](eth-etc-amb-bridge/wetc-amb-extension.md)

## ETH-QDAI AMB <a href="eth-qdai-bridge" id="eth-qdai-bridge"></a>

* [About the qDai chain](eth-qdai-bridge/about-the-qdai-chain.md)
* [About the ETH-qDai AMB](eth-qdai-bridge/about-the-eth-qdai-amb.md)
* [qDai bridge extension](eth-qdai-bridge/qdai-bridge-extension.md)
* [Using the qDai Bridge](eth-qdai-bridge/using-the-qdai-bridge/README.md)
  * [Configuring MetaMask](eth-qdai-bridge/using-the-qdai-bridge/configuring-metamask.md)
  * [Transfer DAI with UI](eth-qdai-bridge/using-the-qdai-bridge/transfer-dai-with-ui.md)
  * [Transfer DAI without UI](eth-qdai-bridge/using-the-qdai-bridge/transfer-dai-without-ui.md)

## ETH-BNC Bridge

* [About ETH-BNC bridge](eth-bnc-bridge/about-eth-bnc-bridge.md)
* [Demo: ETH-BNC bridge](eth-bnc-bridge/running-an-eth-bnc-bridge-demo.md)
* [Creating a Local Binance DEX Testnet](eth-bnc-bridge/creating-a-local-binance-dex-testnet.md)

## Media

* [Contact Us](media/contact-us.md)
* [Media Kit](media/media-kit.md)
* [Social Media](media/social-media.md)
