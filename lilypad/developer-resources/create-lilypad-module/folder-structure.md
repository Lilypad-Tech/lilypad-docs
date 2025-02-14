---
description: The folder structure output from using `create-lilypad-module`
---

# Folder Structure

## Output

After creation, your project should look like this:

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

For the module to run, **these files must exist with exact filenames**:

* `src/run_inference.py` is the `Dockerfile` `ENTRYPOINT`.
  * If you change this files name or location, you must also update the `ENTRYPOINT` in your `Dockerfile` and `lilypad_module.json.tmpl` file to match.
* `config/constants.py` is the configuration file that stores the `DOCKER_REPO`, `DOCKER_TAG`, `MODULE_REPO`, and `TARGET_COMMIT`.
  * If you change this files name or location, you must also update the `import` statements in `scripts/docker_build.py` and `scripts/run_module.py`.
* `Dockerfile` is required to build your module into a Docker image, and push the image to Docker Hub where it can be accessed by Lilypad Network.
* `requirements.txt` is used by the `Dockerfile` to install dependencies required by your module.
  * Technically, this file can be deleted or renamed, but this naming convention is highly recommended as an industry standard best practice.
* `lilypad_module.json.tmpl` is the Lilypad configuration file.

You can delete or rename the other files.

You may create subdirectories inside `src`. For faster builds and smaller Docker images, only files inside `src` are copied by Docker. You need to put any files required to run your module inside `src`, otherwise Docker won’t copy them.

You can create more top-level directories. They will not be included in the final Docker image so you can use them for things like documentation.

If you have Git installed and your project is not part of a larger repository, then a new repository will be initialized resulting in an additional top-level `.git` directory.
