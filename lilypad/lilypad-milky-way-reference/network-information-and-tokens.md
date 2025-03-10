---
description: >-
  The below are instructions for setting up and running on the public Lilypad
  testnet, including adding a node, obtaining necessary funds, installing
  required software, and ensuring security measures.
---

# Run a Node

### Adding a node

The testnet has a base currency of ETH, as well as a utility token called LP. LP is used for both paying for jobs and staking nodes. To add a node to the testnet, follow these steps:

#### MetaMask

We recommend using MetaMask with custom settings to make things easier. Once you have it installed and setup, here are the settings you should use:

* Network name: Lilypad v3 Milky Way testnet
* New RPC URL:[ http://testnet.lilypad.tech:8545](http://testnet.lilypad.tech:8545/)
* Chain ID: 1337
* Currency symbol: ETH
* Block explorer URL: (leave blank)

#### Fund your wallet with ETH and LP

To obtain testnet ETH and LP, go to the [Lilypad faucet](http://faucet.lilypad.tech) and enter your ETH address.

The faucet will give you both ETH (to pay for gas) and LP (to stake and pay for jobs).

### Prerequisites

* Linux (latest Ubuntu LTS recommended)
* Nvidia GPU
* Nvidia drivers
* Docker
* Nvidia docker drivers

#### Install Bacalhau

Bacalhau is a peer-to-peer network of nodes that enables decentralized communication between computers. The network consists of two types of nodes, which can communicate with each other.

To install Bacalhau, run the following in your terminal:

```bash
cd /tmp

wget https://github.com/bacalhau-project/bacalhau/releases/download/v1.3.0/bacalhau_v1.3.0_linux_amd64.tar.gz

tar xfv bacalhau_v1.3.0_linux_amd64.tar.gz

sudo mv bacalhau /usr/bin/bacalhau

sudo mkdir -p /app/data/ipfs

sudo chown -R $USER /app/data
```

#### Install Lilypad

1.  **With Go toolchain**

    ```bash
    go install github.com/lilypad-tech/lilypad@latest
    ```
2.  **Via official released binaries**

    ```bash
    # Detect your machine's architecture and set it as $OSARCH
    OSARCH=$(uname -m | awk '{if ($0 ~ /arm64|aarch64/) print "arm64"; else if ($0 ~ /x86_64|amd64/) print "amd64"; else print "unsupported_arch"}') && export OSARCH
    # Detect your operating system and set it as $OSNAME
    OSNAME=$(uname -s | awk '{if ($1 == "Darwin") print "darwin"; else if ($1 == "Linux") print "linux"; else print "unsupported_os"}') && export OSNAME;
    # Download the latest production build
    curl https://api.github.com/repos/lilypad-tech/lilypad/releases/latest | grep "browser_download_url.*lilypad-$OSNAME-$OSARCH" | cut -d : -f 2,3 | tr -d \" | wget -i - -O lilypad
    # Make Lilypad executable and install it
    chmod +x lilypad
    sudo mv lilypad /usr/local/bin/lilypad
    ```

#### Write env file

You will need to create an environment file for your node. `/app/lilypad/resource-provider-gpu.env` should contain:

```
WEB3_PRIVATE_KEY=<YOUR_PRIVATE_KEY> (the private key from a NEW MetaMask wallet FOR THE COMPUTE NODE)
```

This is the key where you will get paid in LP tokens for jobs run on the network.

{% hint style="warning" %}
You must not reuse your compute node key as a client, even for testing: this will result in failed jobs and will negatively impact your compute node since the wallet address is how nodes are identified on the network.
{% endhint %}

#### Install systemd unit for Bacalhau

systemd is a system and service manager for Linux operating systems. systemd operates as a central point of control for various aspects of system management, offering features like parallelization of service startup, dependency-based service management, process supervision, and more.

To install systemd, open `/etc/systemd/system/bacalhau.service` in your preferred editor:

{% hint style="info" %}
Hint: `sudo editor /etc/systemd/system/bacalhau.service`
{% endhint %}

<pre><code>[Unit]
Description=Lilypad V2 Bacalhau
After=network-online.target
Wants=network-online.target systemd-networkd-wait-online.service

[Service]
Environment="LOG_TYPE=json"
Environment="LOG_LEVEL=debug"
Environment="HOME=/app/lilypad"
Environment="BACALHAU_SERVE_IPFS_PATH=/app/data/ipfs"
<strong>Restart=always
</strong>RestartSec=5s
ExecStart=/usr/bin/bacalhau serve --node-type compute,requester --peer none --private-internal-ipfs=false

[Install]
WantedBy=multi-user.target
</code></pre>

#### Install systemd unit for GPU provider

Open `/etc/systemd/system/lilypad-resource-provider.service` in your preferred editor.

{% hint style="info" %}
Hint: `sudo editor /etc/systemd/system/lilypad-resource-provider.service`
{% endhint %}

```
[Unit]
Description=Lilypad V2 Resource Provider GPU
After=network-online.target
Wants=network-online.target systemd-networkd-wait-online.service

[Service]
Environment="LOG_TYPE=json"
Environment="LOG_LEVEL=debug"
Environment="HOME=/app/lilypad"
Environment="OFFER_GPU=1"
EnvironmentFile=/app/lilypad/resource-provider-gpu.env
Restart=always
RestartSec=5s
ExecStart=/usr/bin/lilypad resource-provider 

[Install]
WantedBy=multi-user.target
Reload systemd's units/daemons (you will need to do this again if you ever change the systemd unit files that we wrote, above)
sudo systemctl daemon-reload
Start systemd units:
sudo systemctl start bacalhau
sudo systemctl start lilypad-resource-provider
```

Check that they are running with systemctl status as usual, and debug with journalctl if needed.

For example: `sudo journalctl -uf lilypad-resource-provider` will give you the live output from your Lilypad node. You should see your resource provider start accepting jobs on the network in the logs.

{% hint style="info" %}
Please report issues on Bacalhau #lilypad-general Slack.&#x20;
{% endhint %}

### Security

If you want to allowlist only certain modules (e.g. Stable Diffusion modules), so that you can control exactly what code runs on your nodes (which you can audit to ensure that they are secure and will have no negative impact on your nodes), you can do that by setting an environment variable `OFFER_MODULES` in the GPU provider to a comma separated list of module names, e.g. `sdxl:v0.9-lilypad1,stable-diffusion:v0.0.1`

Visit the [Lilypad GitHub](https://github.com/bacalhau-project/lilypad/#available-modules) for a full list of available modules.
