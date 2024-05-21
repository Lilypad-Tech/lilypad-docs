---
description: Javascript / Nodejs CLI Wrapper API
---

# Javascript CLI Wrapper

## Overview

This API allows you to run AI/ML inference on the Lilypad Network with a POST request.

## **Usage**

### **Endpoint**

To initiate an inference task, send a POST request to the following endpoint:

```bash
 POST http://js-cli-wrapper.lilypad.tech
```

### Request Headers

Include the following headers in your request:

* `Content-Type`: `"application/json"`
* `Accept`: `"application/json"`

### Request Body Parameters

The request body should be a JSON object containing the following parameters:

* `pk`: Your Web3 private key. This key is used to authenticate your request and should be kept secure.
* `module`: The specific Lilypad module you want to run. Modules are pre-configured AI/ML models available on the Lilypad Network.
* `inputs`: The input parameters for the module in the format `key=value`. These inputs will vary depending on the module you choose.
* `opts?`: Additional options for customizing the module execution such as:
  * `stream`: Boolean value to specify if the output should be streamed (`true`) or not (`false`).

### Example Request Body

Here's an example of what your request body might look like:

<pre class="language-json"><code class="lang-json">{
    "pk": "&#x3C;PRIVATE_KEY>",
    "module": "cowsay:v0.0.3",
<strong>    "inputs": "Message='moo'",
</strong><strong>    "opts": { "stream": true }
</strong><strong>}
</strong></code></pre>

In this example:

* `pk` is your unique Web3 private key.
* `module` specifies the module to run, in this case, the "cowsay" module version 0.0.3.
* `inputs` includes the input parameters for the module. Here, it sends a message saying "moo".
* `opts` includes the "stream" parameter

## Resources

Check out [running-lilypad-in-a-front-end.md](running-lilypad-in-a-front-end.md "mention") for examples running Lilypad locally!
