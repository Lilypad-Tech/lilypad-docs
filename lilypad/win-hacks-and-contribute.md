---
description: Here's some ideas for building on or contributing to Lilypad!
---

# 🙌 Win Hacks & Contribute

## Hackathon & Project Ideas for Lilypad (Milky Way)

Here's some ideas for what you could build with Lilypad Milky Way!

{% hint style="info" %}
💚 Good first project (Lilypadawan)

💛 Moderate skill needed

❤️ Jedi mode!&#x20;
{% endhint %}

### 🤝 Crossover POCs, Integrations & Plugins!

{% hint style="success" %}
Earn those double bounty dollars building out crossover POCs to Lilypad!
{% endhint %}

Lilypad is aiming to build out a full suite of decentralised AI projects which means we want to collaborate with other projects in the ecosystem to make this vision a reality.&#x20;

These include linking Lilypad compute with storage providers, data streams, databases & more.

This also means adding layers like privacy or extending usage into other frameworks like unity or react native projects.\
\
Some examples include:

* Using Filecoin aggregators like Banyan or Tableland Basin with Lilypad
* Extending the Chainsafe Unity SDK to add Lilypad jobs as an option
* Building Lilypad into Mona or creating a module to use on Mona
* Integrating with The Graph
* Doing a POC with data from someone like WeatherXM
* Adding privacy layers for data with Lit Protocol.

There's also opportunities to extend the functionality of Lilypad compute with items like\
\- CICD pipelines\
\- vector databases\
\- Autonomous agents\
\- Batching jobs with an external script\
\- Chaining jobs together in a pipeline\


### 💅 Contribute a Module

Contributing a module is one of the coolest things to contribute to Lilypad.

As a quick refresher, the current Module Making Pipeline ([see a fuller resource here](https://docs.lilypad.tech/lilypad/lilypad-milky-way-reference/build-a-job-module)) looks like this:

1. Find or build a compute script ([for example a python script on Huggingface like sdxl](https://huggingface.co/docs/diffusers/en/using-diffusers/sdxl))
2. **NOTE**: You must [make sure your compute job is deterministic](https://docs.lilypad.tech/lilypad/lilypad-milky-way-reference/build-a-job-module#ensuring-determinism) (this is possible with AI scripts also! [See this reference](https://huggingface.co/docs/diffusers/v0.27.2/en/using-diffusers/reusing\_seeds#reproducible-pipelines))
3. Containerise the script with Docker ([see this blog for more info](https://blog.lilypad.tech))
4. Add a Lilypad Spec - this is simply a github repo - [you can grab a template here](https://github.com/Lilypad-Tech/lilypad-module-boilerplate)!

{% hint style="warning" %}
Share your module with us by submitting a pull request to the [github here](https://github.com/Lilypad-Tech/awesome-Lilypad?tab=readme-ov-file#modules)!
{% endhint %}

### ✨ DX Enhancements

Lilypad is still evolving and is currently mostly in Beta phase. This means there are A LOT of opportunities to help build out better DX for your fellow dev's.

One of the main opportunities is in the module making pipeline. See [#contribute-a-module](win-hacks-and-contribute.md#contribute-a-module "mention") for a quick breakdown on the developer journey).\
\
Some of the opportunities to improve this process include:

* 💛 An application that can auto-containerise (or auto-dockerise) a given compute script
  * ❤️ BONUS IDEA: You could even then make a module to run the auto-containerising script on Lilypad after it's built! 🧙
* 💚 You could go one further and also have it auto-generate the Lilypad spec as well!
* ❤️ A determinism checker that could help determine if there is any obvious parts of the script (like timestamps) that would make it non-deterministic and show an error for this.
* 💛💛 Ways to make it easy for folks without GPUs at home to build & test a module
* 💛 Build a UI for folks to share their modules with

### 👾 End User Projects

Build out other end user projects across a broad range of verticals. We are super interested to hear the type of projects people are looking to build on the Lilypad Network and have released a Javascript wrapper to help folks build easily.\
\
Projects across DeFi, DeSci, Gaming, & Metaverse, NFTs, IOT and more, as well [#crossover-pocs-integrations-and-plugins](win-hacks-and-contribute.md#crossover-pocs-integrations-and-plugins "mention")!\


### 🐐 Need more inspiration?

See the [project-showcase.md](use-cases/project-showcase.md "mention") page!

{% hint style="info" %}
Pssst... We'd love to share your projects here too! Feel free to [submit a PR](https://github.com/Lilypad-Tech/lilypad-docs)!
{% endhint %}

<figure><img src=".gitbook/assets/showcase.gif" alt=""><figcaption></figcaption></figure>

