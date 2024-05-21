---
description: Ollama Pipeline modules for Lilypad
---

# Llama LLM

## Overview

Based on Ollama, the Ollama Pipeline modules for Lilypad allow you generate text on Lilypad using various models.

### Available models

* #### Llama3

## Llama3

Llama3 is a machine learning model used for natural language processing. It is based on a transformer architecture, which enables it to handle tasks like text generation, summarization, translation, and more. When integrated with Lilypad, it leverages the platform's capabilities to provide efficient text processing for various applications.

### Usage

#### Lilypad

{% hint style="warning" %}
Make sure you have installed [all requirements](../lilypad-milky-way-testnet/install-run-requirements.md)
{% endhint %}

To run Ollama Pipeline in Lilypad, you can use the following commands:

```bash
lilypad run ollama-pipeline:llama3-8b-lilypad1 -i Prompt='Something awesome this way comes'
```

If you wish to specify more than one tunable, such as the number of steps, simply add more `-i` flags, like so:

```bash
lilypad run sdxl-pipeline -i Prompt="an astronaut floating against a white background" -i Steps=69
```

#### Docker

To run these modules in Docker, you can use the following commands:

```bash
docker run -ti --gpus all \
    -v $PWD/outputs:/outputs \
    -e PROMPT="an astronaut floating against a white background" \
    zorlin/ollama:llama3-8b-lilypad1
```

If you wish to specify more than one tunable, such as the number of steps, simply add more `-e` flags, like so:

```bash
-e PROMPT="an astronaut floating against a white background" \
-e STEPS=69 \
-e SIZE=2048 \
```

### Links

* [Lilypad Ollama Pipeline modules README](https://github.com/Lilypad-Tech/lilypad-module-ollama-pipeline/blob/main/README.md)
* [Source code](https://github.com/Lilypad-Tech/lilypad-module-ollama-pipeline)



