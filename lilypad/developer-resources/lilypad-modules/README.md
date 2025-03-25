---
description: Introduction to Lilypad modules
---

# Lilypad Modules

Lilypad modules are the compute jobs that are run on the Lilypad network of Resource Provider nodes. Lilypad nodes are set up to run GPU compute jobs such as AI inference, and can be used for other GPU-intensive tasks.

There are two ways that participants in the network can interact with Lilypad Modules: As _Job Creators_ who run modules, or as _Module Creators_ who create modules.

## Running Modules

Running Jobs (participating as a 'Job Creator') is just a few simple steps:

* Use our [AI inference API](../inference-api.md) or [install our CLI](../../quickstart/cli/installation.md)
* Choose a module to run, and send a job request

### **Example Modules**

Try out some of the Lilypad team modules:

* [cowsay.md](cowsay.md "mention")
* [llama2.md](llama2.md "mention")
* [stable-diffusion-turbo-pipeline.md](stable-diffusion-turbo-pipeline.md "mention")

Additional modules from the community are available in the [awesome-lilypad repo](https://github.com/Lilypad-Tech/awesome-Lilypad?tab=readme-ov-file#modules)

## Creating Modules

Modules can be developed by any member of the community (participating as a 'Module Creator'). If there is an AI model (or other compute job) you wish to run using the Lilypad Network resources, you can create your own job module!

### Developer Resources

* [build-a-job-module.md](build-a-job-module.md "mention")
* [create-lilypad-module](create-lilypad-module/ "mention")
