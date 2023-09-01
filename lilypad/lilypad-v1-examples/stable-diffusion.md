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



Use contract:

```solidity
// SPDX-License-Identifier: GPLv3
pragma solidity ^0.8.6;

interface ModicumContract {
  function runModuleWithDefaultMediators(string calldata name, string calldata params) external payable returns (uint256);
}

contract NaiveExamplesClient {
  address public _contractAddress;
  ModicumContract remoteContractInstance;
  string public resultCID;

  event ReceivedJobResults(uint256 jobID, string cid);

  constructor (address contractAddress) {
    require(contractAddress != address(0), "NaiveExamplesClient: contract cannot be zero address");
    _contractAddress = contractAddress;
    remoteContractInstance = ModicumContract(contractAddress);
  }

  function runCowsay(string memory sayWhat) public payable returns (uint256) {
    return runModule("cowsay:v0.0.1", sayWhat);
  }

  function runSDXL(string memory prompt) public payable returns (uint256) {
    return runModule("sdxl:v0.9-lilypad1", prompt);
  }

  function runModule(string memory name, string memory params) public payable returns (uint256) {
    return remoteContractInstance.runModuleWithDefaultMediators{value: msg.value}(name, params);
  }

  function receiveJobResults(uint256 jobID, string calldata cid) public {
    resultCID = cid;
    emit ReceivedJobResults(jobID, cid);
  }
}
```
