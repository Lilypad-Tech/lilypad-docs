---
description: Get Testnet Lilypad Tokens (LP) and Arbitrum Sepolia Testnet ETH
---

# Funding your wallet

To obtain funds, first connect your wallet to the Arbitrum Sepolia network. Collect the following tokens from the faucets:

* [Lilypad Testnet tokens (LP) ](https://faucet-testnet.lilypad.tech/)
* [Arbitrum Sepolia ETH](https://arbitrum.faucet.dev/ArbSepolia) (3rd party faucet list)

## Get Testnet LP tokens

Copy your MetaMask wallet address into the input and click the "Request" button.

<figure><img src="../../.gitbook/assets/faucet-step-1.png" alt="" width="563"><figcaption></figcaption></figure>

## Get Arbitrum Sepolia Testnet ETH

Each faucet in [this third party faucet list](https://arbitrum.faucet.dev/ArbSepolia) is designed differently, so just follow the instructions provided and you'll get the tokens you need.

{% hint style="info" %}
If you need more tokens and already have Sepolia ETH, you can use the [official Arbitrum bridge](https://bridge.arbitrum.io/) to transfer it over to Arbitrum Sepolia.
{% endhint %}

Now you're ready to run Lilypad jobs with the Lilypad CLI!

## Import Testnet tokens

Once the Arbitrum Sepolia testnet has been added to the wallet, you will need to import the Lilypad tokens (LP) into the wallet.

Select "Import tokens" at the bottom of the MetaMask pop-up:

<figure><img src="../../.gitbook/assets/import-token-step-1.png" alt="" width="353"><figcaption></figcaption></figure>

Click on the "Custom token" tab and add the Lilypad token contract address and token symbol and click "Save".

* Token contract address: `0x0352485f8a3cB6d305875FaC0C40ef01e0C06535`
* Token symbol: `LP`

<figure><img src="../../.gitbook/assets/import-token-step-2.png" alt="" width="350"><figcaption></figcaption></figure>

You should now see both of the tokens imported!

<figure><img src="../../.gitbook/assets/funded-wallet.png" alt="" width="352"><figcaption></figcaption></figure>
