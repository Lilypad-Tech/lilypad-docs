---
description: >-
  Get Started with Lilypad v0 - Call off-chain distributed compute from your
  smart contract!
---

# 🎮 Lilypad v0 Quick Start

## How it Works

<figure><img src=".gitbook/assets/Lilypad Architecture.png" alt=""><figcaption><p>Lilypad v0 Architecture<br></p></figcaption></figure>

## Quick Start Guide

{% hint style="info" %}
The Lilypad Contracts are not currently importable via npm (though this is in progress), so to import them to you own project, you'll need to use their github links
{% endhint %}

Using Lilypad in your own solidity smart contract requires the following steps

1.  Create a contract that implements the [LilypadCaller interface](https://github.com/bacalhau-project/lilypad/blob/main/hardhat/contracts/LilypadCallerInterface.sol).&#x20;

    As part of this interface you need to implement 2 functions:

    * `lilypadFulfilled` - a callback function that will be called when the job completes successfully
    * `lilypadCancelled` - a callback function that will be called when the job fails
2. Provide a public [Docker Spec compatible for use on Bacalhau](https://docs.bacalhau.org/getting-started/docker-workload-onboarding) in JSON format to the contract.
3. To trigger a job from your contract, you need to call the `LilypadEvents` contract which the Lilypad bridge is listening to and which connects to the Bacalhau public network. Create an instance of [`LilypadEvents`](https://github.com/bacalhau-project/lilypad/blob/main/hardhat/contracts/LilypadEvents.sol) by passing the public contract address on the network you are using (see [deployed-network-details.md](lilypad-v0-reference/deployed-network-details.md "mention")) to the `LilypadEvents` constructor.
4. Call the [LilypadEvents contract](https://github.com/bacalhau-project/lilypad/blob/main/hardhat/contracts/LilypadEventsUpgradeable.sol) function `runLilypadJob()` passing in the following parameters.&#x20;

|      Name     |                                                               Type                                                              |                                                                                                              Purpose                                                                                                             |
| :-----------: | :-----------------------------------------------------------------------------------------------------------------------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|    `_from`    |                                                            `address`                                                            |                                          The address of the calling contract, to which success or failure will be passed back. You should probably use address(this) from your contract.                                         |
|    `_spec`    |                                                             `string`                                                            |                                                                    A Bacalhau job spec in JSON format. See below for more information on creating a job spec.                                                                    |
| `_resultType` | [`LilypadResultType`](https://github.com/bacalhau-project/lilypad/blob/main/hardhat/contracts/LilypadCallerInterface.sol#L4-L9) | The type of result that you want to be returned. If you specify CID, the result tree will come back as a retrievable IPFS CID. If you specify StdOut, StdErr or ExitCode, those raw values output from the job will be returned. |



## Implement the LilypadCaller Interface in your contract

Create a contract that implements [`LilypadCallerInterface`](https://github.com/bacalhau-project/lilypad/blob/main/hardhat/contracts/LilypadCallerInterface.sol). As part of this interface you need to implement 2 functions:

* `lilypadFulfilled` - a callback function that will be called when the job completes successfully
* `lilypadCancelled` - a callback function that will be called when the job fails

```solidity
  /** === LilypadCaller Interface === **/
  pragma solidity >=0.8.4;
  import 'https://github.com/bacalhau-project/lilypad/blob/main/hardhat/contracts/LilypadCallerInterface.sol' //Location of file link

  /** === User Contract Example === **/
  contract MyContract is LilypadCallerInterface {

      function lilypadFulfilled(address _from, uint _jobId,   
          LilypadResultType _resultType, string calldata _result)        
          external override {
          // Do something when the LilypadEvents contract returns    
          // results successfully
      }

      function lilypadCancelled(address _from, uint _jobId, string 
          calldata _errorMsg) external override {
          // Do something if there's an error returned by the
          // LilypadEvents contract
      }
  }

```

## Add a Spec compatible with [Bacalhau](https://www.docs.bacalhau.org)

{% hint style="info" %}
There are several public examples you can try out without needing to know anything about Docker or WASM specification jobs -> see the [Bacalhau Docs](https://www.docs.bacalhau.org). The full specification for Bacalhau jobs can be [seen here](https://docs.bacalhau.org/all-flags).
{% endhint %}

Bacalhau operates by executing jobs within containers. This means it is able to run any arbitrary Docker jobs or WASM images

We'll use the public Stable Diffusion Docker Container[ located here](https://github.com/bacalhau-project/examples/pkgs/container/examples%2Fstable-diffusion-gpu) for this example.

Here's an example JSON job specification for the Stable Diffusion job:

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

Here's an example of using this JSON specification in solidity:

Note that since we need to be able to add the user prompt input to the spec, it's been split into 2 parts.

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

{% hint style="info" %}
See more about how to [onboard your Docker Workloads for Bacalhau](https://docs.bacalhau.org/getting-started/docker-workload-onboarding/), [Onboard WebAssembly Workloads](https://docs.bacalhau.org/getting-started/wasm-workload-onboarding) or [Work with Custom Containers](https://docs.bacalhau.org/examples/workload-onboarding/custom-containers/) in the Bacalhau Docs.
{% endhint %}

## Add the Lilypad Events Address





## Call the LilypadEvents runLilypadJob function

##

##

##

## Requirements

* A Docker Image suitable to run on Bacalhau (hint: see this [guide](https://docs.bacalhau.org/getting-started/docker-workload-onboarding) in the [Bacalhau Docs](https://docs.bacalhau.org/)
* Filecoin Virtual Machine Network wallet (eg. Metamask)

\


##

##

##
