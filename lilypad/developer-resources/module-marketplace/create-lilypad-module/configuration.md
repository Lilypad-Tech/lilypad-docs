---
description: Configure your Lilypad module
---

# Configuration

## Configure Your Module

After bootstrapping your module, additional configuration is required to run it.

### `.env`

```
WEB3_PRIVATE_KEY = ""
```

#### `WEB3_PRIVATE_KEY`

> 🚨 **DO NOT SHARE THIS KEY** 🚨

The private key for the wallet that will be used to run the job.

This is required to run the module on Lilypad Network.

A new development wallet is highly recommended to use for development. The wallet must have enough LP tokens and Arbitrum Sepolia ETH to fund the job.

* [Funding your wallet](../../../quickstart/cli/setting-up-your-wallet.md)

### `config/constants.py`

```python
DOCKER_REPO = ""
MODULE_REPO = ""
TARGET_COMMIT = ""
```

#### `DOCKER_REPO`

The Docker Hub repository storing the container image of the module code.

This is required to push the image to Docker Hub and run the module on Lilypad Network.

e.g. `"<dockerhub_username>/<dockerhub_image>"`

#### `DOCKER_TAG`

The specific tag of the `DOCKER_REPO` containing the module code.

Default: `"latest"`

#### `MODULE_REPO`

The URL for the GitHub repository storing the `lilypad_module.json.tmpl` file. The visibility of the repository must be public.

The `lilypad_module.json.tmpl` file points to a `DOCKER_REPO` and Lilypad runs the module from the image.

e.g. `"github.com/<github_username>/<github_repo>"`

#### `TARGET_COMMIT`

The git branch or commit hash that contains the `lilypad_module.json.tmpl` file you want to run.

Use `git log` to easily find commit hashes.

Default: `"main"`

### Available Scripts

Your module will be bootstrapped with some handy scripts to help you download the model(s) for your module, build and push Docker images, and run your module locally or on Lilypad Network. Some additional configuration may be required.

In the project directory, you can run:

#### `python -m scripts.download_models`

A basic outline for downloading a model from [Hugging Face](https://huggingface.co/) is provided, but the structure of the script and the methods for downloading a model can differ between models and libraries. It’s important to tailor the process to the specific requirements of the model you're working with.

Most (but not all) models that utilize machine learning use the [🤗 Transformers](https://huggingface.co/docs/transformers/index) library, which provides APIs and tools to easily download and train pretrained models.

* [Learn more about downloading models from Hugging Face](https://huggingface.co/docs/hub/en/models-downloading)
* [Learn more about the 🤗 Transformers library](https://huggingface.co/docs/hub/en/transformers)

No matter which model you are using, be sure to thoroughly read the documentation to learn how to properly download and use the model locally.

#### `python -m scripts.docker_build`

Builds and optionally publishes a Docker image for the module to use.

For most use cases, this script should be sufficient and won't require any configuration or modification (aside from setting your `DOCKER_REPO` and `DOCKER_TAG`).

{% hint style="info" %}
In the modules `Dockerfile`, you'll find 3 COPY instructions.

```dockerfile
COPY requirements.txt .
COPY src /src
COPY models /models
```

These instructions copy the `requirements.txt` file, the `src` directory, and the `models` directory from your local machine into the Docker image. It's important to remember that any modifications to these files or directories will necessitate a rebuild of the module's Docker image to ensure the changes are reflected in the container.
{% endhint %}

**`--push` Flag**

Running the script with `--push` passed in pushes the Docker image to Docker Hub.

**`--no-cache` Flag**

Running the script with `--no-cache` passed in builds the Docker image without using the cache. This flag is useful if you need a fresh build to debug caching issues, force system or dependency updates, pull the latest base image, or ensure clean builds in CI/CD pipelines.

#### `python -m scripts.run_module`

This script is provided for convenience to speed up development. It is equivalent to running the Lilypad module with the provided input and private key (unless running the module locally, then no private key is required). Depending on how your module works, you may need to change the default behavior of this script.

**`--local` Flag**

Running the script with `--local` passed in runs the Lilypad module Docker image locally instead of on Lilypad's Network.

**`--demonet` Flag**

Running the script with `--demonet` passed in runs the Lilypad module Docker image on Lilypad's Demonet.

### `lilypad_module.json.tmpl`

The default `lilypad_module.json.tmpl` file is below. Make sure to update the Docker Image to point to your Docker Hub image with the correct tag.

> The default `lilypad_module.json.tmpl` should work for low complexity modules. If your module requires additional resources (such as a GPU) make sure to configure the applicable fields.

```json
{
  "machine": { "gpu": 1, "cpu": 8000, "ram": 16000 },
  "gpus": [{ "vram": "24Gb" }]
  "job": {
    "APIVersion": "V1beta1",
    "Spec": {
      "Deal": { "Concurrency": 1 },
      "Docker": {
        "Entrypoint": [
          "/app/src/run_model", {{ .request }}
        ],
        "Image": "DOCKER_HUB_USERNAME/DOCKER_IMAGE@INDEX_DIGEST"
      },
      "Engine": "Docker",
      "Network": { "Type": "None" },
      "Outputs": [{ "Name": "outputs", "Path": "/outputs" }],
      "Resources": { "GPU": "1", "CPU": "8", "Memory": "16Gb" },
      "Timeout": 1800,
      "Verifier": "Noop"
    }
  }
}
```

#### Template Fields

* **Machine:** Specifies the system resources.
* GPUs: Specifies the minimum VRAM required.
* **Job:** Specifies the job details.
  * **APIVersion:** Specifies the API version for the job.
  * **Metadata:** Specifies the metadata for the job.
  * **Spec:** Contains the detailed job specifications.
    * **Deal:** Sets the concurrency to 1, ensuring only one job instance runs at a time.
    * **Docker:** Configures the Docker container for the job
      * **WorkingDirectory:** Defines the working directory of the Docker image.
      * **Entrypoint:** Defines the command(s) to be executed in the container as part of its initial startup runtime.
      * **EnvironmentVariables:** This can be utilised to set env vars for the containers runtime, in the example above we use Go templating to set the `INPUT` variable dynamically from the CLI.
      * **Image:** Specifies the image to be used (`DOCKERHUB_USERNAME`/`IMAGE`:`TAG`).
    * **Engine:** Sets the container runtime (Default: `"Docker"`).
    * **Network:** Specifies that the container does not require networking (Default: `"Type": "None"`).
    * **Outputs:** Specifies name and path of the directory that will store module outputs.
    * **Resources:** Specify additional resources.
    * **Timeout:** Sets the maximum duration for the job. (Default: `600` \[10 minutes]).
