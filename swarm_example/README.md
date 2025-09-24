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
