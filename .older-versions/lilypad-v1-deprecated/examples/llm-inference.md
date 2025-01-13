---
description: A Fast Chat LLM Inference Module for Lilypad
---

# LLM Inference

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

Where "paramsStr" is a question in CID form for the LLM. For example [https://ipfs.io/ipfs/QmcPjQwVcJiFge3yNjVL2NoZsTQ3GBpXAZe21S2Ncg16Gt](https://ipfs.io/ipfs/QmcPjQwVcJiFge3yNjVL2NoZsTQ3GBpXAZe21S2Ncg16Gt) is a bare file CID which contains

{% code overflow="wrap" %}
```
{
    "template": "You are a friendly chatbot assistant that responds conversationally to users' questions. \n Keep the answers short, unless specifically asked by the user to elaborate on something. \n \n Question: {question} \n \n Answer:",
    "parameters": {"question": "What is a chatbot?"}
}
```
{% endcode %}

To use it you would run:

```
lilypad run fastchat:v0.0.1 QmcPjQwVcJiFge3yNjVL2NoZsTQ3GBpXAZe21S2Ncg16Gt
```

\
**Outputs:**

The output will be an IPFS CID, for example running the above input would result in the following link:

[https://ipfs.io/ipfs/QmVNXCAfJgER6U7Z5XT8QaAVFPdwmtSFE6c9sUaAx7ttZs](https://ipfs.io/ipfs/QmVNXCAfJgER6U7Z5XT8QaAVFPdwmtSFE6c9sUaAx7ttZs/output/result.json)

Under link[/output/result.json](https://ipfs.io/ipfs/QmVNXCAfJgER6U7Z5XT8QaAVFPdwmtSFE6c9sUaAx7ttZs/output/result.json) you will see

{% code overflow="wrap" %}
```json
{"question": "What is a chatbot?", "text": "<pad> A  chatbot  is  a  computer  program  that  can  interact  with  users  in  a  conversational  manner.  It  is  designed  to  answer  questions  and  provide  information  in  a  way  that  is  natural  and  conversational.\n"}
```
{% endcode %}

{% hint style="info" %}
Pssst... here's a question on Claude Monet you could try too ;)\
bafybeihu62yl76fcypidaiz35gq3yjguxawy5zzwadzvlcgpnfkuy2do3i\
![](<../../../../.gitbook/assets/image (139).png>)
{% endhint %}

<figure><img src="https://lh4.googleusercontent.com/yX4XLf8IGZSit-vNxTFB255g8R8DbpzsoElPhQBQpRUi7xKubV3u3J_e8Y-aA1Lu6yNf38sQSbG7pXoehfYepmPU5O55L7gvynU9bp0OTEK05ph5mNrQWjt_ySCHPOV2g-eN0N3J_N7llShZMYvuyxZlqQ=s2048" alt=""><figcaption><p>bafybeihu62yl76fcypidaiz35gq3yjguxawy5zzwadzvlcgpnfkuy2do3i</p></figcaption></figure>

## LLM Module Code

{% @github-files/github-code-block url="https://github.com/bacalhau-project/lilypad-modicum/blob/main/src/python/modules/fastchat.py" %}
