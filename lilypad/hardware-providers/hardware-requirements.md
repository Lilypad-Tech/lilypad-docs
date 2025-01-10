# Hardware Requirements

This page overviews the hardware requirements to operate a Lilypad Network node. It's important to note that these requirements continuously evolve as the network grows. If you have questions or suggestions, please join our [Discord](https://lilypad.team/discord) or open a pull request on the [Lilypad documentation repo](https://github.com/Lilypad-Tech/lilypad-docs).

## Minimum Hardware Requirements

* **Processor**: Quad-core x64 Processor or better
* **RAM**: 32GB (see additional details below)
* **Internet**: Internet: 250Mbps download, 100Mbps upload (minimum)
* **GPU**: NVIDIA GPU with a minimum of 8GB VRAM (see additional details below)
* **Storage:** SSD with at least 500gb of free space

## GPU Requirements

Each model operating on Lilypad has specific VRAM (Video Random Access Memory) requirements directly related to the model's complexity and computational demands. For running a Lilypad Resource Provider (RP) with multiple GPUs, a guide using Proxmox can be found [here](https://github.com/Lilypad-Tech/lilypad-tools/blob/main/proxmox/multi-gpu-proxmox.md).

* **Base Requirement:** The simplest model on Lilypad requires a GPU with at least 8GB of VRAM. This is the minimum required to participate in computational tasks on the Lilypad network.

### Model-Specific VRAM Requirements

The capability of your GPU to manage multiple or more complex Lilypad jobs is enhanced by the amount of VRAM available:

* **Standard Models (**[**SDXL**](https://github.com/Lilypad-Tech/lilypad-module-sdxl-pipeline)**,** [**Ollama**](https://github.com/Lilypad-Tech/lilypad-module-ollama-pipeline)**):** Requires 8GB of VRAM.
* **Advanced Models (**[**SDV**](https://github.com/Lilypad-Tech/lilypad-module-sdv-pipeline)**):** Requires 14GB of VRAM.

### Hardware Compatibility

* GPUs with 8GB of VRAM are limited to running models like SDXL, which fit within this specification. Larger GPUs with higher VRAM are required for more demanding models like SDV, which needs at least 14GB of VRAM.

#### For example:

* A node with a GPU containing 8GB of VRAM can execute Lilypad [SDXL](https://github.com/Lilypad-Tech/lilypad-module-sdxl-pipeline) module jobs, which require a minimum of 8GB of VRAM.
* Larger capacity GPUs are needed for heavier compute models like [SDV](https://github.com/Lilypad-Tech/lilypad-module-sdv-pipeline), which require at least 14GB of VRAM.

## RAM Requirements

Lilypad uses the Resource Provider's GPU to load models, initially requiring the temporary storage of the data in the system's RAM. In a production environment with RP Nodes, it is important to have enough RAM to support the model and the underlying system's operational processes.

### Minimum RAM Requirements:

* **Base Requirement:** A minimum of 16GB of RAM is required, with at least 8GB dedicated to the model and another 8GB allocated for system operations and Lilypad processes.

## Additional Considerations

* **Wallets for each GPU:** You need a separate account for each GPU you want to set up on the network. The wallet you use for your account must have both ETH (to run smart contracts on Ethereum) and Lilypad (LP) tokens in order to receive funds for jobs) on the network.

<figure><img src="../../.gitbook/assets/eth-lp-wallet.png.png" alt="" width="355"><figcaption><p>"a wallet funded with both ETH and LP tokens"</p></figcaption></figure>

* **Larger Models:** Jobs involving more substantial models will demand additional RAM. It's important to note that adequate VRAM alone is insufficient; your system must also have enough RAM to load the model into the GPU successfully. Without sufficient system RAM, the model cannot be loaded into the GPU, regardless of available VRAM.
