---
description: >-
  Anura (from Ancient Greek: ἀν-, an- meaning "without," and οὐρά, ourá meaning
  "tail") refers to the order of amphibians that includes all modern frogs and
  toads.
---

# Anura API

Lilypad's official AI inference API.

## Getting Started

To use the Lilypad API, visit the [Anura website](https://anura.lilypad.tech/) to get an API key.

## API Endpoints

### API Clients

{% hint style="info" %}
If you are using an API client such as Bruno or Postman, you can use our provided collections below.
{% endhint %}

{% tabs %}
{% tab title="Bruno" %}
{% file src="../.gitbook/assets/Anura.bruno_collection.json" %}
Bruno collection
{% endfile %}
{% endtab %}

{% tab title="Postman" %}
{% file src="../.gitbook/assets/Anura.postman_collection.json" %}
Postman collection
{% endfile %}
{% endtab %}
{% endtabs %}

### Jobs

* `GET /api/v1/jobs/:id` - Get status and details of a specific job

### Cowsay

* `POST /api/v1/cowsay` - Create a new cowsay job
  * Request body: `{"message": "text to display"}`
* `GET /api/v1/cowsay/:id/results` - Get results of a cowsay job

### Ollama

* `POST /api/v1/ollama` - Create a new Ollama job
* `GET /api/v1/ollama/:id/results` - Get results of an Ollama job
* `POST /api/v1/chat/completions` - Stream chat completions
* `GET /api/v1/models` - Get available models

### Get Available Models

To see which models are available:

```
curl -X GET "https://anura-testnet.lilypad.tech/api/v1/models" \
-H "Content-Type: application/json" \
-H "X-API-Key: your_api_key_here"
```

### Chat Completions API

#### Streaming Chat Completions

`POST /api/v1/chat/completions`

This endpoint provides a streaming interface for chat completions using Server-Sent Events (SSE).

**Request Headers**

* `Content-Type: application/json` (required)
* `Accept: text/event-stream` (recommended for streaming)
* `Authorization: Bearer <your_api_key>` or `X-API-Key: <your_api_key>` (required)

**Request Body**

```json
{
    "model": "llama2:7b",
    "messages": [
        {
            "role": "user",
            "content": "write a haiku about lilypads"
        }
    ],
    "max_tokens": 2048,
    "temperature": 0.7
}
```

| Parameter     | Type    | Description                                                            |
| ------------- | ------- | ---------------------------------------------------------------------- |
| `model`       | string  | **Required**. ID of the model to use (e.g., "llama2:7b")               |
| `messages`    | array   | **Required**. Array of message objects representing the conversation   |
| `max_tokens`  | integer | Maximum number of tokens to generate                                   |
| `temperature` | number  | Controls randomness: 0 is deterministic, higher values are more random |

**Response Format**

The response is a stream of Server-Sent Events (SSE) with the following format:

1. **Processing updates**:

```
data: {"status": "processing", "state": 1}
```

2. **Content delivery**:

```
event: delta
data: {"model":"llama2:7b","created_at":"2025-02-24T19:42:41.3904769Z","message":{"role":"assistant","content":"\nLily pads dance\nOn the water's gentle lap\nSerene beauty"},"done_reason":"stop","done":true,"total_duration":1650031984,"load_duration":1262911467,"prompt_eval_count":29,"prompt_eval_duration":107000000,"eval_count":19,"eval_duration":278000000}
```

3. **Completion marker**:

```
data: [DONE]
```

**Example Request**

```sh
curl -X POST "https://anura-testnet.lilypad.tech/api/v1/chat/completions" \
-H "Content-Type: application/json" \
-H "Accept: text/event-stream" \
-H "Authorization: Bearer your_api_key_here" \
-d '{
    "model": "llama2:7b",
    "messages": [
        {
            "role": "user",
            "content": "write a haiku about lilypads"
        }
    ],
    "max_tokens": 2048,
    "temperature": 0.7
}'
```

**Response Codes**

* `200 OK`: Request successful, stream begins
* `400 Bad Request`: Invalid request parameters
* `401 Unauthorized`: Invalid or missing API key
* `404 Not Found`: Requested model not found
* `500 Internal Server Error`: Server error processing request

**Response Object Fields**

The delta event data contains the following fields:

| Field                  | Description                                     |
| ---------------------- | ----------------------------------------------- |
| `model`                | The model used for generation                   |
| `created_at`           | Timestamp when the response was created         |
| `message`              | Contains the assistant's response               |
| `message.role`         | Always "assistant" for responses                |
| `message.content`      | The generated text content                      |
| `done_reason`          | Reason for completion (e.g., "stop", "length")  |
| `done`                 | Boolean indicating if generation is complete    |
| `total_duration`       | Total processing time in nanoseconds            |
| `load_duration`        | Time taken to load the model in nanoseconds     |
| `prompt_eval_count`    | Number of tokens in the prompt                  |
| `prompt_eval_duration` | Time taken to process the prompt in nanoseconds |
| `eval_count`           | Number of tokens generated                      |
| `eval_duration`        | Time taken for generation in nanoseconds        |

**Conversation Context**

The API supports multi-turn conversations by including previous messages in the request:

```json
{
    "model": "llama2:7b",
    "messages": [
        {
            "role": "user",
            "content": "write a haiku about lilypads"
        },
        {
            "role": "assistant",
            "content": "Lily pads dance\nOn the water's gentle lap\nSerene beauty"
        },
        {
            "role": "user",
            "content": "Now write one about frogs"
        }
    ],
    "max_tokens": 2048,
    "temperature": 0.7
}
```

This allows for contextual follow-up questions and maintaining conversation history.

#### API Calls

This code enables us to communicate directly with the Lilypad Solver. As we progress towards mainnet, Solver will have functionality to enable jobs to submit information and do authorization with smart contract calls.

* First, post a job to Ollama Completions (a one-shot inference command to an LLM).

```sh
curl -X POST "https://anura-testnet.lilypad.tech/api/v1/chat/completions" \
-H "Content-Type: application/json" \
-H "X-API-Key: your_api_key_here" \
-d '{
    "model": "llama2",
    "messages": [{"role": "user", "content": "your prompt here"}],
    "max_tokens": 100,
    "temperature": 0.7
}'
```

* You should see messages like `Job status:1`, which mean the deal is agreed on the Lilypad network. Job status:2 means results are ready (though they should be sent immediately).

#### Get Status/Details of a Job

You can use another terminal to check job status while the job is running.

```
curl -X GET "https://anura-testnet.lilypad.tech/api/v1/jobs/{job_id}" \
-H "Content-Type: application/json" \
-H "X-API-Key: your_api_key_here"
```

#### Get Outputs from a Job

Once your job has run, you should get output like this:

```
data: {
    "id": "cmpl-e654be2df70700d27c155d4d",
    "object": "text_completion",
    "created": 1738614839,
    "model": "llama2",
    "choices": [{
        "text": "<output text here>
        "finish_reason": "stop"
    }]
}
```
