# Build a Job Module

A Lilypad module is a Git repository that can be used to perform various tasks using predefined templates and inputs.&#x20;

This guide will walk you through the process of creating a Lilypad module, including defining a JSON template, handling inputs, ensuring determinism, and other best practices.

## Module Structure

1. Start by creating a Git repository for your Lilypad module. The module's versions will be represented as Git tags.
2. Inside your module's repository, create a file named `lilypad_module.json.tmpl`. This file will serve as a JSON template with Go text/template style sections, like `{{.Message}}`, which will be replaced by Lilypad with JSON-encoded inputs.
3. You can also use Go templates to set defaults and perform other template-related operations. Refer to the `cowsay` example for inspiration.

## Handling Inputs

Inputs are passed to your Lilypad module as a map of strings to strings. You can pass inputs using the following command:

```bash
lilypad run github.com/username/repo:tag -i Message=moo
```

Ensure that your module can accept and process inputs as specified.

## Ensuring Determinism

To ensure that your Lilypad module is deterministic, follow these guidelines:

* Make the output of your module reproducible.
* Strip timestamps and time measurements from the output, including to stdout and stderr.
* Avoid reading from sources of entropy, such as /dev/random.
* When referencing Docker images, specify their sha256 hashes.

If your module is not deterministic, it may not be adopted by compute providers, and it won't be added to their allowlists.

## Testing Your Module

During development, you can use the Git hash to test your module. Ensure that your module functions correctly and produces deterministic results.

## Examples

Here are some example Lilypad modules for reference:

* [**Cowsay**](https://github.com/bacalhau-project/lilypad-module-cowsay)**:** Lilypad "Hello World" example
* [**SDXL v0.9/v1.0**](https://github.com/Lilypad-Tech/lilypad-module-sdxl-pipeline): Text to image generation.
* [**SDV v1.0/1.1**](https://github.com/Lilypad-Tech/lilypad-module-sdv-pipeline): Text to video generation.

Deprecated examples:

* [**lora-training**](https://github.com/bacalhau-project/lilypad-module-lora-training)**:** An example module for LoRa training tasks.
* [**lora-inference**](https://github.com/bacalhau-project/lilypad-module-lora-inference)**:** An example module for LoRa inference tasks.
* [**duckdb**](https://github.com/bacalhau-project/lilypad-module-duckdb)**:** An example module related to DuckDB.

These examples can help you understand how to structure your Lilypad modules and follow best practices.

## Conclusion

In this guide, we've covered the essential steps to create a Lilypad module, including defining a JSON template, handling inputs, ensuring determinism, and testing your module. Follow these best practices to create reliable and reusable modules for Lilypad.

For more information and examples, refer to the official Lilypad documentation and the cowsay example module.
