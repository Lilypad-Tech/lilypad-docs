---
description: How to run a cowsay job from a Smart contract!
---

# \[Smart Contract] Run "Hello, World!" Job

## Remix

**Open the Contract**

{% hint style="info" %}
Click [this link](https://remix.ethereum.org/bacalhau-project/lilypad-modicum/blob/main/src/js/contracts/ExampleClient.sol) to open the ExampleClient.sol contract in remix
{% endhint %}

Alternatively, open [the Remix IDE](https://remix.ethereum.org) in your browser and copy in the below ExampleClient.sol [contract](https://github.com/bacalhau-project/lilypad-modicum/blob/main/src/js/contracts/ExampleClient.sol):

{% @github-files/github-code-block url="https://github.com/bacalhau-project/lilypad-modicum/blob/main/src/js/contracts/ExampleClient.sol" %}

**Connect to the Testnet**

1. Connect MetaMask to the Lalechuza testnet & ensure you have testnet lilETH funds.
2. In the deploy tab in remix \[fourth tab in the side bar], ensure you set the environment to "Injected Provider - MetaMask"

<figure><img src="../../../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Connect to the Lilypad Lalechuza network in MetaMask</p></figcaption></figure>

<figure><img src="../../../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Change Remix Environment to Injected Provider - MetaMask</p></figcaption></figure>

\
**Deploy the Contact**\
In remix, compile the ExampleClient.sol contract \[third tab in the side bar]

<figure><img src="../../../../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Compile ExampleClient.sol</p></figcaption></figure>

Deploy a new contract by pasting in the Modicum contract address ([found here](https://github.com/bacalhau-project/lilypad-modicum/blob/main/latest.txt)) to the constructor

<figure><img src="../../../../../.gitbook/assets/image (3) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Deploy a new contract passing in the Modicum contract address to the constructor</p></figcaption></figure>

Deploy an existing ExampleClient.sol contract by using the "At Address" with the following pre-deployed contract address: `0x035C7593D3355b9bE0459dF2296053f887d051f1`

<figure><img src="../../../../../.gitbook/assets/image (7) (1) (1) (1).png" alt=""><figcaption><p>Run the previously deployed ExampleClient.sol contract</p></figcaption></figure>

**Call the runCowsay function**

The moment of truth! Let's run the cowsay example!!

:warning::exclamation:First, ensure you set remix to pay 2 lilETH to the function by setting the "value" field

<figure><img src="../../../../../.gitbook/assets/image (11) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Then add the string parameter for what you want the cow to say and click the transact button! Your MetaMask wallet should pop up asking you to confirm the transaction.

<figure><img src="../../../../../.gitbook/assets/image (12) (1) (1).png" alt=""><figcaption></figcaption></figure>

Wait a couple of minutes for the job to complete on the compute network. Then you will be able to click the fetchAllResults button to get your IPFS CID result.

<figure><img src="../../../../../.gitbook/assets/image (13) (1) (1).png" alt=""><figcaption></figcaption></figure>

**See the Results** :cow2:

Open the string starting with "https://ipfs.io/" in your browser which contains the output of the compute job:

<figure><img src="../../../../../.gitbook/assets/image (14) (1) (1).png" alt=""><figcaption></figcaption></figure>

The cowsay result is found under "stdout"

<figure><img src="../../../../../.gitbook/assets/image (15) (1) (1).png" alt=""><figcaption></figcaption></figure>

**Congrats!**

<figure><img src="../../../../../.gitbook/assets/image (11) (1) (1).png" alt=""><figcaption></figcaption></figure>
