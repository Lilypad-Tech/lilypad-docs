---
description: >-
  An agent-based system that monitors HubSpot for recently modified contacts,
  fetches enriched data from LinkedIn, and updates HubSpot automatically.
---

# 📊 HubSpot-LinkedIn Agent

## Agent Details

Automate customer relationship management, internal company management, etc. with the [HubSpot-LinkedIn agent](https://github.com/Lilypad-Tech/HubSpot-LinkedIn-AgentSync)! Scale inference using the Lilypad network deploying any of the models supported by the [Lilypad Inference API](https://docs.lilypad.tech/lilypad/developer-resources/inference-api).

This workflow serves as a proof of concept (PoC) illustrating the capabilities of agents to interface with platform APIs, specifically those of HubSpot and RapidAPI.&#x20;

Github repo [here](https://github.com/Lilypad-Tech/HubSpot-LinkedIn-AgentSync).

## Getting Started

A guide to launch the HubSpot-LinkedIn agent locally and run inference on the Lilypad Network with the [Lilypad Inference API](https://github.com/Lilypad-Tech/HubSpot-LinkedIn-AgentSync).

### Prerequisites

* Python 3.8+
* A HubSpot account with a Private App token
  * [Sign up for HubSpot](https://www.hubspot.com/)
  * [Create a Private App](https://developers.hubspot.com/docs/guides/apps/private-apps/overview)\
    &#xNAN;_&#x53;teps_: Log in > Settings > Integrations > Private Apps > Create private app > Name it > Scopes: `crm.objects.contacts` (read/write contacts) > Create app > Click app name > Auth tab > View access token > Copy token
* A RapidAPI account with a LinkedIn Data API key
  * [Sign up for RapidAPI](https://rapidapi.com/signup)\
    &#xNAN;_&#x53;teps_: Create an account > Subscribe to [LinkedIn Data API](https://rapidapi.com/rockapis-rockapis-default/api/linkedin-data-api) > Go to [Developer Dashboard > Authorization](https://rapidapi.com/developer/authorization) > Select "default-application" > Copy "Application Key"
* An OpenAI-compatible API
  * [Lilypad Inference API](https://example.com/anura-api-docs) (Sign up and generate an API key)'
  * Choose the model you would like to use

### Setup

1.  **Clone the Repository**

    ```
    git clone https://github.com/mavericb/HubSpot-LinkedIn-AgentSync.git
    cd HubSpot-LinkedIn-AgentSync
    ```
2.  **Install Dependencies**

    ```
    pip install -r requirements.txt
    ```

    _Note_: If `requirements.txt` is missing, install:

    ```
    pip install python-dotenv hubspot-api-client requests schedule phi
    ```
3. **Configure Environment Variables**
   *   Create a `.env` file:

       ```
       touch .env
       ```
   *   Add your keys:

       ```
       HUBSPOT_ACCESS_TOKEN=your-private-app-token
       RAPIDAPI_KEY=your-default-app-token
       API_KEY=your-openai-compatible-key
       BASE_URL=https://anura-testnet.lilypad.tech/api/v1  # Adjust for your provider
       AGENT_MODEL=qwen2.5:7b  # Adjust for your provider
       ```

### Usage

1.  **Start the Daemon**

    ```
    python main.py
    ```

    * Checks HubSpot every minute for contacts modified in the last 7 days (or since `last_processed.json`).
    * Fetches LinkedIn data and updates HubSpot.
    * Runs for 5 minutes (adjustable in `main.py`).
2. **Monitor Logs**
   * Look for "Found X contacts", "HubSpot update: ...", "Attempting to save last\_processed timestamp".
   * If no contacts are found, `last_processed.json` won’t save—edit a HubSpot contact to test.

### File Structure

* `main.py`: Entry point and daemon logic.
* `/tools/hubspot_tools.py`: HubSpot API utilities (fetch/update contacts).
* `/tools/linkedin_tools.py`: LinkedIn API utility (fetch profile data).
* `/agents/hubspot_agent.py`: Agent for updating HubSpot.
* `/agents/linkedin_agent.py`: Agent for fetching LinkedIn data.
