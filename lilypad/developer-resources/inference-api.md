---
description: Anura, Lilypad's official AI inference API
---

# Inference API

## Getting Started

Use Anura to start running AI inference job modules on Lilypad's decentralized compute network:

1. Get an API key from the [Anura website](https://anura.lilypad.tech/).



### NEW! See All Models Available (GraphQL)

You can run the following endpoints to view all Anura-supported models on the Lilypad network.\
\
These queries are available as graphQL queries [here](https://lilypad-quest-api.vercel.app/api/graphql).\
\
You can also view all available queries by opening [Apollo Server](https://studio.apollographql.com/sandbox/explorer) and putting this url in:&#x20;

```
https://lilypad-model-api.vercel.app/api/graphql
```

#### Curl Requests

Get all Models:

```bash
curl -X POST https://lilypad-model-api.vercel.app/api/graphql \
  -H "Content-Type: application/json" \
  -d '{"query": "{ allModels { id name category } }"}'
```

Response example:

```json
{
  "data": {
    "allModels": [
      {
        "id": "llama3.1:8b",
        "name": "Llama 3.1 8B",
        "category": "text-generation"
      },
      {
        "id": "sdxl-turbo",
        "name": "SDXL Turbo", 
        "category": "image-generation"
      }
    ]
  }
}
```

You can also fetch a selection of multiple model types using the following endpoint:

```bash
curl -X POST https://lilypad-model-api.vercel.app/api/graphql \
  -H "Content-Type: application/json" \
  -d '{"query": "{ chatModels { id name supportsTools } imageModels { id name maxPrompt } }"}'
```

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

#### Tooling calls

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

#### Vision Support

The chat completions API also supports vision requests allowing for image-to-text search against a base64 encoded image. This will allow you to make a query against an image asking a LLM what the image is or about particular details around it. Currently vision is only supported via the following models (more coming soon):

* llava:7b
* gemma3:4b

Additionally, the vision capability is limited by the following constraints:

* Images must only be base64 encoded (you cannot pass a link to an image at this time)
* Maximum image size is 512px x 512px
* Support for JPEG or PNG format

**Request:**

```json
{
    "model": "llava:7b",
    "messages": [
        {
            "role": "system",
            "content": "you are a helpful AI assistant"
        },
        {
            "role": "user",
            "content": [
                {
                    "type": "text",
                    "text": "What's in this image?"
                },
                {
                    "type": "image_url",
                    "image_url": "data:image/png;base64,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"
                }
            ]
        }
    ],
    "temperature": 0.6,
    "stream": false
}
```

**Response:**

```json
{
    "id": "jobId-QmcJohc71DrHnVbXbLRt7drDyPSU1dyNTskU3a1yRR7zBu-jobState-ResultsSubmitted",
    "object": "chat.completion",
    "created": 1744411025,
    "model": "llava:7b",
    "system_fingerprint": "",
    "choices": [
        {
            "index": 0,
            "message": {
                "role": "assistant",
                "content": " The image shows a creature that appears to be a blend of a frog and some form of robotic or mechanical structure. It has the body shape of a frog, with prominent eyes and limbs. The creature is depicted with a sleek, technologically advanced design, featuring metallic parts and futuristic elements. The color scheme includes blues, blacks, and greens, giving it a high-tech aesthetic. This creature could be an example of concept art for a video game or science fiction story. "
            },
            "finish_reason": "stop"
        }
    ],
    "usage": {
        "prompt_tokens": 600,
        "completion_tokens": 106,
        "total_tokens": 706
    }
}
```

### Embeddings

Use the embeddings endpoint to compute embeddings for user queries supported by the `nomic-embed-text` model. This endpoint is OpenAI compliant which means you can use it with the OpenAI SDK (see the end of the Embeddings section for a code example)

**Endpoint**

`POST /api/v1/embeddings`

**Request Headers**

* `Content-Type: application/json`<mark style="color:red;">\*</mark>
* `Authorization: Bearer YOUR_API_KEY`<mark style="color:red;">\*</mark>

**Request Parameters**

<table><thead><tr><th width="117">Parameter</th><th width="365.47265625">Description</th><th width="264.9296875">Type</th></tr></thead><tbody><tr><td><code>model</code><mark style="color:red;">*</mark></td><td>Model ID used to generate the response (e.g. <code>nomic-embed-text</code>). <strong>Required</strong>.</td><td><code>string</code></td></tr><tr><td><code>input</code><mark style="color:red;">*</mark></td><td>The input to create embeddings from. This can be either a single string or an array of strings. <strong>Required</strong></td><td><code>string or array of strings</code></td></tr></tbody></table>

**Request Sample (single input)**

```json
{
    "model": "nomic-embed-text",
    "input": "why is the sky blue?",
}
```

**Response Sample (single input)**

```json
{
    "object": "list",
    "data": [
        {
            "object": "embedding",
            "embedding": [
                0.009716383,
                0.0443843,
                -0.14053911,
                0.0011783413,
                0.031978477,
                0.1073299,
                -0.008574652,
                ...,
                -0.009498251,
                -0.041506674,
                0.020256031
            ],
            "index": 0
        },
    ],
    "model": "nomic-embed-text",
    "usage": {
        "prompt_tokens": 6,
        "total_tokens": 6
    }
}
```

**Request Sample (multiple input)**

```json
{
    "model": "nomic-embed-text",
    "input": ["why is the sky blue?", "why is the grass green?"],
}
```

**Response Sample (multiple input)**

```json
{
    "object": "list",
    "data": [
        {
            "object": "embedding",
            "embedding": [
                0.009716383,
                0.0443843,
                -0.14053911,
                0.0011783413,
                0.031978477,
                0.1073299,
                -0.008574652,
                ...,
                -0.009498251,
                -0.041506674,
                0.020256031
            ],
            "index": 0
        },
        {
            "object": "embedding",
            "embedding": [
               0.028126348,
                0.043248065,
                -0.18586768,
                0.03491587,
                0.055507593,
                0.12088179,
                -0.009062298
                ...,
                -0.035023507,
                -0.07451658,
                0.011851714
            ],
            "index": 1
        }

    ],
    "model": "nomic-embed-text",
    "usage": {
        "prompt_tokens": 12,
        "total_tokens": 12
    }
}
```

**Response Codes**

* `200 OK`: Request successful, stream begins
* `400 Bad Request`: Invalid request parameters
* `401 Unauthorized`: Invalid or missing API key
* `404 Not Found`: Requested model not found
* `500 Internal Server Error`: Server error processing request

**Example Code using the OpenAI SDK**

```typescript
import OpenAI from 'openai'

const openai = new OpenAI({
  baseURL: 'https://anura-testnet.lilypad.tech/api/v1/',
  apiKey: 'YOUR_KEY_HERE',
})

const embedding = await openai.embeddings.create({
  model: "nomic-embed-text",
  input: ["why is the sky blue?", "why is the grass green?"],
})
```

### Image Generation

The Anura API enables you to run stable diffusion jobs to generate images executed through our decentralized compute network. It's really easy to get started generating your own generative AI art using Anura through the endpoints we provide.

**Retrieve the list supported image generation models**

`GET /api/v1/image/models`&#x20;

**Request Headers**

* `Content-Type: application/json`<mark style="color:red;">\*</mark>
* `Authorization: Bearer YOUR_API_KEY`<mark style="color:red;">\*</mark>

**Request Parameters**

<table><thead><tr><th width="117">Parameter</th><th width="515.5">Description</th><th width="105.5">Type</th></tr></thead><tbody><tr><td><code>model</code><mark style="color:red;">*</mark></td><td>Model ID used to generate the response (e.g. <code>sdxl-turbo</code>). <strong>Required</strong>.</td><td><code>string</code></td></tr><tr><td><code>prompt</code><mark style="color:red;">*</mark></td><td>The prompt input to generate your image from (max limit of 1000 characters)</td><td><code>string</code></td></tr></tbody></table>

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

### Video Generation

The Anura API enables you to run long running jobs to generate videos executed through our decentralized compute network. It's really easy to get started generating your own videos using Anura through the endpoints we provide.&#x20;

**Note**: Video generation can take anywhere between 4-8 mins to produce a video

**Retrieve the list supported video generation models**

`GET /api/v1/video/models`&#x20;

Currently we support `wan2.1`; however, we are always adding new models, so stay tuned!

**Request Headers**

* `Content-Type: application/json`<mark style="color:red;">\*</mark>
* `Authorization: Bearer YOUR_API_KEY`<mark style="color:red;">\*</mark>

**Request Sample**

```bash
curl -X GET "https://anura-testnet.lilypad.tech/api/v1/video/models" \
-H "Content-Type: application/json" \
-H "Authorization: Bearer your_api_key_here"
```

**Response**

```json
{
    "data": {
        "models": [
            "wan2.1"
        ]
    },
    "message": "Retrieved models successfully",
    "status": 200
}
```

**Response Codes**

* `200 OK`: Request successful
* `401 Unauthorized`: Invalid or missing API key
* `500 Internal Server Error`: Server error processing request

**Send out a request to create an AI generated video**

`POST /api/v1/video/create-job`

**Request Headers**

* `Content-Type: application/json`<mark style="color:red;">\*</mark>
* `Authorization: Bearer YOUR_API_KEY`<mark style="color:red;">\*</mark>

**Request Parameters**

<table><thead><tr><th width="166.12890625">Parameter</th><th width="486.68359375">Description</th><th width="105.5">Type</th></tr></thead><tbody><tr><td><code>model</code><mark style="color:red;">*</mark></td><td>Model used to generate the response (e.g. <code>wan2.1</code>). <strong>Required</strong>.</td><td><code>string</code></td></tr><tr><td><code>prompt</code><mark style="color:red;">*</mark></td><td>The prompt input to generate your video from (max limit of 1000 characters). <strong>Required</strong>.</td><td><code>string</code></td></tr><tr><td><code>negative_prompt</code></td><td>An optional field to specify to the model what to <strong>exclude</strong> from the generated scene</td><td><code>string</code></td></tr></tbody></table>

**Request Sample**

```json
{
    "prompt": "Two frogs sit on a lilypad, animatedly discussing the wonders and quirks of AI agents. As they ponder whether these digital beings can truly understand their froggy lives, the serene pond serves as a backdrop to their lively conversation.",
    "negative_prompt": "Dull colors, grainy texture, washed-out details, static frames, incorrect lighting, unnatural shadows, distorted faces, artifacts, low-resolution elements, flickering, blurry motion, repetitive patterns, unrealistic reflections, overly simplistic backgrounds, three legged people, walking backwards.",
    "model": "wan2.1"
}
```

**Response**

This endpoint will return an `job_offer_id` which is an unique identifier corresponding to the job that's running to create your video. What you'll want to do with this id is pass it into our `/video/results` endpoint (see below) which will provide you the output as a `webp` file or report that the job is still running. In the latter case, you then can continue to call the endpoint at a later time to eventually retrieve your video. As mentioned in the beginning of this section, video generation can take anywhere between 4-8 mins to complete.

```json
{
    "status": 200,
    "message": "Video job created successfully",
    "data": {
        "job_offer_id": "<your-job-offer-id-here>"
    }
}
```

**Response Codes**

* `200 OK`: Request successful, stream begins
* `400 Bad Request`: Invalid request parameters
* `401 Unauthorized`: Invalid or missing API key
* `404 Not Found`: Requested model not found
* `500 Internal Server Error`: Server error processing request

**Retrieve your video**

`GET /api/v1/video/results/:job_offer_id`&#x20;

<table><thead><tr><th width="166.12890625">Parameter</th><th width="434.75390625">Description</th><th width="105.5">Type</th></tr></thead><tbody><tr><td><code>job_offer_id</code><mark style="color:red;">*</mark></td><td>The id returned to you in the video creation request i.e <code>/api/v1/video/create-job</code><strong>Required</strong>.</td><td><code>string</code></td></tr></tbody></table>

**Request Headers**

* `Content-Type: application/json`<mark style="color:red;">\*</mark>
* `Authorization: Bearer YOUR_API_KEY`<mark style="color:red;">\*</mark>

**Response**

If the video is still in the process of being generated you will see a response that looks like the following:

```json
{
    "status": 102,
    "message": "Request is still processing",
    "data": {
        "job_offer_id": "<job-offer-id>",
        "job_state": "DealAgreed"
    }
}
```

**Response Codes**

* `102 Processing`: Request is still processing the creation of the video
* `200 OK`: Request successful
* `400 Bad Request`: Invalid request parameters
* `401 Unauthorized`: Invalid or missing API key
* `500 Internal Server Error`: Server error processing request

However, once the video has be generated you'll be returned the video in `webp` format with its raw bytes which you can save to a file in the following manner:

```bash
curl -X GET "https://anura-testnet.lilypad.tech/api/v1/video/results/<your-job-offer-id>" \
-H "Content-Type: application/json" \
-H "Authorization: Bearer your_api_key_here" \
--output video.webp
```

The result of the above command will be the `video.webp` file being saved in the directory from which you ran it from:

<figure><img src="../.gitbook/assets/frogs_chatting_listening.webp" alt=""><figcaption><p>Two frogs sit on a lilypad, animatedly discussing the wonders and quirks of AI agents. As they ponder whether these digital beings can truly understand their froggy lives, the serene pond serves as a backdrop to their lively conversation.</p></figcaption></figure>

### Audio Generation

The Anura API enables you to generate audio from text executed through our decentralized compute network. It's really easy to get started generating your own audio using Anura through the endpoints we provide.&#x20;

**Note**: Audio generation can take anywhere between 40 seconds to 3 mins to complete depending on the input length

**Retrieve the list supported audio generation models**

`GET /api/v1/audio/models`&#x20;

Currently we support `kokoro`; however, we are always adding new models, so stay tuned!

**Request Headers**

* `Content-Type: application/json`<mark style="color:red;">\*</mark>
* `Authorization: Bearer YOUR_API_KEY`<mark style="color:red;">\*</mark>

**Request Sample**

```bash
curl -X GET "https://anura-testnet.lilypad.tech/api/v1/audio/models" \
-H "Content-Type: application/json" \
-H "Authorization: Bearer your_api_key_here"
```

**Response**

```json
{
    "data": {
        "models": [
            "kokoro"
        ]
    },
    "message": "Retrieved models successfully",
    "status": 200
}
```

**Response Codes**

* `200 OK`: Request successful
* `401 Unauthorized`: Invalid or missing API key
* `500 Internal Server Error`: Server error processing request

**Send out a request to create an AI generated audio**

`POST /api/v1/audio/create-job`

**Request Headers**

* `Content-Type: application/json`<mark style="color:red;">\*</mark>
* `Authorization: Bearer YOUR_API_KEY`<mark style="color:red;">\*</mark>

**Request Parameters**

<table><thead><tr><th width="166.12890625">Parameter</th><th width="486.68359375">Description</th><th width="105.5">Type</th></tr></thead><tbody><tr><td><code>model</code><mark style="color:red;">*</mark></td><td>Model used to generate the response (e.g. <code>kokoro</code>). <strong>Required</strong>.</td><td><code>string</code></td></tr><tr><td><code>input</code><mark style="color:red;">*</mark></td><td>The prompt input to generate your audio from (max limit of 420 characters). <strong>Required</strong>.</td><td><code>string</code></td></tr><tr><td><code>voice</code><mark style="color:red;">*</mark></td><td>The voice to use when generating the audio sample. Possible values are <code>heart</code>, <code>puck</code>, <code>fenrir</code>, and <code>bella</code><strong>Required</strong>.</td><td><code>string</code></td></tr></tbody></table>

**Voice samples**

**Heart**

{% file src="../.gitbook/assets/heart.wav" %}
Heart Voice Sample
{% endfile %}

**Puck**

{% file src="../.gitbook/assets/puck.wav" %}
Puck Voice Sample
{% endfile %}

**Fenrir**

{% file src="../.gitbook/assets/fenrir.wav" %}
Fenrir Voice Sample
{% endfile %}

**Bella**

{% file src="../.gitbook/assets/bella.wav" %}
Bella Voice Sample
{% endfile %}

**Request Sample**

```json
{
    "input": "Hello my name is Heart and this is AI speech generated from text using the Kokoro module running on the Lilypad Network",
    "voice": "heart",
    "model": "kokoro"
}
```

**Response**

This endpoint will return an `job_offer_id` which is an unique identifier corresponding to the job that's running to create your audio. What you'll want to do with this id is pass it into our `/audio/results` endpoint (see below) which will provide you the output as a `wav` file or report that the job is still running. In the latter case, you then can continue to call the endpoint at a later time to eventually retrieve your audio. As mentioned in the beginning of this section, audio generation can take anywhere between 40 seconds to 3 mins to complete.

```json
{
    "status": 200,
    "message": "Audio job created successfully",
    "data": {
        "job_offer_id": "QmTmTWxffQrosK2nb3a4oeeZd9KRMUGwApEUFhioFUe4Y9"
    }
}
```

**Response Codes**

* `200 OK`: Request successful
* `400 Bad Request`: Invalid request parameters
* `401 Unauthorized`: Invalid or missing API key
* `404 Not Found`: Requested model not found
* `500 Internal Server Error`: Server error processing request

**Retrieve your video**

`GET /api/v1/audio/results/:job_offer_id`&#x20;

<table><thead><tr><th width="166.12890625">Parameter</th><th width="434.75390625">Description</th><th width="105.5">Type</th></tr></thead><tbody><tr><td><code>job_offer_id</code><mark style="color:red;">*</mark></td><td>The id returned to you in the audio creation request i.e <code>/api/v1/audio/create-job</code><strong>Required</strong>.</td><td><code>string</code></td></tr></tbody></table>

**Request Headers**

* `Content-Type: application/json`<mark style="color:red;">\*</mark>
* `Authorization: Bearer YOUR_API_KEY`<mark style="color:red;">\*</mark>

**Response**

If the audio is still in the process of being generated you will see a response that looks like the following:

```json
{
    "status": 102,
    "message": "Request is still processing",
    "data": {
        "job_offer_id": "QmTmTWxffQrosK2nb3a4oeeZd9KRMUGwApEUFhioFUe4Y9",
        "job_state": "DealAgreed"
    }
}
```

**Response Codes**

* `102 Processing`: Request is still processing the creation of the audio
* `200 OK`: Request successful
* `400 Bad Request`: Invalid request parameters
* `401 Unauthorized`: Invalid or missing API key
* `500 Internal Server Error`: Server error processing request

However, once the audio has be generated you'll be returned the audio in `wav` format with its raw bytes which you can save to a file in the following manner:

```bash
curl -X GET "https://anura-testnet.lilypad.tech/api/v1/audio/results/<your-job-offer-id>" \
-H "Content-Type: application/json" \
-H "Authorization: Bearer your_api_key_here" \
--output audio.wav
```

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
