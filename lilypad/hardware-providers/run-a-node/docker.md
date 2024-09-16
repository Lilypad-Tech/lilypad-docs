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

To set up your environment for running a Lilypad Resource Provider, you'll need to install and configure several key components.&#x20;

### Pull the pre-built Docker image

The pre-built Docker image is a crucial component in setting up your Lilypad Resource Provider with this approach. It encapsulates the environment in which your node will operate, including all necessary dependencies, configurations, and commands to run the Lilypad services.

Before pulling the image, you must be logged in to Docker by running `docker login` and follow the prompts.

In the root directory of the Lilypad repo, run the following command to pull the pre-built Docker image:

```bash
docker pull ghcr.io/lilypad-tech/resource-provider:latest
```

## Usage <a href="#heading-run-the-docker-image" id="heading-run-the-docker-image"></a>

Before we run the Docker image, we will need to retrieve the private key from your wallet you set up in the first steps of this guide. You can find out how to do that using this official MetaMask guide for [exporting your private key](https://support.metamask.io/managing-my-wallet/secret-recovery-phrase-and-private-keys/how-to-export-an-accounts-private-key/). Once you've copied your private key we can move on and run the Docker image.

### Run the Docker Image <a href="#heading-run-the-docker-image" id="heading-run-the-docker-image"></a>

Please keep this private key safe and practice safe key management, as it will be primarily responsible for keeping track of the resource providers' proof of works and tracking rewards, amongst other things. Never expose or share it!

Replace `<your_private_key_here>` with your actual private key and run the following command:

```bash
docker run -d --gpus all -p 1234:1234 -e WEB3_PRIVATE_KEY=<private key> --restart always 
ghcr.io/lilypad-tech/resource-provider:latest
```

This will run the Lilypad services in a container in the background. You can get the container ID by running `sudo docker ps`. To check the logs of the Lilypad services, run `docker logs <container ID>`. You can also add a tail to the logs by running `docker logs -f --tail <number of lines> <container ID>`.

Here is an example of what they might look like with 10 log lines:&#x20;

```bash
docker logs -f --tail 10 2a7a74f133c1
```

Alternatively you can name your container explicitly when running it using the `--name` flag, like in your example:

```bash
docker run -d --name lilypad-resource-provider --gpus all -p 1234:1234 -e WEB3_PRIVATE_KEY=<private key> --restart always ghcr.io/lilypad-tech/resource-provider:latest
```

When you want to check the logs, you do not have to reference the container ID, you can simply reference the name you set. In this case it is `lilypad-resource-provider`:

```bash
docker logs -f --tail 10 lilypad-resource-provider
```

If everything has ran successfully, you will see logs from your terminal. You can copy your web3 public address from MetaMask and paste it in to the [Lilypad Leaderboard](https://info.lilypad.tech/leaderboard) or [GPU dashboard](https://gpu.lilypad.tech/) to view if your node is online and running!

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

