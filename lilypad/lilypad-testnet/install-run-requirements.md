---
description: Instructions for installing the Lilypad CLI on your machine
---

# Installation (CLI)

## Install Lilypad CLI

The installation process for the Lilypad CLI involves several automated steps to configure it for your specific system. Initially, the setup script identifies your computer's architecture and operating system to ensure compatibility. It will then download the latest production build of the Lilypad CLI directly from the official GitHub repository using `curl` and `wget`.

Once the CLI tool is downloaded, the script sets the necessary permissions to make the executable file runnable. It then moves the executable to a standard location in your system's path to allow it to be run from any terminal window.

### 1. Install via officially released binaries

Lilypad offers two distinct installation options to cater to different roles within the network: one for the users of Lilypad and another for resource providers who supply the computational resources to the Lilypad Network.

Select the appropriate installation based on your role:

{% tabs %}
{% tab title="CLI Users" %}
```bash
# Detect your machine's architecture and set it as $OSARCH
OSARCH=$(uname -m | awk '{if ($0 ~ /arm64|aarch64/) print "arm64"; else if ($0 ~ /x86_64|amd64/) print "amd64"; else print "unsupported_arch"}') && export OSARCH;
# Detect your operating system and set it as $OSNAME
OSNAME=$(uname -s | awk '{if ($1 == "Darwin") print "darwin"; else if ($1 == "Linux") print "linux"; else print "unsupported_os"}') && export OSNAME;
# Download the latest production build
curl https://api.github.com/repos/lilypad-tech/lilypad/releases/latest | grep "browser_download_url.*lilypad-$OSNAME-$OSARCH-cpu" | cut -d : -f 2,3 | tr -d \" | wget -qi - -O lilypad

# Make Lilypad executable and install it
chmod +x lilypad
sudo mv lilypad /usr/local/bin/lilypad
```
{% endtab %}

{% tab title="Resource Providers" %}
```bash
# Detect your machine's architecture and set it as $OSARCH
OSARCH=$(uname -m | awk '{if ($0 ~ /arm64|aarch64/) print "arm64"; else if ($0 ~ /x86_64|amd64/) print "amd64"; else print "unsupported_arch"}') && export OSARCH;
# Detect your operating system and set it as $OSNAME
OSNAME=$(uname -s | awk '{if ($1 == "Darwin") print "darwin"; else if ($1 == "Linux") print "linux"; else print "unsupported_os"}') && export OSNAME;
# Download the latest production build
curl https://api.github.com/repos/lilypad-tech/lilypad/releases/latest | grep "browser_download_url.*lilypad-$OSNAME-$OSARCH-gpu" | cut -d : -f 2,3 | tr -d \" | wget -qi - -O lilypad

# Make Lilypad executable and install it
chmod +x lilypad
sudo mv lilypad /usr/local/bin/lilypad
```
{% endtab %}
{% endtabs %}

### 2. Set WEB3\_PRIVATE\_KEY

You're required to set your private key environment variable, `WEB3_PRIVATE_KEY`, to interact securely with the network.&#x20;

{% hint style="info" %}
A [`WEB3_PRIVATE_KEY`](https://docs.lilypad.tech/lilypad/lilypad-milky-way-testnet/install-run-requirements#id-2.-set-web3\_private\_key) can be retrieved from the Metamask account details menu. For more info, check out [this](https://support.metamask.io/managing-my-wallet/secret-recovery-phrase-and-private-keys/how-to-export-an-accounts-private-key/) official guide from Metamask on viewing a wallet's private key.
{% endhint %}

```bash
export WEB3_PRIVATE_KEY=<your private key>
```

{% hint style="warning" %}
To use the Lilypad CLI, the set private key will need to hold [Lilypad testnet tokens](quick-start/funding-your-wallet-from-faucet.md) and Arbitrum Sepolia ETH ([3rd party faucet list](https://arbitrum.faucet.dev/ArbSepolia)).&#x20;
{% endhint %}

### 3. Verify installation

To verify the installation, running `lilypad` in the terminal should display a list of available commands, indicating that Lilypad CLI is ready to use.

```bash
Lilypad

Usage:
  lilypad [command]

Available Commands:
  completion        Generate the autocompletion script for the specified shell
  help              Help about any command
  mediator          Start the lilypad mediator service.
  resource-provider Start the lilypad resource-provider service.
  run               Run a job on the Lilypad network.
  solver            Start the lilypad solver service.

Flags:
  -h, --help   help for lilypad

Use "lilypad [command] --help" for more information about a command.
```

Thats it! You've successfully installed the Lilypad CLI on your machine! [🎉](https://emojipedia.org/party-popper)
