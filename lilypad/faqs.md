---
description: Frequently Asked Questions for Lilypad Network
---

# ⚡ FAQs

## 🍃 General Questions

### What is the Lilypad Network?

Lilypad is developing a serverless, distributed compute network that enables internet-scale data processing for AI, ML & other arbitrary computation from blockchains, while unleashing idle processing power & unlocking a new marketplace for compute.

Lilypad provides decentralized AI computational services. By extending unrestricted, global access to computational power, Lilypad strategically collaborates with decentralized infrastructure networks, such as Filecoin, to formulate a transparent, efficient, and accessible computational ecosystem.&#x20;

Perform off-chain decentralized compute over data, with on-chain guarantees, and to call this functionality directly from a smart contract, CLI and an easy to use abstraction layer, opens the door to a multitude of possible applications.

### Lilypad Litepaper

Lilypad released a [Litepaper](https://docs.lilypad.tech/lilypad/research-and-vision/whitepaper) and will release a Whitepaper soon!

### Roadmap

Lilypad Network is currently in Testnet. The team is currently ironing out some remaining known issues and working on a fair model for our Incentivized Testnet.

Find the full Lilypad Network [roadmap](https://lilypad.tech/roadmap.html) on our website!

<figure><img src=".gitbook/assets/Roadmap.png" alt=""><figcaption></figcaption></figure>

### Wait, didn’t Lilypad used to rely on determinism and optimistic reproducibility for verifiable compute?&#x20;

Previously, Lilypad required deterministic jobs on the network and used optimistic reproducibility to randomly re-run jobs to ensure trust, however this method has been deprecated due to:

1. the limitation the determinism requirement placed on what jobs were available to run on the network
2. the inability to realistically be able to determine a “deterministic” job to be deterministic easily

### Has Lilypad raised VC money?

Yes, Lilypad closed our seed round of funding in March 2024.

## 🌐 Incentivized Testnet Questions

### When will the Incentivized Testnet launch?

The Lilypad Incentivized testnet is on track to launch by the end of June 2024. Stay tuned on [the Lilypad Discord](https://lilypad.team/discord) for more info!

### How do LilyBit\_ rewards work?

Lilybit\_ rewards will be awarded to nodes for time on the network (up to a 4x multiplier) and compute power brought to the network. Rewards will be redeemable, for the Lilypad ERC20 Utility Token at Mainnet Launch, with between 5% and 10% of the total token supply (depending on IncentiveNet demand and tokenomics finalization) being allocated to this phase of the Lilypad Network.

### Who can earn LilyBit\_ rewards

Phase 1 of the Incentivized Testnet is focused on rewarding nodes on the network, referred to as Resource Providers. The earlier a provider joins the network, the more Lilybits\_ will be available.

Phases 2 and onward will provide rewards for Lilypad modules created as well as developer tools/apps (in addition to rewarding nodes)

## ⚙️ Hardware Provider Questions

### What do I need to do before I can run a Lilypad node?

The required steps before running a Lilypad node include adding the node, adding the Lilypad network information, obtaining tokens and installing the required software.

Refer to the [Running a Node](broken-reference) documentation for a detailed guide on the prerequisites.

### What are the hardware requirements to run a Lilypad node?

The minimum hardware requirements to run a Lilypad node are:

* **Processor**: Quad-core x64 Processor
* **RAM**: 16GB (see additional details below)
* **Internet**: 250Mbps Download Speed
* **GPU**: NVIDIA GPU with a minimum of 8GB VRAM (see additional details below)

For more information, please visit [Hardware Requirements](hardware-providers/hardware-requirements.md).

### What are the updates required for maintaining my node software?

Resource providers are expected to have the latest Lilypad versions installed on their machines.&#x20;

The instructions can be found in our [installation documentation](lilypad-testnet/install-run-requirements.md).

### How can I check the status of my Lilypad node?

To check if the RP is running use the following command: `sudo systemctl status lilypad-resource-provider`.

This will give a live output from the Lilypad node. The logs will show the node running and accepting jobs on the network. To get more information from your node, run the following: `sudo journalctl -u lilypad-resouce-provider.service -f`

Find more information in [Running a Node](hardware-providers/run-a-node.md).

## 👩‍💻 Developer Questions

### What is a Lilypad Module?

To run a ML model like Stable Diffusion on Lilypad, the model must be setup as a Lilypad Module (see instructions below). Once setup, modules are run with the Lilypad [CLI](https://docs.lilypad.tech/lilypad/lilypad-milky-way-testnet/install-run-requirements).

### How to run a ML job on Lilypad

To run a ML job on Lilypad (Stable Diffusion, Mistral 7b, Stable Diffusion Video, and more) using the Lilypad CLI, follow the [CLI instructions](https://docs.lilypad.tech/lilypad/lilypad-milky-way-testnet/install-run-requirements) to get started.&#x20;

To build an application with Lilypad compute and modules on the backend, check out this [guide](https://blog.lilypadnetwork.org/setting-up-your-lilypad-front-end).

### How to add a ML model to run on Lilypad

A Lilypad module is a Git repository that can be used to perform various tasks using predefined templates and inputs. This ["build a job module" guide](https://docs.lilypad.tech/lilypad/lilypad-milky-way-reference/build-a-job-module) will walk you through the process of creating a Lilypad module, including defining a JSON template, handling inputs, ensuring determinism, and other best practices.

### How to run a Lilypad node

Lilypad is an open network that allows anyone to contribute GPU computing capacity. There is currently no cost or incentives for running a Lilypad node. Find [instructions](hardware-providers/run-a-node.md)[ for running a node](hardware-providers/run-a-node.md) in the docs.

### Node hardware specs

* Linux (latest Ubuntu LTS recommended)
* Nvidia GPU
* Nvidia drivers
* Docker
* Nvidia docker drivers

For more information on the requirements to run a Lilypad node, please refer to the [hardware requirements](hardware-providers/hardware-requirements.md) documentation.

## 📖 Token Questions

### Lilypad Tokenomics

Currently, there's no cost to run jobs and no incentive. Tokenomics and research papers are currently being developed and expected by early Q3 2024.&#x20;

### Expected TGE

Although the launch date is not finalized, the launch of Lilypad Mainnet and the TGE for LP tokens is scheduled for Q4 2024.



Can't find the answer you were looking for? Join [the Lilypad Discord server](https://lilypad.team/discord) for live support! 🪷
