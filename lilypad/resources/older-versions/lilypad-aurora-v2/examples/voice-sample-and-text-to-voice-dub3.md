---
description: This module is contributed by Fabri from Dub3
---

# Voice Sample & Text to Voice \[Dub3]

### Overview

This module takes a voice sample as an input and can then output another voice sample for a given text prompt - in multiple languages.

### OSS Model

The OSS Model is based on this model: [https://github.com/coqui-ai/TTS](https://github.com/coqui-ai/TTS)

### Lilypad Module

{% @github-files/github-code-block url="https://github.com/dub3-space/lily-synthetizoor/blob/main/README.md" %}

### Run in CLI

First upload a voice .wav file to IPFS

{% hint style="info" %}
Use [https://web3.storage](https://web3.storage) is an easy way to upload files to IPFS.\
Use [https://cloudconvert.com/](https://cloudconvert.com/) to convert recordings to .wav files
{% endhint %}

Here's are two voice recording examples:&#x20;

```bash
https://bafybeibrum5bqhslpoemqiyvikbg3b5ujte6qppvk2cbdstwxnhejypxl4.ipfs.w3s.link/ally-voice.wav
```

```bash
https://bafybeif3qp2sd7qb67kjhds65b6qr5ecerib76cjclyo625ovledffabfu.ipfs.w3s.link/
```

Then use the command below to run the module. Note the parameters for changing the language and adding a prompt.

{% code overflow="wrap" %}
```bash
lilypad run github.com/dub3-space/lily-synthetizoor:b4d2e078c3447e1df12588ee854360087ce7f081 -i URL=https://bafybeibrum5bqhslpoemqiyvikbg3b5ujte6qppvk2cbdstwxnhejypxl4.ipfs.w3s.link/ally-voice.wav -i SENTENCE='Hello! Youre listening to voice translation on Lilypad with dub3!' -i LANGUAGE=en -i INPUT_FOLDER=/inputs -i OUTPUT_FOLDER=/outputs
```
{% endcode %}



You should see Lilypad run something like this:&#x20;

<figure><img src="../../../../.gitbook/assets/image (22) (1).png" alt=""><figcaption><p>Lilypad running in the CLI</p></figcaption></figure>

\
You'll find your results under the output folder:

<figure><img src="../../../../.gitbook/assets/image (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

