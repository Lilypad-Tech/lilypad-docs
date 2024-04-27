---
description: Run a Stable Diffusion Text to Video Job
---

# Stable Diffusion Video (SDV1.0 & 1.1)

{% embed url="https://drive.google.com/file/d/19_oEBcpKSe1n91AyGdIePJdQMzz1KjoD/view?usp=drive_link" %}

Based on ComfyUI, the SDV Pipeline modules for Lilypad allow you generate videos from text prompts on Lilypad using Stable Diffusion Video and related models.&#x20;

The SDV Pipeline modules are designed to take your text prompt, generate a still frame using SDXL, then use that as the input to the SDV model, producing an APNG (animated PNG), WebP video, and an MP4 video all in one go.

## Running Stable Diffusion Video SDV1.0 and SDV1.1

{% hint style="info" %}
Ensure you have installed all requirements [https://github.com/noryev/lilypad-docs/blob/main/lilypad/lilypad-milkyway-testnet/quick-start/install-run-requirements.md](https://github.com/noryev/lilypad-docs/blob/main/lilypad/lilypad-milkyway-testnet/quick-start/install-run-requirements.md)
{% endhint %}

### Lilypad

To run SDV1.0 or 1.1 Pipeline in Lilypad, you can use the following commands:

#### SDV 1.0

```
lilypad run sdv-pipeline:v1.0-lilypad2 -i ImageSeed="696721260153400" -i Prompt="an astronaut floating against a white background" -i Steps=200 -i VideoSteps 70
```

#### SDV 1.1

```
lilypad run sdv-pipeline:v1.1-lilypad2 -i ImageSeed="696721260153400" -i Prompt="an astronaut floating against a white background" -i Steps=200 -i VideoSteps 70
```

#### Specifying tunables

If you wish to specify more than one tunable, such as the number of steps, simply add more `-i` flags. For example, to change or improve the quality of the image generated add "Steps=x" with x = (up to 70):

```
lilypad run sdv-pipeline -i Prompt="an astronaut floating against a white background" -i Steps=69
```

{% hint style="info" %}
See the options and tunables section for more information on what tunables are available.
{% endhint %}

The output will look like this:

<figure><img src="../.gitbook/assets/sdvJob.png" alt=""><figcaption></figcaption></figure>

**SDV Output**

Take the ipfs link given in the results and paste it into your browser:

```
https://ipfs.io/ipfs/QmZ9jvBxfwdeHTXpvDWnTqkLLWvdANzkDstph2EnXMfU4w
```

{% hint style="info" %}
Please be patient! IPFS can take some time to propagate and doesn't always work immediately.
{% endhint %}

You could also check the output folder that would have been downloaded at the end of running the job:

```
open /tmp/lilypad/data/downloaded-files/QmbjEKwZn5vSBoArudUEAPJDEiesVPk5tNkYxFvNkdFs6t
```

<figure><img src="../.gitbook/assets/sdvOutput.png" alt=""><figcaption></figcaption></figure>

**Results of SDV job on Output Directory**

In the **/outputs** folder, you'll find the video and associated images:

{% embed url="https://drive.google.com/file/d/19_oEBcpKSe1n91AyGdIePJdQMzz1KjoD/view?usp=drive_link" %}

**The video in the outputs folder**

Since modules are deterministic, running this command with the same text prompt will produce the same image, since the same seed is also used (the default seed is 0).

{% hint style="info" %}
See this [beginner-friendly article](https://aituts.com/stable-diffusion-seed/) on how seed's work for more info on this
{% endhint %}

## Options and tunables

The following tunables are available. All of them are optional, and have default settings that will be used if you do not provide them.

| Name             | Description                                    | Default                           | Available options                                                                                                                                                                                                                                                                                         |
| ---------------- | ---------------------------------------------- | --------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Prompt`         | A text prompt for the model                    | "question mark floating in space" | Any string                                                                                                                                                                                                                                                                                                |
| `Framerate`      | The framerate of the video                     | 8                                 | Any valid positive integer between 1 and 20                                                                                                                                                                                                                                                               |
| `Seed`           | A seed for the image model                     | 42                                | Any valid non-negative integer                                                                                                                                                                                                                                                                            |
| `Steps`          | The number of steps to run the model for       | 50                                | Any valid non-negative integer from 5 to 200 inclusive                                                                                                                                                                                                                                                    |
| `Scheduler`      | The scheduler to use for the model             | `normal`                          | `normal`, `karras`, `exponential`, `sgm_uniform`, `simple`, `ddim_uniform`                                                                                                                                                                                                                                |
| `Sampler`        | The sampler to use for the model               | `euler_ancestral`                 | `"euler"`, `"euler_ancestral"`, `"heun"`, `"heunpp2"`, `"dpm_2"`, `"dpm_2_ancestral"`, `"lms"`, `"dpm_fast"`, `"dpm_adaptive"`, `"dpmpp_2s_ancestral"`, `"dpmpp_sde"`, `"dpmpp_sde_gpu"`, `"dpmpp_2m"`, `"dpmpp_2m_sde"`, `"dpmpp_2m_sde_gpu"`, `"dpmpp_3m_sde"`, `"dpmpp_3m_sde_gpu"`, `"ddpm"`, `"lcm"` |
| `Batching`       | How many images to produce                     | `1`                               | `1`, `2`, `4`, `8`                                                                                                                                                                                                                                                                                        |
| `VideoSeed`      | A seed for the video model                     | 42                                | Any valid non-negative integer                                                                                                                                                                                                                                                                            |
| `VideoSteps`     | The number of steps to run the video model for | 50                                | Any valid non-negative integer from 5 to 70 inclusive                                                                                                                                                                                                                                                     |
| `VideoScheduler` | The scheduler to use for the video model       | `normal`                          | `normal`, `karras`, `exponential`, `sgm_uniform`, `simple`, `ddim_uniform`                                                                                                                                                                                                                                |
| `VideoSampler`   | The sampler to use for the video model         | `euler_ancestral`                 | `"euler"`, `"euler_ancestral"`, `"heun"`, `"heunpp2"`, `"dpm_2"`, `"dpm_2_ancestral"`, `"lms"`, `"dpm_fast"`, `"dpm_adaptive"`, `"dpmpp_2s_ancestral"`, `"dpmpp_sde"`, `"dpmpp_sde_gpu"`, `"dpmpp_2m"`, `"dpmpp_2m_sde"`, `"dpmpp_2m_sde_gpu"`, `"dpmpp_3m_sde"`, `"dpmpp_3m_sde_gpu"`, `"ddpm"`, `"lcm"` |

Learn more about this Lilypad module on [Github](https://github.com/Lilypad-Tech/lilypad-module-sdv-pipeline).
