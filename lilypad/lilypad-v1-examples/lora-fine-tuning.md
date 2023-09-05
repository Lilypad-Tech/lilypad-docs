---
description: Fine-tuning models from inputs.
---

# LoRA Fine Tuning

## Overview of LoRA Fine Tuning

LoRA stands for Low Rank Adaptation and is a mathematical technique to reduce the number of parameters that are trained in a model - so instead of fine-tuning all the weights that constitute the weight matrix of the pre-trained large language model, two smaller matrices that approximate this larger matrix are fine-tuned. &#x20;

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

What this means in practice is that instead of needing to build a custom model off all the original input data material (and needed many many GPUs to do so), LoRA means you can fine-tune an existing model (such as SDXL 0.9 Stable Diffusion) to be biased towards a certain result on just one GPU.&#x20;

\
For example, an open source Stable Diffusion model can be fine-tuned to produce images in the style of Claude Monet paintings using LoRA.\
\
Fun fact: This is how [Waterlily.ai](../use-cases/waterlily.ai.md) trains artist models - look how good the results are even without an up to date Stable Diffusion model like SDXL0.9!

<figure><img src="https://lh5.googleusercontent.com/hann2gpaFy8pSOPCc4n8j5Lg02bFhEBiKLdE8bhy30NIofwFKDDVFCkrw89Kea2QPnKICOAZ11TWFD-MGMaA3xBtH1DVFlLDCIUvJe0iLj2mfyyW0tpZIz-xV1mfKIhEYL6KgoIAy1DubSN1arQgkrQ" alt=""><figcaption><p>Original Claude Monet Pictures used as additional data and added to a Stable Diffusion Model by LoRA</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (28).png" alt=""><figcaption><p>The results of running Stable Diffusion with the LoRA trained Model.</p></figcaption></figure>

##

## !!!! UNDER CONSTRUCTION STILL BELOW HERE !!!!

##

## \[CLI] Running LoRA Fine Tuning

{% hint style="danger" %}
Ensure you have installed all requirements [install-run-requirements.md](../lilypad-v1-testnet/quick-start/install-run-requirements.md "mention")
{% endhint %}

To run a LoRA fine-tuning job, just provide the training data for the job to the command:

```bash
lilypad run lora_training:v0.1.7-lilypad1 '{images_cid: "bafybeiah7ib5mhzlckolwlkwquzf772wl6jdbhtbuvnbuo5arq7pcs4ubm", seed: 3}'
```

This will output a result model CID, which can then be used to generate new images in this particular style:

{% code overflow="wrap" %}
```bash
lilypad run lora_inference:v0.1.7-lilypad1 '{lora_cid: <CID result from above>, prompt: "an astronaut riding a unicorn in the style of <s1><s2>", seed: 3}'
```
{% endcode %}



## \[Smart Contract] Running LoRA Fine Tuning

{% hint style="danger" %}
Ensure you have set up your Metamask for Lalechuza Network and have funded your wallet. [setting-up-metamask.md](../lilypad-v1-testnet/quick-start/setting-up-metamask.md "mention") & [funding-your-wallet-from-faucet.md](../lilypad-v1-testnet/quick-start/funding-your-wallet-from-faucet.md "mention")
{% endhint %}





## LoRA Module Code

See the code repo [here](https://github.com/bacalhau-project/lilypad-modicum/blob/main/src/python/modules/lora.py)

{% @github-files/github-code-block url="https://github.com/bacalhau-project/lilypad-modicum/blob/main/src/python/modules/lora.py" %}
