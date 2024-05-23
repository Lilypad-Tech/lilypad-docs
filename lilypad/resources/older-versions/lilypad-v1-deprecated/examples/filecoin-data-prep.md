---
description: Filecoin Data Prep
---

# Filecoin Data Prep

{% hint style="danger" %}
Code not tested.
{% endhint %}

## Overview

The Filecoin Data Prep Module is designed to chunk data into CAR files from an S3 bucket - hence the name, since it prepares the data to be uploaded to Filecoin.\
\
The repo for this module can be found [here](https://github.com/bacalhau-project/lilypad-modicum/blob/main/src/python/modules/filecoin\_data\_prep.py).

## \[CLI] Usage

{% hint style="warning" %}
Ensure you have installed all requirements [install-run-requirements.md](../reference/quick-start/install-run-requirements.md "mention")
{% endhint %}

Run the module

```
lilypad run filecoin_data_prep:v0.0.1 '{"ipfs_cid": "CID"}'
```

Execution:

<figure><img src="https://lh5.googleusercontent.com/B5aqsXNvkxmZCs32zEErs_2OzLU-DKV_0mrYwE-MNPgDx7Wew5EeEJovauH7Rz541imlJFDSzTk5PujSbrRhi3g3UXCS1MUxHScma90W50AnnCXGfY5-MoKW0ZvelEEdK3pmrn-IuDAvP0Ii-5PwT9wmPg=s2048" alt=""><figcaption></figcaption></figure>

Results:

<figure><img src="https://lh5.googleusercontent.com/Hxn4eUFYW_QAik1YRalr8KyOWBqqtruj71uKaZdQAWyy4JWcGaCYP4C0sWl1oLp1jPi8TGt-KXGhg1S837mHfWBACBbxZx3Y5aVthmN_z51xpMWIoGyyH1yV5LhSB101CPNM2uX7hdbCGwUsK2Odb1a0aQ=s2048" alt=""><figcaption></figcaption></figure>

## Full Module

{% @github-files/github-code-block url="https://github.com/bacalhau-project/lilypad-modicum/blob/main/src/python/modules/filecoin_data_prep.py" %}
