---
description: Javascript / Nodejs CLI Wrapper API
---

# Javascript CLI Wrapper

This API allows you to run AI/ML inference on the Lilypad Network with a post request.

```bash
 POST http://js-cli-wrapper.lilypad.tech
```

#### Request Headers

```bash
Content-Type: "application/json"
Accept: "application/json"
```

#### Request Body Parameters

* `pk`: your web3 private key
* `module`: The Lilypad module that you would like to run
* `inputs`: Prompt (key=value)

#### Example Request Body

<pre class="language-json"><code class="lang-json">{
    "pk": "&#x3C;PRIVATE_KEY>",
    "module": "cowsay:v0.0.3",
<strong>    "inputs (key=value)": "Message='moo'"
</strong><strong>}
</strong></code></pre>



Check out [running-lilypad-in-a-front-end.md](running-lilypad-in-a-front-end.md "mention") for examples running Lilypad locally!
