---
description: 'Lilypad: A Protocol for Open Intelligence Infrastructure'
hidden: true
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

We treat infrastructure not as a system of encoded values: who can build, who gets paid, and what rules apply.

Today’s centralized AI infrastructure imposes extractive defaults:

* Compute access intermediated by monopolistic brokers
* Models abstracted behind opaque APIs
* No native attribution, provenance, or monetization

Lilypad offers a counter-architecture: modular, verifiable, permissionless. It builds a trustless execution layer where models can be exposed, reused, and paid on-chain. Not to replace existing systems, but to reroute economic gravity back toward creators and contributors.

It’s a programmable substrate for intelligence—one that expands access, reinforces agency, and creates new terrain for open coordination.

***

### 2. Design Philosophy

Lilypad’s architecture is informed by a decade of experiments in decentralized compute—Golem, Truebit, Modicum, Bacalhau, BOINC, and other pioneering systems from academia and the open-source world. Each advanced the state of the art. But none offered the combination of open participation, verifiable execution, and built-in economic coordination.

Golem struggled with adoption and required determinism at the cost of generality. Modicum introduced a promising recomputation-based system, but was constrained by deterministic job assumptions and verifier logic entanglement.\
\
Bacalhau, which underpins our execution layer, was built to solve decentralised job distribution but left incentive mechanisms out of scope. We designed and implemented those incentives as first-class protocol logic: token-driven payments, staking, routing, and verification coordination, all executed through on-chain contracts and off-chain job resolution. Lilypad is an intelligent, incentive-aligned coordination protocol designed to operate compute executions at network scale.

Lilypad is built to enable modular and independent verification, with clear separation from the execution layer. This architectural choice lets the protocol flexibly support deterministic models, probabilistic audits, and log-based validation without compromising performance or developer freedom. Rather than treating auditability as a constraint, Lilypad treats it as a programmable layer for innovation where multiple strategies can coexist and evolve.

We’ve taken lessons from these systems to architect Lilypad differently:

* We decouple verification from execution, enabling multiple verification strategies depending on job type, latency, and value.
* We don’t assume determinism. Instead, we build modularity into verification layers with upgade capability.
* We avoid hardwiring compute to consensus. Lilypad coordinates compute jobs via constraint-solving and smart contract validation, not consensus-layer integration.

Most importantly, we do not assume a monolithic trust architecture. We treat verifiability, coordination, and monetization as primitives.

Lilypad is structured around three core design principles:

1. **Modularity**: Infrastructure should be upgradeable. Each layer of the protocol—from compute to registry to settlement—is designed to evolve independently.
2. **Verifiability**: Every job run should leave a legible, auditable trail. Not all trust needs to be cryptographic—but all trust should be accountable.
3. **Economic symmetry**: Value created by the network should circulate within it. Contributors—whether model authors, solvers, or compute providers—are paid at the protocol level.

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

#### Blockchain-based Value

Blockchain is the foundation of Lilypad's coordination logic. It enables atomic settlement, actor-level accountability, and programmable infrastructure at a scale traditional systems cannot replicate.

Smart contracts enforce job flows. Tokens encode trust and incentives directly into the network. No middlemen. No billing overhead. No platform dependencies.

Blockchain offers core properties that general-purpose infrastructure still can't:

* **Instant settlement** — No billing cycles. Compute providers, agents, and creators are paid atomically when jobs are completed.
* **Resilience** — Workload routing happens across a global mesh. There's no single point of failure.
* **Verifiability** — Every job, output, and payment is recorded on-chain, with signatures and manifests.
* **Provenance** — Model authorship and job reuse are recorded cryptographically in the registry.
* **Coordination** — Smart contracts execute logic that would otherwise require middleware or manual enforcement.
* **Distribution** — Anyone with a GPU or a model can participate—from solo developers to research labs to DAOs.

Lilypad flips the script on extractive AI platforms by embedding value flows directly into the infrastructure layer. Model creators, compute providers, mediators, and agents all interact through transparent, programmable incentives. This creates new contribution pathways and aligns every participant to the health and growth of the network. These aren’t speculative mechanisms—they’re live and accruing value on every job.

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

Lilypad supports layered verification through signed job manifests, output log digests, and mediation sampling. These are implemented through on-chain job state commitments and optional mediator-sampled audits. Model fingerprinting and FHE are future considerations, but not currently active components of the system.

Read our paper on verification here: [https://arxiv.org/abs/2501.05374](https://arxiv.org/abs/2501.05374)

***

### 6. Economics and Coordination

Lilypad introduces LILY: a fixed-supply token used to route incentives and economic coordination across the protocol. The system is designed to fairly compensate compute providers, model contributors, and protocol participants, while maintaining integrity through collateral and verifiable actions.

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

* Game Theory Mechanics for compute providers
* Protections for job creators
* Economic throughput that aligns incentives across the network

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

The Lilypad roadmap is structured around three major phases—each aligned to protocol capabilities and the evolving demands of decentralised AI.

#### Phase 1: Compute & Coordination (2024)

| Capability                  | Description                                                                                |
| --------------------------- | ------------------------------------------------------------------------------------------ |
| Job execution pipeline      | Streaming and multi-stage inference workflows with DAG-based job coordination.             |
| Smart contract coordination | Secure, gas-efficient execution payments, state transitions, and refund logic.             |
| Identity and actor roles    | Lightweight on-chain tracking for job creators, solvers, mediators, and compute providers. |
| Validator-in-the-loop       | Optional mediation for job integrity using dispute resolution logic.                       |

#### Phase 2: AI Tooling & Incentives (2025)

| Capability                  | Description                                                                                   |
| --------------------------- | --------------------------------------------------------------------------------------------- |
| SaaS-tier integration       | Anura APIs, hosted endpoints, and fiat billing interface for developers and non-crypto users. |
| Reputation-weighted routing | Actor scores influence job distribution and protocol incentives.                              |
| Persistent job graphs       | Long-running, stateful pipelines for agentic applications.                                    |
| TrainPad                    | Lightweight, distributed finetuning engine with reward-weighted checkpoints.                  |
| Mainnet Deployment & TGE    | Finalisation of token mechanics and mainnet readiness.                                        |

#### Phase 3: Interoperability & Governance (2026)

| Capability               | Description                                                                                           |
| ------------------------ | ----------------------------------------------------------------------------------------------------- |
| ForgeNet                 | Network of remixable, interdependent model forks with royalty logic.                                  |
| Cross-chain execution    | Job layer integration with Taisu and Somnia ecosystems.                                               |
| Governance               | Lilypad DAO activation with protocol parameter control, actor slashing appeals, and grant allocation. |
| Multi-chain pipelines    | Modular jobs distributed across chains, with universal attribution and payment routing.               |
| Additional token utility | Further ecosystem mechanics, including potential L2 expansion or sovereign chain launch.              |

This roadmap ensures Lilypad evolves from job execution into a full composability and coordination layer for decentralised AI systems

### 8. Lilypad SaaS and Enterprise

Lilypad's modular infrastructure powers more than just on-chain coordination. It also supports standalone SaaS deployments and tailored enterprise integrations.

#### 8.1 Lilypad SaaS

For builders who want plug-and-play access to Lilypad's capabilities, our SaaS offering includes:

* Anura-based APIs for running inference on open models
* Hosted dashboards for tracking job execution and usage
* Integration modules for n8n, LangChain, and agent frameworks
* Standard billing interfaces for fiat and non-crypto workflows

SaaS users interact with the full power of the Lilypad job mesh—without needing to touch tokens, wallets, or on-chain logic. It's ideal for developers, startups, and researchers seeking scale and flexibility without overhead.

#### 8.2 Lilypad Enterprise

Enterprise partners can deploy Lilypad in fully private or hybrid environments:

* Dedicated job queues with custom SLAs
* On-prem inference and agent execution
* Compliance tooling for pharma, science, and defence workflows
* Integration with corporate identity and data privacy systems

Enterprise stacks inherit the full Lilypad coordination layer—compute orchestration, verification, monetisation—while retaining local control and data isolation.

Both offerings are backed by the same protocol primitives: smart contracts, verifiable execution, and economic coordination.

***

### 8. Closing: The Coordination Engine for Agentic AI at Scale

Lilypad is a programmable coordination system for decentralised intelligence infrastructure.

Imagine swarms of agents coordinating scientific research or building decentralised AI systems - not tied to one API, but operating across a permissionless network with embedded attribution and payment.

Blockchain makes this coordination possible. Payments happen in real time. Coordination logic is encoded into smart contracts. And the system is globally resilient and auditable by default.

Why blockchain matters here:

* **Instant settlement**: No billing cycles. Compute, coordination, and creators are paid atomically.
* **Resilience**: Jobs route across a global mesh, not a single provider.
* **Verifiability**: Cryptographic job manifests, signed results, on-chain records.
* **Provenance**: Model authorship and reuse tracked natively in the registry.
* **Coordination**: Smart contract logic replaces the need for gatekeepers.
* **Distribution**: Actors anywhere can participate—from solo devs to academic labs.

We believe the intelligence economy should be:

* **Verifiable**: Every output traceable, reproducible, auditable.
* **Composable**: Jobs, modules, agents—all interoperable.
* **Fair**: Value flows to contributors, not just platforms.

So we built it. Lilypad is the compute substrate and coordination economy for decentralised AI - a programmable foundation for open-access AI and innovation unlocks.

***

Docs → [https://docs.lilypad.tech](https://docs.lilypad.tech/)\
GitHub → [https://github.com/Lilypad-Tech](https://github.com/Lilypad-Tech)\
Pitch → [https://docsend.com/v/8bnyr/lilypadpitch](https://docsend.com/v/8bnyr/lilypadpitch)

***

**Lilypad.tech | docs.lilypad.tech | github.com/Lilypad-Tech**
