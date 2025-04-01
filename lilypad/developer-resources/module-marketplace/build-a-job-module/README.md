---
description: How to build your own compute job for Lilypad
---

# Build a Job Module

A Lilypad module is a Git repository that allows you to perform various tasks using predefined templates and inputs. This guide will walk you through creating a Lilypad module, including defining a JSON template, handling inputs, and following best practices.

For a more in-depth look at building modules, refer to this [end-to-end guide](https://blog.lilypadnetwork.org/lilypad-module-builder-guide).

{% hint style="info" %}
If you're new to Docker, consider exploring this [step-by-step tutorial](https://docs.docker.com/get-started/) on creating, building, and running a Docker image for a simple Hello World style application.
{% endhint %}

## Modules on Lilypad

Below are a few examples of modules you can run on Lilypad. From language models to image generators and fun utilities, the network supports a growing list of AI modules.

<table data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td>Llama2</td><td>An open-source language model, used for generating and understanding text.</td><td><a href="llama2.md">llama2.md</a></td></tr><tr><td>Stable Diffusion Turbo Pipeline</td><td>A fast, high-performance version of Stable Diffusion XL for generating high-quality images with minimal latency</td><td><a href="stable-diffusion-turbo-pipeline.md">stable-diffusion-turbo-pipeline.md</a></td></tr><tr><td>Cowsay</td><td>A playful CLI tool that displays text as if spoken by an ASCII-art cow</td><td><a href="cowsay.md">cowsay.md</a></td></tr></tbody></table>

To view the full list of available modules on Lilypad, please check out [the awesome-lilypad repo](https://github.com/Lilypad-Tech/awesome-Lilypad?tab=readme-ov-file#modules)!

## Module Structure

Start by creating a Git repository for your Lilypad module. The module's versions will be represented as Git tags. Below is the basic structure of a Lilypad Module.

```
your-module/
├── model-directory            # Stores locally downloaded model files 
├── download_model.[py/js/etc] # Script to download model files locally
├── requirements.txt           # Module dependencies
├── Dockerfile                 # Container definition
├── run_script.[py/js/etc]     # Main execution script
├── lilypad_module.json.tmpl   # Lilypad configuration
└── README.md                  # Documentation
```

## Prepare Your Model

* Download model files
* Handle all dependencies (`requirements.txt`)
* Implement input/output through environment variables
* Write outputs to `/outputs` directory

### **1. Download the model locally**

To use a model offline, you first need to download it and store it in a local directory. This guarantees that your code can load the model without requiring an internet connection. Here's a simple process to achieve this:

1. Install required libraries
2. Use a script to download the model (eg: `python download_model.py`)
3. Verify that the model files are in your directory

{% hint style="info" %}
The method to download and save a model and tokenizer may vary based on the model's architecture and the framework you are using. Always refer to the documentation of the specific model to ensure compatibility and proper usage.
{% endhint %}

```python
from transformers import AutoTokenizer, AutoModelForSeq2SeqLM

def download_model():
    model_name = "<namespace>/<model_identifier>"
    # Ensure you have a directory named 'model' in your current working directory or specify a path
    tokenizer = AutoTokenizer.from_pretrained(model_name)
    model = AutoModelForSeq2SeqLM.from_pretrained(model_name)

    # Save the tokenizer and model
    tokenizer.save_pretrained('./model')
    model.save_pretrained('./model')

if __name__ == "__main__":
    download_model()
```

### **2. Create Run Script (run\_model.py for example) that will be used in conjunction with Docker**

```python
import os
import json
from transformers import AutoModel, AutoTokenizer

def main():
    # Load model and tokenizer from local directory
    model_path = '/model'  # Path to the local model directory
    tokenizer = AutoTokenizer.from_pretrained(model_path)
    model = AutoModel.from_pretrained(model_path)

    # Get inputs from environment variables
    input_var = os.environ.get('INPUT_VAR', 'default')
    
    # Your model code here
    result = your_model_function(input_var, model, tokenizer)
    
    # Save outputs
    output_path = '/outputs/result.json'
    with open(output_path, 'w') as f:
        json.dump({'result': result}, f)

if __name__ == "__main__":
    main()

```

### 3. Create a Dockerfile that functions with your run script

```dockerfile
# Use specific base image
FROM base-image:version

# Set working directory
WORKDIR /workspace

# Install dependencies
RUN apt-get update && apt-get install -y \
    your-dependencies && \
    rm -rf /var/lib/apt/lists/*

# Install model requirements
RUN pip install your-requirements

# Environment variables for running offline and using the local model 
# HF_HOME points to the directory where the model code is
ENV HF_HOME=/model
ENV TRANSFORMERS_OFFLINE=1

# Create necessary directories
RUN mkdir -p /outputs

# Copy execution script
COPY run_script.* /workspace/

# Set entrypoint
ENTRYPOINT ["command", "/workspace/run_script"]
```

### 4. Build and Publish Image

To make sure your Docker image is compatible with Lilypad, you need to define the architecture explicitly during the build process. This is particularly important if you are building the image on a system like macOS, which uses a different architecture (`darwin/arm64`) than Lilypad's infrastructure (`linux/amd64`).

The examples below are for building, tagging and pushing an image to DockerHub, but you can use any platform you prefer for hosting the image.&#x20;

For Linux: `docker buildx build -t <USERNAME>/<MODULE_NAME>:<MODULE_TAG> --push .`

For MacOS:&#x20;

<pre class="language-bash"><code class="lang-bash">docker buildx build \
<strong>--platform linux/amd64 \
</strong>-t &#x3C;USERNAME>/&#x3C;MODULE_NAME>:&#x3C;MODULE_TAG> \
--push \
.
</code></pre>

### 5. Create a lilypad\_module.json.tmpl Template

```json
{
    "machine": {
        "gpu": 1,          # Set to 0 if GPU not needed
        "cpu": 1000,       # CPU allocation
        "ram": 8000        # Minimum RAM needed to run the module
    },
    "gpus": [ { "vram": 100 }, { "vram": 4096 } ] # VRAM in MBs. Solver will default to largest one 
    "job": {
        "APIVersion": "V1beta1",
        "Spec": {
            "Deal": {
                "Concurrency": 1
            },
            "Docker": {
                "Entrypoint": ["command", "/workspace/run_script"],
                "WorkingDirectory": "/workspace",
                "EnvironmentVariables": [
                    # Environment variables with defaults
                    {{ if .var_name }}"VAR_NAME={{ js .var_name }}"{{ else }}"VAR_NAME=default_value"{{ end }}
                ],
                # Specify the Docker image to use for this module
                "Image": "repo-owner/repo-name:tag"
            },
            "Engine": "Docker",
            "Network": {
                "Type": "None"
            },
            "Outputs": [
                {
                    "Name": "outputs",
                    "Path": "/outputs"
                }
            ],
            "PublisherSpec": {
                "Type": "ipfs"
            },
            "Resources": {
                "GPU": "1"    # Must match machine.gpu
            },
            "Timeout": 1800
        }
    }
}
```

## Environment Variables

Format in template:&#x20;

```
{{ if .variable }}"VARNAME={{ js .variable }}"{{ else }}"VARNAME=default"{{ end }}
```

Usage in CLI:

```
lilypad run repo:tag -i variable=value
```

## Formatting your module run command

During development, you will need to use the Git hash to test your module. This allows you to verify that your module functions correctly and produces the expected results.

Below is a working Lilypad module run cmd for reference. (you can use this to run a Lilypad job within the Lilypad CLI):

### Test Module before running on Lilypad

Use the following command syntax to run your Module on Lilypad Testnet.

```
lilypad run github.com/Lilypad-Tech/module-sdxl:6cf06f4038f1cff01a06c4eabc8135fd9835a78a --web3-private-key <your-private-key> -i prompt="a lilypad floating on a pond"
```

If the job run appears to be stuck after a few minutes (sometimes it takes time for the Module to download to the RP node), cancel the job and try again. Open a ticket in [Discord](https://discord.com/channels/1212897693450641498/1230231823674642513) with any issues that persist.&#x20;

{% hint style="info" %}
If many jobs have been run on the machine previosuly, clear `Lilypad` from the `/tmp` folder locally and try running the job again.
{% endhint %}

### Run Module on Lilypad

```bash
lilypad run github.com/noryev/module-sdxl-ipfs:ae17e969cadab1c53d7cabab1927bb403f02fd2a -i prompt="your prompt here"
```

## Examples

Here are some example Lilypad modules for reference:

* [**Cowsay**](https://github.com/Lilypad-Tech/lilypad-module-cowsay)**:** Lilypad "Hello World" example
* [**Llama2**](llama2.md): Text to text
* [**SDXL-turbo pipeline**](stable-diffusion-turbo-pipeline.md): Text to image generation
* [**create-lilypad-module**](../create-lilypad-module/)&#x20;

Deprecated examples:

* [**lora-training**](https://github.com/Lilypad-Tech/lilypad-module-lora-training)**:** An example module for LoRa training tasks.
* [**lora-inference**](https://github.com/Lilypad-Tech/lilypad-module-lora-inference)**:** An example module for LoRa inference tasks.
* [**duckdb**](https://github.com/Lilypad-Tech/lilypad-module-duckdb)**:** An example module related to DuckDB.

These examples can help you understand how to structure your Lilypad modules and follow best practices.

## Conclusion

In this guide, we've covered the essential steps to create a Lilypad module, including defining a JSON template, handling inputs, and testing your module. By following these best practices, you can build reliable and reusable modules for Lilypad.&#x20;

For more information and additional examples, refer to the official Lilypad documentation and the Cowsay example module.
