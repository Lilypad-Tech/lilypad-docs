---
description: Get Started with Lilypad v0 - Call docker jobs from a smart contract!
---

# Quick Start

## Quick Start Example

Using Lilypad in your own solidity smart contract requires 3 steps

1. Implement the LilypadCaller interface in your smart contract
2. Provide a docker spec compatible with Bacalhau
3. Call the LilypadEvents contract function runLilypadJob() passing in the specification from 2.

## Requirements

* A Docker Image suitable to run on Bacalhau (hint: see some examples in the \[Bacalhau Docs]\([https://docs.bacalhau.org/](https://docs.bacalhau.org/))
* Filecoin Virtual Machine Network wallet (eg. Metamask)

## Implement the LilypadCaller Interface in your contract

The Lilypad Contracts are not currently importable via npm (though this is in progress), so to import them to you own project, you'll need to copy over the LilypadCallerInterface and the LilypadEvents contract into your own project.\
\


{% embed url="https://github.com/bacalhau-project/lilypad/blob/main/hardhat/contracts/LilypadCallerInterface.sol" %}

Create a Smart Contract that implements the LilypadCaller Interface

```solidity
  /** === LilypadCaller Interface === **/
  pragma solidity >=0.8.4;
  
  enum LilypadResultType {
    CID,
    StdOut,
    StdErr,
    ExitCode
  }

  interface LilypadCallerInterface {
    function lilypadFulfilled(address _from, uint _jobId, LilypadResultType _resultType, string calldata _result) external;
    function lilypadCancelled(address _from, uint _jobId, string calldata _errorMsg) external;
  }

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



## How do I get started on using Lilypad in my project?🧑‍💻

1. Create a contract that implements [`LilypadCallerInterface`](https://github.com/bacalhau-project/lilypad/blob/main/hardhat/contracts/LilypadCallerInterface.sol). As part of this interface you need to implement 2 functions:
   * `lilypadFulfilled` - a callback function that will be called when the job completes successfully
   * `lilypadCancelled` - a callback function that will be called when the job fails
2. To trigger a job from your contract, you need to call our `LilypadEvents` contract which the bridge is listening to. You will connect to Bacalhau network via this bridge. Create an instance of [`LilypadEvents`](https://github.com/bacalhau-project/lilypad/blob/main/hardhat/contracts/LilypadEvents.sol) by passing the public contract address above to the `LilypadEvents` constructor. See our [example](https://github.com/bacalhau-project/lilypad/blob/main/examples/contracts/StableDiffusionCaller.sol#L29).
3.  To make a call to Bacalhau, call `runLilypadJob` from your function. You need to pass the following parameters:

    |      Name     |                                                               Type                                                              |                                                                                                              Purpose                                                                                                             |
    | :-----------: | :-----------------------------------------------------------------------------------------------------------------------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
    |    `_from`    |                                                            `address`                                                            |                                          The address of the calling contract, to which success or failure will be passed back. You should probably use address(this) from your contract.                                         |
    |    `_spec`    |                                                             `string`                                                            |                                                                    A Bacalhau job spec in JSON format. See below for more information on creating a job spec.                                                                    |
    | `_resultType` | [`LilypadResultType`](https://github.com/bacalhau-project/lilypad/blob/main/hardhat/contracts/LilypadCallerInterface.sol#L4-L9) | The type of result that you want to be returned. If you specify CID, the result tree will come back as a retrievable IPFS CID. If you specify StdOut, StdErr or ExitCode, those raw values output from the job will be returned. |

####

\


##

##

##
