---
description: Current State
---

# Verification & Mediation on Lilypad v1

## Verification & Mediation on Lilypad v1

We didn't want to hold back on releasing a testnet build that developers could use straight away to build their awesome ideas on, however, it's worth noting that Lilypad v1 is a minimal modicum-based testnet and the implemented mediation and game theory on this testnet is very much at baby :baby: stage - as are many other aspects of the robust compute network that we are working hard to build.\


### **Verification on Lilypad v1**

There is currently **no** verification on smart contract-called Lilypad jobs&#x20;

Verification **DOES** exist on the CLI version, however.

### **Mediation on Lilypad v1**

How can nodes be trusted to do the compute job?

A resource provider node (compute node), is currently required to put down a deposit of funds before any compute jobs arrive.&#x20;

On a network of compute nodes, there is also mediator nodes, whose job is to check that nodes in the network are correctly running the submitted jobs (eg. by running the job itself to check for correctness)

If a resource node is found to have cheated and not run the job, the penalty for doing so is high & their deposit is significantly slashed.\
\
While not every job will be verified for truthiness, a good analogy is to think of a train ticket inspector on a train. You may not always have your ticket checked, but if the fine for not buying a train ticket is high enough (let's say several ether!), then you will more than likely spend a small amount of gwei buying the ticket, rather than risking the fine and being kicked off the train. :railway\_car:\
\
Currently, the mediation (or checking that nodes in the network are correctly running submitted jobs) that happens on a smart contract called job is provided by a Lilypad default mediator. \
However, if you don't trust our mediator then you can run your own mediator and run compute nodes that trust your mediator instead.\
\


\
\
Read more about these in the [whitepaper.md](../research-and-vision/whitepaper.md "mention")\
