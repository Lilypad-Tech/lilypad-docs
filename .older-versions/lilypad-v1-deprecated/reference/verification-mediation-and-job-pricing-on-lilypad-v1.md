---
description: Current State
---

# Verification, Mediation & Job Pricing on Lilypad v1

{% hint style="info" %}
You can read a much more thorough and academic explanation on these ideas in the [Broken link](broken-reference "mention") and [v1-documents](../../../../research-and-vision/v1-documents/ "mention")
{% endhint %}

This page also comes with a warning:

<figure><img src="https://slack-imgs.com/?c=1&#x26;o1=ro&#x26;url=https%3A%2F%2Fmedia1.giphy.com%2Fmedia%2Fl1KVb2dUcmuGG4tby%2Fgiphy.gif%3Fcid%3D6104955ea8qj2n7xnvh6l1xcxpj51fc5alkzf89gyhu960lk%26ep%3Dv1_gifs_translate%26rid%3Dgiphy.gif%26ct%3Dg" alt=""><figcaption><p>We &#x3C;3 Nerds</p></figcaption></figure>

## Overview

We didn't want to hold back on releasing a testnet build that developers could use straight away to build their awesome ideas on, however, it's worth noting that Lilypad v1 is a minimal modicum-based testnet and the implemented mediation and game theory on this testnet is very much at baby :baby: stage - as are many other aspects of the robust compute network that we are working hard to build.

### **Verification on Lilypad v1**

There is currently **no** verification on smart contract-called Lilypad jobs

Verification **DOES** exist on the CLI version, however.

### **Mediation on Lilypad v1**

How can nodes be trusted to do the compute job?

A resource provider node (compute node), is currently required to put down a deposit of funds before any compute jobs arrive.

On a network of compute nodes, there is also mediator nodes, whose job is to check that nodes in the network are correctly running the submitted jobs (eg. by running the job itself to check for correctness)

:bulb:**Fun fact**: This is also why all jobs on the network currently need to be deterministic!

If a resource node is found to have cheated and not run the job, the penalty for doing so is high & their deposit is significantly slashed.\
\
While not every job will be verified for truthiness, a good analogy is to think of a train ticket inspector on a train. You may not always have your ticket checked, but if the fine for not buying a train ticket is high enough (let's say several ether!), then you will more than likely spend a small amount of Gwei buying the ticket, rather than risking the fine and being kicked off the train. :railway\_car:\
\
Currently, the mediation (or checking that nodes in the network are correctly running submitted jobs) that happens on a smart contract called job is provided by a Lilypad default mediator.\
However, if you don't trust our mediator then you can run your own mediator and run compute nodes that trust your mediator instead.

### Job Pricing

While not every job will take the same amount of time or compute resources to run, currently the network prices all jobs at the same amount.\
\
This will change in future versions to more accurately calculate and charge for the compute resource requirements of a job as well as compensating the compute nodes appropriately.

{% hint style="info" %}
Read more about these ideas in the [Broken link](broken-reference "mention") & [v1-documents](../../../../research-and-vision/v1-documents/ "mention")
{% endhint %}
