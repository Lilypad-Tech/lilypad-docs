---
description: >-
  Lilypad v0 is a "bridge" for running Bacalhau compute jobs via a smart
  contracts.
---

# Architecture

### Overview

Lilypad is a ‘bridge’ to enable computation jobs from smart contracts. The aim of Lilypad v0 was to create an integration for users to call Bacalhau jobs directly from their solidity smart contracts and hence enable interactions and innovations between on-chain and off-chain compute.\
\
Lilypad v0 is a proof of concept bridge which runs off the public (free to use) Bacalhau compute network. As such, the reliability of jobs on this network are not guaranteed.

> If you have a need for reliable compute based on this infrastructure - get in touch with us.

<figure><img src="../../../../.gitbook/assets/Lilypad Architecture.png" alt=""><figcaption><p>Lilypad v0 on the FVM Network</p></figcaption></figure>

A user contract implements the LilypadCaller interface and to call a job, they make a function call to the deployed LilypadEvents contract.

This contract emits an event which the Lilypad bridge daemon listens for and then forwards on to the Bacalhau network for processing.

Once the job is complete, the results are returned back to the originating user contract from the bridge code.

<figure><img src="https://user-images.githubusercontent.com/12529822/224299570-366bde1c-1f48-4af9-9d7c-0d4f8a0fc1fc.png" alt=""><figcaption><p>Note: runBacalhauJob() is now runLilypadJob()</p></figcaption></figure>

See more about how Bacalhau & Lilypad are related below

{% embed url="https://www.notion.so/7-Introduction-to-Bacalhau-Decentralised-Compute-over-Data-AI-ML-DeSci-fbef1ef73b4e479a9b209be8d29cb58f" %}

{% embed url="https://youtu.be/drwcj2kk6bA" %}
