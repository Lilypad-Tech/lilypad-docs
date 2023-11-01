---
description: Lilypad setup
---

# \[CLI] Install Run Requirements

## Install Requirements

{% hint style="info" %}
**Supported platforms**: only supports x86_64 Linux
{% endhint %}

## Install CLI

### 1. With GO toolchain
```bash
go install github.com/bacalhau-project/lilypad@latest
```

You may then need to set:
```bash
export SERVICE_SOLVER="0x3C44CdDdB6a900fa2b585dd299e03d12FA4293BC"
export SERVICE_MEDIATORS="0x90F79bf6EB2c4f870365E785982E1f101E93b906"
export WEB3_PRIVATE_KEY=<your private key>
```

### 2. Via officially released binaries
```bash
curl -sSL -o lilypad https://github.com/bacalhau-project/lilypad/releases/download/v2.0.0-6afc1cc/lilypad
chmod +x lilypad
sudo mv lilypad /usr/local/bin
```

You may then need to set:
```bash
export SERVICE_SOLVER="0x3C44CdDdB6a900fa2b585dd299e03d12FA4293BC"
export SERVICE_MEDIATORS="0x90F79bf6EB2c4f870365E785982E1f101E93b906"
export WEB3_PRIVATE_KEY=<your private key>
```

Verifying if the install is successful. Execute `lilypad` on your terminal an it should prodcce the following response.

```bash
Lilypad

Usage:
  lilypad [command]

Available Commands:
  completion        Generate the autocompletion script for the specified shell
  help              Help about any command
  mediator          Start the lilypad mediator service.
  resource-provider Start the lilypad resource-provider service.
  run               Run a job on the Lilypad network.
  solver            Start the lilypad solver service.

Flags:
  -h, --help   help for lilypad

Use "lilypad [command] --help" for more information about a command.
```