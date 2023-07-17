---
description: Lilypad v1 Litepaper
---

# Litepaper

{% hint style="info" %}
This is a living document.&#x20;
{% endhint %}

## Introduction

"Distributed computing could unlock the next generation of models and applications if brought online properly. However, despite decades of existence, distributed computing platforms using consumer hardware, like BOINC, have become overshadowed by the giants of the tech industry. For companies and researchers, this has resulted in higher costs, vendor lock-in, and in some cases, insufficient resiliency and redundancy. Additionally, the lost potential has been enormous; mountains of underused hardware have piled up in e-wastelands, with associated massive overproduction of hardware and much higher costs, and countless potentially transformative scientific projects were abandoned in their infancy. What is to be done?\


### Blockchains and Off-Chain Compute

Blockchains achieve security by having many nodes execute the same operations and achieve consensus using Byzantine Fault Tolerant (BFT) algorithms. While there is movement towards cryptographic security based on zero knowledge proofs (ZKPs), these methods are still in their infancy and have a very high overhead, the benefit of which is the publishing of short proofs on-chain that can be easily verified by many nodes. Crucially, blockchain environments require global consensus - that is, all nodes must agree on the state of the state machine. However, there are many applications where only local consensus is necessary (like two-sided marketplaces) - that is, only a subset of nodes, maybe even only one, needs to be convinced by the output of a computation. In such cases, the computational overhead is much lower, as it avoids replication by many nodes, and the high computational cost of of ZKPs.



In most real-world applications today, these computations are either done locally, or using the services of major cloud providers. However, these options come with trade-offs, such as managing hardware locally (in the former option) and higher costs. Additionally, while centralized providers are generally considered to be trusted third parties, verification costs can be high when relying on other centralized providers. Furthermore, proving that there has been malicious behavior on the part of a centralized provider is difficult without reliable provenance of inputs and outputs of jobs.

### Bacalhau

Bacalhau is an open source distributed computing platform originally developed at Protocol Labs. It is a modern, high-performing platform with the central mission of bringing compute to data. It is governed by a foundation, just like Linux, Docker, and other major open source software projects. Bacalhau aims to become the Linux of distributed computing. It can run arbitrary Docker containers and WASM workloads over arbitrary data.\


### Lilypad

Lilypad is a trustless distributed computing platform built on Bacalhau, leveraging key features of blockchains to enable developers to call arbitrary computation from smart contracts. Lilypad aims to become the standard distributed computing platform for all blockchains and distributed ledger technologies to come.

## Testnet and Modicum

We are designing novel implementations for anti-cheating mechanisms and pricing models, described in the following section. To build an initial testnet, Modicum was used as a base implementation, as it provided an already-functioning codebase that implemented much of the logic of two-sided computation marketplaces managed by blockchains and smart contracts.\


The original version of Modicum had five key components: Job Creators (JC), Resource Providers (RP), Solvers (market makers), Mediators (agreed-upon third parties for mediation), and Directories (file systems). Job Creators are clients, the ones who have computations that need to be done and are willing to pay. Resource Providers are those with computational resources that they are willing to rent out for the right price. Solvers are market-makers; they match the offers from JCs and RPs. Mediators are third parties trusted by both JCs and RPs to arbritrate disagreements. The directories are network storage services available to both JCs and RPs.\


There are a number of issues with Modicum that we needed to address for our v1 testnet, and more that we will have to address in the future. First, there are substantial improvements that can be made to the Mediator architecture. The Mediator exists to check for non-deterministic tasks submitted by the JC (which can be used by the JC as an attack vector to get free results), and fake results returned by the RP. However, Modicum entangles what should be two separate ideas: checking the result from a RP to see if it is correct, and checking a result from a job submitted by a JC to see if the job was deterministic or not. That is, there is no capability for a client to simply check whether a result is correct or not, without the possibility of its collateral being slashed. Furthermore, the method for determining whether a job is deterministic or not is for the Mediator to run a job n times and check to see whether it receives different answers. Intuitively, this can be replaced by n Mediators each running the tasks a single time, which leaves far less room for manipulation. Additionally, we have enforced determinism in other ways, so this attack vector is prevented from a technical perspective, and there is no slashing of client collateral.



Furthermore, the issue of collusion (the RP and Mediator colluding to return a fake result) is not addressed by this protocol. However, it can be addressed either by relying on smart contract counter-collusion protocols (see "Betrayal, Distrust, and Rationality: Smart Counter-Collusion Contracts for Verifiable Cloud Computing"), or by replacing the Mediator with a consortium as described above and assuming a traditional Byzantine environment (in fact, if only one node is honest, and is willing to put stake behind its claims, then collusion attacks are far less threatening). For our initial testnet, we assume that the Mediator is a Trusted Third Party (TTP), and plan to upgrade this in our next version.\


As a minor note, a JC or RP can remove a Mediator from their list of trusted Mediators if they no longer trust it, but that still leaves room to cheat at least once, which is a situation that should be disincentivized from the outset.\


There is also the issue of collateralization. The Modicum protocol, as well as a number of other protocols, assume approximate guesses as to the cost of jobs in advance, so that RPs can deposit the correct amount of colleratal, which is to be slashed if they are found to have cheated. While we have substantially improved this model, we have not yet implemented it in our testnet. For now, we are assuming fixed prices per jobs across all compute nodes. Intuitively, if a RP is checked for cheating 1\\% of the time for a repeated fixed price type of job, and it is cheating, then it will be caught in expectation after 100 jobs (by the properties of the geometric distribution). Thus, the RP would have to post 100 times the fixed cost of a job in order to disincentivize cheating. While the economics of collaterization is necessarily much more complex, we start with this simple version.\


## Verification: Autonomous Agents, Anti-Cheating Mechanisms, and Pricing Models

How are tasks verified? While Bacalhau will support trusted execution environments (TEEs) and ZKPs, the primary method it will use is verification-via-replication, or optimistic compute. In simple terms, compute nodes (and clients, which will be discussed later) put up collateral as insurance that they will compute tasks correctly, and have that collateral slashed if they are found to have been cheating. The precise methodology for doing this has been approached from a number of different angles (for just a few, see X, Y, Z). We provide a brief description here, with the full details to be published in a separate document.\


At its core, the issue is one of incentive-compatibility. Most protocols designed to mitigate cheating assume rational, utility-maximizing agents, which for the most part, do not exist in real life. However, they can be designed using autonomous agents and reinforcement learning. If autonomous agents can be trained to act in a utility-maximizing manner, and simultaneously, the protocol/game can be designed to disincentive cheating by occasionally verifying work, then this would be a robust verification-via-replication based distributed computing platform. This approach draws inspiration from the revelation principle, a core concept in mechanism design, which basically states that under some conditions, any allocation mechanism to which agents are submitting preferences can be modified so that agents are incentivized to submit their true preferences.\


Likewise, the presence or absence of different modules (such as Prisoner's Contracts, post-task collateral staking, etc.) can improve or undermine the success of the protocol in successfully disincentivizing cheating.\


While this paradigm is being used primarily to design anti-cheating mechanisms and pricing models, it also has implications for scheduling, as these autonomous agents will in effect be scheduling compute jobs on behalf of clients.\


### Defense in Depth

Defense in Depth is a widely used concept in a variety of computational fields. Due to its robust capabilities and flexible architecture, Bacalhau can provide many layers of security, with optimistic compute, TEEs, and ZKPs, and support for other cryptographic protocols to come.\


## Applications

### Artificial Intelligence

As AI, especially generative AI, has exploded in the past year, the interest in combining blockchain technology and artificial intelligence has surged. Bacalhau is currently the best option for invoking a generic AI inference task from a smart contract.\


The possibilities go far beyond AI inference (and training). The autonomous agents that represent nodes must be aligned with human (and ideally planetary) interests. Furthermore, looking beyond worst-case behavior to average-case behavior and benevolent/altruistic behavior, these autonomous agents can act in a cooperative manner in order to achieve many different goals, as exemplified by the emerging field of cooperative AI.\


### Zero Knowledge Proofs

The explosive growth of blockchains in the past decade has prompted and massively accelerated the research and development of zero-knowledge proofs. Much of the focus of ZKPs development for blockchains has been focuses on ZK-rollups, privacy-preserving transactions, and so on. While there is much interest in other applications, like zero-knowlege machine learning (ZKML), there is currently no way to invoke a generic ZK computation from a blockchain. Bacalhau already supports Filecoin data onboarding, which is the single largest use of ZKPs in the world in terms of computational power and financial payments, and has recently become a major provider of data onboarding services. Since Bacalhau supports arbitrary compute over arbitrary data, it will also be able to support generic ZK computations, making it the first platform that supports generic ZK computations in combination with arbitrary compute.\


### Bridges

Bridges have been the topic of much attention in the blockchain world for a number of years. Cross-chain interoperability is a challenging task, as exemplified by the many hacks of such protocols. As a distributed computing standard, Bacalhau can provide a unified codebase upon which to build bridge protocols. It can complement existing bridge protocols, including ambitious ones like zkBridge, as well as provide a platform for developers to build their own.\


Additionally, most blockchains do not have built-in storage protocols. Bacalhau has the native ability to take IPFS CIDs as inputs, meaning it can provide arbitrary compute over arbitrary data in a totally distributed manner.  \


### Federated Learning

Federated learning is in its infancy, poised to become a massive industry in the coming decade. Many applications of federated learning still require consensus over outputs and aggregation of information - a task well suited for blockchains. With Bacalhau's built in functionalities for federated learning (called insulated jobs), core mission of bringing compute to the data, and cross-chain smart contract compatibility, developers will be able to deploy their own federated learning algorithms with much lower overhead.



### Sensor Data

Bacalhau's mission for bringing compute to the data enables practitioners to use sensor data such as weather/temperature/pressure data, air quality and CO2 measurements, radar/sonar/lidar data, satellite imagery, and others, compute over it locally, automatically cross-check for accuracy and anomalies using blockchains for consensus (where applicable), and open up new use cases in the process. For example, environmental data gathered by drones is becoming increasingly valuable for climate change tracking, forest fire and other natural disaster mitigation, search and rescue operations, and so on. With enough processing power on board, drones can compute over data locally and send only what is needed to centralized servers or distributed ledgers, whichever is more applicable.\


### Mobile User Data

Most consumers today do not directly profit from their data - at best, they receive free services in return for giving up their data. While this is slowly changing due to regulation, businesses have been slow to design their profit models to enable their users to profit from their own data. Similarly to sensor data, verifiably crowd-sourcing information in real-time opens up many possibilities in traffic control, public transport congestion, mesh networks, and many other areas.\


For example, there has been much research in cooperatively owned and blockchain-governed self-driving cars that substantially reduce overall costs for consumers.\


### Digital Twins

Digital twins are projected to become much more prevalent in the coming years, scaling to an industry in the billions of dollars. Many digital twins model cyber-physical systems. Bacalhau and Lilypad can together provide both a platform for the construction and simulation of digital twins, as well as operate elements of the digital twins (e.g. compute nodes). Harking back to the autonomous agents, sensor data, and mobile user data, Bacalhau can provide a seamless platform for integrating these components.\


### Supply Chain

Supply chain management has long been considered a valuable use-case for blockchains. With Bacalhau and Lilypad, the tracking of goods along the supply chain can be augmented with arbitrary compute, enabling new use cases.

### Public Goods Computing

Prior distributed computing projects such as BOINC demonstrated the popularity and feasibility of volunteer computing for scientific projects, which are in effect a public good. Early cryptocurrencies such as Gridcoin attempted to crypto-economically incentivize participation in BOINC, and while achieving many successes (for example, having among the most nodes and being the most decentralized cryptocurrencies, as well as having an organic and passionate community), failed to achieve its long-term vision, including increasing participation in volunteer scientific computing. However, with modifications and improvements, the pitfalls of BOINC and Gridcoin can be avoided, and their original missions driven forward.

### Hardware Profiling

Hardware profiling plays an important role in the tech and software engineering industries. Bacalhau/Lilypad can easily enable the largest and most robust hardware profiling database in the world. Such a database can be used by scientists, researchers, consumers, hardware enthusiasts, and tech companies, large and small, to better enable their purchasing choices.

### Compute Sharing and Cooperatives

Following up on hardware profiling, it is clear that some machines are better suited for some tasks than others. Machines can pool their resources together in order to derive higher revenue for all, and in the case of public good computing, can balance their preferences over projects with their machines' capabilities (for example, with Top Trading Cycles, though more advanced algorithms are constantly being developed).

### Data Prep/ETL

Bacalhau/Lilypad has already demonstrated the ability to handle the transformation and onboarding of colossal amounts of data for the Filecoin ecosystem.

### Privacy

The issue of private computations is especially tricky in permissionless and trustless distributed computing environments. While TEEs and homomorphic encryption provide solutions to this problem, they are not fully mature technologies capable of providing the same level of efficiency and trust as centralized cloud providers. For the time being, Bacalhau/Lilypad will use symmetric/asymmetric encryption in order to assure clients that only compute providers could see their data, unless the latter decided to leak it.



## Revenue and Profit

### Fee-based Model

The simplest way to generate revenue is to take a fee for every job executed by the network (which can optionally be waved for public goods projects). This has a number of advantages over launching a network token, namely that it maintains the Lilypad's chain-agnosticism, makes it clear to each L1/L2 that the project only increases demand for its native coin/token, and avoids complicated regulatory issues.

### Liquidity Providers in DeFi Protocols

If the revenues from fees aren't sold or invested in some other way, an immediate way to put them to use is by providing liquidity to DeFi protocols.

### Community and User Ownership

A truly decentralized protocol would be owned by its stakeholders - the communities and users who rely on its services. Thus, over the long-term, it would be necessary for ownership over the protocol to become widely dispersed. This still presents a massive financial opportunity during the growth of the protocol, but in order to stay true to its principles, ownership would have to become distributed.

### Investing in Distributed Computing Projects

As the network matures, the network will accrue reserves of many different cryptocurrencies and tokens. Due to prior efforts to bootstrap widespread adoption and make Bacalhau/Lilypad the standard distributed computing platform, the capital reserves and deep in-house knowledge will enable the network to begin investing in distributed computing projects built on top of the protocol. Thus, in a manner similar to how Amazon and Google invest in, and give free computing credits to, startups which use their platforms, Bacalhau/Lilypad can provide similar investments and services to Web3 startups.\


## Conclusion

The space is ripe for the taking. Are you in?

\
\
\
