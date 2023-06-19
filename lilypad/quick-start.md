---
description: >-
  Get Started with Lilypad v0 - Call off-chain distributed compute from your
  smart contract!
---

# 🎮 Quick Start

## How it Works

<figure><img src=".gitbook/assets/Lilypad Architecture.png" alt=""><figcaption><p>Lilypad v0 Architecture<br></p></figcaption></figure>

## Quick Start Guide

{% hint style="info" %}
The Lilypad Contracts are not currently importable via npm (though this is in progress), so to import them to you own project, you'll need to use their github links
{% endhint %}

{% embed url="https://youtu.be/B0l0gFYxADY" %}
Calling Bacalhau from FEVM Smart Contracts with Lilypad
{% endembed %}

Using Lilypad in your own solidity smart contract requires the following steps

1.  Create a contract that implements the [LilypadCaller interface](https://github.com/bacalhau-project/lilypad/blob/main/hardhat/contracts/LilypadCallerInterface.sol).&#x20;

    As part of this interface you need to implement 2 functions:

    * `lilypadFulfilled` - a callback function that will be called when the job completes successfully
    * `lilypadCancelled` - a callback function that will be called when the job fails
2. Provide a public [Docker Spec compatible for use on Bacalhau](https://docs.bacalhau.org/getting-started/docker-workload-onboarding)
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



## Add a docker spec compatible with [Bacalhau](https://www.docs.bacalhau.org)

&#x20;



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
