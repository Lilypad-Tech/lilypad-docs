---
description: 'Lilypad: A Protocol for Open Intelligence Infrastructure'
---

# Lilypad Litepaper

***

### Building the Infrastructure for an Open AI Economy

#### Abstract

Lilypad is a coordination protocol for intelligence infrastructure. It provides permissionless access to verifiable compute, model monetization by default, and cryptographically auditable execution for any AI workload. Lilypad abstracts compute primitives into a modular, trust-minimized protocol that can serve inference, agents, and pipeline-based workflows across open and enterprise systems.

This paper outlines the core thesis, architectural structure, cryptoeconomic system, and forward-looking roadmap for Lilypad. Our goal: to create a programmable substrate that supports open AI as a public good—and enables the next era of agentic computation, composable intelligence, and developer-owned ecosystems.

***

### 1. Introduction: Infrastructure Shapes Intelligence

From Turing’s foundational thought experiments to the cloud boom of the 2000s, compute has mirrored—and magnified—our evolving social architectures. Each leap in processing capability has triggered new markets, new models of coordination, and new vulnerabilities. And now, with AI becoming not just an application layer but a decision substrate, the question isn’t just what we build—but where, and who gets to participate.

We’re at a convergence point of three arcs:

* The **Arc of Compute**—from mainframes to hyperscale cloud to edge devices, with increasing decentralization and specialization at the hardware layer.
* The **Arc of AI**—from statistical tooling to foundational models to agentic systems running autonomous workflows.
* The **Arc of Coordination**—from institutionally brokered trust to cryptographic primitives, on-chain settlement, and composable economic logic.

Lilypad sits at the intersection of these arcs.

We treat infrastructure not as a neutral backend, but as a system of encoded values: who can build, who gets paid, and what rules apply.

Today’s centralized AI infrastructure imposes extractive defaults:

* Compute access intermediated by monopolistic brokers
* Models abstracted behind opaque APIs
* No native attribution, provenance, or monetization

Lilypad offers a counter-architecture: modular, verifiable, permissionless. It builds a trustless execution layer where models can be exposed, reused, and paid on-chain. Not to replace existing systems, but to reroute economic gravity back toward creators and contributors.

The result is not just infrastructure. It’s a programmable substrate for intelligence—one that expands access, reinforces agency, and creates new terrain for open coordination.

We call this: compute as protocol.

The generative AI boom has surfaced a clear reality: inference is cheap, unless you’re running it. Models are open, until you try to use them at scale. Infrastructure is accessible, until you read the fine print—or the bill.

At the base of the stack, centralized coordination remains the bottleneck:

* Compute access is intermediated by hyperscalers and brokers.
* Models are hosted behind permissioned APIs.
* There’s no native mechanism for attribution, remixing, or payment.

We believe infrastructure dictates the rules of economic participation. Today’s systems are extractive, brittle, and opaque. But it doesn’t have to be that way.

Lilypad exists to provide an alternative: a modular, permissionless, and verifiable infrastructure protocol where anyone can:

* Upload and earn from their models
* Execute inference and pipelines across a distributed GPU mesh
* Prove job completion, pricing, and origin—all on-chain

Our goal is not to replace cloud platforms. It’s to make them optional.

***

### 2. Design Philosophy

Lilypad’s architecture is informed by a decade of experiments in decentralized compute—Golem, ICP, Modicum, and others. Each made meaningful contributions. But each hit a wall.

Golem struggled with adoption and required determinism at the cost of generality. ICP's compute verification model was tightly coupled to protocol consensus, limiting general-purpose task execution. Modicum introduced a promising recomputation-based system, but was constrained by its requirement for deterministic jobs and tightly entangled verifier logic.

We’ve taken lessons from these systems to architect Lilypad differently:

* We decouple verification from execution, enabling multiple verification strategies depending on job type, latency, and value.
* We don’t assume determinism. Instead, we build modularity into verification layers: job hash commitment, attestable logs, mediation, and—eventually—FHE and model fingerprinting.
* We avoid hardwiring compute to consensus. Lilypad coordinates compute jobs via constraint-solving and smart contract validation, not consensus-layer integration.

Most importantly, we do not assume a monolithic trust architecture. We treat verifiability, coordination, and monetization as primitives—not as features.

Lilypad is structured around three core design principles:

1. **Modularity**: Infrastructure should be upgradeable. Each layer of the protocol—from compute to registry to settlement—is designed to evolve independently.
2. **Verifiability**: Every job run should leave a legible, auditable trail. Not all trust needs to be cryptographic—but all trust should be accountable.
3. **Economic symmetry**: Value created by the network should circulate within it. Contributors—whether model authors, solvers, or compute providers—are paid at the protocol level.

Lilypad is not a product wrapper. It’s the infrastructure others will build products on. draws from first principles in distributed systems, cryptographic trust, and programmable coordination. The protocol is structured around three foundational commitments:

1. **Modularity**: Infrastructure should not be bundled. Lilypad is composed of discrete layers—compute, registry, coordination, identity—each designed to be interoperable and forkable.
2. **Verifiability**: Jobs must be traceable and reproducible. We prioritize cryptographic proofs, containerized execution, and open metadata.
3. **Economic symmetry**: Value should flow to contributors by default. Our monetization system routes earnings directly to model creators, node operators, and protocol actors.

We don’t make assumptions about what should be run—only that it should be provable, priced, and portable.

***

### 3. Protocol Architecture

```
┌──────────────────────────────────────────────┐
│              Lilypad Protocol Stack          │
├──────────────────────────────────────────────┤
│         Halo Identity & Auth Layer           │
├──────────────────────────────────────────────┤
│       Ophir Coordination (Smart Contracts)   │
├──────────────────────────────────────────────┤
│          Ampli Model Registry (IP, Metadata) │
├──────────────────────────────────────────────┤
│             Anura Inference API              │
├──────────────────────────────────────────────┤
│         Atlas Compute (Bacalhau / WASM)      │
└──────────────────────────────────────────────┘
```

**Atlas Compute**: Container-based execution using Bacalhau, backed by verifiable job manifests and node-level attestation. Supports WASM and GPU workloads.

**Ampli Registry**: Version-controlled registry for models, modules, and pipelines. Each asset includes signatures, pricing, and lineage.

**Ophir Coordination**: EVM-based contract layer that handles job creation, staking, slashing, and payments. Runs on Arbitrum with upcoming extensions.

**Halo Identity**: Credentialing and authorship framework for model creators, node operators, and agents. Optional enterprise modes and delegated authority.

**Anura API**: Interface layer for querying models, exposing endpoints, and integrating agentic workflows. Compatible with LangChain, OpenRouter, and n8n.

***

### 4. Actors and Execution Flow

Lilypad uses a modular actor model, with responsibilities and incentives structured across roles:

| Role               | Function                                             |
| ------------------ | ---------------------------------------------------- |
| Job Creators       | Submit jobs, define inputs, fund usage upfront       |
| Resource Providers | Execute jobs on local or cloud GPUs, earn per output |
| Module Providers   | Publish reusable pipelines and tools                 |
| Solvers            | Match jobs to compute via constraint solving         |
| Mediators          | Sample and verify job execution correctness          |
| Smart Contracts    | Route payments, validate signatures, update state    |

Jobs follow a lifecycle: submission → matching → execution → optional mediation → payment. All state is auditable, and all components are modular.

***

### 5. Verification and Provenance

Lilypad supports multiple trust layers:

* **Job Hash Commitment**: Each manifest is hashed, signed, and timestamped.
* **Container Logs + Digest**: Output verification via deterministic artifact hashing.
* **Mediation Sampling**: Random audits via Mediator nodes.
* **Model Fingerprinting**: (Planned) support for source-model inference tracking.
* **FHE (planned)**: For fully private AI compute and encrypted inputs.

This composable framework allows Lilypad to balance verifiability and performance for a wide range of use cases.

***

### 6. Economics and Coordination

Lilypad introduces LILY—a fixed-supply token used to route incentives and economic coordination across the protocol. The system is designed to fairly compensate compute providers, model contributors, and protocol participants, while maintaining integrity through collateral and verifiable actions.

#### 6.1 Payment Modes

* **Pay-as-you-go Execution**: JCs fund jobs at submission. If the job is not run, the unused funds are returned automatically. No prepayment subscriptions, no lock-in.
* **Stake-Weighted Routing**: RPs and Solvers are prioritized by stake and historical performance.

#### 6.2 Actor Value and Rewards

Each actor in the Lilypad ecosystem is assigned a dynamic **value function** Vᵢ(t) based on their activity, contributions, and reputation. This value function determines their share of protocol rewards for a given epoch.

Example: Resource Provider Value

V\_RPᵢ(t) = \[ R̄ᵢ^α₁ \* ( Σ Fⱼ(t) )^α₂ \* C̄ᵢ^α₃ ]

Where:

* R̄ᵢ: average reputation of RP over time window W
* C̄ᵢ: average collateral
* Fⱼ(t): fee earned from job j in timestep t
* α₁, α₂, α₃: weight coefficients

Rewards are distributed proportionally:

Rᵢₖ(t) = \[ Vᵢₖ(t) / ΣVᵢₖ(t) ] \* Rₖ(t)

Where:

* Rₖ(t): total reward pool for actor class k in epoch t
* Vᵢₖ(t): value of actor i in class k

#### 6.3 Collateral Mechanics

To accept jobs, RPs must stake a base collateral amount C\_min, which scales with the job price and reputation. For mediation-eligible jobs:

C\_active ≥ ρ × P\_job, where ρ ≥ 2.5

Higher staked collateral improves job routing probability and early unlock of vesting rewards. Failed jobs or dishonest behavior result in slashing.

This system balances:

* Skin in the game for compute providers
* Protections for job creators
* Economic throughput that aligns incentives across the network

Lilypad introduces LILY—a fixed-supply token used to route incentives and economic coordination across the protocol.

#### 6.1 Payment Modes

* **Pay-as-you-go Execution**: JCs fund jobs at submission. If the job is not run, the unused funds are returned automatically. No prepayment subscriptions, no lock-in.
* **Stake-Weighted Routing**: RPs and Solvers are prioritized by stake + reputation.

#### 6.2 Reputation & Value

Each actor has a dynamic reputation score and value metric, used to:

* Filter job preferences
* Prioritize matching
* Allocate protocol rewards

These metrics evolve over time, encouraging consistency and reliability.

***

### 7. Roadmap

Lilypad’s roadmap is structured into three progressive phases:

**Phase 1 – Compute & Coordination (2024)**\
Focus: Deliver verifiable distributed compute and robust economic pipelines for job routing and execution.

| Quarter | Milestone            |
| ------- | -------------------- |
| Q2 2024 | Compute Coordination |
| Q3 2024 | Core Infrastructure  |

**Phase 2 – Provenance & Incentives (late 2024)**\
Focus: Introduce deeper attribution, reputation weighting, and prepare economic systems for model-level incentive routing.

| Quarter | Milestone                                       |
| ------- | ----------------------------------------------- |
| Q4 2024 | SpecLang (DSL for agents), DAG-native pipelines |

**Phase 3 – Interoperability & Governance (2025+)**\
Focus: Expand across chains, decentralize actor control, and scale coordination to support open market formation.

| Quarter | Milestone                                               |
| ------- | ------------------------------------------------------- |
| 2025+   | TrainPad, ForgeNet, provenance APIs, enterprise rollout |

Our primary focus has been to build the compute layer and coordination pipelines with the right economic incentives first. Mainnet features like remix royalties, data provenance bonding, and advanced model attribution will roll out next.

| Quarter | Milestone                                               |
| ------- | ------------------------------------------------------- |
| Q2 2024 | Streaming pipelines, identity v1                        |
| Q3 2024 | Audit tooling, cross-chain relay                        |
| Q4 2024 | SpecLang (DSL for agents), DAG-native pipelines         |
| 2025+   | TrainPad, ForgeNet, provenance APIs, enterprise rollout |

We are currently live on testnet (Arbitrum Sepolia) with >5k jobs/day. Mainnet launch is scheduled for Q3.

Our primary focus has been to build the compute layer and coordination pipelines with the right economic incentives first. Mainnet features like remix royalties, data provenance bonding, and advanced model attribution will roll out next.

***

### 8. Closing: The Coordination Engine for Agentic AI at Scale

Lilypad isn’t an interface or a wrapper—it’s a programmable coordination system for decentralised intelligence infrastructure.

The vision is simple: in a world where thousands of autonomous agents transact, generate, analyse, and interact in real time—Lilypad is the layer they run on. Not just to query models, but to find compute, post jobs, resolve execution, pay each other, and trace provenance.

Imagine swarms of agents coordinating scientific research, synthetic biology design, or decentralised AI-powered search. Not tied to a single provider, but orchestrated across a permissionless GPU network—with cryptographic audit trails, automatic payments, and composable modules.

None of this feels like "crypto" to the end user. Payments settle instantly. Execution is verifiable. Attribution is native. Pricing is driven by the network, not a platform. This is what blockchain makes possible when used correctly—not a feature, but an invisible enabler of open coordination at scale.

Why blockchain matters here:

* **Instant settlement**: No billing cycles. Compute, coordination, and creators are paid atomically.
* **Resilience**: Jobs route across a global mesh, not a single provider.
* **Verifiability**: Cryptographic job manifests, signed results, on-chain records.
* **Provenance**: Model authorship and reuse tracked natively in the registry.
* **Coordination**: Smart contract logic replaces the need for gatekeepers.
* **Distribution**: Actors anywhere can participate—from solo devs to academic labs.

This isn’t speculative infrastructure. This is infrastructure that scales as demand increases, as model ecosystems fragment, and as applications multiply.

Each job fuels the network:

* Job fees route through smart contracts
* LILY flows to compute providers, solvers, and model authors
* Rewards compound through protocol-native attribution

We believe Lilypad is how decentralised AI becomes real—not a narrative, but a functioning coordination protocol that scales across use cases, networks, and agents.

We’re not here to host one model. We’re here to support millions.

We’re building the compute substrate and coordination economy for decentralised AI.

And we’re just getting started.

Lilypad is not a compute marketplace. It’s a programmable foundation for composable AI.

We believe the intelligence economy should be:

* **Verifiable**: Every output traceable, reproducible, auditable.
* **Composable**: Jobs, modules, agents—all interoperable.
* **Fair**: Value flows to contributors, not just platforms.

We’re not asking to be the only layer. But we intend to be the best one to build on.

***

Docs → [https://docs.lilypad.tech](https://docs.lilypad.tech/)\
GitHub → [https://github.com/Lilypad-Tech](https://github.com/Lilypad-Tech)\
Pitch → [https://docsend.com/v/8bnyr/lilypadpitch](https://docsend.com/v/8bnyr/lilypadpitch)

***

**Lilypad.tech | docs.lilypad.tech | github.com/Lilypad-Tech**
