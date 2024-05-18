---
description: Javascript / Nodejs CLI Wrapper API
---

# Javascript CLI Wrapper

This API allows you to run AI/ML inference on the Lilypad Network with a post request.

```bash
 POST http://js-cli-wrapper.lilypad.tech
```

Request Headers

```bash
Content-Type: "application/json"
```

Request Body:

<pre class="language-bash"><code class="lang-bash">{
"private-key": "string",
"module name": "Lilypad Module",
<strong>"payload (key=value)": "prompt"
</strong><strong>}
</strong></code></pre>

Request Body Parameters

`private-key`: your web3 private key

`module name`: The Lilypad module that you would like to run

`payload`: Prompt



Check out [running-lilypad-in-a-front-end.md](running-lilypad-in-a-front-end.md "mention") for examples running Lilypad locally!
