---
description: How to build your own compute job for Lilypad
---

# Build a Job Module

A Lilypad module is a Git repository that allows you to perform various tasks using predefined templates and inputs.&#x20;

This guide will walk you through the process of creating a Lilypad module, including defining a JSON template, handling inputs, and following best practices.

{% hint style="info" %}
If you're new to Docker, consider exploring this [step-by-step tutorial](https://docs.docker.com/get-started/) on creating, building, and running a Docker image for a simple Hello World style application.
{% endhint %}

## Module Structure

1. Start by creating a Git repository for your Lilypad module. The module's versions will be represented as Git tags.
2. Inside your module's repository, create a file named `lilypad_module.json.tmpl`. This file will serve as a JSON template with Go text/template style sections, like `{{.Message}}`, which will be replaced by Lilypad with JSON-encoded inputs.
3. You can also use Go templates to set defaults and perform other template-related operations. Refer to [the `cowsay` example](../lilypad-modules/hello-cow-world.md) for inspiration.

## Handling Inputs

Inputs are passed to your Lilypad module as key-value pairs, where both the keys and values are strings. You can pass inputs using the following command:

```bash
lilypad run github.com/username/repo:tag -i Message=moo
```

Ensure that your module is set up to accept and process inputs according to the specified format.

## Testing Your Module

During development, you can use the Git hash to test your module. This allows you to verify that your module functions correctly and produces the expected results.

## Examples

Here are some example Lilypad modules for reference:

* [**Cowsay**](https://github.com/Lilypad-Tech/lilypad-module-cowsay)**:** Lilypad "Hello World" example
* [**SDXL v0.9/v1.0**](https://github.com/Lilypad-Tech/lilypad-module-sdxl-pipeline): Text to image generation.
* [**SDV v1.0/1.1**](https://github.com/Lilypad-Tech/lilypad-module-sdv-pipeline): Text to video generation.

Deprecated examples:

* [**lora-training**](https://github.com/Lilypad-Tech/lilypad-module-lora-training)**:** An example module for LoRa training tasks.
* [**lora-inference**](https://github.com/Lilypad-Tech/lilypad-module-lora-inference)**:** An example module for LoRa inference tasks.
* [**duckdb**](https://github.com/Lilypad-Tech/lilypad-module-duckdb)**:** An example module related to DuckDB.

These examples can help you understand how to structure your Lilypad modules and follow best practices.

## Conclusion

In this guide, we've covered the essential steps to create a Lilypad module, including defining a JSON template, handling inputs, and testing your module. By following these best practices, you can build reliable and reusable modules for Lilypad.&#x20;

For more information and additional examples, refer to the official Lilypad documentation and the Cowsay example module.
