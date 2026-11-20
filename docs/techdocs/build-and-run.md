# Build and Run

## Prerequisites

From `README.md`, the project expects:

- Python 3.12, 3.13, or 3.14
- `uv` for dependency management
- an API key or credentials for a supported LLM provider
- optionally a container runtime (`podman` or `docker`) for local OGX/container flows

## Local dependency setup

The documented default path is:

```bash
uv sync --group dev --group ogxlibdev
```

If using tracing with in-process PII redaction, the README also calls out downloading a spaCy model.

## Local run flow

The repository README and `Makefile` show a typical workflow:

1. Generate or prepare `run.yaml`
2. Export provider credentials such as `OPENAI_API_KEY`
3. Run the stack

Example:

```bash
./scripts/generate_local_run.sh
export OPENAI_API_KEY=...
make run
```

`make run` starts dependent services and then runs the API service.

## Direct vs containerized execution

The `Makefile` shows two major paths:

- `run-ogx` for direct execution
- `run` for execution with dependent services/container orchestration

`run-ogx` ultimately executes the Python service entrypoint with `uv run python src/lightspeed_stack.py -c <config>` or wraps it with OpenTelemetry instrumentation depending on environment variables.

## Container orchestration

`docker-compose.yaml` indicates a richer local/e2e environment that can include:

- the main lightspeed-stack service
- OGX container/runtime
- mock JWKS
- mock MCP server
- mock OTEL collector
- mock guardian server
- mock TLS inference server

This makes the repo useful for integration and end-to-end validation, not just ad hoc local development.

## Config files to know

- `lightspeed-stack.yaml` - main stack configuration
- `run.yaml` - OGX/runtime config
- `examples/*.yaml` - scenario-specific examples

For RHDH consumers, these are the main files to inspect when documenting deployment profiles or building templates.
