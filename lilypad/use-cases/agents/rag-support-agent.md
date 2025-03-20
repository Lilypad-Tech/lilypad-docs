---
description: >-
  A retrieval-augmented generation (RAG) agent that retrieves relevant context
  and generates AI-powered responses using the Lilypad Network.
---

# 🧠 RAG Support agent

The Lilypad RAG Support Agent is a Retrieval-Augmented Generation (RAG) AI assistant that retrieves relevant information and generates AI-powered responses using the Lilypad Network. It enables automated support and troubleshooting by leveraging vector search and AI-based text generation.

### **Features**

* **Context-Aware Responses** – Uses `all-MiniLM-L6-v2` embeddings to retrieve relevant information.
* **AI-Powered Answer Generation** – Sends retrieved context and user query to the Lilypad API, which processes it using Llama3 8B.
* **Customizable Knowledge Base** – Modify the agent’s context source (`issues.md`) to adapt it for different use cases.

### **How It Works**

1. **Embedding Queries with `all-MiniLM`**
   * Converts user queries and stored knowledge into dense vector embeddings for similarity-based retrieval
2. **Retrieving Relevant Context**
   * Searches a pre-indexed database to find the most relevant information.
3. **Generating Responses with Llama3 using the** Lilypad API
   * Sends retrieved context and user prompt to the Lilypad API, where Llama3 8B generates a structured response

### **Expanding to Your Own Support Agent**

The Lilypad RAG Support Agent can be adapted to different projects by modifying its retrieval source.

#### **Updating the Knowledge Base (`issues.md`)**

By default, the agent retrieves information from `issues.md`, a markdown file containing troubleshooting steps.

To customize:

* Open `issues.md` in the repository.
* Replace or expand the content with relevant support information for your project.
* Format the content clearly to improve retrieval accuracy.
* Restart the agent to index the updated knowledge base.

For more advanced use cases, the agent can be extended to support multiple files or external knowledge sources.

### **Installation**

Follow these steps to set up the RAG Support Agent and configure it with your Lilypad API key.

#### **Get a Lilypad API Key**

Sign up at [Anura API](https://anura.lilypad.tech) and generate an API key.

#### **Clone the Repository**

```sh
git clone https://github.com/PBillingsby/lilypad-rag-agent.git
cd lilypad-rag-agent
```

#### **Configure Your API Key**

Export your Lilypad API Token as an environment variable:

```sh
export LILYPAD_API_TOKEN="your-api-key-here"
```

To make it persistent, add it to `~/.bashrc` or `~/.zshrc`.

#### **Install Dependencies**

Ensure Python 3 is installed, then run:

```sh
pip install -r requirements.txt
```

### **Usage**

After setting up the API key and dependencies, the agent is ready to process queries using Lilypad’s AI-powered retrieval system.

#### **Run the Agent**

Execute the agent from the project's root directory:

```sh
python3 cli.py
```

### **Resources**

* [Lilypad Docs](https://docs.lilypad.tech)
* [Lilypad Anura API](https://anura.lilypad.tech/)
* [Source code](https://github.com/PBillingsby/lilypad-rag-agent)
