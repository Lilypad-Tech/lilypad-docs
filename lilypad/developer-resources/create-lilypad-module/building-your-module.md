---
description: Building a Lilypad job module
---

# Building Your Module

In this guide, we'll be recreating a sentiment analysis module using [`distilbert/distilbert-base-uncased-finetuned-sst-2-english`](https://huggingface.co/distilbert/distilbert-base-uncased-finetuned-sst-2-english) (which I will be referring to as Distilbert from now on). We will be referring back to the Hugging Face page throughout this guide, so it's best to keep it open and accessible.

- [View the final source code for the module](https://github.com/DevlinRocha/lilypad-module-sentiment)

## Downloading The Model(s)

The first thing you'll need for your module is a local model to use.

A basic outline for downloading a model from [Hugging Face](https://huggingface.co/) is provided in `scripts/download_models.py`. The structure of the script and the methods for downloading a model can differ between models and libraries. It’s important to tailor the process to the specific requirements of the
model you're working with.

You can get started by attempting to run the script.

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

You should see a handy modal explaining how to use the model with the `Transformers` library. For most models, you'd want to use this. However, Distilbert has a specific tokenizer and model class. Close the modal and scroll to the [How to Get Started With the Model](https://huggingface.co/distilbert/distilbert-base-uncased-finetuned-sst-2-english#how-to-get-started-with-the-model) section to use this instead.

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
