---
description: Get started with Lilypad v1
---

# Quick Start

The cloud is just somebody else's computer...

<div data-full-width="true">

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

</div>

## Overview

This guide will take you through

* Setting up [Metamask Wallet](https://metamask.io) for the Lilypad Lalechuza (eth) Testnet
* Funding your wallet with Lilypad Testnet tokens from the [faucet](https://testnet.lilypadnetwork.org).
* Running a Hello, (cow) World! Example :cow:

## Setting up Metamask

1. Install metamask Extension [here](https://metamask.io/)
2. Next, add the Lalechuza testnet chain to metamask.

{% hint style="info" %}
Network name: `Lilypad Lalechuza testnet`

New RPC URL: `http://testnet.lilypadnetwork.org:8545`

Chain ID: `1337`

Currency symbol: lil`ETH`

Block explorer URL: (leave blank)
{% endhint %}

To do this, open metamask then click on the network button at the top left of the popup (in the menu bar):

## ![](<../.gitbook/assets/image (3).png>) \`\`  ![](<../.gitbook/assets/image (5).png>)

Then click the "Add Network" Button.&#x20;

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

Next, click on "Add a network manually" at the bottom of the page and enter the Lilypad Testnet details:

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

Click Save. :tada:

<figure><img src="../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>



## Funding your wallet

To obtain funds, connect to the lilypad lalechuza network and head to the faucet at [testnet.lilypadnetwork.org](https://testnet.lilypadnetwork.org)

{% hint style="info" %}
Faucet: [https://testnet.lilypadnetwork.org](https://testnet.lilypadnetwork.org)
{% endhint %}

Copy your metamask wallet address into the bar and click request.

<figure><img src="../.gitbook/assets/Screenshot 2023-07-13 at 1.19.16 pm.png" alt=""><figcaption><p>Lilypad Lalechuza Testnet Faucet</p></figcaption></figure>

Yay we're rich! :moneybag:\


<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

## Running "Hello, :cow: World!" Job

Let's run our first computation job!!!&#x20;



### Install Requirements

**Install Docker**

{% hint style="info" %}
[Docker](https://www.docker.com/products/docker-desktop/) :whale: installed
{% endhint %}

**Install Lilypad CLI in your terminal / command line**

{% code overflow="wrap" %}
```bash
curl -sSL -O https://bit.ly/get-lilypad && sudo install get-lilypad /usr/local/bin/lilypad
```
{% endcode %}

**Add your private key to your terminal / command line instance:**

Get your private key from metamask: Accounts -> Account Details -> Show private key

<div>

<figure><img src="../.gitbook/assets/Screenshot 2023-07-13 at 2.31.17 pm.png" alt=""><figcaption></figcaption></figure>

 

<figure><img src="../.gitbook/assets/Screenshot 2023-07-13 at 2.31.25 pm.png" alt=""><figcaption></figcaption></figure>

</div>

Set your private key in terminal

```bash
export PRIVATE_KEY=<the private key you copied>
```

You can verify you have set it with:

```bash
echo $PRIVATE_KEY
```

### \[Mac] Run Hello, :cow: World! Job

Start Docker

Open a Terminal window and run the following command:

```bash
lilypad run --template cowsay:v0.0.1 --params "hello lilypad"
```

(ensure your user is in the docker group if necessary on your platform)\


Results:

<figure><img src="../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

### \[Mac] Run Hello, :cow: World! Node

To contribute your resources to the network and get paid

```bash
sudo -E lilypad serve
```

That's it!\
\
This will run a lilypad docker node on your local machine which can accept and run jobs.\


<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>
