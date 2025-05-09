---
description: >-
  Configure a crypto wallet to receive testnet tokens used to interact with the
  Lilypad Network
---

# Setting Up Your Wallet

Both Resource Providers (GPU compute nodes) and those looking to run jobs on the Lilypad network need to set up a Metamask account in order to run jobs on Lilypad. The public key of your wallet address is how you are identified on the network, and is how you can look up the transactions you make on the [Arbitrum Sepolia blockchain explorer](https://etherscan.io/token/0xb50721bcf8d664c30412cfbc6cf7a15145234ad1). You need an account for running jobs, and a separate account for each GPU you want to set up on the network.

The wallet you use for your account must have both ETH (to run smart contracts on Ethereum) and Lilypad (LP) tokens in order to pay for jobs (or receive funds for jobs) on the network.

<figure><img src="../../.gitbook/assets/eth-lp-wallet (1).png" alt="Metamask wallet funded with ETH Arbitrum and Lilypad tokens" width="358"><figcaption><p>A wallet funded with Arbitrum ETH and Lilypad tokens</p></figcaption></figure>

## Create a MetaMask wallet

End users of Lilypad can decide which crypto wallet they would like to use. In this guide, we advise using a [MetaMask](https://metamask.io/) crypto wallet.

* Install [MetaMask Extension](https://metamask.io/download/)

## Connect to the Arbitrum Sepolia Testnet in MetaMask.

The Lilypad Testnet (IncentiveNet) is currently running on the Arbitrum L2 network built on Ethereum.

In order to change to the Arbitrum network in the wallet, open MetaMask and click the network button in the top left of the menu bar:

<figure><img src="../../.gitbook/assets/metamask-step-1.png" alt="" width="355"><figcaption></figcaption></figure>

Then select "Add network":

<figure><img src="../../.gitbook/assets/metamask-step-2.png" alt="" width="352"><figcaption></figcaption></figure>

Next, select "Add a network manually":

<figure><img src="../../.gitbook/assets/metamask-step-3.png" alt="" width="563"><figcaption></figcaption></figure>

Input the required Arbitrum Sepolia Testnet network info, and then "Save":

{% hint style="info" %}
Network info is referenced directly from the Arbitrum Sepolia [documentation](https://docs.arbitrum.io/arbitrum-bridge/quickstart#step-2-add-the-preferred-network-to-your-wallet).
{% endhint %}

* **Network name**: Arbitrum Sepolia
* **New RPC URL**: [https://sepolia-rollup.arbitrum.io/rpc](https://sepolia-rollup.arbitrum.io/rpc)
* **Chain ID**: 421614
* **Currency symbol**: ETH
* **Block explorer URL**: [https://sepolia.arbiscan.io](https://sepolia.arbiscan.io) (optional)

<figure><img src="../../.gitbook/assets/metamask-step-4.png" alt="" width="375"><figcaption></figcaption></figure>

### Import the Testnet LP token

The wallet is now setup and will display an ETH (Arbitrum Sepolia) token balance. In order to also display the LP token balance, the LP token will need to be imported.

Select "Import tokens" from the three dot menu next to the network name:

<figure><img src="../../.gitbook/assets/import token (1).png" alt="" width="351"><figcaption></figcaption></figure>

Select "Custom token" and add the Lilypad token contract address and token symbol. Then "Save".

* Token contract address: `0x0352485f8a3cB6d305875FaC0C40ef01e0C06535`
* Token symbol: `LP`

<figure><img src="../../.gitbook/assets/import-token-step-2 (1).png" alt="" width="350"><figcaption></figcaption></figure>

You should now see both ETH and LP listed in the wallet (initial ETH and LP balances will be 0).

<figure><img src="../../.gitbook/assets/import-token-step-3 (1).png" alt="" width="352"><figcaption></figcaption></figure>

Now you're ready to fund the wallet with testnet LP and ETH tokens!

## Funding Your Wallet

Get Testnet Lilypad Tokens (LP) and Arbitrum Sepolia Testnet ETH

**tldr:** To obtain funds, first ensure the wallet is connected to the Arbitrum Sepolia network. then, collect LP and ETH tokens from these faucets:

* [Lilypad Testnet tokens (LP)](https://faucet-testnet.lilypad.tech/)
* [Arbitrum Sepolia ETH](https://arbitrum.faucet.dev/ArbSepolia) (3rd party faucet list)

## Faucet Guide

### Get Testnet LP tokens

Find out why you need tokens in the [FAQs](../../faq.md)

{% hint style="info" %}
You must be a member of [the Lilypad Discord](https://discord.gg/tnE8SMmsxW) to claim tokens
{% endhint %}

Follow these steps to successfully claim your Testnet LP tokens:&#x20;

1. Navigate to the Lilypad Testnet [faucet](https://faucet-testnet.lilypad.tech/).&#x20;
2. Authenticate with Discord.
3. Copy your MetaMask wallet address into the input.
4. Click "Request".

Testnet LP tokens will be sent to the wallet address provided to the faucet.

<figure><img src="../../.gitbook/assets/faucet-step-1.png" alt="" width="563"><figcaption></figcaption></figure>

### Get Arbitrum Sepolia Testnet ETH

Get Arbitrum Sepolia ETH from this list of [third party faucets](https://arbitrum.faucet.dev/ArbSepolia). Each faucet is designed differently, so follow the instructions provided.

{% hint style="info" %}
If you need more tokens and already have Sepolia ETH, use the [official Arbitrum bridge](https://bridge.arbitrum.io/) to transfer the tokens over to Arbitrum Sepolia.
{% endhint %}

### View tokens

With a balance of both LP and ETH, you're ready to run jobs with the Lilypad CLI!

<figure><img src="../../.gitbook/assets/funded-wallet.png" alt="" width="352"><figcaption></figcaption></figure>
