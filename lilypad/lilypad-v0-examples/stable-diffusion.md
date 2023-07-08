---
description: Running a Stable Diffusion Job from a smart contract with Lilypad v0
---

# Stable Diffusion

{% hint style="info" %}
Open this contract in Remix -> [Click here](https://remix.etheruem.org/bacalhau-project/lilypad-v0/blob/main/examples/contracts/StableDiffusionCallerv2.sol)
{% endhint %}

## Introduction

This example uses the Stable Diffusion Docker image found on the [Bacalhau Docs](https://docs.bacalhau.org/examples/model-inference/stable-diffusion-gpu/).

For more info on how to create the Stable Diffusion Script and Docker Image see [this tutorial](https://developerally.com/build-your-own-ai-generated-art-nft-dapp) or watch the video below.

{% embed url="https://youtu.be/53uY48e1lis" %}
Create an open source text to image script to run on Bacalhau
{% endembed %}



## Code

This example can be found in the Examples folder in the Lilypad Project Github.

To run this example, you can simply deploy it to any supported network and pass in the contact address to the constructor which corresponds to your network. See [deployed-network-details.md](../lilypad-v0-reference/deployed-network-details.md "mention").

{% hint style="info" %}
Open this example in remix -> [click here](https://remix.ethereum.org/bacalhau-project/lilypad/edit/main/examples/contracts/StableDiffusionCallerv2.sol)
{% endhint %}

{% @github-files/github-code-block url="https://github.com/bacalhau-project/lilypad-v0/blob/main/examples/contracts/StableDiffusionCallerv2.sol" %}

## Job Results

In this example the Lilypad Stable Diffusion Job Results are returned as an [IPFS v0 CID](https://docs.ipfs.tech/concepts/content-addressing/). You can use Brave browser or an [IPFS gateway](https://docs.ipfs.tech/concepts/ipfs-gateway/) to see the results.

For example for a given return CID, type the following into your browser url&#x20;

* In Brave: `ipfs://[CID]`
* In Other Browsers: `www.w3s.link/ipfs/[CID]` or `www.ipfs.io/ipfs/[CID]`



A folder of the Outputs will be shown:

<figure><img src="https://lh6.googleusercontent.com/6IvDLxN0kKF9ng6StFvKQQBe52r6n1qFAvV6D3gnILDL64XLZ535bioFhwJOdNNXY3I5UoXnT6-UMt56I8YqcrLNxyag2Sz4Pbf0EZ_d1RVY_mlz5kLtw26wrwHPNvBBA4WBpnLaNfo5Ek98wWzIpoYziw=s2048" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh4.googleusercontent.com/oa5LX6P9NjgpVXwmFzeCLLFslHulpQ5WZfufLnceXC5cG99LZrpPmP1fCI_cMo2Xa8Qm3o46u6vAjw6kZLHSke27MjKzjMfWIAPOiZjvPzPzWKqa_mTzlWfZzRtJdk8JvpnsfpzwV8pBrV_x_zi1N-GRbg=s2048" alt=""><figcaption></figcaption></figure>

You can also access the image directly by navigating to

* In Brave: `ipfs://[CID]/outputs/image0.png`
* In Other Browsers: `www.w3s.link/ipfs/[CID]` or `www.ipfs.io/ipfs/[CID]/outputs/image0.png`

<figure><img src="https://lh5.googleusercontent.com/3S4DIyrH9E5uMgDKrXmOk8GhVXARbdW5BjFWQTe3BShJCDUlJDPFVg3L3KJr55edsN9ufeD50U5jUkFtzoBVe3AGHo1i986ypWdivv-mmt_1I2gYy05vZ8cS71_Gl6h3VUmwpFKzt23yOHzPszJLfgc-Qw=s2048" alt=""><figcaption><p>Yay a Rainbow unicorn! Lilypad's spirit animal!</p></figcaption></figure>



