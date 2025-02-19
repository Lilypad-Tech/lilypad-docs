---
description: Common FAQs when running a Lilypad node
---

# Troubleshooting

{% hint style="info" %}
Please view these resources before asking questions!

* [Lilybit Rewards info](https://blog.lilypadnetwork.org/update-to-the-lilybit-rewards-calculation)
* [Lilybit Leaderboard](https://info.lilypad.tech/leaderboard)
{% endhint %}

## Don't see your issue below?

For **complex issues, bug reports, or feature requests,** open a discussion in the Lilypad-Tech Github organization discussion [board](https://github.com/orgs/Lilypad-Tech/discussions).

* Navigate to the discussion [board](https://github.com/orgs/Lilypad-Tech/discussions), select "New Discussion", choose "rp-issues", and fill out the template.
* Without a discussion opened, our team will not be able to support the problem.

**For quick questions or minor issues,** use the Lilypad Discord [#i-need-help](https://discord.com/channels/1212897693450641498/1230231823674642513) channel and provide the following info.

* Description (including Lilypad version running on your node)
* Hardware Info (including Linux/Windows version)
* Related blockchain/ETH addresses of transaction hashes
* Output Logs - `sudo systemctl status lilypad-resource-provider`
* Related links/urls
* Screenshots

{% hint style="info" %}
**IMPORTANT:** When sharing screenshots of your logs or node information, make sure to **remove or block out any references to your node's private key.** Keeping your private key safe and away from the public eye is crucial!
{% endhint %}

## FAQ

### Common issues to check first!

1. Ensure the RP (node) is running the latest [Lilypad version](https://docs.lilypad.tech/lilypad/hardware-providers/run-a-node#update-lilypad-version) for your preferred environment
2. Does the RP have [enough](https://docs.lilypad.tech/lilypad/hardware-providers/run-a-node#fund-your-wallet-with-eth-and-lp) Lilypad Tokens (LP) and Arbitrum ETH?
3. Updating and restarting the Lilypad services regularly (daily) is encouraged throughout IncentiveNet.

## Run a node (Resource Provider - RP)

### How do I keep track of Lilypad version releases and other important announcements?

The [updates-rp](https://discord.com/channels/1212897693450641498/1256179769356189707) Discord channel is the primary location for Resource Provider announcements. Announcements in this channel are also posted on the Lilypad [updates](https://updates.lilypad.tech/) page.

Lilypad supports Resource Providers using the Docker find instructions [here](https://docs.lilypad.tech/lilypad/hardware-providers/docker).&#x20;

If this doesn't solve the problem, [raise a ticket](https://discord.com/channels/1212897693450641498/1230231823674642513) with our team.

### **How can I check the status of my Lilypad RP once it's running?**

To check if the RP is running use the following command:

```bash
docker logs resource-provider
```

This will give a live output from the Lilypad node. The logs will show the node running and accepting jobs on the network.

Run the following command to get info from Bacalhau

```bash
docker logs bacalhau
```

### Can I become a Lilypad RP with just a CPU and no GPU?

Resource Providers can run on the Lilypad Network without a GPU, however only hardware with a GPU is currently rewarded with Lilybit\_ rewards.

### My docker RP is turning on, but showing errors stating it is not providing a Resource Offer.

Typically this occurs when an old version of Lilypad is still running on the instance.&#x20;

1. Ensure the Bacalhau and Lilypad systemd services are stopped and removed.

```bash
sudo systemctl stop bacalhau
```

```bash
sudo systemctl stop lilypad-resource-provider
```

2. Disable the systemd services so they start on boot:

```bash
sudo systemctl disable bacalhau
```

```bash
sudo systemctl disable lilypad-resource-provider
```

3. Delete the service files from the systemd directory.

\*\*Note: Be extremely careful when using `sudo` to remove files.

```bash
 sudo rm /etc/systemd/system/bacalhau.service
```

```bash
 sudo rm /etc/systemd/system/lilypad-resource-provider.service
```

4. Reload the systemd daemon to apply the changes.

```bash
sudo systemctl daemon-reload
```

### Can I run a Lilypad RP on Windows?

Lilypad RPs currently only support Linux installs. Running a RP on Windows is currently experimental.

### How do I run multiple GPU’s on one server?

Recommendation guide using Proxmox found [here](https://github.com/Lilypad-Tech/lilypad-tools/blob/main/proxmox/multi-gpu-proxmox.md). More on this coming soon!

### Can I run multiple Lilypad RPs on one GPU?

No, this would be considered detrimental to the Lilypad network and cannot be rewarded at this time.

In order to run jobs successfully, Lilypad RPs must ensure all resources on the server are available. If a single GPU is running many RPs and splitting the server resources between them, this causes each RP to not have enough resources to run a Lilypad job.

### How do I setup a personal RPC for Arbitrum Sepolia?

Here's a quick guide on setting up your own RPC for a Lilypad node.

{% embed url="https://www.youtube.com/watch?v=INKpdrfF0Xs" %}

### CompatNotSupportedOnDevice Error

The CUDA version of the RP does not match the GPU driver. Please refer to this [Nvidia GPU Driver guide](https://docs.nvidia.com/deploy/cuda-compatibility) to repair installation.

### Unknown Error Code: 222

Indicates that the CUDA version of the RP is incorrect. Install the CUDA version which suitable for the gpu type and compile Lilypad by themselves.

## Lilypad IncentiveNet details

When do Lilybit\_ rewards earned or rewards slashed appear in the Leaderboard? \*\*The leaderboard is currenlty under maintanence, find Lilybits earned by [RPs](https://rp-points.lilypad.tech/) here.

### Are **there required updates needed to maintain my node software with Lilypad on IncentiveNet?**

Resource providers are expected to have the latest Lilypad version installed on their systems. The installation instructions can be found here:

* [Docker](https://docs.lilypad.tech/lilypad/hardware-providers/run-a-node/docker#enable-automatic-updates)

To stay up to date with the latest releases, check the [updates-rp channel](https://discord.com/channels/1212897693450641498/1256179769356189707) in the Lilypad Discord or visit the [Lilypad GitHub](https://github.com/Lilypad-Tech/lilypad). Along the top menu, click the "Watch" dropdown and you will see a section named "Custom". Selecting "Releases" will allow you to get notified of any new releases!

### Can Lilybit rewards be sent to another wallet? Will this function be added in the future?

Currently, it's not possible. However, it's a very good feature request and the team is evaluating!

### I’m getting an error of “invalid hex character 'r' in private key”

This is more than likely due to you trying to export your mnemonic seed phrase instead of the private key. A private key typically appears like this: `4c0883a69102937d6231471b5dbb6204fe512961708279df95b4a2200eb6b5e7` and consists of 64 hexadecimal characters.

Check out the [MetaMask official guide to retrieve your private key](https://support.metamask.io/managing-my-wallet/secret-recovery-phrase-and-private-keys/how-to-export-an-accounts-private-key/).

### How do I setup my Metamask wallet?

* [Import](https://docs.lilypad.tech/lilypad/lilypad-testnet/quick-start/setting-up-metamask#setting-up-metamask) a custom network (Lilypad)
* [Locate](https://support.metamask.io/managing-my-wallet/secret-recovery-phrase-and-private-keys/how-to-export-an-accounts-private-key/) a wallet's Private Key
* [Import](https://docs.lilypad.tech/lilypad/lilypad-testnet/quick-start/setting-up-metamask#import-the-testnet-lp-token) the Lilypad Token to a wallet

### How do I get testnet LP and ETH (Arbitrum Sepolia ETH)?

* [Fund](https://docs.lilypad.tech/lilypad/lilypad-testnet/quick-start/funding-your-wallet-from-faucet) a wallet with LP and ETH
* No ETH or LP in your wallet? ([import custom network and import the tokens](https://docs.lilypad.tech/lilypad/lilypad-testnet/quick-start/setting-up-metamask#import-the-testnet-lp-token))

Join our [Discord](https://lilypad.team/discord) for more help!
