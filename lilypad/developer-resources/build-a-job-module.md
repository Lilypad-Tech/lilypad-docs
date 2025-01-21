---
description: How to build your own compute job for Lilypad
---

# Build a Job Module

A Lilypad module is a Git repository that allows you to perform various tasks using predefined templates and inputs. This guide will walk you through creating a Lilypad module, including defining a JSON template, handling inputs, and following best practices.

{% hint style="info" %}
If you're new to Docker, consider exploring this [step-by-step tutorial](https://docs.docker.com/get-started/) on creating, building, and running a Docker image for a simple Hello World style application.
{% endhint %}

## Module Structure

Start by creating a Git repository for your Lilypad module. The module's versions will be represented as Git tags. Below is the basic structure of a Lilypad Module.

```
your-module/
├── Dockerfile              # Container definition
├── run_script.[py/js/etc]  # Main execution script
├── lilypad_module.json.tmpl # Lilypad configuration
└── README.md              # Documentation
```

## Prepare Your Model

* Handle all dependencies
* Implement input/output through environment variables
* Write outputs to `/outputs` directory

### **1. Create Run Script (run\_model.py for example) that will be used in conjunction with Docker**

```python
 import os
 import json
 
 def main():
     # Get inputs from environment variables
     input_var = os.environ.get('INPUT_VAR', 'default')
     
     # Your model code here
     result = your_model_function(input_var)
     
     # Save outputs
     output_path = '/outputs/result.json'
     with open(output_path, 'w') as f:
         json.dump({'result': result}, f)
 
 if __name__ == "__main__":
     main()
```

### 2. Create a Dockerfile that functions with your run script

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

# Create necessary directories
RUN mkdir -p /outputs

# Copy execution script
COPY run_script.* /workspace/

# Set entrypoint
ENTRYPOINT ["command", "/workspace/run_script"]
```

### 3. Build and Publish Container(example below uses Dockerhub for storage)

{% hint style="info" %}
To ensure the docker image can run on Lilypad, if building the docker image on a Mac add the linux/amd64 flag in the docker build command `docker build --platform linux/amd64 -t your-username/model-name:latest .`
{% endhint %}

```
docker build -t your-username/model-name:latest .
docker push your-username/model-name:latest
```

### 4. Create a lilypad\_module.json.tmpl Template

```json
{
    "machine": {
        "gpu": 1,          # Set to 0 if GPU not needed
        "cpu": 1000,       # CPU allocation
        "ram": 8000        # RAM in MB
    },
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
                "Image": "repository/image-name@sha256:hash"
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

`lilypad run repo:tag -i variable=value`

## Formatting your module run command

During development, you will need to use the Git hash to test your module. This allows you to verify that your module functions correctly and produces the expected results.

Below is a working lilypad module run cmd for reference. (you can use this to run a lilypad job within the lilypad CLI):

`lilypad run`[`github.com/Lilypad-Tech/module-sdxl:6cf06f4038f1cff01a06c4eabc8135fd9835a78a`](http://github.com/Lilypad-Tech/module-sdxl:6cf06f4038f1cff01a06c4eabc8135fd9835a78a) `--web3-private-key <private-key> -i prompt="a lilypad floating on a pond"`

## Examples

Here are some example Lilypad modules for reference:

* [**Cowsay**](https://github.com/Lilypad-Tech/lilypad-module-cowsay)**:** Lilypad "Hello World" example
* [**SDXL v0.9/v1.0**](https://github.com/Lilypad-Tech/lilypad-module-sdxl-pipeline): Text to image generation.
* [**SDV v1.0/1.1**](https://github.com/Lilypad-Tech/lilypad-module-sdv-pipeline): Text to video generation.

Deprecated examples:

* [**lora-training**](https://github.com/Lilypad-Tech/lilypad-module-lora-training)**:** An example module for LoRa training tasks.
* [**lora-inference**](https://github.com/Lilypad-Tech/lilypad-module-lora-inference)**:** An example module for LoRa inference tasks.
* [**duckdb**](https://github.com/Lilypad-Tech/lilypad-module-duckdb)**:** An example module related to DuckDB.

These examples can help you understand how to structure your Lilypad modules and follow best practices.

## Conclusion

In this guide, we've covered the essential steps to create a Lilypad module, including defining a JSON template, handling inputs, and testing your module. By following these best practices, you can build reliable and reusable modules for Lilypad.&#x20;

For more information and additional examples, refer to the official Lilypad documentation and the Cowsay example module.
