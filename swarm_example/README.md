# Swarm Example Notebooks

This folder contains example Jupyter notebooks demonstrating the use of AG2's swarm orchestration for multi-agent conversational workflows.

## Notebooks Overview

### `agentchat_swarm.ipynb`

This notebook introduces the fundamentals of swarm orchestration in AG2. It walks through building a simple multi-agent workflow in the domain of **flight booking and airline customer service**, inspired by OpenAI's airline customer service example. Key concepts covered include:

- Creating and configuring multiple agents
- Orchestrating agent conversations
- Using handoffs between agents
- Managing global context variables

The notebook is a great starting point for understanding how to coordinate agents to solve tasks collaboratively.

### `agentchat_swarm_enhanced.ipynb`

This notebook builds on the basics and demonstrates advanced swarm orchestration features in the domain of **e-commerce customer service** (e.g., order status and authentication workflows):

- Updating agent state dynamically
- Conditional handoffs based on conversation context
- Nested agent chats for complex workflows

The example simulates a customer service workflow for an e-commerce platform, including authentication and order status checks. It shows how to customize system messages and manage more sophisticated agent interactions.

## Example Outputs

The `example_outputs/` directory contains sample outputs from running the notebooks, so you can see what a typical multi-agent conversation looks like in practice.

## How to Use the Notebooks

1. Open the desired notebook in Jupyter or VS Code.
2. Follow the instructions and run the cells sequentially.
3. Review the outputs and experiment with modifying agent logic or workflow steps.

For more details on AG2's swarm orchestration, see the [official documentation](https://docs.ag2.ai/latest/docs/user-guide/advanced-concepts/orchestration/swarm/deprecation) and [blog post](https://docs.ag2.ai/latest/docs/blog/2024/11/17/Swarm).

## Changing the LLM Provider

Both notebooks load model connection details via `autogen.config_list_from_json(...)`, which reads a JSON file (or environment var) describing one or more model backends. In this repo, the root-level `resources.json` file provides that list.

### Where It Is Used

- In `agentchat_swarm.ipynb` (early setup cell) to build a `config_list` passed into agent or swarm creation.
- In `agentchat_swarm_enhanced.ipynb` similarly for the enhanced workflow.

### Editing `resources.json`

Open the root `resources.json`. Each object in the array is one model option. Common fields:

- `model`: Model name or deployment (e.g. `gpt-4.1-nano`, `gemma3:1b`).
- `api_type`: One of `openai`, `azure`, `ollama`, etc.
- `client_host`: (Ollama) Base URL of the local or remote Ollama server.
- `base_url`: (Azure/OpenAI custom) Full base URL for the API endpoint.
- `api_version`: (Azure) API version string.
- `api_key`: Can be an inline string or a Python expression referencing an env var (e.g. `os.environ['AZURE_OPENAI_API_KEY']`).
- `tags`: Optional list to help filter (e.g. `gpt-4`, `gpt-4o`).

### Switching Providers

1. If necessary, add or modify an entry in `resources.json` for the provider you want (e.g. add an Ollama model or an OpenAI model).
2. Ensure required environment variables (like `OPENAI_API_KEY` or `AZURE_OPENAI_API_KEY`) are exported in your shell before starting the notebook kernel.
3. (Optional) Use model name o tags to allow selective filtering if you modify the notebook code to pass `filter_dict` to `config_list_from_json`.
4. Re-run the initial setup cell in the notebook; the new provider is picked up automatically.

### Azure Specific Note

If you encounter a 404 with Azure, double‑check:

- `base_url` includes `/openai` path segment if required by your deployment.
- Correct `api_version` matches the model family.
- The `model` field matches your Azure deployment *name* (not necessarily the OpenAI public model string).

### Quick Troubleshooting

- Empty `config_list`: Path or env var incorrect; ensure `resources.json` is in the working directory or supply full path.
- Auth errors: Verify `api_key` environment variable spelling and that the kernel inherited the environment.
- Unexpected model behavior: Ensure the model actually supports features you enabled in `model_config` (e.g., function calling).

Adjust `resources.json`, re-run the first configuration cell, and proceed with the conversation cells.
