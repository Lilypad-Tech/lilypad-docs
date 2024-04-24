---
description: The below are instructions for running on the public Lilypad testnet.
---

# Run a Node

### Adding a node

The testnet has a base currency of ETH, as well as a utility token called LP. You will receive LP to pay for jobs (and nodes to stake).

#### Metamask

We suggest using Metamask with custom settings to make things easier. Once you have it installed and setup, here are the settings you should use:

* Network name: Lilypad v3 Milkyway testnet
* New RPC URL:[ http://testnet.lilypad.tech:8545](http://testnet.lilypad.tech:8545/)
* Chain ID: 1337
* Currency symbol: ETH
* Block explorer URL: (leave blank)

#### Fund your wallet with ETH and LP

To obtain funds, go to[ http://faucet.lilypad.tech:8080](http://faucet.lilypad.tech:8080/)

The faucet will give you both ETH (to pay for gas) and LP (to stake and pay for jobs).

### Prerequisites

* Linux (latest Ubuntu LTS recommended)
* Nvidia GPU
* Nvidia drivers
* Docker
* Nvidia docker drivers

#### Install Bacalhau

```
cd /tmp

wget https://github.com/bacalhau-project/bacalhau/releases/download/v1.3.0/bacalhau_v1.3.0_linux_amd64.tar.gz

tar xfv bacalhau_v1.3.0_linux_amd64.tar.gz

sudo mv bacalhau /usr/bin/bacalhau

sudo mkdir -p /app/data/ipfs

sudo chown -R $USER /app/data
```

#### Install Lilypad

```
# Detect your machine's architecture and set it as $OSARCH
OSARCH=$(uname -m | awk '{if ($0 ~ /arm64|aarch64/) print "arm64"; else if ($0 ~ /x86_64|amd64/) print "amd64"; else print "unsupported_arch"}') && export OSARCH
# Detect your operating system and set it as $OSNAME
OSNAME=$(uname -s | awk '{if ($1 == "Darwin") print "darwin"; else if ($1 == "Linux") print "linux"; else print "unsupported_os"}') && export OSNAME;
# Download the latest production build
curl https://api.github.com/repos/lilypad-tech/lilypad/releases/latest | grep "browser_download_url.*lilypad-$OSNAME-$OSARCH" | cut -d : -f 2,3 | tr -d \" | wget -qi - -O lilypad
# Make Lilypad executable and install it
chmod +x lilypad
sudo mv lilypad /usr/local/bin/lilypad
```

#### Write env file

You will need to create an environment file for your node. /app/lilypad/resource-provider-gpu.env should contain:

```
WEB3_PRIVATE_KEY=YOUR_PRIVATE_KEY (the private key from a NEW metamask wallet FOR THE COMPUTE NODE)
```

This is the key where you will get paid in LP tokens for jobs run on the network.

{% hint style="info" %}
NOTE: YOU MUST NOT REUSE YOUR COMPUTE NODE KEY AS A CLIENT, EVEN FOR TESTING: THIS WILL RESULT IN FAILED JOBS AND WILL NEGATIVELY IMPACT YOUR COMPUTE NODE SINCE THE WALLET ADDRESS IS HOW NODES ARE IDENTIFIED ON THE NETWORK
{% endhint %}

#### Install systemd unit for Bacalhau:

Open /etc/systemd/system/bacalhau.service in your favourite editor (hint: sudo editor /etc/systemd/system/bacalhau.service)

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

Open /etc/systemd/system/lilypad-resource-provider.service in your favourite editor&#x20;

{% hint style="info" %}
Hint: sudo editor /etc/systemd/system/lilypad-resource-provider.service
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

Check they are running with systemctl status as usual, and debug with journalctl if needed - eg, sudo journalctl -uf lilypad-resource-provider will give you the live output from your Lilypad node. Please report issues on Bacalhau #lilypad-general Slack. You should see your resource provider start accepting jobs on the network in the logs.

#### Security

If you want to allowlist only certain modules (e.g. Stable Diffusion modules), so that you can control exactly what code runs on your nodes (which you can audit to ensure that they are secure and will have no negative impact on your nodes), you can do that by setting an environment variable OFFER\_MODULES in the GPU provider to a comma separated list of module names, e.g. “sdxl:v0.9-lilypad1,stable-diffusion:v0.0.1”

See https://github.com/bacalhau-project/lilypad/#available-modules for a list of modules.\
