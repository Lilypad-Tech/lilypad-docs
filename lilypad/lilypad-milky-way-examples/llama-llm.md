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

### Prerequisites

Before running the Ollama Pipeline, make sure you have the [Lilypad CLI installed](https://docs.lilypad.tech/lilypad/lilypad-milky-way-testnet/install-run-requirements) on your machine and your private key environment variable is set. This is necessary for operations within the Lilypad network.

```bash
export WEB3_PRIVATE_KEY=<YOUR_PRIVATE_KEY>
```

### Usage

The Ollama Pipeline in Lilypad can be run using the Lilypad CLI or Docker. Below are the instructions for both of those options.

#### Lilypad

To run Ollama Pipeline using the Lilypad CLI, you can use the following command:

```bash
lilypad run ollama-pipeline:llama3-8b-lilypad2 -i Prompt='Something awesome this way comes'
```

#### Docker

To run this module in Docker, you can use the following commands:

```bash
docker run -ti --gpus all \
    -v $PWD/outputs:/outputs \
    -e PROMPT="Something awesome this way comes" \
    zorlin/ollama:llama3-8b-lilypad2
```

### Links

* [Lilypad Ollama Pipeline modules README](https://github.com/Lilypad-Tech/lilypad-module-ollama-pipeline/blob/main/README.md)
* [Source code](https://github.com/Lilypad-Tech/lilypad-module-ollama-pipeline)



