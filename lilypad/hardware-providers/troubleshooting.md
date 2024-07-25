---
description: Common FAQs when running a Lilypad node
---

# Troubleshooting

## Debugging a Lilypad Node

* Ensure the node (Resource Provider ) is running the latest Lilypad version
* Confirm network activity - is the RP transacting on Arbscan? (txs verified and running consistently)
  * [https://sepolia.arbscan.io/address/](https://sepolia.arbiscan.io/)”**your-wallet-address”**
* Check the [node status](https://info.lilypad.tech/node-status)
* Ensure the RP is online and earning Lilybit\_ rewards in the [Leaderboard](https://info.lilypad.tech/leaderboard)
* **If the RP public keys are not found within the Arbscan network or Leaderboard:**
  * Ensure the RP has enough [Arbitrum ETH](https://docs.lilypad.tech/lilypad/lilypad-testnet/quick-start/funding-your-wallet-from-faucet#get-arbitrum-sepolia-testnet-eth) and [Lilypad Tokens](https://docs.lilypad.tech/lilypad/lilypad-testnet/quick-start/funding-your-wallet-from-faucet#get-testnet-lp-tokens)

**To** [**view the logs**](https://docs.lilypad.tech/lilypad/hardware-providers/run-a-node#view-node-status) **from the resource provider use this command on the resource provider:**

`journalctl -u lilypad-resource-provider.service`

## Metamask wallet setup:

* [Import](https://docs.lilypad.tech/lilypad/lilypad-testnet/quick-start/setting-up-metamask#setting-up-metamask) a custom network (Lilypad)
* [Locate](https://support.metamask.io/managing-my-wallet/secret-recovery-phrase-and-private-keys/how-to-export-an-accounts-private-key/) a wallet's Private Key
* [Import](https://docs.lilypad.tech/lilypad/lilypad-testnet/quick-start/funding-your-wallet-from-faucet#import-testnet-tokens) the Lilypad Token to a wallet

## Get testnet LP and ETH (Arbitrum Sepolia ETH)

* [Fund](https://docs.lilypad.tech/lilypad/hardware-providers/run-a-node#write-env-file) a wallet with LP and ETH&#x20;
* No ETH or LP in your wallet? ([import custom network and import the tokens](https://lilypad.team/discord))&#x20;

Join our [Discord](https://lilypad.team/discord) for more help!

