# Hardware Requirements

This page overviews the hardware requirements to operate a Lilypad Network node. It's important to note that these requirements continuously evolve as the network grows. If you have questions or suggestions, please join our [Discord](https://lilypad.team/discord) or open a pull request on the [Lilypad documentation repository](https://github.com/Lilypad-Tech/lilypad-docs).

## Minimum Hardware Requirements

* **Processor**: Quad-core x64 Processor
* **RAM**: 16GB (see additional details below)
* **Internet**: 250Mbps Download Speed
* **GPU**: NVIDIA GPU with a minimum of 8GB VRAM (see additional details below)

## GPU Requirements

Each model operating on Lilypad has specific VRAM (Video Random Access Memory) requirements directly related to the model's complexity and computational demands.

* **Base Requirement:** The simplest model on Lilypad requires a GPU with at least 8GB of VRAM. This is the minimum necessary to engage in any computational tasks within our network.

### Scaling with VRAM

The capability of your GPU to manage multiple or more complex Lilypad jobs is enhanced by the amount of VRAM available:

* **Standard Models (**[**SDXL**](https://github.com/Lilypad-Tech/lilypad-module-sdxl-pipeline)**,** [**Ollama**](https://github.com/Lilypad-Tech/lilypad-module-ollama-pipeline)**):** Requires 8GB of VRAM.
* **Advanced Models (**[**SDV**](https://github.com/Lilypad-Tech/lilypad-module-sdv-pipeline)**):** Requires 14GB of VRAM.

### Hardware Compatibility

* GPUs with only 8GB of VRAM are limited to running models that fit within this specification. Higher VRAM GPUs allow for the processing of heavier models and increase the capacity to handle several jobs simultaneously.

#### For example:&#x20;

* A node with a GPU containing 8GB of VRAM can execute Lilypad [SDXL](https://github.com/Lilypad-Tech/lilypad-module-sdxl-pipeline) module jobs, which require a minimum of 8GB of VRAM.
* Larger capacity GPUs are needed for heavier compute models like [SDV](https://github.com/Lilypad-Tech/lilypad-module-sdv-pipeline), which require at least 14GB of VRAM.

## RAM Requirements

Lilypad uses the Resource Provider's GPU to load models, initially requiring the temporary storage of the data in the system's RAM. In a production environment with RP Nodes, it is important to have enough RAM to support the model and the underlying system's operational processes.

### Minimum RAM Requirements:

* **Base Requirement:** A minimum of 16GB of RAM is required, with at least 8GB dedicated to the model and another 8GB allocated for system operations and Lilypad processes.

## Additional Considerations

* **Larger Models:** Jobs involving more substantial models will demand additional RAM. It's important to note that adequate VRAM alone is insufficient; your system must also have enough RAM to load the model into the GPU successfully. A lack of sufficient system RAM will prevent the model from being loaded, regardless of the VRAM available.
