---
description: Instructions on how to use the Lilypad API
---

# Usage

Once you have your API key, you can start running AI inference jobs using Lilypad's Anura API. Below is a simple **"Hello World"** example to get started.

### Get Available Models

Before running a job, check which models are supported:

```bash
curl -X GET "https://anura-testnet.lilypad.tech/api/v1/models" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_API_KEY"
```

### Run a Job

Use the API to send a simple chat completion request using one of the available models:

```bash
curl -X POST "https://anura-testnet.lilypad.tech/api/v1/chat/completions" \
  -H "Content-Type: application/json" \
  -H "Accept: text/event-stream" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -d '{
    "model": "MODEL_NAME:MODEL_VERSION",
    "messages": [
      {
        "role": "system",
        "content": "You are a helpful AI assistant"
      },
      {
        "role": "user",
        "content": "What order do frogs belong to?"
      }
    ],
    "temperature": 0.6
  }'
```

Replace `"MODEL_NAME:MODEL_VERSION"` with the model you want to use from the previous step.

### Retrieve Job Results

You can check the status of your job and retrieve outputs using the job ID:

```bash
curl -X GET "https://anura-testnet.lilypad.tech/api/v1/jobs/{job_id}" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_API_KEY"
```

This will return details on whether the job is still processing or has completed.

For more advanced usage, including streaming completions, multi-turn conversations, and additional endpoints, check out the [inference API Documentation](https://docs.lilypad.tech/lilypad/developer-resources/inference-api).
