---
description: 'Lilypad: A Protocol for Open Intelligence Infrastructure'
---

# Lilypad Litepaper

***

### Building the Infrastructure for an Open AI Economy

#### Abstract

Lilypad is a coordination protocol for intelligence infrastructure. It provides permissionless access to verifiable compute, model monetisation by default, and cryptographically auditable execution for any AI workload. Lilypad abstracts compute primitives into a modular, trust-minimised protocol that can serve inference, agents, and pipeline-based workflows across open and enterprise systems.

This paper outlines the core thesis, architectural structure, crypto-economic system, and forward-looking roadmap for Lilypad. Our goal: to create a programmable substrate that supports open AI as a public good and enables the next era of agentic computation, composable intelligence, and developer-owned ecosystems.

### 1. Introduction: Infrastructure Shapes Intelligence... and Competitive Edge

#### 1.1 The Technological Convergence Making DeAI Possible

From Turing’s foundational thought experiments to the cloud boom of the 2000s, compute has mirrored, and magnified, our evolving social architectures. Each leap in processing capability has triggered new markets, new models of coordination, and new vulnerabilities. Now, with AI becoming not just an application layer but a decision substrate, the question isn’t just what we build, but where, and who gets to participate.

We’re at a convergence point of three arcs:

* The **Arc of Compute:** from mainframes to hyperscaler cloud to edge devices, with increasing decentralisation and specialisation at the hardware layer.
* The **Arc of AI:** from statistical tooling to foundational models to agentic systems running autonomous workflows.
* The **Arc of Coordination:** from institutionally brokered trust to cryptographic primitives, on-chain settlement, and composable economic logic.

The convergence of open-source AI and crypto-infrastructure is the foundation for a new economic paradigm. Lilypad exists at the intersection of these arcs merging crypto’s programmable market infrastructure with AI’s intelligence primitives to build an AI innovation economy at scale.

#### 1.2 Proprietary AI & Centralised Infrastructure Challenges&#x20;

Today’s centralised AI infrastructure imposes monopolistic control & extractive defaults:

* Compute access intermediated by monopolistic brokers
* Models abstracted behind opaque APIs with limited visibility&#x20;
* Profit & regulatory arbitrage is prioritised over innovation
* Extractive economic value capture leaves foundational contributors unpaid with no native attribution, provenance, or monetisation available

Centralised AI is also struggling to find moat:

* Oligopolies have (so far) failed to lock in regulatory capture
* In-demand AI talent is increasingly ethically aligned with open source AI (eg. Yann LeCun, Mira Murati)
* Proprietary model companies are now competing on distribution channels rather than model quality or capability due to a convergence of factors including&#x20;
  * The Open Source model movement push narrowing the gap of capability between proprietary & open source AI alongside (even Huggingface's $4.5B valuation is driven by network effect)
  * Models, particularly LLMs, approaching inherent limitations due to data saturation and diminishing returns from scaling, suggesting performance improvements for general models are limited
  * The China-US AI race providing new training methods with less resources and competitive open source models

Additionally, centralised infrastructure is struggling to cope with demand and remain cutting edge with

* New data-centres out of date before the GPU cards arrive or not configured for the latest AI needs
* Overhead costs not competitive with more agile alternatives
* Energy & environmental constraints limiting scaling

#### 1.3 The Decentralised AI Advantage

Decentralised AI Ethical Advantage: Community Led & Owned

* AI as a _commons:_ owned and governed by the communities that contribute to and use it
* Promotes ethical pluralism, avoiding centralised control and opaque value systems from large tech firms
* Open participation ensures ethical alignment and reduces corporate capture and bias - with local knowledge, underrepresented languages, indigenous ontologies, and non-Western value systems—creating a richer, more inclusive model corpus
* Empowers value-aligned innovation across domains accelerating breakthroughs including BioML, climate, regenerative tech, and rare disease research

Decentralised AI Product Advantage: Open Access & Long-Tail Innovation

* Open participation unlocks a massive long tail of use cases, from hobbyist tools to enterprise-grade models
* Lowers barriers to entry for solopreneurs and domain experts to contribute, run, and monetize specialized models
* Diversity from open participation & access expands the long-tail of use cases fostering a pluralistic AI landscape that better reflects and serves humanity at large

Decentralised AI Technological Advantage: Modular, Scalable, Verifiable Infrastructure

* DePIN&#x20;
  * provides dynamically scalable compute infrastructure with locational advantages
  * provides more efficient compute networks that capture idle compute power
* Market & Monetisation Mechanics
  * Marketplaces provide cost, distribution & performance benefits&#x20;
  * Monetisation pushes state-of-the-art hardware & model accessibility&#x20;
  * Monetisation provides pathways to collective data collection & collaborative training efforts
  * Marketplaces & Monetisation solves energy needs efficiently - driving costs to underlying physics needs.&#x20;
* Trust & Coordination
  * Permissionless coordination capabilities provide broad-based participation and drive collaboration
  * Provenance pipelines & codified trust enable solutions to near-term AI challenges such as data sharing & collection, IP rights and proof of truth and personhood
  * Built-in provenance, module validation, and job reproducibility ensures verifiability and scientific integrity
  * Permissionless coordination supports agent workflows, registry systems, and autonomous pipelines

#### 1.4 DeAI Challenges

Decentralised AI is not without it's challenges:

* Supply-First DePIN Imbalance
  * Many DePIN projects are supply heavy - with web3 being uniquely good at large scale network coordination, hardware for compute and storage is readily available.&#x20;
  * However, many DePIN projects lack a corresponding "demand engine" - with low usage of a fundamentally valuable asset.&#x20;
* Fragmentation & Lack of Collaboration
  * The deAI ecosystem is fragmented: agents, compute networks, model hubs & data platforms are building in silos.
  * A unified coordination layer or interoperable standards are missing, limiting network effects and cross-project capabilities.
  * A collaborative effort across the deAI space is required to compete with centralised solutions.
* Product Immaturity or Pain Points vs Centralised Competitors
  * UX for decentralised compute, model monetisation, and orchestration often lags behind centralised tools
  * Lack of plug-and-play SDKs, agent orchestration tools, or composable pipelines limits adoption outside crypto-native devs.
  * Blockchain payments & primitives can hamper adoption
* Incentive Misalignment Across Layers
  * DePIN operators, model builders, and app developers are incentivised separately: yet success relies on end-to-end alignment.
  * Lack of shared revenue or reputation mechanisms limits module reuse, collaboration, and scale.

While no single project is capable of solving this alone, Lilypad is one of the few projects orchestrating compute, data provenance, and economic incentives in a composable stack capable of collaborative integrations.\
\
Lilypad helps brings the DeAI vision to life by providing a flywheel for DePIN, a distribution path for model training networks, integrations to agentic frameworks, data & storage and a full stack AI service platform for developers, businesses and solopreneurs, all powered by transparent and user-owned economics.

#### 1.5 Lilypad’s Core Philosophy

> "AI should be a public good - not a corporate asset."

Lilypad offers a counter-architecture to centralised models: modular, verifiable & permissionless. It builds a trustless execution layer where models can be exposed, reused, and paid on-chain and reroutes economic gravity back towards creators and contributors.

It’s a programmable substrate for intelligence that expands access, reinforces agency, and creates new terrain for open coordination, utilising the competitive edge of decentralised AI for the collective benefit of humanity.

### 2. Design Philosophy

Lilypad’s architecture is informed by a decade of experiments in decentralized compute: Golem, Truebit, Modicum, Bacalhau, BOINC, and other pioneering systems from academia and the open-source world. Each advanced the state of the art. But none offered the combination of open participation, verifiable execution, and built-in economic coordination.

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

* **Instant settlement:** No billing cycles. Compute providers, agents, and creators are paid atomically when jobs are completed.
* **Resilience:** Workload routing happens across a global mesh. There's no single point of failure.
* **Verifiability**: Every job, output, and payment is recorded on-chain, with signatures and manifests.
* **Provenance:** Model authorship and job reuse are recorded cryptographically in the registry.
* **Coordination**: Smart contracts execute logic that would otherwise require middleware or manual enforcement.
* **Distribution**: Anyone with a GPU or a model can participate—from solo developers to research labs to DAOs.

Lilypad flips the script on extractive AI platforms by embedding value flows directly into the infrastructure layer. Model creators, compute providers, mediators, and agents all interact through transparent, programmable incentives. This creates new contribution pathways and aligns every participant to the health and growth of the network. These aren’t speculative mechanisms—they’re live and accruing value on every job.

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

### 5. Verification and Provenance

Lilypad supports layered verification through signed job manifests, output log digests, and mediation sampling. These are implemented through on-chain job state commitments and optional mediator-sampled audits. Model fingerprinting and FHE are future considerations, but not currently active components of the system.

Read our paper on verification here: [https://arxiv.org/abs/2501.05374](https://arxiv.org/abs/2501.05374)

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

### 8. Lilypad: The Coordination Engine for Collective Intelligence at Scale

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
