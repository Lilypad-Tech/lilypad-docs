---
description: Run a Stable Diffusion Text to Image Job
---

# Stable Diffusion (SDXL0.9)

{% embed url="https://youtu.be/kh5jXuQ6_ww?si=BYIvEW9q8I4C7eS_" %}
Hacker Cafe Girl Running SDXL
{% endembed %}

## Overview

Generically, stable diffusion is what happens when you put a couple of drops of dye into a bucket of water. Given time, the dye randomly disperses and eventually settles into a uniform distribution which colours all the water evenly

In computer science, you define rules for your (dye) particles to follow and the medium this takes place in.

Stable Diffusion is a machine learning model used for text-to-image processing (like Dall-E) and based on a diffusion probabilistic model that uses a transformer to generate images from text.\
\
There are several open-source stable diffusion models out there (made famous by Stability.ai) and they continue to improve and become even more fully featured - SDXL0.9 is one of the more recently open-sourced models.

<figure><img src="https://lh5.googleusercontent.com/eib-z-1r9iZyxuArY_2z-NhPv4OPyFACpFF6-_nWfGaoDlY958NbP5fRcpUNtzuedWM_HmryF7aJplAtiQm3ezeV_cUUQ69sV1MYyvckptTBmIEawnSZivnEb8B8ifITYwgH_k3EISLjSWy0JbM9y2JfTg=s2048" alt=""><figcaption></figcaption></figure>

## \[CLI] Running Stable Diffusion SDXL 0.9

{% hint style="danger" %}
Ensure you have installed all requirements [install-run-requirements.md](../../../../lilypad-milky-way-testnet/quick-start/install-run-requirements.md "mention")
{% endhint %}

To run stable diffusion use the sdxl module like so:

```
lilypad run sdxl:v0.9-lilypad1 -i PromptEnv="PROMPT=beautiful view of iceland with a record player"
```

The output will look like this:

<figure><img src="../../../../.gitbook/assets/sdxl_execution.png" alt=""><figcaption><p>SDXL Output</p></figcaption></figure>

Take the ipfs link given in the results and paste it into your browser:

```bash
https://ipfs.io/ipfs/QmVng1jkMxE9ep4k8mYiiCiWaCRiRLvCeo6bJRXirhz1dZ
```

{% hint style="warning" %}
Please be patient! IPFS can take some time to propagate and doesn't always work immediately.
{% endhint %}

You could also check the output folder that would have been downloaded at the end of running the job

```bash
open /tmp/lilypad/data/downloaded-files/QmZuE29GJVmenRUh72FQDgkMUT1Zdp967oEJvzjaDwGGVo
```

<figure><img src="../../../../.gitbook/assets/sdxl_output.png" alt=""><figcaption><p>Results of SDXL job on Output Directory</p></figcaption></figure>

In the **/outputs** folder, you'll find the image:

<figure><img src="../../../../.gitbook/assets/sdxl_result_output.png" alt=""><figcaption><p>The Image in the outputs folder</p></figcaption></figure>

Since modules are deterministic, running this command with the same text prompt will produce the same image, since the same seed is also used (the default seed is 0).

{% hint style="info" %}
See this [beginner-friendly article](https://aituts.com/stable-diffusion-seed/) on how seed's work for more info on this
{% endhint %}

To change the image, you can pass in a different seed number:

```bash
lilypad run sdxl:v0.9-lilypad1 -i PromptEnv="PROMPT=beautiful view of iceland with a record player" -i SeedEnv="RANDOM_SEED=24" 
```

<figure><img src="../../../../.gitbook/assets/sdxl_result_output2.png" alt=""><figcaption><p>Output using different seed.</p></figcaption></figure>

#### CLI Video

In this video, Sam demos the use of SDXL in the Lilypad network.

{% embed url="https://youtu.be/RBECCMl_fco" %}
Lilypad \[CLI] Stable Diffusion with SDLX 0.9 Demo
{% endembed %}

### Looking for Smart Contracts?

\
Try this to start!

{% @github-files/github-code-block url="https://github.com/bacalhau-project/lilypad/blob/main/docs/smart-contract-jobs.md" %}

