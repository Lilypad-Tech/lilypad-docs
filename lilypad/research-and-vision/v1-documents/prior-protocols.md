---
description: >-
  Investigation of some previous verifiacation-by-replication computing
  protocols
---

# Prior Protocols

## Prior Verification-via-Replication Protocols

Before explaining our approach, we give a short overview of three prior approaches to verification-via-replication distributed computing protocols: Truebit, Modicum, and Smart Contract Counter-Collusion. We will outline potential improvements, and how our work builds on top of, and differs from, prior work.

### [Truebit](https://arxiv.org/pdf/1908.04756.pdf)

Truebit is a protocol for outsourcing computation from blockchains, built using smart contracts on top of Ethereum. The original potential use cases were trustless mining pools, trustless bridges, scaling transaction throughput, and, scalable “on-chain” storage. Since its goal is to scale on-chain computation, it aims for global consensus: "Since there exist no trusted parties on Ethereum’s network, by symmetry we must allow any party to be hired to solve any computational task, and similarly anyone should be able to challenge a Solver’s outcome of a computational task. The latter requirement ensures that TrueBit operates by **unanimous consensus**." (emphasis added)

The components of Truebit are Miners, Task Givers, Solvers, Verifiers, and Judges. In order to incentivize checking results, random errors are forced into computations, with jackpots awarded to those who find them. These jackpots are funded by taxes on computations.

The verification game consists of a series of rounds, where in each round, a smaller and smaller subset of the computation is checked. Eventually, only one instruction is used to determine whether a Solver or Verifier is correct: ["In fact, only one instruction line is used in a verification game. There will be a part of the program code where there is a discrepancy between the Solver and the Verifier. The instruction of that discrepancy point is used to verify who is right."](https://truebit.io/guide/truebit-structure/)

The authors claim that Sybil attacks are mitigated by pairwise Sybil-resistance between the parties of Task Givers, Solvers, and Verifiers, with Judges and Referees, whose roles are played by Miners, assumed to function as intended. Likewise, they claim that attacks to get bogus solutions on-chain by scaring off Verifiers are mitigated by the economics of deposits, taxes, and jackpot rewards. Additionally, a cartel of Solvers who absorb losses until they find a task with a forced error, upon which time they will receive the jackpot, will lose money in the long-term, since the expected Solver deposit per task is higher than the expected jackpot per task. Addressing another attack, the authors claim that an attack involving a flood of Challengers who try to take as much of the jackpot reward resulting from a forced error as possible is mitigated by having the total jackpot reward decrease as the number of Challengers increases.

#### Challenges

* Does not scale to large/complicated/arbitrary computations
* No formal theorems or proofs, no simulations, many plausible but unsubstantiated claims, especially regarding collusion
* Everything is done on-chain
* This model does not work well with two-sided marketplaces, because
  * It aims for global consensus, where any node is allowed to do the computation, whereas in two-sided marketplaces, clients need to be able to choose which nodes they are paying to do the computation
  * Clients may have time restrictions on their computations, and cannot wait for cases where their computations were injected with forced errors
* No accounting for repeated games

#### Takeaways

* Taxes and jackpots are a valuable tool to create a global game that affects local outcomes
* Provides a list of potential client attacks

### [Modicum](https://www.researchgate.net/profile/Aron-Laszka/publication/341640091\_Mechanisms\_for\_Outsourcing\_Computation\_via\_a\_Decentralized\_Market/links/5f14736b299bf1e548c3712a/Mechanisms-for-Outsourcing-Computation-via-a-Decentralized-Market.pdf)

The original version of [Modicum](https://www.researchgate.net/profile/Aron-Laszka/publication/341640091\_Mechanisms\_for\_Outsourcing\_Computation\_via\_a\_Decentralized\_Market/links/5f14736b299bf1e548c3712a/Mechanisms-for-Outsourcing-Computation-via-a-Decentralized-Market.pdf) had five key components: Job Creators (JC), Resource Providers (RP), Solvers (market makers), Mediators (agreed-upon third parties for mediation), and Directories (file systems, which we have replaced with IPFS and Docker registries). Job Creators are clients, the ones who have computations that need to be done and are willing to pay. Resource Providers are those with computational resources that they are willing to rent out for the right price. Solvers are market-makers; they match the offers from JCs and RPs. Mediators are third parties trusted by both JCs and RPs to arbitrate disagreements. The Directories are network storage services available to both JCs and RPs.

Job Creators are only allowed to submit deterministic jobs to the protocol. The Mediator exists to check for non-deterministic tasks submitted by the Job Creator (which can be used by the Job Creator as an attack vector to get free results), and fake results returned by the Resource Provider. The method for determining whether a job is deterministic or not is for the Mediator to run a job n times and check to see whether it receives different answers.

Modicum combines two separate ideas: checking the result from a Resource Provider to see if it is correct, and checking a result from a job submitted by a Job Creator to see if the job was deterministic or not. This implies that there is no capability for a client to simply check whether a result is correct or not, without the possibility of its collateral being slashed.

An alternative to trusting the Mediator (to act as a TTP) by having it run a job n times is having a consortium of n Mediators each run the task a single time. However, this adds the complication of achieving consensus in that consortium.

The issue of the Resource Provider and Mediator colluding to return a fake result is not addressed by this protocol. The authors allow for a Job Creator or Resource Provider to remove a Mediator from their list of trusted Mediators if they no longer trust it. However, that still leaves room to cheat at least once, and ideally this should be disincentivized from the outset.

There is also the issue of collateralization. The Modicum protocol, as well as a number of other protocols, assume (approximate) guesses as to the cost of jobs in advance, so that nodes can deposit the correct amount of collateral. However, doing so is fraught with complications; we provide an alternative approach in the Mechanisms to Explore section.

#### Challenges

* The Mediator is basically a trusted third party
* Client cannot simply check a result without being slashed, which is a consequence of the client attack model
* No accounting for repeated games

#### Takeaways

* Potential client attack, though one that can be mitigated by technical means
* The client has benefit of getting correct results, which needs to be accounted for in simulation
* Useful prototype for a two-sided marketplace (the [follow-up paper](https://par.nsf.gov/servlets/purl/10355144) for stream processing applications is also useful)

### [Smart Contract Counter-Collusion](https://arxiv.org/pdf/1708.01171.pdf)

The authors determine that cryptographic methods for verifiable computation are too expensive for real-world scenarios. For that reason, they rely on verification-via-replication. The scenario is one in which a client _simultaneously_ outsources computation to two clouds, where those two clouds deposit collateral into smart contracts in such a way to create a game between them, where the game incentivizes doing the computation honestly. The central challenge that the authors tackle is the issue of collusion - that is, what if the two clouds collude on an incorrect answer?

In contrast to Modicum, the client is assumed to be honest, and in contrast to Truebit, a trusted third part (TTP) is used to handle disputes.

#### Three Contracts

The authors use a series of three contracts to counter collusion.

The first game is an induced Prisoner's Dilemma - to avoid the two clouds colluding, one cloud can be rewarded the other cloud's deposit (minus payment to the TTP for resolving the dispute) if the former returned the correct result and the latter did not. Thus, each cloud is better off giving the other cloud fake results while computing the correct result itself. This contract is called the **Prisoner's contract**. It is analogous to the equilibrium in the classic prisoner's dilemma being defection <> computing honest result and giving other node fake result if offered to collude.

However, the clouds can agree to collude via a smart contract as well. They could do this by both depositing another amount into a contract, where the leader of the collusion must add a bribe (less than its cost of computing) to the contract as well (disregarding the bribe, both clouds deposit the same amount of collateral). The deposit is such that the clouds have more of an incentive to follow the collusion strategy than to deviate from it. This contract is called the **Colluder's contract**.

In order to counteract the Colluder's contract, a **Traitor's contract** is used to avoid this scenario by incentivizing the clouds to report the Colluder's contract. The basic concept is that the traitor cloud indeed reports the agreed-upon collusion result to the client in order to avoid the punishment in the Colluder's contract, but also honestly computes and returns the result to the client in order to avoid the punishment of the Prisoner's contract. The client must also put down a deposit in the Traitor's contract. Only the first cloud to report the Colluder's contract gets rewarded. The signing and reporting of the contracts must happen in a particular order in order for this process to work.

The authors prove that these games individually and together lead to a sequential equilibrium (which is stronger than a Nash equilibrium), meaning that it is optimal not only in terms of the whole game, but at every information set (basically the set of options each player has at every turn).

#### Challenges

* A Colluder's contract can be signed on different chains (or even off-chain). In order to mitigate this, the Traitor's contracts would have to become cross-chain (which is a major technical challenge), not to mention the possibility of cryptographically secure contracts (e.g. MPC contracts) where one of the parties alone would not be able to prove the existence of this contract
* Relies on trusted third party to resolve disputes
* Every task is replicated (that is, two copies of each job are always computed)
* Assumes client is honest
* Assumes amount of collateral known beforehand
* No accounting for repeated games
  * It is well known that in the repeated Prisoner's dilemma, depending on the assumptions, cooperation becomes the equilibrium

#### Takeaways

* The contracts and the payoffs that they induce offer a valuable toolbox to think about the problem of collusion
* The contracts offer, in a restricted setting, an ironclad way (assuming the proofs are correct) of preventing collusion
