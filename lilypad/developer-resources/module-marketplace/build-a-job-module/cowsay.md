---
description: Run a cowsay job
---

# Cowsay

`cowsay` is a simple, text-based program originally written for Unix-like operating systems that generates ASCII pictures of a cow with a speech bubble containing a specified message.&#x20;

This module was created as a "Hello World" for the Lilypad Network!

## Getting Started

Before running `cowsay`, make sure you have the [Lilypad CLI installed](../../../quickstart/cli/) on your machine and your private key environment variable is set. This is necessary for operations within the Lilypad network.

```bash
export WEB3_PRIVATE_KEY=<YOUR_PRIVATE_KEY>
```

## Run cowsay

Once you've installed the CLI, run the `cowsay` command:

```bash
lilypad run cowsay:v0.0.4 -i Message="hello, lilypad"  
```

### Output

```bash
⠀⠀⠀⠀⠀⠀⣀⣤⣤⢠⣤⣀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⢴⣿⣿⣿⣿⢸⣿⡟⠀⠀⠀⠀⠀    ██╗     ██╗██╗  ██╗   ██╗██████╗  █████╗ ██████╗
⠀⠀⣰⣿⣦⡙⢿⣿⣿⢸⡿⠀⠀⠀⠀⢀⠀    ██║     ██║██║  ╚██╗ ██╔╝██╔══██╗██╔══██╗██╔══██╗
⠀⢰⣿⣿⣿⣿⣦⡙⣿⢸⠁⢀⣠⣴⣾⣿⡆    ██║     ██║██║   ╚████╔╝ ██████╔╝███████║██║  ██║
⠀⣛⣛⣛⣛⣛⣛⣛⠈⠀⣚⣛⣛⣛⣛⣛⣛    ██║     ██║██║    ╚██╔╝  ██╔═══╝ ██╔══██║██║  ██║
⠀⢹⣿⣿⣿⣿⠟⣡⣿⢸⣮⡻⣿⣿⣿⣿⡏    ███████╗██║███████╗██║   ██║     ██║  ██║██████╔╝
⠀⠀⢻⣿⡟⣩⣾⣿⣿⢸⣿⣿⣌⠻⣿⡟⠀    ╚══════╝╚═╝╚══════╝╚═╝   ╚═╝     ╚═╝  ╚═╝╚═════╝ v2.13.0
⠀⠀⠀⠉⢾⣿⣿⣿⣿⢸⣿⣿⣿⡷⠈⠀⠀
⠀⠀⠀⠀⠀⠈⠙⠛⠛⠘⠛⠋⠁⠀ ⠀⠀⠀   Decentralized Compute Network  https://lilypad.tech

🌟  Lilypad submitting job
2025-03-05T12:56:38-06:00 WRN ../runner/work/lilypad/lilypad/cmd/lilypad/utils.go:63 > failed to get GPU info: gpuFillInfo not implemented on darwin
2025-03-05T12:56:38-06:00 INF ../runner/work/lilypad/lilypad/pkg/web3/sdk.go:209 > Connected to arbitrum-sepolia-rpc.publicnode.com
2025-03-05T12:56:38-06:00 INF ../runner/work/lilypad/lilypad/pkg/jobcreator/run.go:27 > Public Address: 0xB86bCAe21AC95BCe7a49C057dC8d911033f8CB7c
Enumerating objects: 42, done.
Counting objects: 100% (22/22), done.
Compressing objects: 100% (4/4), done.
Total 42 (delta 18), reused 19 (delta 18), pack-reused 20 (from 1)
💌  Deal agreed. Running job...
🤔  Results submitted. Awaiting verification...
🤔  Results submitted. Awaiting verification...
✅  Results accepted. Downloading result...
🆔  Data ID: QmP2SQttNC3Hrh2xpY7bNHzV2jHq7MbfLahRC46DVzn5rG

🍂 Lilypad job completed, try 👇
    open /tmp/lilypad/data/downloaded-files/QmQHrsiAuzTLn5VU6jg5LoXBRrAkEVRKiYeJE29w54gg9Q
    cat /tmp/lilypad/data/downloaded-files/QmQHrsiAuzTLn5VU6jg5LoXBRrAkEVRKiYeJE29w54gg9Q/stdout
    cat /tmp/lilypad/data/downloaded-files/QmQHrsiAuzTLn5VU6jg5LoXBRrAkEVRKiYeJE29w54gg9Q/stderr
```

To view the results in a local directory, navigate to the local folder.

```bash
open /tmp/lilypad/data/downloaded-files/QmQHrsiAuzTLn5VU6jg5LoXBRrAkEVRKiYeJE29w54gg9Q
```

Here, you can view the `stdout` and `stderr` as well as the `outputs` folder for the run:

```bash
~ % cat /tmp/lilypad/data/downloaded-files/QmQHrsiAuzTLn5VU6jg5LoXBRrAkEVRKiYeJE29w54gg9Q/stdout
 ________________ 
< hello, lilypad >
 ---------------- 
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
```
