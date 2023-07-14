---
description: How to run a Lilypad Job from a Smart contract!
---

# Run "Hello, World" from a Smart Contract \[WIP]

{% hint style="warning" %}
:construction: This page is still under construction! Check back soon! :construction:
{% endhint %}

Calling Lilypad Jobs from Smart Contracts takes a similar approach to that outlined in Lilypad v0[#quick-start-guide](../../lilypad-v0-reference/lilypad-v0-quick-start.md#quick-start-guide "mention").



The function call needed to run a job from a smart contract can be found below:

{% @github-files/github-code-block url="https://github.com/bacalhau-project/lilypad/blob/client-smart-contract/src/js/contracts/NaiveExamplesClient.sol" %}

In the above script the function to receive the Job results back is `receiveJobResult`() - so it's essential to put this function in your own smart contract.\
\
\
Here's an example of a working script that can trigger the above function calls&#x20;

{% @github-files/github-code-block url="https://github.com/bacalhau-project/lilypad/blob/main/src/js/scripts/smoke-test.js" %}

\


