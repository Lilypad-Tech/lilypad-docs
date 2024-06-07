---
description: Javascript / Nodejs CLI Wrapper API
---

# Javascript CLI Wrapper

## Overview

This API allows you to run AI/ML inference on the Lilypad Network with a POST request.

{% hint style="info" %}
This API is newly developed and we are actively working on improvements and appreciate your understanding as we refine its functionality!\
\
Please report any issues to the [GitHub](https://github.com/Lilypad-Tech/js-cli-wrapper/issues) or [Lilypad Discord server](https://lilypad.team/discord)!
{% endhint %}

## **Usage**

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
* `inputs`: The input parameters for the module in the format `key=value`. These inputs and tunables will vary depending on the module you choose. Each input should be preceded by the `-i` flag.
* `opts?`: Additional options for customizing the module execution such as:
  * `stream`: Boolean value to specify if the output should be streamed (`true`) or not (`false`).

### Example Request

Here's an example of what your request may look like from a client:

```javascript
const url = 'http://js-cli-wrapper.lilypad.tech';
const pk = 'your_private_key';
const module = 'ollama-pipeline:llama3-8b-lilypad2';
const inputs = 'your_input_data';

const body = {
  pk: pk,
  module: module,
  inputs: `-i Prompt='${inputs}'`,
  opts: { stream: true }
};

try {
  const response = await axios.post(url, body, {
    headers: {
      'Content-Type': 'application/json',
      'Accept': 'application/json'
    }
  });
  console.log('Response data:', response.data);
} catch (error) {
  console.error('Error during POST request:', error);
}
```

In this example:

* `pk` is your unique Web3 private key
* `module` specifies the module to run, in this case, the Llama3 model on the Lilypad Ollama Pipeline (`ollama-pipeline:llama3-8b-lilypad2`)
* The `inputs` field includes the input parameters for the module. The `-i` flag represents a new input or tunable. In this context, it sends a prompt to the Llama3 job. This field is also where you would specify tunables, such as the number of steps in a job.
* `opts` includes the "stream" parameter
