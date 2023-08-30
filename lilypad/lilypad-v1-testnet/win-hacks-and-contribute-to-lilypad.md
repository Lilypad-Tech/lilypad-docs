---
description: Ideas and Guides for Contributing to Lilypad
---

# Win Hacks & Contribute to Lilypad

## Hackathon & Project Ideas for Lilypad v1

Here's some ideas for what you could build with Lilypad v1!

{% hint style="info" %}
:green\_heart: Good first project

:yellow\_heart: Moderate skill needed

:heart: God mode!
{% endhint %}

1. :green\_heart: Build cowsay as a service! -> see [hello-cow-world.md](../lilypad-v1-examples/hello-cow-world.md "mention")
2. :green\_heart: Stable diffusion as a service (text to image) -> see [stable-diffusion.md](../lilypad-v1-examples/stable-diffusion.md "mention")
3. :yellow\_heart: Use Stable diffusion fine tuning as a service (e.g. give me pics of you and add a beer or whatever, via LoRA) - **this is a distributed compute network that triggers from a smart contract and that ACTUALLY CONSUMES DATA FROM IPFS and writes output data as CIDs and consumes them from inference -** this is breakthrough computing!&#x20;
4. :yellow\_heart:  Build a Javascript wrapper for the CLI
5. :yellow\_heart:  Filecoin data prep: integrate with Filecoin service providers (requires knowledge of **Filecoin Storage Market**) -> see [filecoin-data-prep.md](../lilypad-v1-examples/filecoin-data-prep.md "mention")
6. :heart: Advanced: arbitrary WASM - write your own code and compile it to WASM and run it
7. :heart: :heart: God Mode: Contribute a module (see below)

## Module Contributions!

Contribute a Module to Lilypad!

{% embed url="https://media4.giphy.com/media/v1.Y2lkPTc5MGI3NjExbHV0NmhjNTFiOHcwcTJ5ZGh3cjgzM2VuZWNiZWd6MjB0ZzI2emp6cCZlcD12MV9naWZzX3NlYXJjaCZjdD1n/wi8Ez1mwRcKGI/200.gif" %}

{% hint style="danger" %}
Modules must be [Deterministic](https://en.wikipedia.org/wiki/Deterministic\_system)!
{% endhint %}

If you're a rockstar dev and want to try your hand at contributing a module to Lilypad, see [CONTRIBUTING.md](https://github.com/bacalhau-project/lilypad/blob/main/CONTRIBUTING.md).&#x20;

Lilypad core dev's enjoy an easy dev environment so hopefully, they've also made it easy for you to contribute too - if you do have any questions of queries though - we're always available in the Slack! (see [join-the-community.md](../tutorials-and-content/join-the-community.md "mention")).\
\
Module code is found [here](https://github.com/bacalhau-project/lilypad/tree/main/src/python/modules).

As an example, check out the cowsay module [here](https://github.com/bacalhau-project/lilypad/blob/main/src/python/modules/cowsay.py).

To contribute, submit a PR including this file [here](https://github.com/bacalhau-project/lilypad/blob/main/src/python/modicum/Modules.py)



## More Inspiration?

* Create a gasless transaction pipeline with Bacalhau
* Build new features for Waterlily.ai
* Peruse the [project-showcase.md](../use-cases/project-showcase.md "mention")page!

