---
description: Run a Stable Diffusion Text to Image Job
---

# Stable Diffusion

{% hint style="warning" %}
Ensure you have installed all requirements [install-run-requirements.md](../lilypad-v1-testnet/quick-start/install-run-requirements.md "mention")
{% endhint %}

## Running Stable Diffusion from the CLI

```
lilypad run sdxl:v0.9-lilypad1 "purple jellyfish in the sky"
```

```
lilypad run sdxl:v0.9-lilypad1 "an astronaut riding on a unicorn"
```

```
lilypad run sdxl:v0.9-lilypad1 '{"prompt": "an astronaut riding on a unicorn", "seed": 99}'
```

{% embed url="https://youtu.be/-ae3M4VtL88" %}
Lilypad \[CLI] Stable Diffusion with SDLX 0.9 Demo
{% endembed %}

## Running Stable Diffusion from a Smart Contract

{% embed url="https://youtu.be/aK12PRx8V0k" %}

Use contract addresses from [https://github.com/bacalhau-project/lilypad-modicum/blob/main/latest.txt](https://github.com/bacalhau-project/lilypad-modicum/blob/main/latest.txt)&#x20;

{% @github-files/github-code-block url="https://github.com/bacalhau-project/lilypad-modicum/blob/main/latest.txt" %}



Use contract [here](https://github.com/bacalhau-project/lilypad-modicum/blob/main/src/js/contracts/ExampleClient.sol):

```solidity
// SPDX-License-Identifier: GPLv3
pragma solidity ^0.8.6;

interface ModicumContract {
  function runModuleWithDefaultMediators(string calldata name, string calldata params) external payable returns (uint256);
}

// Payment is 2 lilETH for all jobs currently
// got to testnet.lilypadnetwork.org to fund your wallet
contract ExampleClient {
  address public _contractAddress;
  ModicumContract remoteContractInstance;

  uint256 public lilypadFee = 2;

  struct Result {
      uint256 jobID;
      string cid;
      string httpString;
  }

  Result[] public results;

  event ReceivedJobResults(uint256 jobID, string cid);

  // The Modicum contract address is found here: https://github.com/bacalhau-project/lilypad-modicum/blob/main/latest.txt
  // Current: 0x422F325AA109A3038BDCb7B03Dd0331A4aC2cD1a
  constructor (address contractAddress) {
    require(contractAddress != address(0), "NaiveExamplesClient: contract cannot be zero address");
    _contractAddress = contractAddress;
    remoteContractInstance = ModicumContract(contractAddress);
  }

  function setLilypadFee(uint256 _fee) public {
      lilypadFee = _fee;
  }

  function runCowsay(string memory sayWhat) public payable returns (uint256) {
    require(msg.value == lilypadFee * 1 ether, string(abi.encodePacked("Payment of 2 Ether is required")));
    return runModule("cowsay:v0.0.1", sayWhat);
  }

  function runStablediffusion(string memory prompt) public payable returns (uint256) {
    require(msg.value == lilypadFee * 1 ether, string(abi.encodePacked("Payment of 2 Ether is required")));
    return runModule("stable_diffusion:v0.0.1", prompt);
  }

  function runSDXL(string memory prompt) public payable returns (uint256) {
    require(msg.value == lilypadFee * 1 ether, string(abi.encodePacked("Payment of 2 Ether is required")));
    return runModule("sdxl:v0.9-lilypad1", prompt);
  }

  function runModule(string memory name, string memory params) public payable returns (uint256) {
    require(msg.value == lilypadFee * 1 ether, string(abi.encodePacked("Payment of 2 Ether is required")));
    return remoteContractInstance.runModuleWithDefaultMediators{value: msg.value}(name, params);
  }

  // Implemented Modicum interface. This saves results to a results array
  function receiveJobResults(uint256 _jobID, string calldata _cid) public {
    Result memory jobResult = Result({
        jobID: _jobID,
        cid: _cid,
        httpString: string(abi.encodePacked("https://ipfs.io/ipfs/", _cid))
    });
    results.push(jobResult);

    emit ReceivedJobResults(_jobID, _cid);
  }

  function fetchAllResults() public view returns (Result[] memory) {
    return results;
  }
}
```



\====== deprecated======

The function call needed to run a job from a smart contract can be found below:

{% @github-files/github-code-block url="https://github.com/bacalhau-project/lilypad/blob/client-smart-contract/src/js/contracts/NaiveExamplesClient.sol" %}

In the above script the function to receive the Job results back is `receiveJobResult`() - so it's essential to put this function in your own smart contract.\
\
\
Here's an example of a working script that can trigger the above function calls&#x20;
