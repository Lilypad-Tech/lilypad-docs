---
description: Learn about modules on Lilypad
hidden: true
---

# 🧩 Lilypad Modules

Lilypad modules are the compute jobs that are run on the Lilypad network of Resource Provider nodes. Lilypad nodes are set up to run GPU compute jobs such as AI inference, and can be used for other GPU-intensive tasks.

There are two ways that participants in the network can interact with Lilypad Modules: As _Job Creators_ who run modules, or as _Module Creators_ who create modules.

## Getting Started

Before running a module, make sure you have the [Lilypad CLI installed](../getting-started/installation.md) on your machine and your private key environment variable is set. This is necessary for operations within the Lilypad network.

```bash
export WEB3_PRIVATE_KEY=<YOUR_PRIVATE_KEY>
```

## Running Modules

Running Jobs (participating as a 'Job Creator') is just a few simple steps. You can get going in less than 15 minutes:

* [**Install the CLI** ](../getting-started/installation.md)or use[ **the API**](../developer-resources/inference-api.md)
* [**Set up a Metamask Wallet**](../getting-started/setting-up-your-wallet.md) then [**Fund your wallet**](../lilypad-testnet/quick-start/funding-your-wallet-from-faucet.md) with Lilypad tokens to run the jobs and get Arbitrum Sepolia Testnet ETH from one of the many faucets for network gas fees to execute jobs
* Choose a module to run, and send the job request

### **Example Modules**

There is a basic example [cowsay module](../lilypad-modules-1/cowsay.md) you can run, or try out some of the Lilypad team-supported modules:

* [**Llama 2**](../lilypad-modules-1/llama2.md)
* [**Stable Diffusion (SDXL0.9 & 1.0)**](../lilypad-modules-1/stable-diffusion-sdxl0.9.md)
* [**Stable Diffusion Turbo Pipeline**](../lilypad-modules-1/stable-diffusion-turbo-pipeline.md)
* [**Stable Diffusion Video (SDV1.0 & 1.1)**](../lilypad-modules-1/stable-diffusion-video-sdv1.0-and-1.1.md)
* [**Llama LLM**](../lilypad-modules-1/llama-llm.md)

Additional modules from the community are available in the [awesome-lilypad repo](https://github.com/Lilypad-Tech/awesome-Lilypad?tab=readme-ov-file#modules)

## Creating Modules

Modules can be developed by any member of the community (participating as a 'Module Creator'). If there is an AI model (or other compute job) you wish to run using the Lilypad Network resources, you can simply:

* Containerize your module
* Create a [Lilypad Config File](https://github.com/Lilypad-Tech/lilypad-module-cowsay/blob/main/lilypad_module.json.tmpl)
* Test your modules

See more in [**Build a Job Module**](../developer-resources/build-a-job-module.md) or for a more in-depth look at building modules, refer to this [end-to-end guide](https://blog.lilypadnetwork.org/lilypad-module-builder-guide).
