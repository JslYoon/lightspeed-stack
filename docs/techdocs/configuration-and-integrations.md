# Configuration and Integrations

## Configuration loading

The runtime configuration is loaded from YAML by `src/configuration.py`. The source shows:

- YAML parsing via `yaml.safe_load`
- env-var substitution with native override preservation
- a process-global configuration object
- lazy/cached runtime helpers for caches, quota limiters, and token usage history

This means runtime behavior is strongly configuration-driven.

## Main config concerns visible in the repo

Based on filenames, examples, and README content, the stack supports configuration for:

- service settings
- OGX backend/runtime settings
- authentication and authorization
- conversation cache and storage
- MCP servers
- quota limiters
- vector stores / RAG
- telemetry and user data collection
- model/provider selection

## Supported providers

The README explicitly mentions support for:

- OpenAI
- Azure OpenAI
- Google VertexAI
- IBM WatsonX
- AWS Bedrock
- RHOAI / vLLM
- RHEL AI / RHAIIS / vLLM

The repo also includes provider-oriented docs under `docs/devel_doc/providers.md`.

## Authentication and authorization

The docs and source tree indicate support for multiple auth modes, including:

- API key token
- JWK token
- Kubernetes-backed auth flows
- RH identity
- Azure Entra ID related authorization helpers

Platform teams cataloging this service in RHDH will likely want to capture the chosen auth mode per environment as part of the component's operational metadata.

## MCP and agentic integrations

The source tree includes dedicated support for:

- MCP server definitions and runtime management
- MCP auth
- agent/tool listing
- A2A protocols and storage

This is one of the distinctive traits of the service: it is more than a plain LLM proxy.

## Observability

The repo references:

- OpenTelemetry
- Splunk
- Sentry
- health and metrics endpoints

There is already upstream documentation for those under `docs/user_doc/` and endpoint coverage in `src/app/endpoints/`.
