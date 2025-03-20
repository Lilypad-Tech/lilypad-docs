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
    "content": "what order do frogs belong to?"
  }],
  "temperature": 0.6
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

{% hint style="info" %}
<mark style="color:red;">\*</mark> = **Required**
{% endhint %}

#### Streaming Chat Completions

`POST /api/v1/chat/completions`

This endpoint provides a streaming interface for chat completions using Server-Sent Events (SSE).

**Request Headers**

* `Content-Type: application/json`<mark style="color:red;">\*</mark>
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
      "content": "what order do frogs belong to?"
    }
  ],
  "temperature": 0.6
}
```

<table><thead><tr><th width="117">Parameter</th><th width="515.5">Description</th><th width="105.5">Type</th></tr></thead><tbody><tr><td><code>model</code><mark style="color:red;">*</mark></td><td>Model ID used to generate the response (e.g. <code>deepseek-r1:7b</code>). <strong>Required</strong>.</td><td><code>string</code></td></tr><tr><td><code>messages</code><mark style="color:red;">*</mark></td><td>A list of messages comprising the conversation so far. <strong>Required</strong>.</td><td>array</td></tr></tbody></table>

<details>

<summary>Optional Parameters and Default Values</summary>

<table><thead><tr><th width="197">Paraneter</th><th width="404">Description</th><th width="83.5">Default</th></tr></thead><tbody><tr><td><code>frequency_penalty</code></td><td>Number between <code>-2.0</code> and <code>2.0</code>. Positive values penalize new tokens based on their existing frequency in the text so far, decreasing the model's likelihood to repeat the same line verbatim.</td><td><code>0</code></td></tr><tr><td><code>max_tokens</code></td><td>The maximum number of tokens that can be generated in the chat completion.</td><td></td></tr><tr><td><code>presence_penalty</code></td><td>Number between <code>-2.0</code> and <code>2.0</code>. Positive values penalize new tokens based on whether they appear in the text so far, increasing the model's likelihood to talk about new topics.</td><td><code>0</code></td></tr><tr><td><code>response_format</code></td><td>An object specifying the format that the model must output. <a href="https://platform.openai.com/docs/api-reference/introduction">Learn more</a>.</td><td></td></tr><tr><td><code>seed</code></td><td>If specified, our system will make a best effort to sample deterministically, such that repeated requests with the same <code>seed</code> and parameters should return the same result. Determinism is not guaranteed, and you should refer to the <code>system_fingerprint</code> response parameter to monitor changes in the backend.</td><td><code>null</code></td></tr><tr><td><code>stop</code></td><td>Up to 4 sequences where the API will stop generating further tokens. The returned text will not contain the stop sequence.</td><td></td></tr><tr><td><code>stream</code></td><td>If set to true, the model response data will be streamed to the client as it is generated using <a href="https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events/Using_server-sent_events#Event_stream_format">server-sent events</a>.</td><td><code>false</code></td></tr><tr><td><code>stream_options</code></td><td>Options for streaming response. Only set this when you set <code>stream: true</code>.</td><td><code>null</code></td></tr><tr><td><code>temperature</code></td><td>What sampling temperature to use, between <code>0</code> and <code>2</code>. Higher values like <code>0.8</code> will make the output more random, while lower values like <code>0.2</code> will make it more focused and deterministic. We generally recommend altering this or <code>top_p</code> but not both.</td><td><code>1</code></td></tr><tr><td><code>tools</code></td><td>A list of tools the model may call. Currently, only functions are supported as a tool. Use this to provide a list of functions the model may generate JSON inputs for. A max of 128 functions are supported. <a href="https://platform.openai.com/docs/api-reference/chat/create#chat-create-tools">Learn more</a>.</td><td></td></tr><tr><td><code>top_p</code></td><td><p>An alternative to sampling with <code>temperature</code>, called nucleus sampling, where the model considers the results of the tokens with <code>top_p</code> probability mass. So <code>0.1</code> means only the tokens comprising the top 10% probability mass are considered.</p><p></p><p>We generally recommend altering this or <code>temperature</code> but not both.</p></td><td><code>1</code></td></tr></tbody></table>

</details>

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
    "temperature": 0.6
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
