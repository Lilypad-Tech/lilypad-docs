---
description: Running the most important Hello World on lilypad
---

# Run Hello World!

> **Note**: Make sure to you have Lilypad CLI installed.

> **Note**: Make sure you have `SERVICE_SOLVER`, `SERVICE_MEDIATORS` and `WEB3_PRIVATE_KEY` env variables in your environment

### Run Cowsay

1. Run the command below

```bash
lilypad run cowsay:v0.0.1 -i Message="moo"
```

2. Wait for the compute to take place and for the results to be published

<figure><img src="../../.gitbook/assets/cowmo_success.png" alt=""><figcaption><p>A successful run</p></figcaption></figure>

3. Viewing your results

```bash
cat /tmp/lilypad/data/downloaded-files/Qma2Ds9uGmtDd3GkerqqKLJe9TjcZC4yxuGRUaFBsQi7yr/stdout
```

<figure><img src="../../.gitbook/assets/cowmo_results.png" alt=""><figcaption><p>Looking at your results</p></figcaption></figure>
