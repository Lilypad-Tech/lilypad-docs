---
description: Trustless Distributed Compute for web3
---

# Overview

Lilypad is a powerful trustless distributed compute platform which leverages [Bacalhau](https://docs.bacalhau.org) and key features of blockchain to enable developers to call arbitrary verifiable compute jobs directly from their smart contracts!\


## Applications

The ability to perform off-chain decentralised compute over data from smart contracts opens the door to a multitude of possible applications including:

* Inference AI jobs
* ML training jobs
* Invoking & supporting generic ZK computations
* Cross-chain interoperability complement to bridge protocols
* Utilising inbuilt storage on IPFS
* Federated Learning consensus (with Bacalhau insulated jobs)
* IOT & Sensor Data integrations
* Providing a platform for Digital twins
* Supply chain tracking & analysis
* ETL & data preparation jobs

## Testnet Implementations

\
Lilypad v1 is currently in early testnet phase and is a custom implementation of the ideas & code contained in the paper: "[Mechanisms for Outsourcing Computation via a Decentralized Market](https://dl.acm.org/doi/pdf/10.1145/3401025.3401737)", which proposed a mediator approach to resolving consensus of deterministic jobs, and also offers insights into running non-deterministic jobs.&#x20;

{% hint style="info" %}
See the [whitepaper.md](../research-and-vision/whitepaper.md "mention") for more info
{% endhint %}

<div data-full-width="true">

<figure><img src="https://lh6.googleusercontent.com/xYT2ks14GGyNWZyvh3sPbbr-phCDqRYkJfrgiYFPgsSPHhgfBK-NR8CnuyYfblqiN4YzI0BSAPh6H4gAHcTMbjeZuvnEssYdCRYItFmL8VEZ9ek_pI79UqO7IApurjYv7ZRtDfQhbpWXGzmKWErDkhkxRg=s2048" alt=""><figcaption><p>Modicum Proposed Architecture</p></figcaption></figure>

</div>

Currently, two testnets are functional, both of which use trusted nodes for running arbitrary compute jobs in a deterministic environment.

1. **Lalechuza** - a testnet built on geth
2. **Larana** - a testnet built on Filecoin [IPC](https://ipc.space) (an advanced scaling solution for blockchain that implements a subnet pattern)

