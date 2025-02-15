---
description: >-
  Instructions for setting up a Resource Provider (node) on the public Lilypad
  testnet using Docker, including obtaining necessary funds and installing
  required software.
---

# Run a node

## Prerequisites

{% hint style="info" %}
Lilypad RPs currently only support Linux installs. Running a RP on Windows is currently experimental.
{% endhint %}

* Linux (_Ubuntu 22.04_ LTS)
* Nvidia GPU
* [Nvidia drivers](https://ubuntu.com/server/docs/nvidia-drivers-installation)
* [Docker](https://docs.docker.com/engine/install/ubuntu/) (Ubuntu install)
* Nvidia Docker drivers

{% hint style="info" %}
For a more in-depth look at the requirements to run a Lilypad node, please refer to the [hardware requirements](hardware-requirements.md) documentation.
{% endhint %}

## Network information and Testnet tokens

The testnet has a base currency of ETH, as well as a utility token called LP. Both are used for running nodes. To add a node to the testnet, follow these steps:

### Metamask Configuration

We recommend using MetaMask with custom settings to make things easier. Once you have it installed and setup, here are the settings you need to use:

{% hint style="info" %}
Network name: Arbitrum Sepolia

New RPC URL: [https://sepolia-rollup.arbitrum.io/rpc](https://sepolia-rollup.arbitrum.io/rpc)

Chain ID: 421614

Currency symbol: ETH

Block explorer URL: (leave blank)
{% endhint %}

For a step by step guide on adding the network, please refer to our [Setting up MetaMask documentation](../lilypad-testnet/quick-start/setting-up-metamask.md).

### Fund your wallet with ETH and LP

To obtain testnet LP, use the [Lilypad faucet](http://faucet.lilypad.tech) and enter your ETH address.

To obtain testnet ETH, use a third party [Arbitrum Sepolia testnet faucet](https://arbitrum.faucet.dev/ArbSepolia) and enter your ETH address.

{% hint style="info" %}
The Arbitrum Sepolia faucet provides 0.0001 tokens per request. If you need more tokens and already have Sepolia ETH, you can use the [official Arbitrum bridge](https://bridge.arbitrum.io/) to transfer it over to Arbitrum Sepolia.
{% endhint %}

The faucet will give you both ETH (to pay for gas) and LP (to stake and pay for jobs).

## Setup Arbitrum RPC (Optional) <a href="#setup-arbitrum-rpc" id="setup-arbitrum-rpc"></a>

The Lilypad Network uses the Arbitrum Sepolia Testnet to settle compute transactions. When a transaction is ready to be saved on-chain, Lilypad cycles through a list of public Arbitrum Sepolia RPC endpoints using the endpoint that settles first to save the compute transaction.

Resource Providers have the option to [setup their own Arbitrum RPC endpoint](https://docs.lilypad.tech/lilypad/hardware-providers/setup-arbitrum-rpc) using Alchemy instead of using the default public RPC endpoints.

A personal RPC endpoint helps RPs to avoid reliability issues with the public RPC endpoints used by Lilypad ensuring rewards can be earned and jobs can be run consistently. RPs running a personal RPC endpoint contribute to the fault tolerance and decentralization of the Lilypad Network! Read more in the Alchemy Arbitrum [docs](https://docs.alchemy.com/reference/arbitrum-api-quickstart).

## Usage <a href="#heading-run-the-docker-image" id="heading-run-the-docker-image"></a>

Before we start the Docker setup, you'll need to retrieve the private key from the wallet you set up earlier in this guide. For guidance on exporting your private key, refer to [this official MetaMask guide](https://support.metamask.io/managing-my-wallet/secret-recovery-phrase-and-private-keys/how-to-export-an-accounts-private-key/). Once you’ve securely copied your private key, proceed to initialize the Docker containers using the commands provided below.

You have two options to start the Lilypad setup: using Docker Compose or directly pulling the image. Both methods will run the containers in the background, allowing you to continue using your terminal while the setup operates.

## Docker Compose Setup

### 1. Export Your Private Key

{% hint style="info" %}
The same WEB3\_PRIVATE\_KEY cannot be used for both a RP and using the Lilypad CLI. If a WEB3\_PRIVATE\_KEY has already been used to run jobs with the CLI, make a new one and [fund](https://docs.lilypad.tech/lilypad/lilypad-testnet/quick-start/funding-your-wallet-from-faucet) the wallet. You can \`unset $WEB3\_PRIVATE\_KEY\` if you want to use a different one to run your RP.
{% endhint %}

Before starting, export your private key from MetaMask. Follow the official MetaMask guide for instructions on safely exporting your private key.

### 2. Download the Docker Compose Configuration

Use `curl` to download the `docker-compose.yml` file from the Lilypad GitHub repository.

```bash
LATEST_VERSION=$(curl -s https://api.github.com/repos/Lilypad-Tech/lilypad/releases/latest | sed -n 's/.*"tag_name": "\(.*\)".*/\1/p')

curl -o docker-compose.yml "https://raw.githubusercontent.com/Lilypad-Tech/lilypad/$LATEST_VERSION/docker/docker-compose.yml"
```

### 3. Check for Existing Containers

{% hint style="warning" %}
If any containers named `resource-provider`, `ipfs`, or `watchtower` are already in use, they will need to be stopped before running this setup to avoid naming conflicts.
{% endhint %}

You can check if these containers are running with:

```bash
docker ps -a | grep -E "resource-provider|ipfs|watchtower"
```

If they are running, stop them with:

```
docker stop <container_name>
```

If there are still conflicts when trying to running with the docker-compose file, remove the containers:

```shell-session
docker rm <container_name>
```

{% hint style="info" %}
Before moving to the next step, ensure older versions of lilypad and bacalhau [are not running](https://docs.lilypad.tech/lilypad/hardware-providers/troubleshooting#my-docker-rp-is-turning-on-but-showing-errors-stating-it-is-not-providing-a-resource-offer) as systemd services.
{% endhint %}

### 4. Start the Resource Provider

Start the Lilypad containers using Docker Compose:

```bash
WEB3_PRIVATE_KEY=<your_private_key> docker compose up -d
```

To include a custom RPC URL:&#x20;

```
WEB3_PRIVATE_KEY=<your_private_key> WEB3_RPC_URL=wss://arb-sepolia.g.alchemy.com/v2/your-alchemy-id docker compose up -d
```

{% hint style="warning" %}
You must not reuse your compute node key as a client, even for testing: this will result in failed jobs and will negatively impact your compute node since the wallet address is how nodes are identified on the network.
{% endhint %}

### 5. Monitor Your Node

Use the following command to check the status of the resource provider and bacalhau.

```bash
docker logs resource-provider
```

```bash
docker logs bacalhau
```

Use the following command to view the containers running after starting Docker Compose.

```bash
docker ps
```

## Update Lilypad version for Docker RP

When a new version of Lilypad is released, it is critical for Resource Providers to update their installations to ensure compatibility and ability to run Lilypad jobs.&#x20;

### 1. If a Docker RP is running stop the system (if the node is not running, disregard this first step)

```bash
docker compose down
```

### 2. View all Docker images

```bash
docker images
```

### 3. Delete old Docker images that are duplicates for Lilypad (Bacalhau, Lilypad)

```bash
docker rmi <image_name_or_id> 
```

### 4. Follow Docker RP install instructions

Using the Lilypad Docker [RP install instructions](https://docs.lilypad.tech/lilypad/hardware-providers/docker#docker-compose-setup) setup a new RP and run.

## View Lilybit\_ rewards

To view your Lilybit\_ rewards, visit one of the following dashboards and paste your node's public address into the input:

* [Grafana dashboard](https://grafana.lilypad.tech/d/adxhou3o1q8sga/rewards-per-wallets?orgId=1\&refresh=1m)

## Troubleshooting

Here are some common troubleshooting techniques when it comes to your resource provider using Docker:

**Checking Docker Runtime**\
To verify your Docker runtime configuration: `sudo docker info | grep Runtimes`

You should see the NVIDIA runtime listed. If you only see: `Runtimes: io.containerd.runc.v2 runc` you will need to configure the NVIDIA runtime.

**Configuring NVIDIA Runtime**\
If the NVIDIA runtime is not showing up or you're experiencing issues, try the following:

1\. Configure the NVIDIA Container Toolkit runtime: `sudo nvidia-ctk runtime configure --runtime=docker --set-as-default`\
2\. Restart the Docker service: `sudo systemctl restart docker`

**Overview of Docker setup**\
For a comprehensive overview of your Docker setup, use: `docker info`. This command provides detailed information about your Docker daemon configuration.
