# Architecture

## High-level model

Lightspeed Stack is organized around a FastAPI application that exposes multiple API surfaces over a shared configuration/runtime layer.

At a high level:

1. `src/lightspeed_stack.py` parses CLI flags, loads configuration, and starts the service.
2. The FastAPI app under `src/app/` registers endpoint routers.
3. Endpoint handlers validate requests, enforce auth/authz, and orchestrate backend calls.
4. OGX/provider integrations perform model-facing work.
5. Optional database and storage layers persist conversation or A2A state.
6. Observability and telemetry modules emit logs, metrics, tracing, and user-data collection artifacts.

## Key architectural layers

### Service bootstrap

`src/lightspeed_stack.py` is the runtime entrypoint. It supports:

- verbose mode
- configuration dump/schema generation
- model schema dump helpers
- migration from legacy config layout
- selecting an alternate `lightspeed-stack.yaml`

This makes the repo useful both as a running API service and as a source for generated configuration and OpenAPI-related assets.

### Application and routing

The FastAPI application lives under `src/app/`. The endpoint package contains handlers for major capabilities such as:

- `query.py`
- `streaming_query.py`
- `responses.py`
- `conversations_v1.py` / `conversations_v2.py`
- `a2a.py`
- `config.py`
- `health.py`
- `info.py`
- `metrics.py`
- `providers.py`
- `models.py`
- `tools.py`
- `vector_stores.py`
- `mcp_servers.py`

The source shows a pattern of:

- FastAPI routers
- auth dependencies
- authorization decorators
- typed request/response models
- tracing helpers
- utility modules for quota, compaction, vector search, MCP, and response shaping

### Configuration and runtime behavior

`src/configuration.py` owns YAML loading and env-var substitution. It keeps a process-global configuration object and cached runtime helpers such as quota limiters, token usage history, and conversation cache references.

This is the main contract between deployment configuration and runtime behavior.

### Storage

The repo includes:

- general DB engine setup in `src/app/database.py`
- SQLite and PostgreSQL support
- dedicated A2A storage implementations under `src/a2a_storage/`

This suggests a split between application persistence and specialized A2A context storage.

### Integration surfaces

From the source tree and examples, major integration areas include:

- LLM providers
- OGX runtime modes
- MCP servers and MCP auth
- vector stores / RAG
- telemetry stacks like OpenTelemetry and Splunk
- authentication providers including API key, JWK, Kubernetes, and RH identity flows

## Architectural docs already in repo

The repository already ships richer architecture material in:

- `docs/devel_doc/ARCHITECTURE.md`
- `docs/devel_doc/architecture.*`
- `docs/devel_doc/query_endpoint.md`
- `docs/devel_doc/streaming_query_endpoint.md`
- `docs/devel_doc/persistent_storage.md`
- `docs/user_doc/*.md`

This TechDocs page is the RHDH-oriented map; use those upstream docs for deeper design detail.
