---
description: Using a local dev environment provides needed testing flexibility
---

# Creating a Local Binance DEX Testnet

The Binance public testnet at [https://testnet-explorer.binance.org](%20https://testnet-explorer.binance.org) is useful for testing DApps and other Binance-based applications. However, limitations include:

* Issuing test tokens costs 500BNB
* Listing test tokens costs 1000 BNB
* [Testnet Faucet](https://www.binance.com/en/dex/testnet/address) only issues 200BNB once per address. If you want to test a full scale application you spend a lot of time acquiring and transferring tokens.

Creating a local dev testnet provides the opportunity to fully test an application without paying fees or visiting the faucet. We provide the necessary steps below. 

Following the tutorial, there are instructions to [move these commands to Docker.](creating-a-local-binance-dex-testnet.md#moving-to-docker)

## Run Binance Testnet Node

### 1\) Download Required Binaries

All binaries are stored in the official GitHub repository \([https://github.com/binance-chain/node-binary](https://github.com/binance-chain/node-binary)\). Required are the latest versions of testnet fullnode and testnet cli. 

In this tutorial,  we use the following executables:

* `fullnode/testnet/0.6.2/linux/bnbchaind`
* `cli/testnet/0.6.2/linux/tbnbcli`

Install [Git-LFS](https://git-lfs.github.com/) \(used by the repository\) and execute the following:

```text
$ mkdir binance-testnet
$ cd binance-testnet
$ git clone --depth 1 https://github.com/binance-chain/node-binary.git
$ cd node-binary
$ git lfs pull -I fullnode/testnet/0.6.2/linux
$ git lfs pull -I cli/testnet/0.6.2/linux
$ cp ./node-binary/fullnode/testnet/0.6.2/linux/bnbchaind ./bnbchaind
$ cp ./node-binary/cli/testnet/0.6.2/linux/tbnbcli ./tbnbcli
```

{% hint style="info" %}
If you experience this error: "Skipping object checkout, Git LFS is not installed" run `git lfs install` again and rerun the git lfs pull command.
{% endhint %}

### 2\) Generate Configs

Create all required configs for testnet validator, genesis block, etc

```text
$ ./bnbchaind testnet --acc-prefix tbnb --chain-id Binance-Dev --v 1
```

* `--acc-prefix` defines used binance BECH32 addresses prefix \(\)
* `tbnb` used for consistency with public testnet
* `--v` denotes an initial number of validators for the Binance Chain, put it `1` for simplicity.

Generated configs will be located in the `./mytestnet/node0/gaiad/config` directory. Important files are `app.toml`, `config.toml`, `genesis.json`.

If needed, modify parameters in these files \(for example setting`BEP12Height = 1` in `app.toml` will allow BEP12 transactions from the first block\).

### 3\) Start Validator Full Node

All necessary files \(chain configs and validator account keys\) are located in the`./mytestnet/node0/gaiad` directory.

1\) Start validator node

```text
$ ./bnbchaind start --home ./mytestnet/node0/gaiad
```

Validator node should start generating new blocks, which can be observed through the terminal.

{% hint style="info" %}
The error message "Couldn't connect to any seeds module=p2p" in the terminal window[ is expected behavior](https://github.com/tendermint/tendermint/issues/2757).
{% endhint %}

2\) Node validator automatically provides Node-RPC service at `http://localhost:26657`. Check it out using `/status` sub-url from a second terminal window.

```text
$ curl -s -X GET http://localhost:26657/status | jq 
```

### 4\): Create a Prefunded Address

At the moment, a single validator account exists in the network. Let’s create another one, and prefund it for future use.

```text
$ echo password | ./tbnbcli keys add test-acc --no-backup
NAME:	TYPE:	ADDRESS:						PUBKEY:
test-acc	local	tbnb1n5d0n9avv3svhe5sd56nt63yygrn794uu6jvdk	bnbp1addwnpepqd0xp73y09yvlk4p5csmzmpu7lwpxg9da9vkkm52d2sqtazylwwtx4dt2xwjwqtq
```

**Note the printed account address**. We will transfer BNB tokens from the validator account to our newly created one.

```text
$ echo 12345678 | ./tbnbcli send \
    --chain-id Binance-Dev \
    --to tbnb1n5d0n9avv3svhe5sd56nt63yygrn794uu6jvdk \
    --amount "10000000000000:BNB" \
    --from node0 \
    --home ./mytestnet/node0/gaiacli \
    --json
```

* `--to` previously generated address
*  `--from` validator node key name \(by default `node0`\)
* `--home` - directory with validator keystore files
* `12345678` - default password for validator keystore.

### Additional Actions

Now you can continue with regular binance dex actions. For example, issue a new token:

```text
$ echo password | ./tbnbcli token issue \
    --chain-id Binance-Dev \
    --symbol DEV \
    --total-supply 10000000000000000 \
    --token-name "DEV Token" \
    --from test-acc
```

### Accessible HTTP API Services

In regular binance mainnet and testnet, three different APIs are available:

* [Node RPC](https://docs.binance.org/api-reference/node-rpc.html) - in our Binance-Dev network it is accessible at `http://localhost:26657`
* [Api-server](https://docs.binance.org/api-reference/api-server.html) - in our testnet, instantiate by running `./tbnbcli api-server --chain-id Binance-Dev`
* [HTTP-API](https://docs.binance.org/api-reference/dex-api/paths.html) - api of the accelerated node is not accessible. There is no way to make your accelerated node, so this api will not work. However, some paths can be covered by the first two api services, or emulated if necessary.

## Moving to Docker

### **Dockerfile for fetching binaries and updating configs**

```text
FROM ubuntu:19.10

ARG BNC_VERSION=0.6.2

RUN apt-get update && \
    apt-get install -y git git-lfs

WORKDIR /binaries

RUN git clone --depth 1 https://github.com/binance-chain/node-binary.git .

RUN git lfs pull -I fullnode/testnet/${BNC_VERSION}/linux
RUN git lfs pull -I cli/testnet/${BNC_VERSION}/linux

RUN ./fullnode/testnet/${BNC_VERSION}/linux/bnbchaind testnet --acc-prefix tbnb --chain-id Binance-Dev --v 1

RUN sed -i "s/BEP12Height = 9223372036854775807/BEP12Height = 1/" ./mytestnet/node0/gaiad/config/app.toml
```

Assume that image built from this file is called `testnet-binaries`

### **Dockerfile for Validator Node**

```text
FROM alpine:3.9.4

ARG BNC_VERSION=0.6.2

WORKDIR /bnc

COPY --from=testnet-binaries /binaries/fullnode/testnet/${BNC_VERSION}/linux/bnbchaind ./
COPY --from=testnet-binaries /binaries/cli/testnet/${BNC_VERSION}/linux/tbnbcli ./
COPY --from=testnet-binaries /binaries/mytestnet/node0/gaiacli /root/.bnbcli
COPY --from=testnet-binaries /binaries/mytestnet/node0/gaiad /root/.bnbchaind

EXPOSE 26657

ENTRYPOINT ["./bnbchaind", "start"]
```

### **Dockerfile for API-Server**

```text
FROM alpine:3.9.4

ARG BNC_VERSION=0.6.2

WORKDIR /api-server

COPY --from=testnet-binaries /binaries/cli/testnet/${BNC_VERSION}/linux/tbnbcli ./

RUN echo 12345678 | ./tbnbcli keys add key

EXPOSE 8080

ENTRYPOINT ["./tbnbcli", "api-server", "--chain-id", "Binance-Dev", "--laddr", "tcp://0.0.0.0:8080", "--node"]
```

### **docker-compose.yml**

```text
version: '3.0'
services:
  node:
    build: node
    image: bnc-node
    networks:
      - binance_rpc_net
    ports:
      - '26657:26657'
    volumes:
      - 'binance_data:/root/.bnbchaind/data'
  api-server:
    build: api-server
    image: bnc-api-server
    networks:
      - binance_rpc_net
    ports:
      - '8080:8080'
    command: ["http://node:26657"]
networks:
  binance_rpc_net:
volumes:
  binance_data:
```



