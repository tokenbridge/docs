---
description: Instructions to deploy the monitor for existing bridges
---

# Monitor deployment for existing bridges

The TokenBridge monitor instance deployment uses [Ansible](https://docs.ansible.com/ansible/latest/index.html). Moreover the process below assumes there are two nodes: one node where Ansible playbooks orchestrate the deployment process (orchestration node) and another node where the monitor instance is deployed (target node).&#x20;

The **orchestration node **must satisfy the following dependencies:

* Python 2 (v2.6-v2.7)/Python3 (v3.5+)
* Ansible v2.3+ (on Ubuntu based systems it could be installed by `apt-get install ansible` )
* Git

The **target node **must** **have a functional Ubuntu 16.04 or 18.04 launched, and recommended 4Gb+  memory.

For these instructions, You will use an [Infura account](https://infura.io) with a project ID. You can create a free account and the id will be located there. Alternately, you can choose a different mainnet endpoint.

## Tasks on Orchestration Node

1\. Login and generate a pair of SSH keys that will be used by the orchestration node to remotely login to the target node. The generated public key must be added to `.ssh/authorized_keys` on the target node in the home directory of the user (usually `root` or `ubuntu`) that will be configured to perform deployment actions. &#x20;

```
ssh-keygen -t rsa
cat ~/.ssh/id_rsa.pub | ssh user@hostname 'cat >> .ssh/authorized_keys'
```

Check that user has appropriate permissions and change if needed. Use `ls -l` to check permissions, if assigned to root and you are using ubuntu user, use the` chown` command to update permissions.

```
ls -l
sudo chown -R ubuntu:ubuntu
```

2\. Clone the TokenBridge git repository and change the working directory:

```bash
git clone --recursive https://github.com/poanetwork/tokenbridge.git
cd tokenbridge/deployment
```

3\. Prepare the following four files in the directory \`group\_vars\`. Every file will be used to send requests to one of the bridges:

* xDai bridge: **`group_vars/xdai.yml`**
* POA bridge: **`group_vars/poa.yml`**
* wETC bridge: **`group_vars/wetc.yml`**
* ETH-xDai Arbitrary message bridge: **`group_vars/amb-xdai.yml`**
* ETH-POA Arbitrary message bridge: **`group_vars/amb-poa.yml`**
* Rinkeby-xDai Arbitrary message bridge: **`group_vars/amb-rinkeby.yml`**
* Kovan-Sokol Arbitrary message bridge (test bed): **`group_vars/amb-test.yml`**

{% hint style="warning" %}
Replace all places templated with tags (<>) with actual values. In order to achieve this it is necessary to define in advance **the port** where the monitor web-service will listen users' requests and **the JSON RPC url** to communicate with Ethereum Mainnet nodes.

The web service port must be specified **only in the first file**.
{% endhint %}

**`group_vars/xdai.yml`**

```yaml
---
MONITOR_BRIDGE_NAME: "xdai"
MONITOR_PORT: <port for web service>

COMMON_HOME_RPC_URL: "https://dai.poa.network"
COMMON_HOME_BRIDGE_ADDRESS: "0x7301CFA0e1756B71869E93d4e4Dca5c7d0eb0AA6"
COMMON_FOREIGN_RPC_URL: "https://mainnet.infura.io/v3/<infura project id>"
COMMON_FOREIGN_BRIDGE_ADDRESS: "0x4aa42145Aa6Ebf72e164C9bBC74fbD3788045016"

COMMON_HOME_GAS_PRICE_FALLBACK: 0
COMMON_FOREIGN_GAS_PRICE_SUPPLIER_URL: "https://gasprice.poa.network/"
COMMON_FOREIGN_GAS_PRICE_SPEED_TYPE: "fast"
COMMON_FOREIGN_GAS_PRICE_FALLBACK: 10000000000
COMMON_FOREIGN_GAS_PRICE_FACTOR: 1

MONITOR_HOME_START_BLOCK: 759
MONITOR_FOREIGN_START_BLOCK: 6478417
MONITOR_VALIDATOR_HOME_TX_LIMIT: 0
MONITOR_VALIDATOR_FOREIGN_TX_LIMIT: 300000
MONITOR_TX_NUMBER_THRESHOLD: 100
```

**`group_vars/poa.yml`**

```yaml
---
MONITOR_BRIDGE_NAME: "poa"

COMMON_HOME_RPC_URL: "https://core.poa.network"
COMMON_HOME_BRIDGE_ADDRESS: "0xB87b6077D59B01Ab9fa8cd5A1A21D02a4d60D358"
COMMON_FOREIGN_RPC_URL: "https://mainnet.infura.io/v3/<infura project id>"
COMMON_FOREIGN_BRIDGE_ADDRESS: "0xd819E948b14cA6AAD2b7Ffd333cCDf732b129EeD"

COMMON_HOME_GAS_PRICE_FALLBACK: 1000000000
COMMON_HOME_GAS_PRICE_FACTOR: 1
COMMON_FOREIGN_GAS_PRICE_SUPPLIER_URL: "https://gasprice.poa.network/"
COMMON_FOREIGN_GAS_PRICE_SPEED_TYPE: "fast"
COMMON_FOREIGN_GAS_PRICE_FALLBACK: 10000000000
COMMON_FOREIGN_GAS_PRICE_FACTOR: 1

MONITOR_HOME_START_BLOCK: 2477327
MONITOR_FOREIGN_START_BLOCK: 5578725
MONITOR_VALIDATOR_HOME_TX_LIMIT: 300000
MONITOR_VALIDATOR_FOREIGN_TX_LIMIT: 300000
MONITOR_TX_NUMBER_THRESHOLD: 100
```

**`group_vars/wetc.yml`**

```yaml
---
MONITOR_BRIDGE_NAME: "wetc"

COMMON_HOME_RPC_URL: "https://ethereumclassic.network"
COMMON_HOME_BRIDGE_ADDRESS: "0x073081832B4Ecdce79d4D6753565c85Ba4b3BeA9"
COMMON_FOREIGN_RPC_URL: "https://mainnet.infura.io/v3/<infura project id>"
COMMON_FOREIGN_BRIDGE_ADDRESS: "0x0cB781EE62F815bdD9CD4c2210aE8600d43e7040"

COMMON_HOME_GAS_PRICE_SUPPLIER_URL: "https://gasprice-etc.poa.network/"
COMMON_HOME_GAS_PRICE_SPEED_TYPE: "standard"
COMMON_HOME_GAS_PRICE_FALLBACK: 15000000000
COMMON_HOME_GAS_PRICE_FACTOR: 1

COMMON_FOREIGN_GAS_PRICE_SUPPLIER_URL: "https://gasprice.poa.network/"
COMMON_FOREIGN_GAS_PRICE_SPEED_TYPE: "standard"
COMMON_FOREIGN_GAS_PRICE_FALLBACK: 10000000000
COMMON_FOREIGN_GAS_PRICE_FACTOR: 1

MONITOR_HOME_START_BLOCK: 7703292
MONITOR_FOREIGN_START_BLOCK: 7412459
MONITOR_VALIDATOR_HOME_TX_LIMIT: 300000
MONITOR_VALIDATOR_FOREIGN_TX_LIMIT: 300000
MONITOR_TX_NUMBER_THRESHOLD: 100
```

**`group_vars/amb-xdai.yml`**

```yaml
---
MONITOR_BRIDGE_NAME: "amb-xdai"

COMMON_HOME_RPC_URL: "https://dai.poa.network"
COMMON_HOME_BRIDGE_ADDRESS: "0x75Df5AF045d91108662D8080fD1FEFAd6aA0bb59"
COMMON_FOREIGN_RPC_URL: "https://mainnet.infura.io/v3/<infura project id>"
COMMON_FOREIGN_BRIDGE_ADDRESS: "0x4C36d2919e407f0Cc2Ee3c993ccF8ac26d9CE64e"

COMMON_HOME_GAS_PRICE_FALLBACK: 1000000000
COMMON_HOME_GAS_PRICE_FACTOR: 1
COMMON_FOREIGN_GAS_PRICE_SUPPLIER_URL: "https://gasprice.poa.network/"
COMMON_FOREIGN_GAS_PRICE_SPEED_TYPE: "fast"
COMMON_FOREIGN_GAS_PRICE_FALLBACK: 10000000000
COMMON_FOREIGN_GAS_PRICE_FACTOR: 1

MONITOR_HOME_START_BLOCK: 7904954
MONITOR_FOREIGN_START_BLOCK: 9298324
MONITOR_VALIDATOR_HOME_TX_LIMIT: 2000000
MONITOR_VALIDATOR_FOREIGN_TX_LIMIT: 2000000
MONITOR_TX_NUMBER_THRESHOLD: 50
```

**`group_vars/amb-poa.yml`**

```yaml
---
MONITOR_BRIDGE_NAME: "amb-poa"

COMMON_HOME_RPC_URL: "https://core.poa.network"
COMMON_HOME_BRIDGE_ADDRESS: "0xD9a3039cfC70aF84AC9E566A2526fD3b683B995B"
COMMON_FOREIGN_RPC_URL: "https://mainnet.infura.io/v3/<infura project id>"
COMMON_FOREIGN_BRIDGE_ADDRESS: "0x2140ECDC45c89ca112523637824513baE72C8671"

COMMON_HOME_GAS_PRICE_FALLBACK: 5000000000
COMMON_HOME_GAS_PRICE_FACTOR: 1
COMMON_FOREIGN_GAS_PRICE_SUPPLIER_URL: "https://gasprice.poa.network/"
COMMON_FOREIGN_GAS_PRICE_SPEED_TYPE: "fast"
COMMON_FOREIGN_GAS_PRICE_FALLBACK: 10000000000
COMMON_FOREIGN_GAS_PRICE_FACTOR: 1

MONITOR_HOME_START_BLOCK: 13259999
MONITOR_FOREIGN_START_BLOCK: 9359576
MONITOR_VALIDATOR_HOME_TX_LIMIT: 2000000
MONITOR_VALIDATOR_FOREIGN_TX_LIMIT: 2000000
MONITOR_TX_NUMBER_THRESHOLD: 50
```

**`group_vars/amb-rinkeby.yml`**

```yaml
---
MONITOR_BRIDGE_NAME: "amb-rinkeby"

COMMON_HOME_RPC_URL: "https://xdai.poanetwork.dev/"
COMMON_HOME_BRIDGE_ADDRESS: "0xc38D4991c951fE8BCE1a12bEef2046eF36b0FA4A"
COMMON_FOREIGN_RPC_URL: "https://rinkeby.infura.io/v3/<infura project id>"
COMMON_FOREIGN_BRIDGE_ADDRESS: "0xD4075FB57fCf038bFc702c915Ef9592534bED5c1"

COMMON_HOME_GAS_PRICE_FALLBACK: 1000000000
COMMON_HOME_GAS_PRICE_FACTOR: 1
COMMON_FOREIGN_GAS_PRICE_FALLBACK: 1000000000
COMMON_FOREIGN_GAS_PRICE_FACTOR: 1

MONITOR_HOME_START_BLOCK: 10030211
MONITOR_FOREIGN_START_BLOCK: 6529875
MONITOR_VALIDATOR_HOME_TX_LIMIT: 2000000
MONITOR_VALIDATOR_FOREIGN_TX_LIMIT: 2000000
MONITOR_TX_NUMBER_THRESHOLD: 50
```

**`group_vars/amb-qdai.yml`**

```yaml
---
MONITOR_BRIDGE_NAME: "amb-qdai"

COMMON_HOME_RPC_URL: "https://quorum-rpc.tokenbridge.net"
COMMON_HOME_BRIDGE_ADDRESS: "0xD4075FB57fCf038bFc702c915Ef9592534bED5c1"
COMMON_FOREIGN_RPC_URL: "https://mainnet.infura.io/v3/<infura project id>"
COMMON_FOREIGN_BRIDGE_ADDRESS: "0xcEb06eCea3F588Cb60e39BD4DB7869013C6f65a5"

COMMON_HOME_GAS_PRICE_FALLBACK: 1000000000
COMMON_HOME_GAS_PRICE_FACTOR: 1
COMMON_FOREIGN_GAS_PRICE_SUPPLIER_URL: "https://gasprice.poa.network/"
COMMON_FOREIGN_GAS_PRICE_SPEED_TYPE: "fast"
COMMON_FOREIGN_GAS_PRICE_FALLBACK: 10000000000
COMMON_FOREIGN_GAS_PRICE_FACTOR: 1

MONITOR_HOME_START_BLOCK: 464831
MONITOR_FOREIGN_START_BLOCK: 10370242
MONITOR_VALIDATOR_HOME_TX_LIMIT: 2000000
MONITOR_VALIDATOR_FOREIGN_TX_LIMIT: 2000000
MONITOR_TX_NUMBER_THRESHOLD: 50
```

**`group_vars/amb-test.yml`**

```yaml
---
MONITOR_BRIDGE_NAME: "amb-test"

COMMON_HOME_RPC_URL: "https://sokol.poa.network"
COMMON_HOME_BRIDGE_ADDRESS: "0xFe446bEF1DbF7AFE24E81e05BC8B271C1BA9a560"
COMMON_FOREIGN_RPC_URL: "https://kovan.infura.io/v3/<infura project id>"
COMMON_FOREIGN_BRIDGE_ADDRESS: "0xFe446bEF1DbF7AFE24E81e05BC8B271C1BA9a560"

COMMON_HOME_GAS_PRICE_FALLBACK: 5000000000
COMMON_HOME_GAS_PRICE_FACTOR: 1
COMMON_FOREIGN_GAS_PRICE_FALLBACK: 5000000000
COMMON_FOREIGN_GAS_PRICE_FACTOR: 1

MONITOR_HOME_START_BLOCK: 9849617
MONITOR_FOREIGN_START_BLOCK: 12372926
MONITOR_VALIDATOR_HOME_TX_LIMIT: 2000000
MONITOR_VALIDATOR_FOREIGN_TX_LIMIT: 2000000
MONITOR_TX_NUMBER_THRESHOLD: 50
```

4\. Return to the deployment directory (`cd ..`) and create the `hosts.yml` file

{% hint style="warning" %}
Replace all variables templated with tags (<>) with actual values.
{% endhint %}

```yaml
---
xdai:
  children:
    monitor:
      hosts:
        <target node ip address 1.2.3.4>:
          ansible_user: <user>
```

Here `<user>` is the account that will ssh into the monitor node for deployment actions. This is typically `ubuntu` or `root`.

5\. Next, the Ansible playbook will deploy the monitor instance on the remote target node, then propagate the rest of configuration to the same system. You will run the playbook each time after re-configuring the hosts.yml file

{% hint style="warning" %}
If the target node contains `python3` instead of `python`, append `-e 'ansible_python_interpreter=/usr/bin/python3' `to the end of the ansible-playbook command (before `-i hosts.yml`). Try this if you get a node connection / ssh error.

Depending on your ssh setup, you may not need the `--private-key` flag

:hourglass\_flowing\_sand: Automated deployment and the remote node configuration can take a few minutes depending on target node resources. Be patient and maybe have a :coffee: during  these operations!
{% endhint %}

```
ansible-playbook --private-key=~/.ssh/<privkey.file> -i hosts.yml site.yml
sed -i 's/xdai/poa/' hosts.yml
ansible-playbook --private-key=~/.ssh/<privkey.file> -i hosts.yml site.yml
sed -i 's/poa/wetc/' hosts.yml
ansible-playbook --private-key=~/.ssh/<privkey.file> -i hosts.yml site.yml
sed -i 's/wetc/amb-xdai/' hosts.yml
ansible-playbook --private-key=~/.ssh/<privkey.file> -i hosts.yml site.yml
sed -i 's/amb-xdai/amb-poa/' hosts.yml
ansible-playbook --private-key=~/.ssh/<privkey.file> -i hosts.yml site.yml
sed -i 's/amb-poa/amb-rinkeby/' hosts.yml
ansible-playbook --private-key=~/.ssh/<privkey.file> -i hosts.yml site.yml
sed -i 's/amb-rinkeby/amb-qdai/' hosts.yml
ansible-playbook --private-key=~/.ssh/<privkey.file> -i hosts.yml site.yml
sed -i 's/amb-qdai/amb-test/' hosts.yml
ansible-playbook --private-key=~/.ssh/<privkey.file> -i hosts.yml site.yml
```

6\. Wait for 5-6 minutes and check availability of the monitor statistic in the web service:&#x20;

1\) By URL:

* http://\<target node ip address:port>/xdai
* http://\<target node ip address:port>/poa
* http://\<target node ip address:port>/wetc
* http://\<target node ip address:port>/amb-xdai
* http://\<target node ip address:port>/amb-poa
* http://\<target node ip address:port>/amb-rinkeby
* http://\<target node ip address:port>/amb-qdai
* http://\<target node ip address:port>/amb-test

2\) If URL method is unavailable you can **login to the target node** and: `curl http://<target node ip address:port>/xdai `from the command line to check operability.
