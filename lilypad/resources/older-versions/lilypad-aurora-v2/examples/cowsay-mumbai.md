---
description: A cowsay job on Mumbai
---

# Hello, (cow) World! on Mumbai

## Getting LilyPad Tokens

To acquire LilyPad tokens, follow these steps:

1. Visit the Lilypad Faucet at [here](http://mumbai-faucet.lilypad.tech:8081/)
2. Enter your wallet address.
3. Receive some LP tokens.

## Setting up Environment Variables

Set the environment variables as shown below:

```bash
export WEB3_CHAIN_ID=80001
export WEB3_RPC_URL=https://polygon-mumbai.infura.io/v3/[YOUR_INFURA_API_KEY]
export WEB3_CONTROLLER_ADDRESS=0xB08492E6Ae019609E6bF3a19873d00D2257f614b
export WEB3_TOKEN_ADDRESS=0xBe72246911F254E3D221C965A50d89C6D660DCc0
export WEB3_MEDIATION_ADDRESS=0x16f1Bb6784D3Fbb735423A3603BA44427c4aDe4F
export WEB3_JOBCREATOR_ADDRESS=0xD5723D6758E93d2E612210127f6Ab9705E606Ac8
export WEB3_PAYMENTS_ADDRESS=0x01B18F94B61253ba63b810ddA371eA54bbACbdC6
export WEB3_STORAGE_ADDRESS=0xC5a58D6BDbdB66c50ecD795C5456E1f6ADc52dD9
export WEB3_USERS_ADDRESS=0x11F3f6e51B822c4f0FF8955510f81B6654a9BD0C
export SERVICE_SOLVER="0x08D118d3300c82CD94a4080805426AB025fe9852"
export SERVICE_MEDIATORS="0xd6244f8c08d4b7bb7ccbd72e585b19ee68a8d1eb"
```

> Note: You will need to set up your own Infura account and get your infura Api Key. You can follow the instructions [here](https://docs.infura.io/getting-started)

## Running cowsay

> Note: Ensure that you have Lilypad installed before proceeding.

To execute cowsay, use the following command:

```bash
lilypad run cowsay:v0.0.1 -i Message="<hello lilypad>"
```

**Output:**

<figure><img src="../../../../.gitbook/assets/cowsay_execution.png" alt=""><figcaption><p>Probably nothing...</p></figcaption></figure>

## See the Results <a href="#see-the-results" id="see-the-results"></a>

1. see the results by navigating to the IPFS CID Navigate to the IPFS CID result output in the Results -> [https://ipfs.io/ipfs/QmNjJUyFZpSg7HC9akujZ6KHWvJbCEytre3NRSMHzCA6NR](https://ipfs.io/ipfs/QmNjJUyFZpSg7HC9akujZ6KHWvJbCEytre3NRSMHzCA6NR)

{% hint style="info" %}
This could take up to a minute to propagate through the IPFS network. Please be patient
{% endhint %}

2. by navigting to the local folder

```bash
open /tmp/lilypad/data/downloaded-files/Qmay5vZ7u5jvn2VkAGMLkkYXGQQd5GFZFuHkbDEFYb5VeF
```

Here, you can view the `stdout` and `stderr` as well as the `outputs` folder for the run

<figure><img src="../../../../.gitbook/assets/cowsay_results.png" alt=""><figcaption><p>The Results....</p></figcaption></figure>
