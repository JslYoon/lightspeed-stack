# API Surface

## Entry style

The application is a FastAPI service. The endpoint package and existing docs indicate a broad API surface spanning both user-facing query flows and operational/configuration flows.

## Major endpoint groups observed in source

### Query and generation

- `query.py` - primary query endpoint using the Responses API
- `streaming_query.py` - streaming query path
- `responses.py` - response-oriented API surface
- `stream_interrupt.py` - interrupt support for in-progress streaming

The `query.py` handler shows integration with:

- auth dependencies
- authorization middleware
- conversation validation
- quota/token accounting
- compaction
- vector search / RAG context assembly
- MCP auth checks
- response preparation and document deduplication

### Conversations and prompts

- `conversations_v1.py`
- `conversations_v2.py`
- `prompts.py`
- `saved_prompts.py`

These appear to cover stored conversation state and reusable prompt assets.

### Discovery and configuration

- `config.py`
- `info.py`
- `models.py`
- `providers.py`
- `rags.py`
- `skills.py`
- `tools.py`
- `vector_stores.py`
- `mcp_servers.py`

These are the endpoints most relevant to platform integration, diagnostics, and environment introspection.

### Operational and support endpoints

- `health.py`
- `metrics.py`
- `authorized.py`
- `feedback.py`
- `shields.py`

### A2A and compatibility APIs

- `a2a.py`
- `a2a_openapi.py`
- `rlsapi_v1.py`

## OpenAPI and deeper endpoint docs

The repo already contains generated and narrative API docs under:

- `docs/devel_doc/openapi.md`
- `docs/devel_doc/openapi.json`
- `docs/devel_doc/conversations_api.md`
- `docs/devel_doc/query_endpoint.md`
- `docs/devel_doc/streaming_query_endpoint.md`
- `docs/devel_doc/responses.md`

In RHDH, those can be linked from the component page or surfaced as additional docs if desired.
