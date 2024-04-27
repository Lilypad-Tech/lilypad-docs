---
description: Run a Stable Diffusion Text to Image Job
---

# Stable Diffusion (SDXL0.9 & 1.0)

{% embed url="https://youtu.be/kh5jXuQ6_ww?si=BYIvEW9q8I4C7eS_" %}

Generically, stable diffusion is what happens when you put a couple of drops of dye into a bucket of water. Given time, the dye randomly disperses and eventually settles into a uniform distribution which colours all the water evenly

In computer science, you define rules for your (dye) particles to follow and the medium this takes place in.

Stable Diffusion is a machine learning model used for text-to-image processing (like Dall-E) and based on a diffusion probabilistic model that uses a transformer to generate images from text.

### \[CLI] Running Stable Diffusion SDXL 0.9 and SDXL 1.0

{% hint style="danger" %}
Ensure you have installed all requirements [https://github.com/noryev/lilypad-docs/blob/main/lilypad/lilypad-milkyway-testnet/quick-start/install-run-requirements.md](https://github.com/noryev/lilypad-docs/blob/main/lilypad/lilypad-milkyway-testnet/quick-start/install-run-requirements.md)
{% endhint %}

### Lilypad

Lilypad can run SDXL v0.9 or SDXL v1.0 with the option to add tunables to improve or change the model output.&#x20;

&#x20;To run SDXL Pipeline in Lilypad, you can use the following commands:

#### SDXL v0.9

Base:

```
lilypad run sdxl-pipeline:v0.9-base-lilypad3 -i Prompt="an astronaut floating against a white background"
```

Refiner:

```
lilypad run sdxl-pipeline:v0.9-refiner-lilypad3 -i Prompt="an astronaut floating against a white background"
```

#### SDXL 1.0

Base:

```
lilypad run sdxl-pipeline:v1.0-base-lilypad3 -i Prompt="an astronaut floating against a white background"
```

Refiner:

```
lilypad run sdxl-pipeline:v1.0-refiner-lilypad3 -i Prompt="an astronaut floating against a white background"
```

#### Specifying tunables

If you wish to specify more than one tunable, such as the number of steps, simply add more `-i` flags. For example, to improve the quality of the image generated add "Steps=x" with x = (up to 200):

```
lilypad run sdxl-pipeline -i Prompt="an astronaut floating against a white background" -i Steps=69
```

{% hint style="info" %}
See the options and tunables section (below) for more information on what tunables are available.
{% endhint %}

The output will look like this:

<figure><img src="https://github.com/noryev/lilypad-docs/raw/main/lilypad/.gitbook/assets/sdxl_execution.png" alt=""><figcaption></figcaption></figure>

**SDXL Output**

Take the ipfs link given in the results and paste it into your browser:

```
https://ipfs.io/ipfs/QmVng1jkMxE9ep4k8mYiiCiWaCRiRLvCeo6bJRXirhz1dZ
```

{% hint style="warning" %}
Please be patient! IPFS can take some time to propagate and doesn't always work immediately.
{% endhint %}

You could also check the output folder that would have been downloaded at the end of running the job

```
open /tmp/lilypad/data/downloaded-files/QmZuE29GJVmenRUh72FQDgkMUT1Zdp967oEJvzjaDwGGVo
```

<figure><img src="https://github.com/noryev/lilypad-docs/raw/main/lilypad/.gitbook/assets/sdxl_output.png" alt=""><figcaption></figcaption></figure>

**Results of SDXL job on Output Directory**

In the **/outputs** folder, you'll find the image:

<figure><img src="https://github.com/noryev/lilypad-docs/raw/main/lilypad/.gitbook/assets/sdxl_result_output.png" alt=""><figcaption></figcaption></figure>

**The Image in the outputs folder**

Since modules are deterministic, running this command with the same text prompt will produce the same image, since the same seed is also used (the default seed is 0).

{% hint style="info" %}
See this [beginner-friendly article](https://aituts.com/stable-diffusion-seed/) on how seed's work for more info on this
{% endhint %}

To change the image, you can pass in a different seed number:

```
`lilypad run sdxl-pipeline:v0.9-base-lilypad3 -i Prompt='a gigantic lilypad shaped space station' -i Steps=150` 
```

<figure><img src="https://github.com/noryev/lilypad-docs/raw/main/lilypad/.gitbook/assets/sdxl_result_output2.png" alt=""><figcaption></figcaption></figure>

Output using different seed.

### Options and tunables

The following tunables are available. All of them are optional, and have default settings that will be used if you do not provide them.

| Name        | Description                              | Default                           | Available options                                                                                                                                                                                                                                                                                         |
| ----------- | ---------------------------------------- | --------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Prompt`    | A text prompt for the model              | "question mark floating in space" | Any string                                                                                                                                                                                                                                                                                                |
| `Seed`      | A seed for the model                     | 42                                | Any valid non-negative integer                                                                                                                                                                                                                                                                            |
| `Steps`     | The number of steps to run the model for | 50                                | Any valid non-negative integer                                                                                                                                                                                                                                                                            |
| `Scheduler` | The scheduler to use for the model       | `normal`                          | `normal`, `karras`, `exponential`, `sgm_uniform`, `simple`, `ddim_uniform`                                                                                                                                                                                                                                |
| `Sampler`   | The sampler to use for the model         | `euler_ancestral`                 | `"euler"`, `"euler_ancestral"`, `"heun"`, `"heunpp2"`, `"dpm_2"`, `"dpm_2_ancestral"`, `"lms"`, `"dpm_fast"`, `"dpm_adaptive"`, `"dpmpp_2s_ancestral"`, `"dpmpp_sde"`, `"dpmpp_sde_gpu"`, `"dpmpp_2m"`, `"dpmpp_2m_sde"`, `"dpmpp_2m_sde_gpu"`, `"dpmpp_3m_sde"`, `"dpmpp_3m_sde_gpu"`, `"ddpm"`, `"lcm"` |
| `Size`      | The output size requested in px          | `1024`                            | `512`, `768`, `1024`, `2048`                                                                                                                                                                                                                                                                              |
| `Batching`  | How many images to produce               | `1`                               | `1`, `2`, `4`, `8`                                                                                                                                                                                                                                                                                        |

See the usage sections for the runner of your choice for more information on how to set and use these variables.

Learn more about this Lilypad module on [Github](https://github.com/Lilypad-Tech/lilypad-module-sdxl-pipeline).

## CLI Video

In this video, Sam demos the use of SDXL in the Lilypad network.

{% embed url="https://youtu.be/RBECCMl_fco" %}

### Looking for Smart Contracts?

\
Try this to start!

{% @github-files/github-code-block url="https://github.com/bacalhau-project/lilypad/blob/main/docs/smart-contract-jobs.md" %}

