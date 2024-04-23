---
description: Run a Stable Diffusion Text to Image Job
---

# Stable Diffusion (SDXL0.9)

{% embed url="https://youtu.be/kh5jXuQ6_ww?si=BYIvEW9q8I4C7eS_" %}

### Overview

Generically, stable diffusion is what happens when you put a couple of drops of dye into a bucket of water. Given time, the dye randomly disperses and eventually settles into a uniform distribution which colours all the water evenly

In computer science, you define rules for your (dye) particles to follow and the medium this takes place in.

Stable Diffusion is a machine learning model used for text-to-image processing (like Dall-E) and based on a diffusion probabilistic model that uses a transformer to generate images from text.\
\
There are several open-source stable diffusion models out there (made famous by Stability.ai) and they continue to improve and become even more fully featured - SDXL0.9 is one of the more recently open-sourced models

### \[CLI] Running Stable Diffusion SDXL 0.9

\{% hint style="danger" %\} Ensure you have installed all requirements [https://github.com/noryev/lilypad-docs/blob/main/lilypad/lilypad-v3-testnet/quick-start/install-run-requirements.md](https://github.com/noryev/lilypad-docs/blob/main/lilypad/lilypad-v3-testnet/quick-start/install-run-requirements.md "mention") \{% endhint %\}

To run stable diffusion use the sdxl module like so:

```
lilypad run sdxl-pipeline:v0.9-base-lilypad3 -i Prompt='a gigantic lilypad shaped space station'
```

The output will look like this:

<figure><img src="https://github.com/noryev/lilypad-docs/raw/main/lilypad/.gitbook/assets/sdxl_execution.png" alt=""><figcaption></figcaption></figure>

SDXL Output

Take the ipfs link given in the results and paste it into your browser:

```
https://ipfs.io/ipfs/QmVng1jkMxE9ep4k8mYiiCiWaCRiRLvCeo6bJRXirhz1dZ
```

\{% hint style="warning" %\} Please be patient! IPFS can take some time to propagate and doesn't always work immediately. \{% endhint %\}

You could also check the output folder that would have been downloaded at the end of running the job

```
open /tmp/lilypad/data/downloaded-files/QmZuE29GJVmenRUh72FQDgkMUT1Zdp967oEJvzjaDwGGVo
```

<figure><img src="https://github.com/noryev/lilypad-docs/raw/main/lilypad/.gitbook/assets/sdxl_output.png" alt=""><figcaption></figcaption></figure>

Results of SDXL job on Output Directory

In the **/outputs** folder, you'll find the image:

<figure><img src="https://github.com/noryev/lilypad-docs/raw/main/lilypad/.gitbook/assets/sdxl_result_output.png" alt=""><figcaption></figcaption></figure>

The Image in the outputs folder

Since modules are deterministic, running this command with the same text prompt will produce the same image, since the same seed is also used (the default seed is 0).

\{% hint style="info" %\} See this [beginner-friendly article](https://aituts.com/stable-diffusion-seed/) on how seed's work for more info on this \{% endhint %\}

To change the image, you can pass in a different seed number:

```
`lilypad run sdxl-pipeline:v0.9-base-lilypad3 -i Prompt='a gigantic lilypad shaped space station' -i Steps=150` 
```

<figure><img src="https://github.com/noryev/lilypad-docs/raw/main/lilypad/.gitbook/assets/sdxl_result_output2.png" alt=""><figcaption></figcaption></figure>

Output using different seed.

## CLI Video

In this video, Sam demos the use of SDXL in the Lilypad network.

{% embed url="https://youtu.be/RBECCMl_fco" %}

### Looking for Smart Contracts?

\
Try this to start!

{% @github-files/github-code-block url="https://github.com/bacalhau-project/lilypad/blob/main/docs/smart-contract-jobs.md" %}

