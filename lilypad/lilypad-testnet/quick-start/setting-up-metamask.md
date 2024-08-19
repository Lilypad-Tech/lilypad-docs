---
description: >-
  Configure a crypto wallet to receive testnet tokens used to interact with the
  Lilypad Network
---

# Setting up MetaMask

## Create a MetaMask wallet

End users of Lilypad can decide which crypto wallet they would like to use. In this guide, we advise using a [MetaMask](https://metamask.io/) crypto wallet.

* Install [MetaMask Extension](https://metamask.io/download/)

### Use the Arbitrum Sepolia Testnet in MetaMask.

The Lilypad Testnet (IcentiveNet) is currently running on the Arbitrum L2 network built on Ethereum.&#x20;

In order to change to the Arbitrum network in the wallet, open MetaMask and click the network button in the top left of the menu bar:

<figure><img src="../../.gitbook/assets/metamask-step-1.png" alt="" width="355"><figcaption></figcaption></figure>

Then , select "Add network":

<figure><img src="../../.gitbook/assets/metamask-step-2.png" alt="" width="352"><figcaption></figcaption></figure>

Next, select "Add a network manually":

<figure><img src="../../.gitbook/assets/metamask-step-3.png" alt="" width="563"><figcaption></figcaption></figure>

Input all the required Arbitrum Sepolia Testnet network info, and then "Save":

{% hint style="info" %}
Network name: Arbitrum Sepolia

New RPC URL: [https://sepolia-rollup.arbitrum.io/rpc](https://sepolia-rollup.arbitrum.io/rpc)

Chain ID: 421614

Currency symbol: ETH

Block explorer URL: (leave blank)
{% endhint %}

{% hint style="info" %}
Network info is referenced directly from the Arbitrum Sepolia [documentation](https://docs.arbitrum.io/arbitrum-bridge/quickstart#step-2-add-the-preferred-network-to-your-wallet).
{% endhint %}

<figure><img src="../../.gitbook/assets/metamask-step-4.png" alt="" width="375"><figcaption></figcaption></figure>

### Import the Testnet LP token

The wallet is now setup and will display an ETH (Arbitrum Sepolia) token balance. In order to also display the LP token balance, the LP token will need to be imported.

Select "Import tokens" at the bottom of the MetaMask pop-up:

<figure><img src="../../.gitbook/assets/import-token-step-1 (1).png" alt="" width="353"><figcaption></figcaption></figure>

Select "Custom token" and add the Lilypad token contract address and token symbol. Then "Save".

* Token contract address: `0x0352485f8a3cB6d305875FaC0C40ef01e0C06535`
* Token symbol: `LP`

<figure><img src="../../.gitbook/assets/import-token-step-2 (1).png" alt="" width="350"><figcaption></figcaption></figure>

You should now see both ETH and LP listed in the wallet (initial ETH and LP balances will be 0).

<figure><img src="../../.gitbook/assets/import-token-step-3 (1).png" alt="" width="352"><figcaption></figcaption></figure>

Now you're ready to fund the wallet with testnet LP and ETH tokens!&#x20;
