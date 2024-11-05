---
description: >-
  Instructions for setting up a Resource Provider (node) on the public Lilypad
  testnet using Docker, including obtaining necessary funds and installing
  required software.
---

# Docker

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
For a more in-depth look at the requirements to run a Lilypad node, please refer to the [hardware requirements](../hardware-requirements.md) documentation.
{% endhint %}

## Network information and testnet tokens

The testnet has a base currency of ETH, as well as a utility token called LP. Both are used for running nodes. To add a node to the testnet, follow these steps:

### Metamask

We recommend using MetaMask with custom settings to make things easier. Once you have it installed and setup, here are the settings you need to use:

{% hint style="info" %}
Network name: Arbitrum Sepolia

New RPC URL: [https://sepolia-rollup.arbitrum.io/rpc](https://sepolia-rollup.arbitrum.io/rpc)

Chain ID: 421614

Currency symbol: ETH

Block explorer URL: (leave blank)
{% endhint %}

For a step by step guide on adding the network, please refer to our [Setting up MetaMask documentation](../../lilypad-testnet/quick-start/setting-up-metamask.md).

### Fund your wallet with ETH and LP

To obtain testnet LP, use the [Lilypad faucet](http://faucet.lilypad.tech) and enter your ETH address.

To obtain testnet ETH, use a third party [Arbitrum Sepolia testnet faucet](https://arbitrum.faucet.dev/ArbSepolia) and enter your ETH address.

{% hint style="info" %}
The Arbitrum Sepolia faucet provides 0.0001 tokens per request. If you need more tokens and already have Sepolia ETH, you can use the [official Arbitrum bridge](https://bridge.arbitrum.io/) to transfer it over to Arbitrum Sepolia.
{% endhint %}

The faucet will give you both ETH (to pay for gas) and LP (to stake and pay for jobs).

## Installation

To set up your environment for running a Lilypad Resource Provider, you'll need to install and configure several key components.

### Pull the pre-built Docker image

The pre-built Docker image is a crucial component in setting up your Lilypad Resource Provider with this approach. It encapsulates the environment in which your node will operate, including all necessary dependencies, configurations, and commands to run the Lilypad services.

Before pulling the image, you must be logged in to Docker by running `docker login` and follow the prompts.

In the root directory of the Lilypad repo, run the following command to pull the pre-built Docker image:

```bash
docker pull ghcr.io/lilypad-tech/resource-provider:latest
```

## Setup Arbitrum RPC <a href="#setup-arbitrum-rpc" id="setup-arbitrum-rpc"></a>

The Lilypad Network uses the Arbitrum Sepolia Testnet to settle compute transactions. When a transaction is ready to be saved on-chain, Lilypad cycles through a list of public Arbitrum Sepolia RPC endpoints using the endpoint that settles first to save the compute transaction.

Resource Providers have the option to [setup their own Arbitrum RPC endpoint](https://docs.lilypad.tech/lilypad/hardware-providers/setup-arbitrum-rpc) using Alchemy instead of using the default public RPC endpoints.

A personal RPC endpoint helps RPs to avoid reliability issues with the public RPC endpoints used by Lilypad ensuring rewards can be earned and jobs can be run consistently. RPs running a personal RPC endpoint contribute to the fault tolerance and decentralization of the Lilypad Network! Read more in the Alchemy Arbitrum [docs](https://docs.alchemy.com/reference/arbitrum-api-quickstart).

## Usage <a href="#heading-run-the-docker-image" id="heading-run-the-docker-image"></a>

Before we start the Docker setup, you'll need to retrieve the private key from the wallet you set up earlier in this guide. For guidance on exporting your private key, refer to [this official MetaMask guide](https://support.metamask.io/managing-my-wallet/secret-recovery-phrase-and-private-keys/how-to-export-an-accounts-private-key/). Once you’ve securely copied your private key, proceed to initialize the Docker containers using the commands provided below.

You have two options to start the Lilypad setup: using Docker Compose or directly pulling the image. Both methods will run the containers in the background, allowing you to continue using your terminal while the setup operates.

### Docker Compose

#### Download the Docker Compose file

Use `curl` to download the `docker-compose.yml` file from the Lilypad GitHub repository.

```bash
curl -O -s https://raw.githubusercontent.com/Lilypad-Tech/lilypad/refs/heads/main/docker/docker-compose.yml
```

#### Prepare to start the Containers

{% hint style="warning" %}
If any containers named `resource-provider`, `ipfs`, or `watchtower` are already in use, they will need to be stopped before running this setup to avoid naming conflicts.
{% endhint %}

You can check if these containers are running with:

```bash
docker ps -a | grep -E "resource-provider|ipfs|watchtower"
```

If they are running, stop them with:

```bash
docker stop <container_name>
```

If there are still conflicts when trying to running with the docker-compose file, remove the containers:

```bash
docker rm <container_name>
```

#### Start the Lilypad Containers

Once any existing conflicts are resolved, start the Lilypad containers by providing your Web3 private key:

```bash
WEB3_PRIVATE_KEY=<your_private_key> docker compose up -d
```

### Docker Image

#### Run the Docker Image <a href="#heading-run-the-docker-image" id="heading-run-the-docker-image"></a>

Important: Safeguard your private key with proper key management practices. This key is crucial for managing resource providers' proof of work, tracking rewards, and other vital functions. Never share or expose it.

To run the Lilypad services in a container as a background process, replace \<your\_private\_key\_here> with your actual private key and execute the following command:

```sh
docker run -d --name lilypad-resource-provider --gpus all -e WEB3_PRIVATE_KEY=<private key> --restart always ghcr.io/lilypad-tech/resource-provider:latest
```

To add your own RPC URL, run add the `WEB3_RPC_URL` as an environment variable and set the URL:

```sh
docker run -d --gpus all -e WEB3_PRIVATE_KEY=<private-key> -e WEB3_RPC_URL=wss://arb-sepolia.g.alchemy.com/v2/some-id-from-alchemy --restart always ghcr.io/lilypad-tech/resource-provider:latest
```

#### Enable Automatic Updates

To automatically monitor and update the Lilypad resource provider container, you can use lilypad-watchtower. It ensures the container is kept up to date by periodically checking for new image versions.

Run the following command to start lilypad-watchtower:

```sh
docker run -d --name lilypad-watchtower --restart always -v /var/run/docker.sock:/var/run/docker.sock containrrr/watchtower lilypad-resource-provider --interval 300
```

When you want to check the logs, run the following command:

```bash
docker logs -f --tail 50 lilypad-resource-provider
```

If everything has ran successfully, you will see logs from your terminal. You can copy your web3 public address from MetaMask and paste it in to the [Lilypad Leaderboard](https://info.lilypad.tech/leaderboard) or [GPU dashboard](https://gpu.lilypad.tech/) to view if your node is online and running!

#### View node status

Use the following command to check the status of the Lilypad Resource provider.

```bash
docker logs lilypad-resource-provider
```

## View Lilybit\_ rewards

To view your Lilybit\_ rewards, visit one of the following dashboards and paste your node's public address into the input:

* [Grafana dashboard](https://grafana.lilypad.tech/d/adxhou3o1q8sga/rewards-per-wallets?orgId=1\&refresh=1m)
* [Lilypad ](https://info.lilypad.tech/leaderboard)

## Troubleshooting

Here are some common troubleshooting techniques when it comes to your resource provider using Docker:

**Checking Docker Runtime**\
To verify your Docker runtime configuration: `sudo docker info | grep Runtimes`

You should see the NVIDIA runtime listed. If you only see: `Runtimes: io.containerd.runc.v2 runc` you will need to configure the NVIDIA runtime.

**Configuring NVIDIA Runtime**\
If the NVIDIA runtime is not showing up or you're experiencing issues, try the following:

1\. Configure the NVIDIA Container Toolkit runtime: `sudo nvidia-ctk runtime configure --runtime=docker`\
2\. Restart the Docker service: `sudo systemctl restart docker`

**Overview of Docker setup**\
For a comprehensive overview of your Docker setup, use: `docker info`. This command provides detailed information about your Docker daemon configuration.
