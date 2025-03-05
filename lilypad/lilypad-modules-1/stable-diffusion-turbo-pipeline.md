---
description: A Lightweight Stable Diffusion Module for Lilypad
---

# Stable Diffusion Turbo Pipeline

These instructions provide steps for running the SDXL Turbo Pipeline module on the Lilypad network using Docker and Lilypad CLI. Find the module repo [here](https://github.com/noryev/module-sdxl-ipfs).

## Getting Started

Before running `sdxl turbo`, make sure you have the [Lilypad CLI installed](https://docs.lilypad.tech/lilypad/lilypad-testnet/install-run-requirements) on your machine and your private key environment variable is set. This is necessary for operations within the Lilypad network.

```bash
export WEB3_PRIVATE_KEY=<YOUR_PRIVATE_KEY>
```

Learn more about installing the Lilypad CLI and running a Lilypad job with this [video guide](https://www.youtube.com/watch?v=RBECCMl_fco).

## Run SDXL Turbo

```
lilypad run github.com/noryev/module-sdxl-ipfs:ae17e969cadab1c53d7cabab1927bb403f02fd2a -i prompt="your prompt here"
```

Example:

```
lilypad run github.com/noryev/module-sdxl-ipfs:ae17e969cadab1c53d7cabab1927bb403f02fd2a -i prompt="a spaceship parked on mountain"
```

### Notes

* Ensure you have the necessary permissions and resources to run Docker containers with GPU support.
* The module version (`ae17e969cadab1c53d7cabab1927bb403f02fd2a`) may be updated. Check for the latest version before running.
* Adjust port mappings and volume mounts as needed for your specific setup.

### Output

To view the results in a local directory, navigate to the local folder.

```
open /tmp/lilypad/data/downloaded-files/<fileID>
```
