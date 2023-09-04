---
description: Fine-tuning models from inputs.
---

# LoRA Fine Tuning

## Overview of LoRA Fine Tuning

LoRA stands for Low-Rank Adaptation and is a mathematical technique to reduce the number of parameters that are trained in a model - so instead of finetuning all the weights that constitute the weight matrix of the pre-trained large language model, two smaller matrices that approximate this larger matrix are fine-tuned.  \
\
What this means in practice is that instead of needing to build a custom model off all the original input data material (and needed many many GPUs to do so), LoRA means you can finetune an existing model (such as SDXL 0.9 Stable Diffusion) to be biased towards a certain result on just one GPU. \
For example, an open source Stable Diffusion model can be fine-tuned to produce images in the style of Claude Monet paintings using LoRA.\
\
(NB: This is how [Waterlily.ai](../use-cases/waterlily.ai.md) trains artist models).

<figure><img src="https://lh5.googleusercontent.com/hann2gpaFy8pSOPCc4n8j5Lg02bFhEBiKLdE8bhy30NIofwFKDDVFCkrw89Kea2QPnKICOAZ11TWFD-MGMaA3xBtH1DVFlLDCIUvJe0iLj2mfyyW0tpZIz-xV1mfKIhEYL6KgoIAy1DubSN1arQgkrQ" alt=""><figcaption><p>Original Claude Monet Pictures used as additional data and added to a Stable Diffusion Model by LoRA</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (28).png" alt=""><figcaption><p>The results of running Stable Diffusion with the LoRA trained Model.</p></figcaption></figure>

## \[CLI] Running LoRA Fine Tuning

{% hint style="danger" %}
Ensure you have installed all requirements [install-run-requirements.md](../lilypad-v1-testnet/quick-start/install-run-requirements.md "mention")
{% endhint %}





## \[Smart Contract] Running LoRA Fine Tuning

{% hint style="danger" %}
Ensure you have set up your Metamask for Lalechuza Network and have funded your wallet. [setting-up-metamask.md](../lilypad-v1-testnet/quick-start/setting-up-metamask.md "mention") & [funding-your-wallet-from-faucet.md](../lilypad-v1-testnet/quick-start/funding-your-wallet-from-faucet.md "mention")
{% endhint %}





