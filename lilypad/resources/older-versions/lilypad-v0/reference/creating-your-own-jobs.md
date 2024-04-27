---
description: Creating Bacalhau Job Spec's
---

# Creating your own Jobs

{% hint style="info" %}
There are several public examples you can try out without needing to know anything about Docker or WASM specification jobs -> see the [Bacalhau Docs](https://www.docs.bacalhau.org). The full specification for Bacalhau jobs can be [seen here](https://docs.bacalhau.org/all-flags).
{% endhint %}

## What do I need to know to make Bacalhau Jobs?

* Bacalhau is language-agnostic, and supports [Docker](https://docs.bacalhau.org/getting-started/docker-workload-onboarding) or [WASM](https://docs.bacalhau.org/getting-started/wasm-workload-onboarding) workloads. As long as you can run your executable in a container, you can run it in Bacalhau.
* You need to supply a Bacalhau job spec. To create a job spec, you can:
  * Run a Bacalhau job successfully, and then get the job spec back using `bacalhau describe <job_id> --format=json`.
  * Generate a job spec without running anything, using `bacalhau docker run --dry-run`.
  * Writing a job spec by hand, by using our [schema](https://schema.bacalhau.org/) as a guide.
* What can I do with Bacalhau now? You can:
  * read from IPFS, Filecoin, or URLs
  * write into Estuary or IPFS

## Bacalhau Specification in JSON format

Bacalhau operates by executing jobs within containers. This means it is able to run any arbitrary Docker jobs or WASM images

Here's an example JSON job specification for a Stable Diffusion job which runs in a Docker container, requires no verification and publishes to [Estuary](https://www.estuary.tech).

```json
{
    "Engine": "docker", 
    "Verifier": "noop",
    "PublisherSpec": {"Type": "estuary"},
    "Docker": {
    "Image": "ghcr.io/bacalhau-project/examples/stable-diffusion-gpu:0.0.1",
    "Entrypoint": ["python", "main.py", "--o", "./outputs", "--p", "A User Prompt Goes here"]},
    "Resources": {"GPU": "1"},
    "Outputs": [{"Name": "outputs", "Path": "/outputs"}],
    "Deal": {"Concurrency": 1}
}
```

Here's an example of using this JSON specification in a solidity smart contract:

Note that since we need to be able to add the user prompt input to the middle of the spec (in the Docker entrypoint), it's been split into 2 parts.

```solidity
string constant specStart = '{'
    '"Engine": "docker",'
    '"Verifier": "noop",'
    '"PublisherSpec": {"Type": "estuary"},'
    '"Docker": {'
    '"Image": "ghcr.io/bacalhau-project/examples/stable-diffusion-gpu:0.0.1",'
    '"Entrypoint": ["python", "main.py", "--o", "./outputs", "--p", "';

string constant specEnd =
    '"]},'
    '"Resources": {"GPU": "1"},'
    '"Outputs": [{"Name": "outputs", "Path": "/outputs"}],'
    '"Deal": {"Concurrency": 1}'
    '}';

//Example of use:
string memory spec = string.concat(specStart, _prompt, specEnd);
```

## Any Example Jobs?

There is a full complement of example jobs you can leverage on the [Bacalhau Docs Site](https://docs.bacalhau.org/)

Try out

* YOLO
* OCR
* Video Editing
* and many, many more!
