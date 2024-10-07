---
description: Information about the Lilybit_ rewards program
---

# Rewards

GPUs contributing to the Lilypad Network can earn Lilybit\_ credits daily, which will be redeemable for Lilypad (LP) mainnet tokens at the Token Generation Event (TGE), expected in Q1 of 2025. To provide compute power and participate in Lilypad's decentralized compute network, Resource Providers (RPs) can accumulate these credits based on their contributions to the network.

Read the in depth breakdown of the Lilybit\_ rewards system [here](https://blog.lilypadnetwork.org/incentivenet-lilybit-reward-calculations).&#x20;

## **tldr:**

* Nodes must be online for a minimum of 4 hours a day continuously (verified with POW efforts) to earn that day’s Lilybit\_ rewards.
* **A 4x multiplier on this base daily rate** is available for nodes that are online and taking jobs over the full day (This is calculated with 1.3195^(number of 4 hour windows GPU is online)).
* The power of the compute being contributed also provides a point multiplier, with the hashrate of a node (determined by the required POW algorithm) determining the multiplier given to a node’s power. 10 points are rewarded for every MHash/sec provided to the network.
* In order to incentivize long term participation in the network, **a node will be slashed 10%** of their total number of points (earned by providing compute power) each day that node isn’t online for at least 4 hours continuously.
* A grace period for RP downtime is now included in the slashing mechanism (Oct-01-2024). RPs will earn 2 days of a “grace period” after every 30 days of continuous service provided. These 2 days will be applied to 2 subsequent down days recorded by the RP allowing the RP to avoid slashing for these 2 days. Grace Period days do not accumulate to more than 2 days ever. Once used the 30 day count to obtain the 2 days restarts. Find more information on slashing in the [IncentiveNet rewards blog post](https://blog.lilypadnetwork.org/incentivenet-lilybit-reward-calculations#heading-continuous-node-service-amp-point-slashing).

## Rewards Leaderboard

The [Lilypad Leaderboard](https://info.lilypad.tech/leaderboard)  provides an up-to-date view of rewards earned by each wallet ID and is updated **once a day** to reflect additional credits earned. RPs can also track the status of their compute contributions with the node status dashboard.

Track the status of a Resource Provider with the [node status dashboard](https://info.lilypad.tech/node-status).

<figure><img src="../.gitbook/assets/Screenshot 2024-08-20 at 1.44.49 PM.png" alt="" width="563"><figcaption></figcaption></figure>
