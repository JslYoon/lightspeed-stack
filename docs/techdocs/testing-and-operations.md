# Testing and Operations

## Testing assets in repo

The repository includes a dedicated `tests/` tree plus numerous mocks and support services referenced by `docker-compose.yaml`.

The existing docs tree also includes:

- `docs/testing/testing.md`
- `docs/testing/e2e_testing.md`
- `docs/testing/e2e_scenarios.md`
- `docs/testing/integration_vs_e2e.md`

This suggests the project already has a mature test/documentation story that should be referenced rather than recreated.

## Operational characteristics visible in source

### Health and metrics

The endpoint package includes:

- `health.py`
- `metrics.py`
- `info.py`

These provide a standard operational footprint for probes, metrics scraping, and service introspection.

### Database options

`src/app/database.py` shows support for:

- SQLite
- PostgreSQL

The code also handles custom PostgreSQL schema creation when configured.

### Quotas and conversation management

The runtime includes quota scheduling and token accounting, plus conversation cache/compaction support. These are important operational behaviors because they affect latency, persistence, and cost control.

### Telemetry and data collection

The README explicitly mentions user data collection and export to Dataverse through a companion service, and the repo docs cover telemetry integrations such as OpenTelemetry, Splunk, and Sentry.

## Verification note for this TechDocs pass

This TechDocs set is based on source inspection in the repository checkout. It does not claim that every local runtime path was executed in this session.

For deployment verification, use the project's own test and run instructions together with your target environment's provider credentials and runtime dependencies.
