---
description: Common FAQs when running a Lilypad node
---

# Troubleshooting

READ THESE RESOURCES BEFORE ASKING QUESTIONS!!!

* [Lilybit Rewards info](https://blog.lilypadnetwork.org/incentivenet-lilybit-reward-calculations)
* [Lilybit Leaderboard](https://info.lilypad.tech/leaderboard)

## Dont see your issue below?

Ask in the Lilypad Discord [#i-need-help](https://discord.com/channels/1212897693450641498/1230231823674642513) channel. Please follow the [Resource Provider Ticket format](https://github.com/Lilypad-Tech/internal/issues/171):

* Description (including Lilypad version running on your node)
* Hardware Info (including Linux/Windows version)
* Related Blockchain/ETH addressers of Transaction hashes
* Output Logs - `sudo systemctl status lilypad-resource-provider`
* Related links/urls
* Screenshots

{% hint style="info" %}
**IMPORTANT:** When sharing screenshots of your logs or node information, make sure to **remove or block out any references to your node's private key.** Keeping your private key safe and away from the public eye is crucial!
{% endhint %}

## FAQ

### Q: I haven’t seen any POW -> Common Issues to check first!

1. Ensure the RP (node) is running the latest [Lilypad version](https://docs.lilypad.tech/lilypad/hardware-providers/run-a-node#update-lilypad-version)
2. Confirm network activity. Is the RP transacting on [Arbiscan](https://sepolia.arbiscan.io/) (Sepolia) with transactions verified and running consistently?

* [https://sepolia.arbiscan.io/address/](https://sepolia.arbiscan.io/address/)”**wallet-address”**
* Is the RP online in the [Leaderboard](https://info.lilypad.tech/leaderboard) and in the [node status dashboard](https://info.lilypad.tech/node-status)?

3. If the RP public keys are not found within the Arbiscan network or Leaderboard

* does the RP have [enough](https://docs.lilypad.tech/lilypad/hardware-providers/run-a-node#fund-your-wallet-with-eth-and-lp) Lilypad Tokens (LP)?
* does the RP have [enough](https://docs.lilypad.tech/lilypad/hardware-providers/run-a-node#fund-your-wallet-with-eth-and-lp) Arbitrum ETH?

4. Updating and restarting the Lilypad services regularly(daily) is encouraged throughout IncentiveNet.

### Q: My node says it isn’t online.

Before restarting the node, check the logs and Arbiscan to see if the RP is running properly. If so, and the node is still listed in the [Leaderboard](https://info.lilypad.tech/leaderboard) as offline, try the steps below. If this doesn't work, raise a ticket with our team.

**Restart lilypad+bacalhau services**

```bash
sudo systemctl restart lilypad

sudo systemctl restart bacalhau
```

Check out this [video guide](https://www.youtube.com/watch?v=I5ZOk-OkFdc) for setting up a Lilypad node using Ubuntu Linux. Note, you may notice in the Metamask setup part of the video the Network name and RPC URL are old. Disregard this, the video was recorded with our old testnet info not the current Lilypad testnet [details](https://docs.lilypad.tech/lilypad/lilypad-testnet/quick-start/setting-up-metamask) on Arbitrum. Otherwise, the directions here are current. Read more about running a Lilypad node in the [docs](https://docs.lilypad.tech/lilypad/hardware-providers/run-a-node).

{% embed url="https://www.youtube.com/watch?v=I5ZOk-OkFdc" %}

### Q: When do Lilybit\_ rewards earned or rewards slashed appear in the Leaderboard?

Once a day at 00:10 UTC. If no rewards appear after 24 hours of expected uptime, view the logs and Arbiscan transactions from the resource provider to ensure online status.

### Q: Can I become a Lilypad Resource Provider with just a CPU and no GPU?

Resource Providers can run on the Lilypad Network without a GPU, however only hardware with a GPU is currently rewarded with Lilybit\_ rewards.

### Q: How do I run multiple GPU’s from a node?

Recommendation guide using Proxmox found [here](https://github.com/Lilypad-Tech/lilypad-tools/blob/main/proxmox/multi-gpu-proxmox.md). More on this coming soon!

### Q: How does slashing work on Lilypad?

Each day of node (RP) downtime, 10% of the total points earned will be slashed (per day). This was implemented with a focus on long term partners contributing meaningfully to the network.  Important as early rewards are worth more than rewards in later stages of the[ IncentiveNet](https://blog.lilypadnetwork.org/incentivenet-lilybit-reward-calculations).&#x20;

The requirement to not be slashed is only 4 hrs/day of uptime. We may reevaluate this mechanism,  please provider any community feedback [here](https://github.com/orgs/Lilypad-Tech/discussions/16)!

### Q: Will I lose reward multipliers if my node is offline?

The way the system is setup currently, a RP will lose the [4X daily multiplier](https://blog.lilypadnetwork.org/incentivenet-lilybit-reward-calculations) if  the hashrate call (every 4 hours) is missed. If the PoW happens in the window of time that a node is restarting/offline, then it's missed.&#x20;

However, a RP will still receive a multiplier relative to how many 4-hour windows of POWs completed in that day. This figure shows the daily multiplier for a given number of 4-hour windows of POWs completed in a day.

<figure><img src="../.gitbook/assets/daily_mult_v_N_POW.png" alt="" width="563"><figcaption></figcaption></figure>

### Q: Are **there required updates needed to maintain my node software with Lilypad?**

Resource providers are expected to have the [latest Lilypad version](https://docs.lilypad.tech/lilypad/hardware-providers/run-a-node#update-lilypad-version) installed on their systems. The installation instructions can be found [here](https://docs.lilypad.tech/lilypad/lilypad-testnet/install-run-requirements).

To stay up to date with the latest releases, check the [updates-rp channel](https://discord.com/channels/1212897693450641498/1256179769356189707) in the Lilypad Discord or visit the [Lilypad GitHub](https://github.com/Lilypad-Tech/lilypad). Along the top menu, click the "Watch" dropdown and you will see a section named "Custom". Selecting "Releases" will allow you to get notified of any new releases!

### Q: Bacalhau ipfs init error

One fix is to install kubo (goipfs) and then export the path to /app/data/ipfs using:

```bash
export IPFS_PATH=/app/data/ipfs
```

Export the path first, then turn bacalhau back on and see if that corrects it.

### Q: CompatNotSupportedOnDevice Error

The CUDA version of the RP does not match the GPU driver. Please refer to this [Nvidia GPU Driver guide](https://docs.nvidia.com/deploy/cuda-compatibility) to repair installation.&#x20;

### Q: Unknown Error Code: 222

Indicates that the cuda version of the RP is incorrect. RP need to install the CUDA which suitable for the gpu type and compile Lilypad by themselves

### Q: **How can I check the status of my Lilypad node once it's running?**

To check if the RP is running use the following command:

```bash
sudo systemctl status lilypad-resource-provider
```

This will give a live output from the Lilypad node. The logs will show the node running and accepting jobs on the network.

Run the following command to get more info from your node:

```bash
sudo journalctl -u lilypad-resouce-provider.service -f
```

Read more in the Lilypad [docs](https://docs.lilypad.tech/lilypad/hardware-providers/run-a-node#view-node-status).

### Q: I’m getting an error of “invalid hex character 'r' in private key”

This is more than likely due to you trying to export your mnemonic seed phrase instead of the private key. A private key typically appears like this: `4c0883a69102937d6231471b5dbb6204fe512961708279df95b4a2200eb6b5e7` and consists of 64 hexadecimal characters.&#x20;

Check out the [MetaMask official guide to retrieve your private key](https://support.metamask.io/managing-my-wallet/secret-recovery-phrase-and-private-keys/how-to-export-an-accounts-private-key/).

### Q: How do I setup my Metamask wallet?

* [Import](https://docs.lilypad.tech/lilypad/lilypad-testnet/quick-start/setting-up-metamask#setting-up-metamask) a custom network (Lilypad)
* [Locate](https://support.metamask.io/managing-my-wallet/secret-recovery-phrase-and-private-keys/how-to-export-an-accounts-private-key/) a wallet's Private Key
* [Import](https://docs.lilypad.tech/lilypad/lilypad-testnet/quick-start/funding-your-wallet-from-faucet#import-testnet-tokens) the Lilypad Token to a wallet

### Q: How do I get testnet LP and ETH (Arbitrum Sepolia ETH)?

* [Fund](https://docs.lilypad.tech/lilypad/hardware-providers/run-a-node#write-env-file) a wallet with LP and ETH&#x20;
* No ETH or LP in your wallet? ([import custom network and import the tokens](https://lilypad.team/discord))&#x20;

Join our [Discord](https://lilypad.team/discord) for more help!

