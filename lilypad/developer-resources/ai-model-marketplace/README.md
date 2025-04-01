---
description: Introduction to running AI models on Lilypad with the Module Marketplace
---

# AI Model Marketplace

Lilypad makes it easy to deploy and run AI models with an AI model hub called the [Lilypad Module Marketplace](https://github.com/Lilypad-Tech/awesome-Lilypad?tab=readme-ov-file#modules).&#x20;

Currently setup in the [awesome-lilypad github repo](https://github.com/Lilypad-Tech/awesome-Lilypad?tab=readme-ov-file#modules), the Module Marketplace makes it easy for AI model creators to distribute their work and for the community to quickly get started running a wide range of open source AI models.

There are two ways that participants in the network can interact with Lilypad Modules: As _Job Creators_ who run modules, or as _Module Creators_ who create modules.

## Running Modules

Running Jobs (participating as a 'Job Creator') is just a few simple steps:

* Use the Lilypad [AI inference API](../inference-api.md) or [install our CLI](../../quickstart/cli/installation.md)
* Choose a module to run and send a job request

### **Example Modules**

Try out some of the Lilypad team modules:

* [cowsay.md](build-a-job-module/cowsay.md "mention")
* [llama2.md](build-a-job-module/llama2.md "mention")
* [stable-diffusion-turbo-pipeline.md](build-a-job-module/stable-diffusion-turbo-pipeline.md "mention")

Additional modules from the community are available in the [awesome-lilypad repo](https://github.com/Lilypad-Tech/awesome-Lilypad?tab=readme-ov-file#modules).

## Creating Modules

A [Lilypad Module](https://docs.lilypad.tech/lilypad/developer-resources/module-marketplace/build-a-job-module) is a standard containerized (Docker) process for running compute workloads on Lilypad.&#x20;

Modules can be developed by any member of the community (participating as a 'Module Creator'). If there is an AI model (or other compute job) you wish to run using the Lilypad Network resources, create a new Module and [add it to the Module Marketplace](https://blog.lilypadnetwork.org/lilypad-module-creator-rewards-beta#heading-submitting-a-module)!

### Developer Resources

* [build-a-job-module](build-a-job-module/ "mention")
* [create-lilypad-module](create-lilypad-module/ "mention")
* [Module Builder Guide](https://blog.lilypadnetwork.org/lilypad-module-builder-guide)
