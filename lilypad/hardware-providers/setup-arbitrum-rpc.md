---
description: Personal RPC endpoint for a Lilypad Resource Provider
---

# Setup Arbitrum RPC

The Lilypad Network uses the Arbitrum Sepolia Testnet to settle compute transactions. This guide walks through the steps of setting up a personal RPC endpoint for Arbitrum Sepolia using [Alchemy](https://www.alchemy.com/).

{% hint style="info" %}
The Lilypad Network is not responsible for issues caused by misconfigured RPC endpoints. Please use at your own risk!
{% endhint %}

This personal RPC endpoint allows Resource Providers (RP) to avoid reliability issues with the RPC endpoints used by Lilypad ensuring rewards can be earned and jobs can be run consistently. RPs running a personal RPC endpoint contribute to the fault tolerance and decentralization of the Lilypad Network! Read more in the Alchemy Arbitrum [docs](https://docs.alchemy.com/reference/arbitrum-api-quickstart).

{% hint style="info" %}
This guide demonstrates how to use Alchemy's RPC, but you can substitute any Arbitrum Sepolia RPC that supports WebSockets.
{% endhint %}

## Setup Alchemy account

[Create an account](https://dashboard.alchemy.com/) and login to the Alchemy dashboard.

Select a “free” account as the compute units provided should be sufficient to run a Lilypad RP. The free service provides 300 million compute units per month.

<figure><img src="../.gitbook/assets/Screenshot 2024-09-17 at 10.39.32 AM.png" alt=""><figcaption></figcaption></figure>

Select “skip bonus” or input a credit card with billing info (the card will not be charged unless the compute credits in the free tier are used).

## Setup RPC endpoint for Arbitrum Sepolia

In the “overview” section of the Alchemy dashboard, navigate to “My app” and select “Endpoints”. If an app was not created upon login, create a new one by selecting "Create new app"

<figure><img src="../.gitbook/assets/alchemy1-1.png" alt=""><figcaption></figcaption></figure>

By selecting “Endpoints”, the “Networks” tab will open providing an option to configure the Arbitrum API.

* Select “Sepolia”
* Select “Websockets”

<figure><img src="../.gitbook/assets/alchemy1.png" alt=""><figcaption></figcaption></figure>

The RPC endpoint for Arbitrum Sepolia is ready to be used with the Lilypad Resource Provider:

<figure><img src="../.gitbook/assets/alchemy3.png" alt=""><figcaption></figcaption></figure>

Metrics for the RPC can be viewed in the “Metrics” tab.

<figure><img src="../.gitbook/assets/Screenshot 2024-09-17 at 11.00.45 AM.png" alt=""><figcaption></figcaption></figure>

## Use the new RPC endpoint

{% hint style="info" %}
This is guide is for individuals running a Lilypad Resource provider, find more info [here](https://docs.lilypad.tech/lilypad/hardware-providers/run-a-node).
{% endhint %}

Lilypad RPs can use a personal RPC endpoint with a few simple steps. Only Web-socket (WSS) connections are supported.

### **Docker users**

Stop the existing Lilypad Resource Provider (RP) before setting up the new RPC.&#x20;

Locate the Lilypad RP Docker container using:

```
docker ps
```

Stop the container using the PID:

```
docker stop <container ID>
```

Use this command to start the lilypad-resource-provider.service with the new RPC:

```
docker run -d --gpus all -e WEB3_PRIVATE_KEY=<private-key> -e WEB3_RPC_URL=wss://arb-sepolia.g.alchemy.com/v2/some-id-from-alchemy --restart always ghcr.io/lilypad-tech/resource-provider:latest
```

Check the status of the container:

```
docker logs <container ID>
```

### **Ubuntu users**

Stop the existing Lilypad RP (if the node is not running, disregard this first step):

```
sudo systemctl stop bacalhau
sudo systemctl stop lilypad-resource-provider
```

Update lilypad-resource-provider.service with the new RPC:

```
sudo nano /etc/systemd/system/lilypad-resource-provider.service
```

Add following line to \[Service] section:

```
Environment="WEB3_RPC_URL=wss://arb-sepolia.g.alchemy.com/v2/some-alchemy-id"
```

<figure><img src="../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

Reboot the node:

```
sudo reboot
```

If the Lilypad RP was [setup](https://docs.lilypad.tech/lilypad/hardware-providers/run-a-node/linux#install-systemd-unit-for-bacalhau) properly as a systemd service, the RP will reboot using the new RPC.
