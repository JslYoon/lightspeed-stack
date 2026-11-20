# Repository Layout

## Top level

Important top-level files and directories observed in this checkout:

- `README.md` - project overview and local run instructions
- `pyproject.toml` - Python project metadata and dependency/tooling configuration
- `uv.lock` - locked dependency graph for `uv`
- `Makefile` - common dev, run, and doc workflows
- `lightspeed-stack.yaml` - primary service configuration example/default
- `run.yaml` - OGX/runtime configuration used by local flows
- `docker-compose.yaml` - multi-service local/e2e composition
- `examples/` - scenario-specific config samples
- `docs/` - existing project documentation
- `src/` - application and library code
- `tests/` - test suites and fixtures
- `.tekton/`, `.konflux/` - CI/CD and build pipeline metadata

## Source tree

### `src/`

Core runtime code.

Notable areas:

- `src/lightspeed_stack.py` - process entrypoint
- `src/configuration.py` - config models/loader/runtime access
- `src/app/` - FastAPI app and routers
- `src/app/endpoints/` - HTTP endpoint handlers
- `src/a2a_storage/` - A2A storage backends

### `src/app/endpoints/`

The endpoint package is broad and indicates a feature-rich API surface. Based on file names alone, major capability groups are:

- query and response handling
- conversation lifecycle APIs
- A2A APIs
- auth/config/info/health endpoints
- prompt and saved prompt management
- provider/model discovery
- tools, MCP server, and vector store management
- safety/shields and feedback

## Documentation tree

The existing `docs/` tree is substantial and already includes:

- user documentation
- developer architecture docs
- auth docs
- model docs
- maintenance/versioning docs
- testing docs
- generated/openapi-related docs
- database docs

For RHDH, the new `docs/techdocs/` subtree acts as an entry layer rather than replacing the existing docs set.

## Examples and deployment references

The `examples/` directory contains multiple deployment and configuration scenarios, including provider variants, A2A state backends, auth modes, RAG/skills/shields, and quota-limiter examples. This is useful for platform teams trying to onboard or compare deployment patterns.
