---
description: Contribute your own module to Lilypad
---

# \[Advanced] DIY Module

{% hint style="warning" %}
Contributing your own module is currently a non-trivial process. The Lilypad team is aiming to make this DX easier as well as to add tutorials, walkthroughs and approaches to making modules over the next month. In the meantime if you try this and do get stuck - please reach out to us in [the Lilypad Discord](https://lilypad.team/discord) for help!
{% endhint %}

## Overview

Contributing your own module to use on Lilypad is possible and welcome!\
\
Essentially modules on Lilypad currently operate like [Bacalhau](https://docs.bacalhau.org) Job Specifications do - take a look at this page on [creating-your-own-jobs.md](../../lilypad-v0-deprecated/reference/creating-your-own-jobs.md "mention") to see more about how this works.\
\
In order that the modules on Lilypad are able to be verified and run on a trustless compute network, the modules also need to be deterministic, so that the job results can be verified by a mediator as needed. See [v1-documents](../../../../research-and-vision/v1-documents/ "mention") for more information on this process.

## Requirements

1. **Modules must be deterministic**: This means that the hash of the results directory will be the same given the same inputs (since we use the same hash tool as IPFS, in practice this means that the CIDs must match). Therefore, as long as a job always converges to the same answer, it does not matter which path it takes to get there. It just matters that the hash CID is the same as this is how mediators validate a result in the trustless network.
2. **Modules should be either Docker or WASM Images** that align to the Bacalhau job specifications (which then have some added metadata that defines the runtime options of the module).

## Module Example

Here is an example of the SDXL module in python:

{% @github-files/github-code-block url="https://github.com/bacalhau-project/lilypad-modicum/blob/main/src/python/modules/sdxl.py" %}

It's a function that given a "string" will return a [bacalhau](../../lilypad-v0-deprecated/reference/creating-your-own-jobs.md) docker job spec. That string can be whatever you want, JSON, csv, raw LLM prompt etc.\
\
In terms of output directories - you can see the SDXL example linked above names the "/outputs" folder and then will use that path in the command inside the Docker container.\
\
Any named folders like this that the Docker image can write files into - will be included as part of the results Lilypad gets back out of the job (and will change the result hash)

## Using Bacalhau as a testing ground

It's currently advisable to develop your module with [bacalhau](https://docs.bacalhau.org) first (because it's FAR easier to get setup as a development environment than Lilypad is currently).\
\
If you can get a function like the one shown above that will, given a string, write a bacalhau job spec that you can test with the bacalhau CLI - then you have already done 98% of the Lilypad module ![:+1:](https://a.slack-edge.com/production-standard-emoji-assets/14.0/apple-medium/1f44d.png)

To add this to Lilypad, submit a PR which also includes this file [here](https://github.com/bacalhau-project/lilypad-modicum/blob/main/src/python/modicum/Modules.py).

## Contributing Guidelines

See more in this guide on contributing to the Lilypad project: [CONTRIBUTING.md](https://github.com/bacalhau-project/lilypad-modicum/blob/main/CONTRIBUTING.md)

## The Future of Community Contributed Modules

From Lilypad incentivised testnet \[Q4 2023] onwards (and perhaps even earlier), its probable modules contributed by community members will be eligible for a % fee of jobs that run these modules in order to encourage the growth of the module ecosystem on the Lilypad Network.
