---
description: Creating a Lilypad job module
---

# Creating Your Module

In this guide, we'll be creating a basic sentiment analysis module using [`distilbert/distilbert-base-uncased-finetuned-sst-2-english`](https://huggingface.co/distilbert/distilbert-base-uncased-finetuned-sst-2-english) (which I will be referring to as Distilbert from now on). We will be referring back to the Hugging Face page throughout this guide, so it's best to keep it open and accessible.

Input:

```sh
lilypad run --network demonet github.com/DevlinRocha/lilypad-module-sentiment:main --web3-private-key 0ec38dd1ee0898dae8460b269859b4fb3cb519b35d82014c909ec4741c790831 -i input="LILYPAD IS AWESOME"
```

Output:

```json
{
  "input": "LILYPAD IS AWESOME",
  "sentiment": "POSITIVE",
  "status": "success"
}
```

- [View the final source code for the module](https://github.com/DevlinRocha/lilypad-module-sentiment)

## Prerequisites

To build and run a module on Lilypad Network, you'll need to have [Python](https://www.python.org/), [pip](https://pip.pypa.io/en/stable/), and [Docker](https://www.docker.com/), on your machine, as well as [GitHub](https://github.com/) and [Docker Hub](https://hub.docker.com/) accounts.

## Downloading The Model

The first thing you'll need for your module is a local model to use.

A basic outline for downloading a model from [Hugging Face](https://huggingface.co/) is provided in `scripts/download_models.py`. The structure of the script and the methods for downloading a model can differ between models and libraries. It’s important to tailor the process to the specific requirements of the
model you're working with.

You can get started by attempting to run the `download_models.py` script.

```sh
python -m scripts.download_models
```

Since the script hasn't been properly configured yet, it will return an error and point you to the file.

```sh
❌ Error: Model download script is not configured.
👉 /scripts/download_models.py
```

Open `scripts/download_models.py` and you will see some `TODO` comments with instructions. Let's go through them each in order. You can remove each `TODO` comment after completing the task.

```python
# TODO: Update ../requirements.txt
# from transformers import AutoTokenizer, AutoModelForSequenceClassification
```

First we have a reminder to update our `requirements.txt` file, which is used by the `Dockerfile` to install the module's dependencies. In the next line is a commented out `import` statement.

To find the dependencies that our model requires, we can refer back to Distilbert's Hugging Face page and click on the "Use this model" dropdown, where you will see the [🤗 Transformers](https://huggingface.co/docs/hub/en/transformers) library as an option. Click it.

{% hint style="info" %}
Most (but not all) models that utilize machine learning use the 🤗 Transformers library, which provides APIs and tools to easily download and train pretrained models.

- [Learn more about downloading models from Hugging Face](https://huggingface.co/docs/hub/en/models-downloading)
- [Read the `🤗 Transformers` documentation](https://huggingface.co/docs/transformers/index)
  {% endhint %}

You should see a handy modal explaining how to use the model with the `Transformers` library. For most models, you'd want to use this. However, Distilbert has a specific tokenizer and model class. Close the modal and scroll to the [How to Get Started With the Model](https://huggingface.co/distilbert/distilbert-base-uncased-finetuned-sst-2-english#how-to-get-started-with-the-model) section of the model card. We're going to use this instead.

For now, let's look at the top 2 lines of the provided code block:

```python
import torch
from transformers import DistilBertTokenizer, DistilBertForSequenceClassification
```

Notice that `torch` is also being used. Copy the `transformers` import statement and paste it over the existing import statement in our `download_models.py` file.

Now open `requirements.txt`:

```txt
# torch==2.4.1
# transformers==4.47.1
```

These are 2 of the most common libraries when working with models. Similar to the `import` statement in the `download_models.py` file, they are provided by default for convenience, but commented out because although they are common, not every model will use them.

Since this model happens to use both of these libraries, we can uncomment both lines and close the file after saving.

{% hint style="info" %}
`torch` is a collection of APIs for extending [PyTorch](https://pytorch.org/)’s core library of operators.

- [Learn more about using `datasets` with `Pytorch`](https://huggingface.co/docs/datasets/en/use_with_pytorch)
- [Read the `torch` documentation](https://pytorch.org/docs/stable/index.html)
  {% endhint %}

Return to the `download_models.py` file, and look for the next `TODO` comment.

```python
# TODO: Set this to your model's Hugging Face identifier
MODEL_IDENTIFIER = ""
```

If we take a look at the [Distilbert Hugging Face page](https://huggingface.co/distilbert/distilbert-base-uncased-finetuned-sst-2-english), we can use the copy button next to the name of the module to get the `MODULE_IDENTIFIER`. Just paste that in as the value.

For our use case, it should look like this:

```python
MODEL_IDENTIFIER = "distilbert/distilbert-base-uncased-finetuned-sst-2-english"
```

You're almost ready to download the model. All you need to do now is replace the following 2 lines:

```python
tokenizer = AutoTokenizer.from_pretrained(MODEL_IDENTIFIER)
model = AutoModelForSequenceClassification.from_pretrained(MODEL_IDENTIFIER)
```

Instead of using `AutoTokenizer` and `AutoModelForSequenceClassification`, replace those with the `DistilBertTokenizer` and `DistilBertForSequenceClassification` we imported.

```python
tokenizer = DistilBertTokenizer.from_pretrained(MODEL_IDENTIFIER)
model = DistilBertForSequenceClassification.from_pretrained(MODEL_IDENTIFIER)
```

The script is now configured! Try running the command again.

```sh
python -m scripts.download_models
```

The `models` directory should now appear in your project. 🎉

{% hint style="info" %}
No matter which model you are using, be sure to thoroughly read the model's documentation to learn how to properly download and use the model locally.
{% endhint %}

## Preparing Your Module

Before you are able to run your module, we need to build the Docker image. You can run the following command:

```sh
python -m scripts.docker_build
```

You should see the following response in the console:

```sh
❌ Error: DOCKER_REPO is not set in config/constants.py.
```

Open the `constants.py` file, it should look like this:

```python
# TODO: Set the Docker Hub repository before pushing the image.
# Example: "devlinrocha/lilypad-module-sentiment"
DOCKER_REPO = ""

# TODO: Set the tag for the Docker image.
# Example: "latest", "v1.0", or a commit SHA
DOCKER_TAG = "latest"

# TODO: Set the GitHub repository URL where your module is stored.
# Example: "github.com/devlinrocha/lilypad-module-sentiment".
MODULE_REPO = ""

# TODO: Specify the target branch name or commit hash.
# Example: "main" or "c3ed392c11060337cae010862b1af160cd805e67"
TARGET_COMMIT = "main"
```

For now, we'll be testing the module locally, so all we need to worry about is the `DOCKER_REPO` variable. We'll use `MODULE_REPO` when it's time to run the module on Lilypad Network. For help or more information, view the [configuration documentation](./configuration.md)

You should be able to successfully build the Docker image now.

{% hint style="info" %}
In the modules Dockerfile, you'll find 3 COPY instructions.

```Dockerfile
COPY requirements.txt .
COPY src /src
COPY models /models
```

These instructions bring the `requirements.txt` file, the `src` directory, and the `models` directory into the Docker image. It's important to remember that any modifications to these files or directories will necessitate a rebuild of the module's Docker image to ensure the changes are reflected in the container.
{% endhint %}

## Building Your Model

Now for the fun part, it's time to start using the model!

This time we'll get started by running the `run_module` script.

```sh
python -m scripts.run_module
```

You should see an error with some instructions.

```sh
❌ Error: No job configured. Implement the module's job before running the module.
        1. Implement job module
                👉 /src/run_inference.py
        2. Delete this code block
                👉 /scripts/run_module.py
```

### 1. Implement Job Module

Let's tackle the `run_inference.py` script first. This is where your modules primary logic and functionality should live. There is a `TODO` comment near the top of the file.

```python
# TODO: Update ../requirements.txt
# import torch
# from transformers import AutoTokenizer, AutoModelForSeq2SeqLM
```

We've already updated the `requirements.txt` file, so we can skip that step. Go ahead and uncomment the `import` statements and replace the `transformers` line with the `DistilBertTokenizer` and `DistilBertForSequenceClassification`.

We should refer back to the "How to Get Started With the Model" section of Distilbert's model card to figure out how to use the model.

```python
tokenizer = DistilBertTokenizer.from_pretrained("distilbert-base-uncased-finetuned-sst-2-english")
model = DistilBertForSequenceClassification.from_pretrained("distilbert-base-uncased-finetuned-sst-2-english")

inputs = tokenizer("Hello, my dog is cute", return_tensors="pt")
with torch.no_grad():
    logits = model(**inputs).logits

predicted_class_id = logits.argmax().item()
model.config.id2label[predicted_class_id]
```

Let's implement this into our `run_inference` script. Scroll down to the `main()` function and you'll see a couple commented out lines.

```python
# tokenizer = AutoTokenizer.from_pretrained(MODEL_DIRECTORY)
# model = AutoModelForSeq2SeqLM.from_pretrained(MODEL_DIRECTORY)
```

Same as before, uncomment and replace `AutoTokenizer` with `DistilBertTokenizer` and `AutoModelForSeq2SeqLM` with `DistilBertForSequenceClassification`. This is now functionally identical to the first 2 lines of code from Distilbert's example.

Below that, the `tokenizer` and `model` are passed into the `run_job()` function. Let's scroll back up and take a look at the function. This is where we'll want to implement the rest of the code from Distilbert's example. The `inputs` are already functionally identical, so let's adjust the `output`.

From the Distilbert model card, copy all of the code below the `inputs` variable declaration, and paste it over the `output` variable declaration in your modules code.

```python
inputs = tokenizer(
    input,
    return_tensors="pt",
    truncation=True,
    padding=True,
)

with torch.no_grad():
    logits = model(**inputs).logits

predicted_class_id = logits.argmax().item()
model.config.id2label[predicted_class_id]

return output
```

All we need to do from here is set the `output` to the last line we pasted.

```python
output = model.config.id2label[predicted_class_id]

return output
```

That's everything we'll need for the modules source code! You can build the Docker image with the new code.

```sh
python -m scripts.docker_build
```

### 2. Delete Code Block

While the Docker image is being built (it can take a while), we still need to finish step 2 that the error in the console gave us earlier. Open the `run_module.py` script.

Find the `TODO` comment and delete the code block underneath.

```python
# TODO: Remove the following print and sys.exit statements and create the module job.
print(
    "❌ Error: No job configured. Implement the module's job before running the module.",
    file=sys.stderr,
    flush=True,
)
print("\t1. Implement job module")
print("\t\t👉 /src/run_inference.py")
print("\t2. Delete this code block")
print("\t\t👉 /scripts/run_module.py")
sys.exit(1)
```

{% hint style="info" %}
Since we are editing a script and not the `src` code that gets used in the Docker image we won't need to rebuild after making these changes.
{% endhint %}

Once the Docker image is finished building, we can run the module!

## Running Your Module

It's finally time to see your module in action.

### Local

Let's start by running it locally.

```sh
python -m scripts.run_module --local
```

The CLI should ask you for an input. Enter whatever you like and hit enter. The module will analyze the sentiment of your input and output the results at `outputs/result.json`.

```json
{
  "input": "LILYPAD IS AWESOME",
  "result": "POSITIVE",
  "status": "success"
}
```

You just used a local LLM! 🎉

### Lilypad Network

Before you can run the module on Lilypad Network, you'll need to push the Docker image to Docker Hub.

```sh
python -m scripts.docker_build --push
```

While the Docker image is being built and pushed, you should configure the rest of the variables in `constants.py`. Make sure that you push your code to a public GitHub repository.

{% hint style="info" %}
Since these variables are only used in scripts and not in any `src` code that gets used in the Docker image we won't need to rebuild after making these changes.
{% endhint %}

Once your Docker image is pushed to Docker Hub, your most recent code is pushed to a public GitHub repository, you can run your module on Lilypad Network by removing the `--local` flag.

```sh
python -m scripts.run_module
```

You just use an LLM on Lilypad's decentralized network! 🎉
