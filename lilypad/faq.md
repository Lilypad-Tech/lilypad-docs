---
description: Frequently Asked Questions for Lilypad Network
---

# ❓ FAQ

## 🍃 General Questions

### What is the Lilypad Network?

Lilypad is developing a serverless, distributed compute network that enables internet-scale data processing for AI, ML & other arbitrary computation from blockchains, while unleashing idle processing power & unlocking a new marketplace for compute.

Lilypad provides decentralized AI computational services. By extending unrestricted, global access to computational power, Lilypad strategically collaborates with decentralized infrastructure networks, such as Filecoin, to formulate a transparent, efficient, and accessible computational ecosystem.

Perform off-chain decentralized compute over data, with on-chain guarantees, and to call this functionality directly from a smart contract, CLI and an easy to use abstraction layer, opens the door to a multitude of possible applications.

### Lilypad Whitepaper

The Lilypad Whitepaper was planned to release by end of Q4 2024, but required further review from our team and advisors. See our [roadmap](https://lilypad.tech/#roadmap) for the current timeline.

### Roadmap

Find the full Lilypad Network [roadmap](https://lilypad.tech/#roadmap) on our website!

### What is the Bacalhau Project?

Bacalhau is a peer to peer computation network enabling compute over data jobs like GPU-enabled AI, ML, analytics, data engineering, data science, de-sci and more.\
\
With the open-source Bacalhau Project, you can streamline your existing workflows without rewriting by running Docker containers and WebAssembly (WASM) images as tasks. This architecture is also referred to as **Compute Over Data** (or CoD).

* To find out more about it, see the [Bacalhau Docs](https://docs.bacalhau.org/)

### Wait, didn’t Lilypad used to rely on determinism and optimistic reproducibility for verifiable compute?

Previously, Lilypad required deterministic jobs on the network and used optimistic reproducibility to randomly re-run jobs to ensure trust, however this method has been deprecated due to:

1. The limitation the determinism requirement placed on what jobs were available to run on the network
2. The inability to realistically be able to determine a “deterministic” job to be deterministic easily

### Has Lilypad raised VC money?

Yes, Lilypad closed our seed round of funding in March 2024.

## 🌐 Incentivized Testnet Questions

### When will the Incentivized Testnet launch?

The Lilypad Incentivized testnet launched in mid June 2024.

### How do LilyBit\_ rewards work?

Lilybit\_ rewards will be awarded to nodes for time on the network (up to a 4x multiplier) and compute power brought to the network. Rewards will be redeemable, for the Lilypad ERC20 Utility Token at Mainnet Launch, with between 5% and 10% of the total token supply (depending on IncentiveNet demand and tokenomics finalization) being allocated to this phase of the Lilypad Network.

Resource Providers (RP) can track their Lilybit\_ earnings with the [RP Leaderboard](https://info.lilypad.tech/leaderboard).

### Who can earn LilyBit\_ rewards?

Phase 1 of the Incentivized Testnet is focused on rewarding nodes on the network, referred to as Resource Providers. The earlier a provider joins the network, the more Lilybits\_ will be available.

Phases 2 and onward will provide rewards for Lilypad modules created as well as developer tools/apps (in addition to rewarding nodes).

### How do I check my Lilybit\_ rewards?

You can check your rewards by pasting your nodes wallet address into the following interfaces:

* [Grafana dashboard](https://grafana.lilypad.tech/d/adxhou3o1q8sga/rewards-per-wallets?orgId=1\&refresh=1m)
* [Lilypad leaderboard](https://info.lilypad.tech/leaderboard)
* [Open Source contributor dashboard](https://oss.lilypad.tech/)

### How does Lilypad use blockchain, and why do I need both ETH and Lilypad tokens to run a job?

On the Lilypad network, The blockchain is used for

* Payment rails
* Storing the deals transparently (on-chain guarantees about the compute)
* Storing any disputes & results

Lilypad Tokens are used to transact on the Lilypad network. They are used as payment by those who want to run jobs (to the resource providers who run them), and as collateral by resource providers.

You need ETH tokens to pay for the gas fees for smart contracts the facilitate transactions, and for records of transactions and disputes that are posted to the Ethereum blockchain.

## ⚙️ Hardware Provider Questions

### What do I need to do before I can run a Lilypad node?

The required steps before running a Lilypad node include adding the node, adding the Lilypad network information, obtaining tokens and installing the required software.

Refer to the [run-a-node.md](resource-providers/run-a-node.md "mention") documentation and select your preferred platform (Linux or Docker) for a detailed guide on the prerequisites.

### What are the hardware requirements to run a Lilypad node?

For more information, please visit [hardware-requirements.md](resource-providers/hardware-requirements.md "mention").

### What are the updates required for maintaining my node software?

Resource providers are expected to have the latest Lilypad versions installed on their machines. These will be included in the Docker files in each release. For more information, please refer to the [Resource Provider docs](broken-reference).

### How can I check the status of my Lilypad node?

Find more information check out the [Run a node](resource-providers/run-a-node.md) docs.

## 👩‍💻 Developer Questions

### What is a Lilypad Module?

View the [Modules section](developer-resources/module-marketplace/).

### How to run a ML job on Lilypad

Follow the [quickstart guides](quickstart/) to get started.

To build an application with Lilypad compute and modules on the backend, check out this [guide](https://blog.lilypadnetwork.org/setting-up-your-lilypad-front-end).

### How to add a ML model to run on Lilypad

A Lilypad module is a Git repository that can be used to perform various tasks using predefined templates and inputs. This ["build a job module" guide](https://docs.lilypad.tech/lilypad/developer-resources/build-a-job-module) will walk you through the process of creating a Lilypad module, including defining a JSON template, handling inputs, ensuring determinism, and other best practices.

### How to run a Lilypad node

Lilypad is an open network that allows anyone to contribute GPU computing capacity. Find instructions for running a node in our [run-a-node.md](resource-providers/run-a-node.md "mention") documentation.

### Node hardware specs

* Linux (latest Ubuntu LTS recommended)
* Nvidia GPU
* Nvidia drivers
* Docker
* Nvidia docker drivers

For more information on the requirements to run a Lilypad node, please refer to the [hardware requirements](resource-providers/hardware-requirements.md) documentation.

## 📖 Token Questions

### Expected TGE

Although the launch date is not finalized, the launch of Lilypad Mainnet and the TGE is scheduled for 2025.
