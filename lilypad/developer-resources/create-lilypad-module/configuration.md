---
description: Configure your Lilypad Modules
---

# Configuration

After bootstrapping your module, additional configuration is required to run it.

## `.env`

```
WEB3_PRIVATE_KEY = ""
```

### `WEB3_PRIVATE_KEY`

> 🚨 **DO NOT SHARE THIS KEY** 🚨

The private key for the wallet that will be used to run the job.

This is required to run the module on Lilypad Network.

A new burner wallet is highly recommended to use for development.
The wallet must have enough LP to fund the job.

- [Funding your wallet](https://docs.lilypad.tech/lilypad/lilypad-testnet/quick-start/funding-your-wallet-from-faucet)

## `config/constants.py`

```python
DOCKER_REPO = ""
MODULE_REPO = ""
TARGET_COMMIT = ""
```

### `DOCKER_REPO`

The Docker Hub repository storing the container image of the module code.

This is required to push the image to Docker Hub and run the module on Lilypad Network.

e.g. `"<dockerhub_username>/<dockerhub_image>"`

### `DOCKER_TAG`

The specific tag of the `DOCKER_REPO` containing the module code.

Default: `"latest"`

### `MODULE_REPO`

The URL for the GitHub repository storing the `lilypad_module.json.tmpl` file.

The `lilypad_module.json.tmpl` file points to the `DOCKER_REPO` and Lilypad runs the module from the image.

e.g. `"github.com/<github_username>/<github_repo>"`

### `TARGET_COMMIT`

The git branch or commit hash that contains the `lilypad_module.json.tmpl` file you want to run.

Use `git log` to easily find commit hashes.

Default: `"main"`

## Available Scripts

Your module will be bootstrapped with some handy scripts to help you download the model(s) for your module, build and push Docker images, and run your module locally and on Lilypad Network.

In the project directory, you can run:

### `python -m scripts.download_models`

A basic outline for downloading a model from [Hugging Face](https://huggingface.co/) is provided, but the structure of the script and the methods for downloading a model can differ between models and libraries. It’s important to tailor the process to the specific requirements of the model you're working with.

Most (but not all) models that utilize machine learning use the [🤗 Transformers](https://huggingface.co/docs/transformers/index) library, which provides APIs and tools to easily download and train pretrained models.

- [Learn more about downloading models from Hugging Face](https://huggingface.co/docs/hub/en/models-downloading)
- [Learn more about the 🤗 Transformers library](https://huggingface.co/docs/hub/en/transformers)

No matter which model you are using, be sure to thoroughly read the documentation to learn how to properly download and use the model locally.

### `python -m scripts.docker_build`

Builds and optionally publishes a Docker image for the module to use.

For most use cases, this script should be sufficient and won't require any configuration or modification (aside from setting your `DOCKER_REPO` and `DOCKER_TAG`).

#### `--push` Flag

Running the script with `--push` passed in pushes the Docker image to Docker Hub.

#### `--no-cache` Flag

Running the script with `--no-cache` passed in builds the Docker image without using the cache. Useful if you are having issues with your local Docker image. This flag is automatically applied when using `--push`.

### `python -m scripts.run_module`

This script is provided for convenience to speed up development. It is equivalent to running the Lilypad module with the provided input and private key (unless running the module locally, then no private key is required). Depending on how your module works, you may need to change the default behavior of this script.

#### `--local` Flag

Running the script with `--local` passed in runs the Lilypad module Docker image locally instead of on Lilypad's Network.
