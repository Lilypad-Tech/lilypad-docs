---
description: Getting started with `create-lilypad-module`
---

# Getting Started

## Installation

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
