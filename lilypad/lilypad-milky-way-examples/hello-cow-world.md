---
description: A cowsay job
---

# Hello, (cow) World!

## \[CLI] Run Hello, 🐮 World! Job with Cowsay <a href="#user-content-run-hello-world-job" id="user-content-run-hello-world-job"></a>

`cowsay` is a simple, text-based program originally written for Unix-like operating systems that generates ASCII pictures of a cow with a speech bubble containing a specified message.

### Prerequisites

Before running `cowsay`, make sure you have the [Lilypad CLI installed](https://docs.lilypad.tech/lilypad/lilypad-milky-way-testnet/install-run-requirements) on your machine and your private key environment variable is set. This is necessary for operations within the Lilypad network.

```bash
export WEB3_PRIVATE_KEY=<YOUR_PRIVATE_KEY>
```

### Usage

Next, run the `cowsay` command:

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

### View Results <a href="#user-content-see-the-results" id="user-content-see-the-results"></a>

#### IPFS

To view the results on IPFS, navigate to the IPFS CID Navigate to the IPFS CID result output in the Results -> [https://ipfs.io/ipfs/QmNjJUyFZpSg7HC9akujZ6KHWvJbCEytre3NRSMHzCA6NR](https://ipfs.io/ipfs/QmNjJUyFZpSg7HC9akujZ6KHWvJbCEytre3NRSMHzCA6NR)

{% hint style="info" %}
This could take up to a minute to propagate through the IPFS network. Please be patient
{% endhint %}

#### Local

To view the results in a local directory, navigate to the local folder.

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

