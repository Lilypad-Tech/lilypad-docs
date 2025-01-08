---
description: Run Llama 2 on the Lilypad network
---

# Llama2

These instructions provide steps for running the Llama2 module on the Lilypad network using Docker and the Lilypad CLI. Find the module repo [here](https://github.com/noryev/module-llama2/tree/main).

## Getting Started <a href="#getting-started" id="getting-started"></a>

#### Prerequisites <a href="#prerequisites" id="prerequisites"></a>

Before running `llama2`, make sure you have the [Lilypad CLI installed](https://docs.lilypad.tech/lilypad/lilypad-testnet/install-run-requirements) on your machine and your private key environment variable is set. This is necessary for operations within the Lilypad network.

```bash
export WEB3_PRIVATE_KEY=<YOUR_PRIVATE_KEY>
```

Learn more about installing the Lilypad CLI and running a Lilypad job with this [video guide](https://www.youtube.com/watch?v=RBECCMl_fco).

## Run Llama2

#### Run Llama2 <a href="#run-sdxl-turbo" id="run-sdxl-turbo"></a>

```bash
lilypad run github.com/noryev/module-llama2:6d4fd8c07b5f64907bd22624603c2dd54165c215 -i prompt="your prompt here"
```

Example:

```bash
lilypad run github.com/noryev/module-llama2:6d4fd8c07b5f64907bd22624603c2dd54165c215 -i prompt="what is a giant sand trout on arrakis?"
```

#### Notes <a href="#notes" id="notes"></a>

* Ensure you have the necessary permissions and resources to run Docker containers with GPU support.
* The module version (6d4fd8c07b5f64907bd22624603c2dd54165c215) may be updated. Check for the latest version before running.
* Adjust port mappings and volume mounts as needed for your specific setup.

### Llama2 Output <a href="#sdxl-output" id="sdxl-output"></a>

To view the results in a local directory, navigate to the local folder provided by the job result.

```
open /tmp/lilypad/data/downloaded-files/<fileID>
```

In the **/outputs** folder, you'll find the image:

To view the results on IPFS, navigate to the IPFS CID result output.

\
