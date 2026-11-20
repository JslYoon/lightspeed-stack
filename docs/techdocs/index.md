# Lightspeed Stack

Lightspeed Stack is a Python-based FastAPI service that fronts LLM and agent workflows through a REST API. In this repository it appears as **Lightspeed Core Stack (LCS)**, with support for provider-backed inference, agentic flows, RAG, conversation history, authentication and authorization, MCP integration, and observability.

This TechDocs set is aimed at RHDH consumption. It summarizes the repository as it exists in source, while linking out to the project's much larger built-in documentation tree under `docs/`.

## What this repo contains

- A FastAPI application under `src/app/`
- CLI/bootstrap entrypoint in `src/lightspeed_stack.py`
- Pydantic-based configuration loading in `src/configuration.py`
- Endpoint handlers for query, streaming, conversations, A2A, tools, providers, models, config, health, metrics, and more
- Database support for SQLite and PostgreSQL
- Local/containerized run flows via `Makefile`, `docker-compose.yaml`, `run.yaml`, and `lightspeed-stack.yaml`
- Extensive existing documentation in `docs/`

## What this service does

Based on the repository README and source layout, Lightspeed Stack provides:

- product-question answering through backend LLM services
- agentic capabilities and MCP-backed tool access
- RAG and vector-store integrations
- conversation management APIs
- authn/authz support across multiple modes
- observability and data-collection hooks

## Recommended RHDH entity shape

This repo fits best as a **Component** of type `service` or `library`, depending on how your catalog models deployable API backends. Given the FastAPI server and operational manifests in the repo, `service` is a reasonable default.

## TechDocs scope

These pages focus on:

- how the codebase is structured
- how the service starts and is configured
- which major API areas exist
- how to run, test, and operate it
- where to find deeper upstream docs already maintained by the project

For implementation detail beyond this summary, prefer the existing upstream docs in `docs/` and the endpoint/configuration modules in `src/`.
