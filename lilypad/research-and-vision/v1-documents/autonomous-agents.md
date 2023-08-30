---
description: Our Approach
---

# Autonomous Agents

### Utility Maximization

A core assumption in much of game theory is that agents are utility-maximizing. That is, agents are completely rational actors, and are able to execute exactly the behavior that maximizes their return, however "return" is defined in the given context.

However, we know that in real life, humans are not completely rational, and are not capable of perfect execution of actions. In that light, how can we look at the game-theoretic approaches in the last section?

Either we can try to account for the irrational behavior of humans, or we can try to emulate the behavior of utility-maximizing agents. While there is a large amount of game-theoretic literature dedicated to the former, we opt for the latter for reasons that will become clear below.

While this problem setting - verifiable computation by way of game theory - is different than many game theoretic settings, we can draw inspiration from commonly used concepts like the [revelation principle](https://en.wikipedia.org/wiki/Revelation\_principle) and [strategyproofness](https://en.wikipedia.org/wiki/Strategyproofness). Both strategyproofness and the revelation principle are centered around the idea of incentivizing agents to truthfully report their preferences. Most approaches in the literature rely on analytic methods to determine what rational agents will do by analyzing their payoffs as a function of their preferences, the behaviors of other agents, and the mechanism under analysis. Ultimately, we are also aiming to find (a) mechanism(s) that lead(s) to an equilibrium where all agents choose to not cheat and not collude.

### Autonomous Agents

Note that the actual environment of a two-sided marketplace for distributed computation is extremely complicated (e.g. the heterogeneity of hardware, types of computation, latencies and bandwidths, etc.). Any theoretical/analytic approach to the problem that is actually correct should also work in simulation, so we opt for a simulation-driven approach.

The way that we can emulate perfectly rational behavior is by training autonomous agents to act on behalf of their human owners in a utility-maximizing manner. At that point, the challenge is to design the global game to drive the probability of cheating to zero - ideally, to make it be equal to zero - which is no small feat in a trustless and permissionless environment. However, the simplifying assumption that we are in fact operating with utility-maximizing agents conceptually simplifies the problem immensely.

The process begins by creating a digital twin of a two-sided marketplace. In this environment, autonomous agents acting on behalf of client and compute nodes will be trained to maximize returns based on data gathered in simulation. For now, we will elide maximizing returns by optimizing scheduling, though this is a future topic of interest. We will use techniques primarily from the field of multi-agent reinforcement learning in order to train the agents. The precise methods we will use (e.g. modes of training and execution, homogenous vs. heterogenous agents, choice of equilibrium, self-play vs. mixed-play, value-based vs. policy-based learning, etc.) will be determined in the course of building the simulation. See the [pre-print](https://www.marl-book.com/) by Albrecht, Christianos, and Schäfer for our reference text.

At a minimum, the action space for an autonomous agent representing a compute node should be to cheat or not to cheat, and to collude or not collude within a mediation protocol. The observable environment for nodes on the network should include all data stored on the blockchain - that is, the sequence of deals, results, and mediations - as well as the information in the orderbook. While the orderbook will be off-chain, we model in the digital twin the orderbook acting as a centralized, single source of truth that all agents have access to. In the long-term, nodes will have (potentially non-identical) local information regarding other job and resource offers on the network.

Further work may explore agents forming beliefs about the hardware and strategies of other agents, but that is beyond the scope of the current work.

### First Principles Approach

We conclude with two "axioms" upon which we will base our simulations:

1. Every agent attempts to maximize its utility, including cheating and/or colluding if necessary.
2. All other components of the game should lead to a "good" solution, as defined in the problem statement.
