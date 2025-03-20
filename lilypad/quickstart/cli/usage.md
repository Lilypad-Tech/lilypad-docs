---
description: Running the most important Hello World on Lilypad!
---

# Usage

Before you run a Lilypad job, make sure you have [Lilypad CLI installed](broken-reference) and have set [a `WEB3_PRIVATE_KEY` env variable](broken-reference) in your environment.

{% hint style="info" %}
Your `WEB3_PRIVATE_KEY` can be retrieved from the MetaMask account details menu.  For more info, check out the [official guide from MetaMask](https://support.metamask.io/managing-my-wallet/secret-recovery-phrase-and-private-keys/how-to-export-an-accounts-private-key/) on how to get a your private key. **Be sure to keep your private key safe** and never share it or store it in unsecured places to prevent unauthorized access to your funds.
{% endhint %}

## Run Cowsay

Run the command:

```bash
lilypad run cowsay:v0.0.4 -i Message="moo"
```

Wait for the compute to take place and for the results to be published:

```
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

View your results:&#x20;

```bash
cat /tmp/lilypad/data/downloaded-files/QmQHrsiAuzTLn5VU6jg5LoXBRrAkEVRKiYeJE29w54gg9Q/stdout
```

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

