---
description: Running the most important Hello World on lilypad
---

# \[CLI] Run "Hello, World!" Job

> **Note**: Make sure to you have Lilypad CLI installed.

> **Note**: Make sure you have `SERVICE_SOLVER`, `SERVICE_MEDIATORS` and `WEB3_PRIVATE_KEY` env variables in your environment

```bash
export SERVICE_SOLVER="0x3C44CdDdB6a900fa2b585dd299e03d12FA4293BC"
export SERVICE_MEDIATORS="0x90F79bf6EB2c4f870365E785982E1f101E93b906"
export WEB3_PRIVATE_KEY=<your private key>
```

### Run Cowsay

```bash
lilypad run cowsay:v0.0.1 -i Message="moo"
```