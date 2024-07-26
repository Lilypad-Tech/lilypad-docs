---
description: Information about the Lilybit_ rewards program
---

# Rewards

Read about the Lilybit\_ rewards program [here](https://blog.lilypadnetwork.org/incentivenet-lilybit-reward-calculations). Use the [Lilypad Leaderboard](https://info.lilypad.tech/leaderboard) to view Lilybit\_ rewards earned and track the status of a Resource Provider.&#x20;

{% hint style="info" %}
This page is a work in progress
{% endhint %}

**TLDR:**

* **GPUs contributing to the Lilypad Network can earn Lilybit\_ credits daily.** Nodes must be online for a minimum of 4 hours a day continuously (verified with POW efforts) to earn that day’s Lilybit\_ rewards.
* **A 4x multiplier on this base daily rate** is available for nodes that are online and taking jobs over the full day (This is calculated with 1.3195^(number of 4 hour windows GPU is online)).
* The power of the compute being contributed also provides a point multiplier, with the hashrate of a node (determined by the required POW algorithm) determining the multiplier given to a node’s power. 10 points are rewarded for every MHash/sec provided to the network.
* In order to incentivize long term participation in the network, **a node will be slashed 10%** of their total number of points (earned by providing compute power) each day that node isn’t online for at least 4 hours continuously.
