---
description: How to deploy erc677-to-erc677 Arbitrary Message Bridge extension
---

# ERC677 to ERC677 AMB bridge extension

Instructions for deploying a pair of ERC677-compatible tokens and the bridge mediator contract on top of the Arbitrary Message Bridge \(AMB\). 

{% hint style="info" %}
**An AMB bridge extension** is a pair of mediator contracts associated with a specific pair of Arbitrary Message Bridge contracts.
{% endhint %}

The steps below assume that the AMB is up and running and serves the bridge between Kovan \(Foreign\) chain and Sokol \(Home\) chain. Addresses of the deployed AMB bridge contracts:

* [Kovan](https://blockscout.com/eth/kovan/address/0xfe446bef1dbf7afe24e81e05bc8b271c1ba9a560/contracts) Foreign testnet
* [Sokol](https://blockscout.com/poa/sokol/address/0xfe446bef1dbf7afe24e81e05bc8b271c1ba9a560/contracts) Home testnet

## Instructions

1. `git clone https://github.com/poanetwork/tokenbridge-contracts.git`
2. `cd tokenbridge-contracts`
3. `git checkout 3.2.0`
4. Create an empty .env file in the deploy directory.  `touch deploy/.env` 
5. `docker-compose up --build`
6. `docker-compose images bridge-contracts`
7. `docker cp tokenbridge-contracts_bridge-contracts_1:/contracts/flats ./`
8. Deploy the contract `ERC677BridgeToken` from `flats/ERC677BridgeToken_flat.sol` using Remix or MyEtherWallet to the Foreign \(Kovan\) chain. _**Note:** In the steps below we assume that the address of the deployed token contract is_ `0x1e402513B7305F758476409da8048fd5b045C0AA`
9. Verify the contract in the block explorer \(contract name: `ERC677BridgeToken`, compiler version: `v0.4.24+commit.e67f0147`, optimization is enabled, automatic identification of constructor arguments\)
10. Mint some amount of tokens for an account.
11. Prepare `deploy/.env` as follows:

    ```text
    # The type of bridge. Defines set of contracts to be deployed.
    BRIDGE_MODE=AMB_ERC_TO_ERC

    # The private key hex value of the account responsible for contracts
    # deployments and initial configuration. The account's balance must contain
    # funds from both networks.
    DEPLOYMENT_ACCOUNT_PRIVATE_KEY=
    # Extra gas added to the estimated gas of a particular deployment/configuration transaction
    # E.g. if estimated gas returns 100000 and the parameter is 0.2,
    # the transaction gas limit will be (100000 + 100000 * 0.2) = 120000
    DEPLOYMENT_GAS_LIMIT_EXTRA=0.2
    # The "gasPrice" parameter set in every deployment/configuration transaction on
    # Home network (in Wei).
    HOME_DEPLOYMENT_GAS_PRICE=10000000000
    # The "gasPrice" parameter set in every deployment/configuration transaction on
    # Foreign network (in Wei).
    FOREIGN_DEPLOYMENT_GAS_PRICE=10000000000
    # The timeout limit to wait for receipt of the deployment/configuration
    # transaction.
    GET_RECEIPT_INTERVAL_IN_MILLISECONDS=3000

    # The name of the ERC677 token to be deployed on the Home network.
    BRIDGEABLE_TOKEN_NAME=YourTokenName
    # The symbol name of the ERC677 token to be deployed on the Home network.
    BRIDGEABLE_TOKEN_SYMBOL=YourTokenSymbol
    # The number of supportable decimal digits after the "point" in the ERC677 token
    # to be deployed on the Home network.
    BRIDGEABLE_TOKEN_DECIMALS=18
    # The flag defining whether to use ERC677BridgeTokenRewardable contract instead of
    # ERC677BridgeToken on Home network.
    DEPLOY_REWARDABLE_TOKEN=false

    # The RPC channel to a Home node able to handle deployment/configuration
    # transactions.
    HOME_RPC_URL=https://sokol.rpc.endpoint/
    # Address on Home network with permissions to change parameters of the bridge contract.
    # For extra security we recommended using a multi-sig wallet contract address here.
    HOME_BRIDGE_OWNER=0x
    # Address on Home network with permissions to upgrade the bridge contract
    HOME_UPGRADEABLE_ADMIN=0x
    # The daily transaction limit in Wei. As soon as this limit is exceeded, any
    # transaction which requests to relay assets will fail.
    HOME_DAILY_LIMIT=30000000000000000000000000
    # The maximum limit for one transaction in Wei. If a single transaction tries to
    # relay funds exceeding this limit it will fail. HOME_MAX_AMOUNT_PER_TX must be
    # less than HOME_DAILY_LIMIT.
    HOME_MAX_AMOUNT_PER_TX=1500000000000000000000000
    # The minimum limit for one transaction in Wei. If a transaction tries to relay
    # funds below this limit it will fail. This is required to prevent dryout
    # validator accounts.
    HOME_MIN_AMOUNT_PER_TX=500000000000000000

    # The RPC channel to a Foreign node able to handle deployment/configuration
    # transactions.
    FOREIGN_RPC_URL=https://kovan.rpc.endpoint/
    # Address on Foreign network with permissions to change parameters of the bridge contract.
    # For extra security we recommended using a multi-sig wallet contract address here.
    FOREIGN_BRIDGE_OWNER=0x
    # Address on Foreign network with permissions to upgrade the bridge contract and the
    # bridge validator contract.
    FOREIGN_UPGRADEABLE_ADMIN=0x
    # The daily limit in Wei. As soon as this limit is exceeded, any transaction
    # requesting to relay assets will fail.
    FOREIGN_DAILY_LIMIT=15000000000000000000000000
    # The maximum limit per one transaction in Wei. If a transaction tries to relay
    # funds exceeding this limit it will fail. FOREIGN_MAX_AMOUNT_PER_TX must be less
    # than FOREIGN_DAILY_LIMIT.
    FOREIGN_MAX_AMOUNT_PER_TX=750000000000000000000000
    # The minimum limit for one transaction in Wei. If a transaction tries to relay
    # funds below this limit it will fail.
    FOREIGN_MIN_AMOUNT_PER_TX=500000000000000000
    # The address of the existing ERC20/ERC677 compatible token in the Foreign network to
    # be exchanged to the ERC20/ERC677 token deployed on Home.
    ERC20_TOKEN_ADDRESS=0x1e402513B7305F758476409da8048fd5b045C0AA

    # The address of the existing AMB bridge in the Home network that will be used to pass messages
    # to the Foreign network.
    HOME_AMB_BRIDGE=0xFe446bEF1DbF7AFE24E81e05BC8B271C1BA9a560
    # The address of the existing AMB bridge in the Foreign network that will be used to pass messages
    # to the Home network.
    FOREIGN_AMB_BRIDGE=0xFe446bEF1DbF7AFE24E81e05BC8B271C1BA9a560
    # The gas limit that will be used in the execution of the message passed to the mediator contract
    # in the Foreign network.
    HOME_MEDIATOR_REQUEST_GAS_LIMIT=3000000
    # The gas limit that will be used in the execution of the message passed to the mediator contract
    # in the Home network.
    FOREIGN_MEDIATOR_REQUEST_GAS_LIMIT=3000000
    ```

12. `docker-compose run bridge-contracts deploy.sh`. Output will look similar to this:

    ```text
    {
        "homeBridge": {
            "homeBridgeMediator": {
                "address": "0xFaD73D79952041332554e11d896F430a2ecA1Fa8"
            },
            "bridgeableErc677": {
                "address": "0xAFb605e4463D1326249075b3367A3353DeA34a6D"
            }
        },
        "foreignBridge": {
            "foreignBridgeMediator": {
                "address": "0x1a2546B27293e127fF9a3d0D71A43Dd3733fa1F7"
            }
        }
    }
    ```

13. Verify the token contract `0xAFb605e4463D1326249075b3367A3353DeA34a6D` on the Home \(Sokol\) side using `flats/ERC677BridgeToken_flat.sol` \(contract name: `ERC677BridgeToken`, compiler version: `v0.4.24+commit.e67f0147`, optimization is enabled, automatic identification of constructor arguments\)
14. Verify the mediator contract `0xFaD73D79952041332554e11d896F430a2ecA1Fa8` on Home side
    * verify the proxy contract by `flats/EternalStorageProxy_flat.sol` \(contract name: `EternalStorageProxy`, compiler version: `v0.4.24+commit.e67f0147`, optimization is enabled, no constructor arguments\)
    * go to the implementation contract from the _Read Contract_ tab
    * verify the implementation contract by `flats/amb_erc677_to_erc677/HomeAMBErc677ToErc677_flat.sol` \(contract name: `HomeAMBErc677ToErc677`, compiler version: `v0.4.24+commit.e67f0147`, optimization is enabled, no constructor arguments\)
15. Verify the mediator contract `0x1a2546B27293e127fF9a3d0D71A43Dd3733fa1F7` on Foreign side
    * verify the proxy contract by `flats/EternalStorageProxy_flat.sol` \(contract name: `EternalStorageProxy`, compiler version: `v0.4.24+commit.e67f0147`, optimization is enabled, no constructor arguments\)
    * go to the implementation contract from the _Read Contract_ tab
    * verify the implementation contract by `flats/amb_erc677_to_erc677/ForeignAMBErc677ToErc677_flat.sol` \(contract name: `ForeignAMBErc677ToErc677`, compiler version: `v0.4.24+commit.e67f0147`, optimization is enabled, no constructor arguments\)
16. Execute `transferAndCall` method from the token contract on the Foreign side by using NiftyWallet, MyEtherWallet or Remix. The argument `to` for the call must contain the address of the mediator contract `0x1a2546B27293e127fF9a3d0D71A43Dd3733fa1F7`. The `data` argument must be `0x`. The sender of the transaction is the account-recipient used in the mint operation. Make sure:
    1. the amount of tokens must be equal or greater the `FOREIGN_MIN_AMOUNT_PER_TX` parameter used in the deployment
    2. the transaction verified successfully and included into a block.
17. Check the balance of the sender on the Home side.

