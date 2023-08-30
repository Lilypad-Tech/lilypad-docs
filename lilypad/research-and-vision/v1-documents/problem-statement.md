---
description: The Distributed Compute Problem
---

# Problem Statement

### Problem Setup

The setup is a trustless, permissionless, two-sided marketplace for compute, where clients can purchase compute services from compute nodes. Trustless means that by default, the protocol does not assume that any particular node behaves in a trustworthy manner, and that each node should be considered as rationally self-interested (note that this excludes intentionally malicious behavior). Permissionless means that any node can join or leave the network at will.

Matches for compute jobs are made off-chain, with the resulting deals and results recorded on-chain. Both clients and compute nodes need to agree to matches before they become deals, and make deposits to the protocol to enable rewards and punishments. Results are verified using verification-via-replication, and clients can check the results of any job after it has been completed, but before it needs to pay. It does so by calling upon a mediation protocol. The mediation protocol is the ultimate source of truth, and the outcome of the mediation protocol determines how payouts to nodes are made.

The issue of preventing fake results in the presence of a Trusted Third Party (TTP) as a mediator is effectively a solved problem (for example, see the section on prior verification-via-replication protocols, though there is much more literature on this topic). Given the assumption that the mediation protocol is the source of truth, we can treat the mediation protocol as a TTP. Since the fake results problem is basically already solved in this case, the cheating problem reduces down to solving the collusion problem within the mediation protocol. (Note, however, that we will address both cheating and collusion; the framework described here exists to conceptually simplify the problem.)

This is a typical scenario of a Byzantine environment, and we can use well-established approaches to Byzantine Fault Tolerance when invoking mediation. However, most BFT algorithms and cryptographic methods rely on assumptions regarding some fraction of honest nodes. The problem is that rational, utility-maximizing agents can still collude, even in a mediation consortium, in order to converge on incorrect results. One the one hand, we could assume that some fraction of nodes are honest, as is often done. One the other hand, can we do better?

## Problem Statement

### Task

The task is to find the mechanisms that incentivizes all nodes to behave honestly.

### Adversary model

All agents in the protocol are utility-maximizing. This will be elucidated in a subsequent section. Most of the literature has focused on the case where compute nodes are dishonest. However, the client can also behave dishonestly in some manner that maximizes their utility. For example, if the client has some level of control over the choice of mediator, and dishonest nodes have their collateral slashed, the client could collude with the mediator in order to deem a correct result incorrect and get a cut of the honest compute node's collateral.

### What is a good solution?

"Good" solutions can take a number of forms:

1. Nodes never have an incentive to be dishonest.
2. Nodes have an incentive to be dishonest that goes to zero as a function of the parameters of the protocol.
3. (1) or (2), but under some simplifying assumptions, such as there being some fraction of honest nodes within every mediation protocol.

A good solution would achieve any of these goals. Alternatively, another valuable outcome of this research would be to discover under what assumptions these goals can or cannot be met, or if the goals are even possible to achieve at all.

### Mechanisms for achieving these goals

There are a number of ways that these goals may be achieved. The approach will be to construct a digital twin of the protocol and test a number of different mechanisms in simulation. These mechanisms include variations on mediation protocols, collateralization, staking, taxes and jackpots, and others; see the Mechanisms to Explore section for details.
