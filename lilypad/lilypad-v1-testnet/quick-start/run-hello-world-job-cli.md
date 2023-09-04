---
description: A cowsay job
cover: ../../.gitbook/assets/Screenshot 2023-09-02 at 11.23.19 am.png
coverY: 0
---

# \[CLI] Run "Hello, World!" Job

The following is how to run the "Hello, :cow:World!" Job from the Lilypad CLI.

{% hint style="info" %}
To Run from a smart contract skip to the section [run-hello-world-from-a-smart-contract.md](run-hello-world-from-a-smart-contract.md "mention")
{% endhint %}

## Run Hello, :cow: World! Job

* Start Docker
* Open a Terminal window and run the following command:

```bash
lilypad run cowsay:v0.0.1 "hello lilypad"
```

(ensure your user is in the docker group if necessary on your platform)

Results:

<figure><img src="../../.gitbook/assets/image (16) (1).png" alt=""><figcaption></figcaption></figure>

## See the Results

Navigate to the IPFS CID result output in the Results -> [https://ipfs.io/ipfs/QmNjJUyFZpSg7HC9akujZ6KHWvJbCEytre3NRSMHzCA6NR](https://ipfs.io/ipfs/QmNjJUyFZpSg7HC9akujZ6KHWvJbCEytre3NRSMHzCA6NR)

{% hint style="info" %}
Patience! This could take up to a minute to propagate through the IPFS network.
{% endhint %}

<div data-full-width="true">

<figure><img src="../../.gitbook/assets/image (11) (1) (1).png" alt=""><figcaption><p>Output of Lilypad Job</p></figcaption></figure>

</div>

Then click on the stdout folder and you should see the job result!

<div data-full-width="false">

<figure><img src="../../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption><p>This is udderly fantastic!</p></figcaption></figure>

</div>
