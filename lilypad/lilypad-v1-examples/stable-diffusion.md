---
description: Run a Stable Diffusion Text to Image Job
---

# Stable Diffusion (SDXL0.9)

## Running Stable Diffusion from the CLI

{% hint style="warning" %}
Ensure you have installed all requirements [install-run-requirements.md](../lilypad-v1-testnet/quick-start/install-run-requirements.md "mention")
{% endhint %}

To run stable diffusion use the sdxl module like so:

```
lilypad run sdxl:v0.9-lilypad1 "an astronaut riding on a unicorn"
```

The output will look like this:&#x20;

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

Take the ipfs link given in the results and paste it into your browser:

{% hint style="warning" %}
Please be patient! IPFS can take some time to propagate and doesn't always work immediately. We have informed the IPFS team.
{% endhint %}

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption><p>Results of SDXL job on IPFS Directory (<a href="https://ipfs.io/ipfs/QmSXkyM9bkKPCWaDSvViS14nvbNekGQTJTTeNv7JitSeWZ">https://ipfs.io/ipfs/QmSXkyM9bkKPCWaDSvViS14nvbNekGQTJTTeNv7JitSeWZ</a>)</p></figcaption></figure>

In the **/outputs** folder, you'll find the image:

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption><p>The Image in the outputs folder</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption><p><a href="https://ipfs.io/ipfs/QmSXkyM9bkKPCWaDSvViS14nvbNekGQTJTTeNv7JitSeWZ">https://ipfs.io/ipfs/QmSXkyM9bkKPCWaDSvViS14nvbNekGQTJTTeNv7JitSeWZ</a><a href="stable-diffusion.md#running-stable-diffusion-from-the-cli">/outputs/image-0.png</a> or <a href="ipfs://bafybeib6i434yl6ql46jyyydz2boqulysmksye3f5khs24c6uoqpnxkp3y/outputs/image-0.png">ipfs://bafybeib6i434yl6ql46jyyydz2boqulysmksye3f5khs24c6uoqpnxkp3y/outputs/image-0.png</a> in IPFS supported browsers like Brave</p></figcaption></figure>

Since modules are deterministic, running this command with the same text prompt will produce the same image, since the same seed is also used (the default seed is 0).

{% hint style="info" %}
See this [beginner-friendly article](https://aituts.com/stable-diffusion-seed/) on how seed's work for more info on this
{% endhint %}

To change the image, you can pass in a different seed number:

```
lilypad run sdxl:v0.9-lilypad1 '{"prompt": "an astronaut riding on a unicorn", "seed": 9}'
```

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption><p>Passing in a seed to change the image when using the same text prompt.</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption><p>The IPFS results directory</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption><p>The image labelled as image-&#x3C;seed>.png</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption><p><a href="https://ipfs.io/ipfs/QmY7k6bigPrKhcQFfakrzvqnBfob147FYFjZtvUm49Veg3/outputs/image-9.png">https://ipfs.io/ipfs/QmY7k6bigPrKhcQFfakrzvqnBfob147FYFjZtvUm49Veg3/outputs/image-9.png</a> or ipfs://bafybeierizuso2u3agwyriz54odqnnl6ai4alfmcjl2f5ug5q4apqfcwjq/outputs/image-9.png in IPFS supported brosers like Brave</p></figcaption></figure>

#### CLI Video

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
