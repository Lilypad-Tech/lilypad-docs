---
description: A cowsay job
---

# Hello, (cow) World!

### Run Hello, 🐮 World! Job \[CLI] <a href="#user-content-run-hello-world-job" id="user-content-run-hello-world-job"></a>

{% hint style="info" %}
Ensure you have installed all requirements

[install-run-requirements.md](../lilypad-milky-way-testnet/quick-start/install-run-requirements.md "mention")
{% endhint %}

1. Make sure to have the following `env` in your shell session.

```bash
export WEB3_PRIVATE_KEY=YOUR_PRIVATE_KEY
```

2. Run `lilypad`

```bash
lilypad run cowsay:v0.0.3 -i Message="hello, lilypad"  
```

**Output:**

```bash
Lilypad: v2.0.0-d58a991

⠀⠀⠀⠀⠀⠀⣀⣤⣤⢠⣤⣀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⢴⣿⣿⣿⣿⢸⣿⡟⠀⠀⠀⠀⠀    ██╗     ██╗██╗  ██╗   ██╗██████╗  █████╗ ██████╗ 
⠀⠀⣰⣿⣦⡙⢿⣿⣿⢸⡿⠀⠀⠀⠀⢀⠀    ██║     ██║██║  ╚██╗ ██╔╝██╔══██╗██╔══██╗██╔══██╗
⠀⢰⣿⣿⣿⣿⣦⡙⣿⢸⠁⢀⣠⣴⣾⣿⡆    ██║     ██║██║   ╚████╔╝ ██████╔╝███████║██║  ██║
⠀⣛⣛⣛⣛⣛⣛⣛⠈⠀⣚⣛⣛⣛⣛⣛⣛    ██║     ██║██║    ╚██╔╝  ██╔═══╝ ██╔══██║██║  ██║
⠀⢹⣿⣿⣿⣿⠟⣡⣿⢸⣮⡻⣿⣿⣿⣿⡏    ███████╗██║███████╗██║   ██║     ██║  ██║██████╔╝
⠀⠀⢻⣿⡟⣩⣾⣿⣿⢸⣿⣿⣌⠻⣿⡟⠀    ╚══════╝╚═╝╚══════╝╚═╝   ╚═╝     ╚═╝  ╚═╝╚═════╝ v2
⠀⠀⠀⠉⢾⣿⣿⣿⣿⢸⣿⣿⣿⡷⠈⠀⠀                                                  
⠀⠀⠀⠀⠀⠈⠙⠛⠛⠘⠛⠋⠁⠀ ⠀⠀⠀   Decentralized Compute Network  https://lilypad.tech

🌟  Lilypad submitting job
2023-12-02T07:01:42+05:30 INF Decenter/lilypad/pkg/module/utils.go:149 > updating cached git repo=/tmp/lilypad/data/repos/bacalhau-project/lilypad-module-cowsay
🤔  Results submitted. Awaiting verification...
🤝  Job submitted. Negotiating deal...
💌  Deal agreed. Running job...
✅  Results accepted. Downloading result...
🤔  Results submitted. Awaiting verification...
✅  Results accepted. Downloading result...

🍂 Lilypad job completed, try 👇
    open /tmp/lilypad/data/downloaded-files/QmYiX2GkDDkqXGsnBaEUuGuNc93ZWoBWPNbNSz2AnFQcMk
    cat /tmp/lilypad/data/downloaded-files/QmYiX2GkDDkqXGsnBaEUuGuNc93ZWoBWPNbNSz2AnFQcMk/stdout
    cat /tmp/lilypad/data/downloaded-files/QmYiX2GkDDkqXGsnBaEUuGuNc93ZWoBWPNbNSz2AnFQcMk/stderr
    https://ipfs.io/ipfs/QmNjJUyFZpSg7HC9akujZ6KHWvJbCEytre3NRSMHzCA6NR
```

#### See the Results <a href="#user-content-see-the-results" id="user-content-see-the-results"></a>

1. View the results by navigating to the IPFS CID Navigate to the IPFS CID result output in the Results -> [https://ipfs.io/ipfs/QmNjJUyFZpSg7HC9akujZ6KHWvJbCEytre3NRSMHzCA6NR](https://ipfs.io/ipfs/QmNjJUyFZpSg7HC9akujZ6KHWvJbCEytre3NRSMHzCA6NR)

{% hint style="info" %}
This could take up to a minute to propagate through the IPFS network. Please be patient
{% endhint %}

2. View the results by navigating to the local folder:

<pre class="language-bash"><code class="lang-bash"><strong>open /tmp/lilypad/data/downloaded-files/Qmay5vZ7u5jvn2VkAGMLkkYXGQQd5GFZFuHkbDEFYb5VeF
</strong></code></pre>

Here, you can view the `stdout` and `stderr` as well as the `outputs` folder for the run:

<pre class="language-bash"><code class="lang-bash"><strong>% cat /tmp/lilypad/data/downloaded-files/QmYiX2GkDDkqXGsnBaEUuGuNc93ZWoBWPNbNSz2AnFQcMk/stdout
</strong>
 _______________
&#x3C; hello lilypad >
 ---------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
</code></pre>
