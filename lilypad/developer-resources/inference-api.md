---
description: Anura, Lilypad's official AI inference API
---

# Inference API

## Getting Started

Use Anura to start running AI inference job modules on Lilypad's decentralized compute network:

1. Get an API key from the [Anura website](https://anura.lilypad.tech/).
2. Find which models we support:

```sh
curl GET "https://anura-testnet.lilypad.tech/api/v1/models" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_API_KEY"
```

3. Choose a model and customize your request:

```sh
curl -X POST "https://anura-testnet.lilypad.tech/api/v1/chat/completions" \
-H "Content-Type: application/json" \
-H "Accept: text/event-stream" \
-H "Authorization: Bearer YOUR_API_KEY" \
-d '{
  "model": "MODEL_NAME:MODEL_VERSION",
  "messages": [{
    "role": "system",
    "content": "you are a helpful AI assistant"
  },
  {
    "role": "user",
    "content": "what taxonomic order are frogs classified under?"
  }],
  "stream": false,
  "options": {
    "temperature": 1.0
  }
}'
```

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

### Get Available Models

To see which models are available:

```
curl -X GET "https://anura-testnet.lilypad.tech/api/v1/models" \
-H "Content-Type: application/json" \
-H "Authorization: Bearer YOUR_API_KEY"
```

### Chat Completions API

#### Streaming Chat Completions

`POST /api/v1/chat/completions`

This endpoint provides a streaming interface for chat completions using Server-Sent Events (SSE).

**Request Headers**

* `Content-Type: application/json` (required)
* `Accept: text/event-stream` (recommended for streaming)
* `Authorization: Bearer YOUR_API_KEY`

**Request Body**

```json
{
  "model": "deepseek-r1:7b",
  "messages": [
    {
      "role": "system",
      "content": "you are a helpful AI assistant"
    },
    {
      "role": "user",
      "content": "what taxonomic order are frogs classified under?"
    }
  ],
  "stream": false,
  "options": {
    "temperature": 1.0
  }
}
```

<table><thead><tr><th width="143">Parameter</th><th width="521">Description</th><th width="307">Type</th></tr></thead><tbody><tr><td><code>model</code></td><td><strong>Required</strong>. ID of the model to use (e.g., "deepseek-r1:7b")</td><td>string</td></tr><tr><td><code>messages</code></td><td><strong>Required</strong>. Array of message objects representing the conversation</td><td>array</td></tr><tr><td><code>stream</code></td><td>Receive responses as streaming JSON objects or a single JSON object.</td><td>boolean</td></tr><tr><td><code>options</code></td><td>Additional model parameters listed in the table below</td><td>object</td></tr></tbody></table>

#### Valid Options Parameters and Default Values

<table><thead><tr><th width="165">Parameter</th><th width="498">Description</th><th>Default</th></tr></thead><tbody><tr><td>mirostat</td><td>Enable Mirostat sampling for controlling perplexity. (0 = disabled, 1 = Mirostat, 2 = Mirostat 2.0)</td><td><code>0</code></td></tr><tr><td>mirostat_eta</td><td>Influences how quickly the algorithm responds to feedback from the generated text. A lower learning rate will result in slower adjustments, while a higher learning rate will make the algorithm more responsive.</td><td><code>0.1</code></td></tr><tr><td>mirostat_tau</td><td>Controls the balance between coherence and diversity of the output. A lower value will result in more focused and coherent text.</td><td><code>5</code></td></tr><tr><td>num_ctx</td><td>Sets the size of the context window used to generate the next token.</td><td><code>2048</code></td></tr><tr><td>repeat_last_n</td><td>Sets how far back for the model to look back to prevent repetition. (0 = disabled, -1 = num_ctx)</td><td><code>64</code></td></tr><tr><td>repeat_penalty</td><td>Sets how strongly to penalize repetitions. A higher value (e.g., 1.5) will penalize repetitions more strongly, while a lower value (e.g., 0.9) will be more lenient.</td><td><code>1.1</code></td></tr><tr><td>temperature</td><td>The temperature of the model. Increasing the temperature will make the model answer more creatively.</td><td><code>0.8</code></td></tr><tr><td>seed</td><td>Sets the random number seed to use for generation. Setting this to a specific number will make the model generate the same text for the same prompt.</td><td><code>0</code></td></tr><tr><td>stop</td><td>Sets the stop sequences to use. When this pattern is encountered the LLM will stop generating text and return. Multiple stop patterns may be set by specifying multiple separate stop parameters in a modelfile.</td><td></td></tr><tr><td>num_predict</td><td>Maximum number of tokens to predict when generating text. (-1 = infinite generation)</td><td><code>-1</code></td></tr><tr><td>top_k</td><td>Reduces the probability of generating nonsense. A higher value (e.g. 100) will give more diverse answers, while a lower value (e.g. 10) will be more conservative.</td><td><code>40</code></td></tr><tr><td>top_p</td><td>Works together with top-k. A higher value (e.g., 0.95) will lead to more diverse text, while a lower value (e.g., 0.5) will generate more focused and conservative text.</td><td><code>0.9</code></td></tr><tr><td>min_p</td><td>Alternative to the top_p, and aims to ensure a balance of quality and variety. The parameter p represents the minimum probability for a token to be considered, relative to the probability of the most likely token. For example, with p=0.05 and the most likely token having a probability of 0.9, logits with a value less than 0.045 are filtered out.</td><td><code>0.0</code></td></tr></tbody></table>

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

**Response Codes**

* `200 OK`: Request successful, stream begins
* `400 Bad Request`: Invalid request parameters
* `401 Unauthorized`: Invalid or missing API key
* `404 Not Found`: Requested model not found
* `500 Internal Server Error`: Server error processing request

**Response Object Fields**

The delta event data contains the following fields:

<table><thead><tr><th width="383">Field</th><th>Description</th></tr></thead><tbody><tr><td><code>model</code></td><td>The model used for generation</td></tr><tr><td><code>created_at</code></td><td>Timestamp when the response was created</td></tr><tr><td><code>message</code></td><td>Contains the assistant's response</td></tr><tr><td><code>message.role</code></td><td>Always "assistant" for responses</td></tr><tr><td><code>message.content</code></td><td>The generated text content</td></tr><tr><td><code>done_reason</code></td><td>Reason for completion (e.g., "stop", "length")</td></tr><tr><td><code>done</code></td><td>Boolean indicating if generation is complete</td></tr><tr><td><code>total_duration</code></td><td>Total processing time in nanoseconds</td></tr><tr><td><code>load_duration</code></td><td>Time taken to load the model in nanoseconds</td></tr><tr><td><code>prompt_eval_count</code></td><td>Number of tokens in the prompt</td></tr><tr><td><code>prompt_eval_duration</code></td><td>Time taken to process the prompt in nanoseconds</td></tr><tr><td><code>eval_count</code></td><td>Number of tokens generated</td></tr><tr><td><code>eval_duration</code></td><td>Time taken for generation in nanoseconds</td></tr></tbody></table>

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
    "stream": false,
    "options": {
        "temperature": 1.0
    }
}
```

This allows for contextual follow-up questions and maintaining conversation history.

### Jobs

* `GET /api/v1/jobs/:id` - Get status and details of a specific job

#### Get Status/Details of a Job

You can use another terminal to check job status while the job is running.

```
curl -X GET "https://anura-testnet.lilypad.tech/api/v1/jobs/{job_id}" \
-H "Content-Type: application/json" \
-H "Authorization: Bearer your_api_key_here"
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

### Cowsay

* `POST /api/v1/cowsay` - Create a new cowsay job
  * Request body: `{"message": "text to display"}`
* `GET /api/v1/cowsay/:id/results` - Get results of a cowsay job
