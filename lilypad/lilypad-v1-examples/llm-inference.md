---
description: A Fast Chat LLM Inference Module for Lilypad
---

# LLM Inference \[coming soon]

{% hint style="danger" %}
Under Construction&#x20;
{% endhint %}

## Overview

This LLM Inference Module is a community-contributed module developed at AugmentHack.xyz\
\
The repo for this module can be found [here.](https://github.com/bacalhau-project/lilypad-modicum/blob/main/src/python/modules/fastchat.py)

See the original AugmentHack entry below:

{% embed url="https://devpost.com/software/carpai-fmecgh" %}

{% embed url="https://www.youtube.com/watch?v=bqhNbgqF6ks" %}

## \[CLI] Usage

**Usage:**

```
lilypad run fastchat:v0.0.1 "paramsStr"
```

**Inputs:**

Where "paramsStr" is a question in CID form for the LLM. E.g this question on Claude Monet

```
bafybeihu62yl76fcypidaiz35gq3yjguxawy5zzwadzvlcgpnfkuy2do3i
```

<figure><img src="https://lh4.googleusercontent.com/yX4XLf8IGZSit-vNxTFB255g8R8DbpzsoElPhQBQpRUi7xKubV3u3J_e8Y-aA1Lu6yNf38sQSbG7pXoehfYepmPU5O55L7gvynU9bp0OTEK05ph5mNrQWjt_ySCHPOV2g-eN0N3J_N7llShZMYvuyxZlqQ=s2048" alt=""><figcaption><p>bafybeihu62yl76fcypidaiz35gq3yjguxawy5zzwadzvlcgpnfkuy2do3i</p></figcaption></figure>

**Outputs:**

IPFS CID\
\


## LLM Module Code

{% @github-files/github-code-block url="https://github.com/bacalhau-project/lilypad-modicum/blob/main/src/python/modules/fastchat.py" %}
