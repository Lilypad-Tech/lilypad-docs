---
description: Run a Stable Diffusion Text to Image Job
---

# Stable Diffusion (SDXL0.9)

## Overview

Generically, stable diffusion is what happens when you put a couple of drops of dye into a bucket of water. Given time, the dye randomly disperses and eventually settles into a uniform distribution which colours all the water evenly

In computer science, you define rules for your (dye) particles to follow and the medium this takes place in.

Stable Diffusion is a machine learning model used for text-to-image processing (like Dall-E) and based on a diffusion probabilistic model that uses a transformer to generate images from text. \
\
There are several open-source stable diffusion models out there (made famous by Stability.ai) and they continue to improve and become even more fully featured - SDXL0.9 is one of the more recently open-sourced models.

<figure><img src="https://lh5.googleusercontent.com/eib-z-1r9iZyxuArY_2z-NhPv4OPyFACpFF6-_nWfGaoDlY958NbP5fRcpUNtzuedWM_HmryF7aJplAtiQm3ezeV_cUUQ69sV1MYyvckptTBmIEawnSZivnEb8B8ifITYwgH_k3EISLjSWy0JbM9y2JfTg=s2048" alt=""><figcaption></figcaption></figure>

## \[CLI] Running Stable Diffusion SDXL 0.9

{% hint style="danger" %}
Ensure you have installed all requirements [install-run-requirements.md](../lilypad-v1-testnet/quick-start/install-run-requirements.md "mention")
{% endhint %}

To run stable diffusion use the sdxl module like so:

```
lilypad run sdxl:v0.9-lilypad1 "an astronaut riding on a unicorn"
```

The output will look like this:&#x20;

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1).png" alt=""><figcaption><p>SDXL Output</p></figcaption></figure>

Take the ipfs link given in the results and paste it into your browser:

{% hint style="warning" %}
Please be patient! IPFS can take some time to propagate and doesn't always work immediately.&#x20;
{% endhint %}

<figure><img src="../.gitbook/assets/image (2) (1).png" alt=""><figcaption><p>Results of SDXL job on IPFS Directory (<a href="https://ipfs.io/ipfs/QmSXkyM9bkKPCWaDSvViS14nvbNekGQTJTTeNv7JitSeWZ">https://ipfs.io/ipfs/QmSXkyM9bkKPCWaDSvViS14nvbNekGQTJTTeNv7JitSeWZ</a>)</p></figcaption></figure>

In the **/outputs** folder, you'll find the image:

<figure><img src="../.gitbook/assets/image (3) (1).png" alt=""><figcaption><p>The Image in the outputs folder</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (5) (1).png" alt=""><figcaption><p><a href="https://ipfs.io/ipfs/QmSXkyM9bkKPCWaDSvViS14nvbNekGQTJTTeNv7JitSeWZ">https://ipfs.io/ipfs/QmSXkyM9bkKPCWaDSvViS14nvbNekGQTJTTeNv7JitSeWZ</a><a href="stable-diffusion.md#running-stable-diffusion-from-the-cli">/outputs/image-0.png</a> or <a href="ipfs://bafybeib6i434yl6ql46jyyydz2boqulysmksye3f5khs24c6uoqpnxkp3y/outputs/image-0.png">ipfs://bafybeib6i434yl6ql46jyyydz2boqulysmksye3f5khs24c6uoqpnxkp3y/outputs/image-0.png</a> in IPFS supported browsers like Brave</p></figcaption></figure>

Since modules are deterministic, running this command with the same text prompt will produce the same image, since the same seed is also used (the default seed is 0).

{% hint style="info" %}
See this [beginner-friendly article](https://aituts.com/stable-diffusion-seed/) on how seed's work for more info on this
{% endhint %}

To change the image, you can pass in a different seed number:

```
lilypad run sdxl:v0.9-lilypad1 '{"prompt": "an astronaut riding on a unicorn", "seed": 9}'
```

<figure><img src="../.gitbook/assets/image (6) (1).png" alt=""><figcaption><p>Passing in a seed to change the image when using the same text prompt.</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption><p>The IPFS results directory</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption><p>The image labelled as image-&#x3C;seed>.png</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption><p><a href="https://ipfs.io/ipfs/QmY7k6bigPrKhcQFfakrzvqnBfob147FYFjZtvUm49Veg3/outputs/image-9.png">https://ipfs.io/ipfs/QmY7k6bigPrKhcQFfakrzvqnBfob147FYFjZtvUm49Veg3/outputs/image-9.png</a> or ipfs://bafybeierizuso2u3agwyriz54odqnnl6ai4alfmcjl2f5ug5q4apqfcwjq/outputs/image-9.png in IPFS supported brosers like Brave</p></figcaption></figure>

#### CLI Video

{% embed url="https://youtu.be/-ae3M4VtL88" %}
Lilypad \[CLI] Stable Diffusion with SDLX 0.9 Demo
{% endembed %}

## \[Smart Contract] Running Stable Diffusion SDXL 0.9

{% hint style="warning" %}
Make sure you have connected to the Lalechuza testnet and funded your wallet with testnet lilETH. See [funding-your-wallet-from-faucet.md](../lilypad-v1-testnet/quick-start/funding-your-wallet-from-faucet.md "mention") & [setting-up-metamask.md](../lilypad-v1-testnet/quick-start/setting-up-metamask.md "mention")
{% endhint %}

\
To trigger the SDXL0.9 module from a smart contract, firstly you need to create your own client contract to call the module from.\
\
In order to receive results back from the Lilypad network, you will also need to \
1\. Connect to the [Lilypad Modicum Contract](https://github.com/bacalhau-project/lilypad-modicum/blob/main/src/js/contracts/Modicum.sol) (and create an instance of it in your own contract using the [current address found here](https://github.com/bacalhau-project/lilypad-modicum/blob/main/latest.txt))\
2\. Implement the [Modicum Contract receiveJobResults()](https://github.com/bacalhau-project/lilypad-modicum/blob/main/src/js/contracts/Modicum.sol) interface.

```solidity
// SPDX-License-Identifier: GPLv3
pragma solidity ^0.8.6;

// give it the ModicumContract interface 
// NB: this will be a separate import in future.
interface ModicumContract {
  function runModuleWithDefaultMediators(string calldata name, string calldata params) external payable returns (uint256);
}

contract SDXLCaller {
  address public contractAddress;
  ModicumContract remoteContractInstance;
  
  // See the latest result.
  uint256 public resultJobId;
  string public resultCID;

  // The Modicum contract address is found here: https://github.com/bacalhau-project/lilypad-modicum/blob/main/latest.txt
  // Current: 0x422F325AA109A3038BDCb7B03Dd0331A4aC2cD1a
  constructor(address _modicumContract) {
    require(_modicumContract != address(0), "Contract cannot be zero address");
    contractAddress = _modicumContract;
    //make a connection instance to the remote contract
    remoteContractInstance = ModicumContract(_modicumContract);
  } 

  /*
  * @notice Run the SDXL Module
  * @param prompt The input text prompt to generate the stable diffusion image from
  */
  function runSDXL(string memory prompt) public payable returns (uint256) {
    require(msg.value == 2 ether, "Payment of 2 Ether is required"); //all jobs are currently 2 lilETH
    return remoteContractInstance.runModuleWithDefaultMediators{value: msg.value}("sdxl:v0.9-lilypad1", prompt);
  }
  
  // This must be implemented in order to receive the job results back!
  function receiveJobResults(uint256 _jobID, string calldata _cid) public {
    resultJobId =_jobID;
    resultCID = _cid;
  }

}
```

NB: You could also add the seed as a parameter to run this. &#x20;

`return remoteContractInstance.runModuleWithDefaultMediators{value: msg.value}("sdxl:v0.9-lilypad1",`` `**`params`**`);`

#### **Remix**

Try it yourself!&#x20;

{% hint style="info" %}
Click [this link](https://remix.ethereum.org/bacalhau-project/lilypad-modicum/blob/main/src/js/contracts/SDXLCaller.sol) to open [the contract](https://github.com/bacalhau-project/lilypad-modicum/blob/main/src/js/contracts/SDXLCaller.sol) in Remix IDE!
{% endhint %}

1. Ensure your metamask wallet is set to the [Lalechuza testnet ](../lilypad-v1-testnet/quick-start/setting-up-metamask.md)and has [lilETH testnet funds](../lilypad-v1-testnet/quick-start/funding-your-wallet-from-faucet.md) from the [faucet](https://testnet.lilypadnetwork.org).&#x20;
2. Set the remix environment to "Injected Provider - Metamask" (& ensure metamask has the lalechuza chain selected)
3. Then \
   \-  Deploy a new contract passing in the [Modicum Contract address found here](https://github.com/bacalhau-project/lilypad-modicum/blob/main/latest.txt) **OR**\
   \-  Open the contract at this example address: `0x31e7bF121EaB1C0B081347D8889863362e9ad53A`

<figure><img src="../.gitbook/assets/image (22).png" alt=""><figcaption><p>At Address: 0x31e7bF121EaB1C0B081347D8889863362e9ad53A</p></figcaption></figure>

4. Call the runSDXL Module, passing in a prompt and sending 2 lilETH in the value field. Your Metamask wallet should pop up for you to confirm the payment and transaction.

<figure><img src="../.gitbook/assets/image (24).png" alt=""><figcaption><p>runSDXL passing in the text prompt string &#x26; ensuring you set 2 ETH to the Value field</p></figcaption></figure>

5. Give it some time and check the resultCID variable. You can then open this result in your browser with \
   https://ipfs.io/ipfs/\<resultCID> **or** ipfs://\<resultCID> in IPFS compatible browsers like Brave.

<figure><img src="../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (26).png" alt=""><figcaption><p><a href="https://ipfs.io/ipfs/QmQx6RDxxjqJYeame9SryMvkjxbXRm32hb3zo3RmiTno4R/outputs/image-0.png">https://ipfs.io/ipfs/QmQx6RDxxjqJYeame9SryMvkjxbXRm32hb3zo3RmiTno4R/outputs/image-0.png</a>  OR <a href="ipfs://bafybeibgzpcxn2cfwvz7ao3jztqphd2k2ebccmxpfm4ig3ug5r2lsclrqy/outputs/image-0.png">ipfs://bafybeibgzpcxn2cfwvz7ao3jztqphd2k2ebccmxpfm4ig3ug5r2lsclrqy/outputs/image-0.png</a> in Brave</p></figcaption></figure>

#### **Video**

{% embed url="https://youtu.be/aK12PRx8V0k" %}

{% hint style="info" %}
FYI! You can try all examples in one contract. See [run-hello-world-from-a-smart-contract.md](../lilypad-v1-testnet/quick-start/run-hello-world-from-a-smart-contract.md "mention")
{% endhint %}



## SDXL Module Code

Find the [SDXL module code here](https://github.com/bacalhau-project/lilypad-modicum/blob/main/src/python/modules/sdxl.py). There's also a generic [Stable Diffusion module here](https://github.com/bacalhau-project/lilypad-modicum/blob/main/src/python/modules/stable\_diffusion.py).

{% @github-files/github-code-block url="https://github.com/bacalhau-project/lilypad-modicum/blob/main/src/python/modules/sdxl.py" %}

