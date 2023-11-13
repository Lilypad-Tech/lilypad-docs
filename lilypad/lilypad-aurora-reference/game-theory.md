# Lilypad Game Theory Documentation

In this talk, Levi Rybalovd iscusses the prevention of cheating in a two-sided marketplace for compute. The focus is on using a game theoretic approach to verifiable computing without relying on cryptographic tools. The talk explores the difference between global consensus and local consensus and assumes non-malicious but utility maximizing agents. 

{% embed url="https://youtu.be/hvlBkh6XJto?si=NEAmNc2X7u9bL2AC" %}
Lilypad: An Adversary First Approach to Game Theoretic Verifiable Computing
{% endembed %}

## Introduction
Lilypad is a verifiable trustless decentralized compute network that aims to prevent cheating in the network. The network consists of clients and compute nodes, and it assumes deterministic results. The main goal is to establish a game theoretic approach to verifiable computing, where clients can trust the results they receive from compute nodes. The approach used in Lilypad is pure verification by replication, without relying on cryptographic tools like snarks or trusted execution environments.

## Global Consensus vs Local Consensus
In the context of Lilypad, it's important to understand the difference between global consensus and local consensus. Global consensus, as seen in blockchains, ensures that every node knows the result of a computation is correct due to massive replication across many nodes. However, in Lilypad's two-sided marketplace, only the client needs to be convinced that the result is correct. Local consensus is sufficient for the client, while other nodes like verifying nodes, requesters, and market makers may also need to be convinced.

## Adversary Model
Lilypad assumes non-malicious but utility-maximizing agents, including both clients and compute nodes. Utility-maximizing means that nodes will do anything to maximize their return, including returning false results if necessary. However, they are not malicious and won't purposely send back false results. The adversary model assumes that all nodes are utility-maximizing and does not consider malicious behavior.

## Good Solutions
Lilypad aims to achieve the best outcome, where nodes never have any incentive to cheat. If that's not possible, the goal is to minimize the incentive to cheat as a function of the protocol's parameters. Another option is to achieve the first two outcomes under simplifying assumptions, such as having a fraction of honest nodes in every mediation protocol. Lilypad also considers the possibility of not being able to achieve any of these outcomes and aims to understand the limitations.

## Reinforcement Learning Approach
Lilypad takes an adversary-first approach by designing the most powerful adversary possible and then optimizing against it. The team uses multi-agent reinforcement learning to train agents to act as utility-maximizing agents on behalf of clients and compute nodes. Reinforcement learning has shown impressive results in various domains, and Lilypad aims to leverage its capabilities to train agents that can maximize their utility in the network.

## Anti-Cheating Mechanisms
Lilypad plans to test various anti-cheating mechanisms once the reinforcement learning agents are implemented. These mechanisms include:
1. Consortium of mediators: A group of trusted mediators can check the results, reducing the likelihood of cheating.
2. Prediction markets and staking: Nodes can stake behind other nodes and lose their collateral if the node they stake behind is found to have cheated.
3. Taxes and jackpots: A tax is imposed on every job, and the taxes go into a jackpot that is awarded to nodes that find other nodes to have cheated.
4. Reputation: Nodes can build up a reputation based on the number of jobs they've done and the honesty of their results.
5. Sorting inputs and outputs: Storing inputs and outputs for longer periods allows for easier verification but increases collateralization requirements.
6. Frequency of checking results: Autonomous agents can decide when to check results, balancing the need for verification with the cost of collateralization.

## Future Developments
In the future, Lilypad aims to take into account the preferences of nodes, such as computational requirements, time requirements, and scheduling requirements. The long-term goal is to have compute nodes and clients negotiate with each other automatically over these aspects of a job. Lilypad acknowledges that game-theoretic verifiable computing is a less studied form of verifiable computing compared to zero-knowledge proofs and trusted execution environments. However, the team is committed to exploring this approach and conducting rigorous research to find effective solutions.

## Conclusion
Lilypad's game-theoretic approach to verifiable computing aims to prevent cheating in a decentralized compute network. By using reinforcement learning and testing various anti-cheating mechanisms, Lilypad strives to create a trustless environment where clients can have confidence in the results they receive from compute nodes. The team is actively working on implementing reinforcement learning agents and conducting simulations to evaluate the effectiveness of different strategies.
