---
description: Anura, Lilypad's official AI inference API
---

# Inference API

## Getting Started

Use Anura to start running AI inference job modules on Lilypad's decentralized compute network:

1. Get an API key from the [Anura website](https://anura.lilypad.tech/).

### Get Started with Text Generation

1. Find which models we support:

```sh
curl GET "https://anura-testnet.lilypad.tech/api/v1/models" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_API_KEY"
```

2. Choose a model, customize your request and fire away:

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
  "stream": true,
  "temperature": 0.6
}'
```

### Get Started with Image Generation

1. Find which models we support:

```bash
curl GET "https://anura-testnet.lilypad.tech/api/v1/image/models" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_API_KEY"
```

2. Choose a model and generate your first image

```bash
curl -X POST https://anura-testnet.lilypad.tech/api/v1/image/generate \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -d '{"prompt": "A spaceship parked on a lilypad", "model": "sdxl-turbo"}' \
  --output spaceship.png
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

### Rate limits

Currently the rate limit for the api is set to 20 calls per second

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

#### Chat Completions

`POST /api/v1/chat/completions`&#x20;

**Note**: Due to the decentralized nature of the Lilypad Network we recommend using the streaming variant where possible at this time

This endpoint provides both a streaming interface using Server-Sent Events (SSE) and non-streaming interface for chat completions which is compliant with the OpenAI specification.  This means that you can plug and play Anura using the OpenAI SDK by simply passing in the Anura Url and API Key into your client like so:

```typescript
import OpenAI from 'openai';

const client = new OpenAI({
    baseURL: 'https://anura-testnet.lilypad.tech/api/v1',
    apiKey: process.env.ANURA_API_KEY || '',
});

const completion = await client.chat.completions.create({
  model: 'llama3.1:8b',
  messages: [
    { role: 'system', content: 'You are a helpful AI assistant.' },
    { role: 'user', content: 'Are semicolons optional in JavaScript?' },
  ],
});

return completion.choices[0].message.content;
```

**Request Headers**

* `Content-Type: application/json`<mark style="color:red;">\*</mark>
* `Accept: text/event-stream` (recommended for streaming)
* `Authorization: Bearer YOUR_API_KEY`<mark style="color:red;">\*</mark>

**Request Parameters**

<table><thead><tr><th width="117">Parameter</th><th width="515.5">Description</th><th width="105.5">Type</th></tr></thead><tbody><tr><td><code>model</code><mark style="color:red;">*</mark></td><td>Model ID used to generate the response (e.g. <code>deepseek-r1:7b</code>). <strong>Required</strong>.</td><td><code>string</code></td></tr><tr><td><code>messages</code><mark style="color:red;">*</mark></td><td>A list of messages comprising the conversation so far. <strong>Required</strong>.</td><td>array</td></tr></tbody></table>

<details>

<summary>Optional Parameters and Default Values</summary>

<table><thead><tr><th width="197">Paraneter</th><th width="404">Description</th><th width="83.5">Default</th></tr></thead><tbody><tr><td><code>frequency_penalty</code></td><td>Number between <code>-2.0</code> and <code>2.0</code>. Positive values penalize new tokens based on their existing frequency in the text so far, decreasing the model's likelihood to repeat the same line verbatim.</td><td><code>0</code></td></tr><tr><td><code>max_tokens</code></td><td>The maximum number of tokens that can be generated in the chat completion.</td><td></td></tr><tr><td><code>presence_penalty</code></td><td>Number between <code>-2.0</code> and <code>2.0</code>. Positive values penalize new tokens based on whether they appear in the text so far, increasing the model's likelihood to talk about new topics.</td><td><code>0</code></td></tr><tr><td><code>response_format</code></td><td>An object specifying the format that the model must output. <a href="https://platform.openai.com/docs/api-reference/introduction">Learn more</a>.</td><td></td></tr><tr><td><code>seed</code></td><td>If specified, our system will make a best effort to sample deterministically, such that repeated requests with the same <code>seed</code> and parameters should return the same result. Determinism is not guaranteed, and you should refer to the <code>system_fingerprint</code> response parameter to monitor changes in the backend.</td><td><code>null</code></td></tr><tr><td><code>stop</code></td><td>Up to 4 sequences where the API will stop generating further tokens. The returned text will not contain the stop sequence.</td><td></td></tr><tr><td><code>stream</code></td><td>If set to true, the model response data will be streamed to the client as it is generated using <a href="https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events/Using_server-sent_events#Event_stream_format">server-sent events</a>.</td><td><code>false</code></td></tr><tr><td><code>stream_options</code></td><td>Options for streaming response. Only set this when you set <code>stream: true</code>.</td><td><code>null</code></td></tr><tr><td><code>temperature</code></td><td>What sampling temperature to use, between <code>0</code> and <code>2</code>. Higher values like <code>0.8</code> will make the output more random, while lower values like <code>0.2</code> will make it more focused and deterministic. We generally recommend altering this or <code>top_p</code> but not both.</td><td><code>1</code></td></tr><tr><td><code>tools</code></td><td><p>A list of tools the model may call. Currently, only functions are supported as a tool. Use this to provide a list of functions the model may generate JSON inputs for. A max of 128 functions are supported. At the moment only a select number models support tooling including:</p><ul><li>llama3.1:8b</li><li>qwen2.5:7b</li><li>qwen2.5-coder:7b</li><li>phi4-mini:3.8b</li><li>mistral:7b</li></ul></td><td></td></tr><tr><td><code>top_p</code></td><td><p>An alternative to sampling with <code>temperature</code>, called nucleus sampling, where the model considers the results of the tokens with <code>top_p</code> probability mass. So <code>0.1</code> means only the tokens comprising the top 10% probability mass are considered.</p><p></p><p>We generally recommend altering this or <code>temperature</code> but not both.</p></td><td><code>1</code></td></tr></tbody></table>

</details>

**Request Body (non-streaming)**

```json
{
  "model": "llama3.1:8b",
  "messages": [
    {
      "role": "system",
      "content": "you are a helpful AI assistant"
    },
    {
      "role": "user",
      "content": "write a haiku about lilypads"
    }
  ],
  "temperature": 0.6
}
```

**Response Format (non-streaming)**

The response is an OpenAI ChatCompletion Object with the following format:

```json
{
    "id": "jobId-Qmds4fif8RLVKrSKfWVGHe7fDkBwizzV5omd3kPSnc8Xdf-jobState-ResultsSubmitted",
    "object": "chat.completion",
    "created": 1742509938,
    "model": "llama3.1:8b",
    "system_fingerprint": "",
    "choices": [
        {
            "index": 0,
            "message": {
                "role": "assistant",
                "content": "Lily pads dance\nOn the water's gentle lap\nSerene beauty"
            },
            "finish_reason": "stop"
        }
    ],
    "usage": {
        "prompt_tokens": 2048,
        "completion_tokens": 184,
        "total_tokens": 2232
    }
}
```

**Response Codes**

* `200 OK`: Request successful, stream begins
* `400 Bad Request`: Invalid request parameters
* `401 Unauthorized`: Invalid or missing API key
* `404 Not Found`: Requested model not found
* `500 Internal Server Error`: Server error processing request

**Response Object Fields**

The response data contains the following fields:

<table><thead><tr><th width="383">Field</th><th>Description</th></tr></thead><tbody><tr><td><code>id</code></td><td>A unique identifier for the chat completion</td></tr><tr><td><code>object</code></td><td>The object type</td></tr><tr><td><code>created</code></td><td>Timestamp when the response was created</td></tr><tr><td><code>model</code></td><td>The model used for generation</td></tr><tr><td><code>choices</code></td><td>The array containing the assistant's response</td></tr><tr><td><code>choices[0].message.role</code></td><td>Always "assistant" for responses</td></tr><tr><td><code>choices[0].message.content</code></td><td>The generated text content</td></tr><tr><td><code>choices[0].message.tool_calls</code></td><td>The array containing the corresponding tool response objects (this is only applicable if you make a tool request)</td></tr><tr><td><code>choices[0].finish_reason</code></td><td>Reason for completion (e.g., "stop", "length")</td></tr><tr><td><code>usage.prompt_tokens</code></td><td>The number of tokens used in the prompt</td></tr><tr><td><code>usage.completion_tokens</code></td><td>The number of tokens in the generated completion</td></tr><tr><td><code>usage.total_tokens</code></td><td>The sum of the prompt_tokens and the completion_tokens</td></tr></tbody></table>

**Request Body (streaming)**

```json
{
  "model": "llama3.1:8b",
  "messages": [
    {
      "role": "system",
      "content": "you are a helpful AI assistant"
    },
    {
      "role": "user",
      "content": "write a haiku about lilypads"
    }
  ],
  "stream": true,
  "temperature": 0.6
```

**Response Format (streaming)**

The response is a stream of Server-Sent Events (SSE) with chunked OpenAI ChatCompletion objects with the following format:

**Initial response**:

```json
data: {
    "id": "jobId-QmZXDGS7m8VuJrURqsKvByGKHCM749NMVFmEA2hH2DtDWs-jobState-DealNegotiating",
    "object": "chat.completion.chunk",
    "created": 1742425132,
    "model": "llama3.1:8b",
    "system_fingerprint": "",
    "choices": [
        {
            "index": 0,
            "delta": {
                "role": "assistant",
                "content": null
            },
            "finish_reason": null
        }
    ],
    "usage": {
        "prompt_tokens": 0,
        "completion_tokens": 0,
        "total_tokens": 0
    }
}
```

**Processing updates**:

```json
data: {
    "id": "jobId-QmZXDGS7m8VuJrURqsKvByGKHCM749NMVFmEA2hH2DtDWs-jobState-DealAgreed",
    "object": "chat.completion.chunk",
    "created": 1742425135,
    "model": "llama3.1:8b",
    "system_fingerprint": "",
    "choices": [
        {
            "index": 0,
            "delta": {
                "role": "assistant",
                "content": null
            },
            "finish_reason": null
        }
    ],
    "usage": {
        "prompt_tokens": 0,
        "completion_tokens": 0,
        "total_tokens": 0
    }
}
```

**Content delivery**:

```json
data: {
    "id": "jobId-QmZXDGS7m8VuJrURqsKvByGKHCM749NMVFmEA2hH2DtDWs-jobState-ResultsSubmitted",
    "object": "chat.completion.chunk",
    "created": 1742425147,
    "model": "llama3.1:8b",
    "system_fingerprint": "",
    "choices": [
        {
            "index": 0,
            "delta": {
                "role": "assistant",
                "content": "Lily pads dance\nOn the water's gentle lap\nSerene beauty"
            },
            "finish_reason": "stop"
        }
    ],
    "usage": {
        "prompt_tokens": 2048,
        "completion_tokens": 456,
        "total_tokens": 2504
    }
}
```

**Completion marker**:

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

<table><thead><tr><th width="383">Field</th><th>Description</th></tr></thead><tbody><tr><td><code>id</code></td><td>A unique identifier for the chat completion</td></tr><tr><td><code>object</code></td><td>The object type</td></tr><tr><td><code>created</code></td><td>Timestamp when the response was created</td></tr><tr><td><code>model</code></td><td>The model used for generation</td></tr><tr><td><code>choices</code></td><td>The array containing the assistant's response</td></tr><tr><td><code>choices[0].delta.role</code></td><td>Always "assistant" for responses</td></tr><tr><td><code>choices[0].delta.content</code></td><td>The generated text content</td></tr><tr><td><code>choices[0].delta.tool_calls</code></td><td>The array containing the corresponding tool response objects (this is only applicable if you make a tool request)</td></tr><tr><td><code>choices[0].finish_reason</code></td><td>Reason for completion (e.g., "stop", "length")</td></tr><tr><td><code>usage.prompt_tokens</code></td><td>The number of tokens used in the prompt</td></tr><tr><td><code>usage.completion_tokens</code></td><td>The number of tokens in the generated completion</td></tr><tr><td><code>usage.total_tokens</code></td><td>The sum of the prompt_tokens and the completion_tokens</td></tr></tbody></table>

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

**Tooling Calls**&#x20;

The Anura chat completions endpoint supports requests with tooling allowing for function calling through many popular AI frameworks and sdks. &#x20;

At the moment only a select number models support tooling including:

* llama3.1:8b
* qwen2.5:7b
* qwen2.5-coder:7b
* phi4-mini:3.8b
* mistral:7b

Below is a sample request and response

**Request:**

```json
{
    "model": "mistral:7b",
    "messages": [
        {
            "role": "system",
            "content": "you are a helpful AI assistant"
        },
        {
            "role": "user",
            "content": "What's the weather in Tokyo?"
        }
    ],
    "tools": [
        {
            "type": "function",
            "function": {
                "name": "get_current_weather",
                "description": "Get the current weather for a city",
                "parameters": {
                    "type": "object",
                    "properties": {
                        "city": {
                            "type": "string",
                            "description": "The name of the city"
                        }
                    },
                    "required": [
                        "city"
                    ]
                }
            }
        }
    ],
    "temperature": 0.6,
    "stream": false
}
```

**Response:**

```json
{
    "id": "jobId-QmTm3E4oEu4TYp1FLykHdnrkPyX6cLz2UUYS45YrmrzqdN-jobState-ResultsSubmitted",
    "object": "chat.completion",
    "created": 1742790608,
    "model": "mistral:7b",
    "system_fingerprint": "",
    "choices": [
        {
            "index": 0,
            "message": {
                "role": "assistant",
                "content": "",
                "tool_calls": [
                    {
                        "id": "call_syyia0kt",
                        "index": 0,
                        "type": "function",
                        "function": {
                            "name": "get_current_weather",
                            "arguments": "{\"city\":\"Tokyo\"}"
                        }
                    }
                ]
            },
            "finish_reason": "tool_calls"
        }
    ],
    "usage": {
        "prompt_tokens": 88,
        "completion_tokens": 22,
        "total_tokens": 110
    }
}
```

### Image Generation

The Anura API enables you to run stable diffusion jobs to generate images executed through our decentralized compute network. It's really easy to get started generating your own generative AI art using Anura through the endpoints we provide.

**Retrieve the list supported image generation models**

`GET /api/v1/image/models`&#x20;

**Request Headers**

* `Content-Type: application/json`<mark style="color:red;">\*</mark>
* `Authorization: Bearer YOUR_API_KEY`<mark style="color:red;">\*</mark>

**Request Sample**

```bash
curl -X GET "https://anura-testnet.lilypad.tech/api/v1/image/models" \
-H "Content-Type: application/json" \
-H "Authorization: Bearer your_api_key_here"
```

**Response**

```json
{
    "data": {
        "models": [
            "sdxl-turbo"
        ]
    },
    "message": "Retrieved models successfully",
    "status": 200
}
```

**Response Codes**

* `200 OK`: Request successful, stream begins
* `400 Bad Request`: Invalid request parameters
* `401 Unauthorized`: Invalid or missing API key
* `404 Not Found`: Requested model not found
* `500 Internal Server Error`: Server error processing request

Currently we support `sdxl-turbo`; however, we are always adding new models, so stay tuned!

**Generate an AI Image**

`POST /api/v1/image/generate`

**Request Headers**

* `Content-Type: application/json`<mark style="color:red;">\*</mark>
* `Authorization: Bearer YOUR_API_KEY`<mark style="color:red;">\*</mark>

**Request Parameters**

<table><thead><tr><th width="117">Parameter</th><th width="515.5">Description</th><th width="105.5">Type</th></tr></thead><tbody><tr><td><code>model</code><mark style="color:red;">*</mark></td><td>Model ID used to generate the response (e.g. <code>sdxl-turbo</code>). <strong>Required</strong>.</td><td><code>string</code></td></tr><tr><td><code>prompt</code><mark style="color:red;">*</mark></td><td>The prompt input to generate your image from (max limit of 1000 characters)</td><td><code>string</code></td></tr></tbody></table>

**Request Sample**

```json
{
    "prompt": "A spaceship parked on a lilypad",
    "model": "sdxl-turbo"
}
```

Alternatively you can also make the same request through a curl command and have the image be output to a file on your machine

```bash
curl -X POST https://anura-testnet.lilypad.tech/api/v1/image/generate \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer your_api_key_here" \
  -d '{"prompt": "A spaceship parked on a lilypad", "model": "sdxl-turbo"}' \
  --output spaceship.png
```

The result of running this command will be the creation of the `spaceship.png` file in the directory you ran the command from.&#x20;

**Response**

This endpoint will return the raw bytes value of the image that was generated which you can output to a file (like shown in the curl command above) or place it in a buffer to write to a file in your app, e.g.&#x20;

```javascript
const fs = require("fs");
const fetch = require("node-fetch");

async function generateImage() {
  const response = await fetch("https://anura-testnet.lilypad.tech/api/v1/image/generate", {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
      "Authorization": "Bearer your_api_key_here"
    },
    body: JSON.stringify({
      prompt: "A spaceship parked on a lilypad",
      model: "sdxl-turbo"
    }),
  });
  
  if (!response.ok) {
    console.error(`Error generating image: StatusCode: ${response.status} Error: ${response.message}`);
    return;
  }

  const buffer = await response.buffer();
  fs.writeFileSync("spaceship.png", buffer);
}

generateImage();
```

**Note:** Should you ever need to know what the corresponding Job Offer ID for image generation, it is provided in the response header as `Job-Offer-Id`

**Response Codes**

* `200 OK`: Request successful, stream begins
* `400 Bad Request`: Invalid request parameters
* `401 Unauthorized`: Invalid or missing API key
* `404 Not Found`: Requested model not found
* `500 Internal Server Error`: Server error processing request

### Web Search

The Anura API provides developers with a web search capability enabling you to add a powerful tool to your AI Agent building arsenal. LLM's are only as great as their training data and are taken to the next level when provided with additional context from the web. With web search you can power your AI Agent workflow with live web search data providing your LLM the most up to date information on the latest on goings in the world.

It's easy to get started searching the web through the Anura API using our endpoint:

`POST /api/v1/websearch`

**Request Headers**

* `Content-Type: application/json`<mark style="color:red;">\*</mark>
* `Authorization: Bearer YOUR_API_KEY`<mark style="color:red;">\*</mark>

**Request Parameters**

<table><thead><tr><th width="193.38671875">Parameter</th><th width="515.5">Description</th><th width="91.625">Type</th></tr></thead><tbody><tr><td><code>query</code><mark style="color:red;">*</mark></td><td>The web search query you wish to execute</td><td><code>string</code></td></tr><tr><td><code>number_of_results</code><mark style="color:red;">*</mark></td><td>The number of search results you want returned (limited to 1 to 10 inclusive)</td><td><code>number</code></td></tr></tbody></table>

**Request Sample**

```json
{
    "query": "What's the Lilypad Network?",
    "number_of_results" : 3
}
```

**Response Sample**

The response will include the following fields:

<table><thead><tr><th width="176.0234375">Field</th><th width="557.90234375">Description</th></tr></thead><tbody><tr><td><code>results</code></td><td>The array of search results where each result object is made up of the strings: <code>title</code>, <code>url</code> and <code>description</code></td></tr><tr><td><code>related_queries</code></td><td>An array of strings containing similar queries based on the one you supplied</td></tr><tr><td><code>count</code></td><td>The number of search results returned</td></tr></tbody></table>

```json
{
    "results": [
        {
            "title": "Lilypad Network",
            "url": "https://lilypad.tech",
            "description": "Lilypad Network Lilypad offers a seamless and efficient way to access the computing power you need for AI and other demanding tasks—no need to invest in expensive hardware or navigate complex cloud setups. Simply submit your job; our decentralized network connects you with the best available resources. Benefit from competitive pricing, secure ..."
        },
        {
            "title": "Lilypad Network - internet-scale off-chain distributed compute solution",
            "url": "https://blog.lilypadnetwork.org",
            "description": "Verifiable, truly internet-scale distributed compute network Efficient off-chain computation for AI & ML DataDAO computing The next frontier of web3. Follow. ... Check out the docs https://docs.lilypad.tech/lilypad! Lilypad Builder-verse! Devlin Rocha. 4 min read. Fuel the Future by Building on Lilypad and Accelerate Open Source AI. Alex Mirran."
        },
        {
            "title": "What is the Lilypad Decentralized Compute Network?",
            "url": "https://blog.lilypadnetwork.org/what-is-the-lilypad-decentralized-compute-network",
            "description": "Lilypad democratizes AI high-performance computing, offering affordable, scalable solutions for researchers and startups. Follow. Follow. What is the Lilypad Decentralized Compute Network? A Crowdsourced Network for HPC Tasks. Lindsay Walker"
        }
    ],
    "related_queries": [
        "Lilypad Tech",
        "LilyPad github",
        "Lilypad website",
        "Lilypad AI",
        "Lily pad Minecraft server",
        "Lilypad crypto",
        "LilyPad Arduino"
    ],
    "count": 3
}
```

**Response Codes**

* `200 OK`: Request successful, stream begins
* `400 Bad Request`: Invalid request parameters
* `401 Unauthorized`: Invalid or missing API key
* `404 Not Found`: Requested model not found
* `500 Internal Server Error`: Server error processing request

### Jobs

* `GET /api/v1/jobs/:id` - Get status and details of a specific job

#### Get Status/Details of a Job

You can use another terminal to check job status while the job is running.

```bash
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
