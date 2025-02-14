---
description: Use `create-lilypad-module` to create Lilypad modules
---

# \`create-lilypad-module\`

## Getting Started

A Lilypad module is a Git repository that allows you to perform various tasks using predefined templates and inputs. This guide will walk you through creating a Lilypad module using our [`create-lilypad-module` package](https://pypi.org/project/create-lilypad-module/). You'll need to have the [Lilypad CLI](https://docs.lilypad.tech/lilypad/lilypad-testnet/install-run-requirements), [Python](https://www.python.org/), [pip](https://pip.pypa.io/en/stable/), and [Docker](https://www.docker.com/) on your machine, as well as [GitHub](https://github.com/) and [Docker Hub](https://hub.docker.com/) accounts.

{% hint style="info" %}
If you're new to Docker, consider exploring this [step-by-step tutorial](https://docs.docker.com/get-started/) on creating, building, and running a Docker image for a simple Hello World style application.
{% endhint %}

### Installation

First, you'll need to install the package:

```sh
pip install create-lilypad-module
```

If you've previously installed `create-lilypad-module`, you should to ensure that you're using the latest version:

```sh
pip install --upgrade create-lilypad-module
```

Now run `create-lilypad-module`:

```sh
create-lilypad-module
```

The CLI will ask for the name of your project. Alternatively, you can run:

```sh
create-lilypad-module project_name
cd project_name
```

Output

```
project_name
├── config
│   └── constants.py
├── scripts
│   ├── docker_build.py
│   ├── download_models.py
│   └── run_module.py
├── src
│   └── run_inference.py
├── .dockerignore
├── .env
├── .gitignore
├── Dockerfile
├── lilypad_module.json.tmpl
├── README.md
└── requirements.txt
```
