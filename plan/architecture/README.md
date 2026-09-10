# Architecture - Component Index

**Updated:** <!-- YYYY-MM-DD -->

## System Diagram

```
<!-- ASCII diagram showing how components connect -->
<!-- Example: -->
[Client] → [API Gateway] → [Service A] → [Database]
                         → [Service B] → [External API]
```

## Components

| Component | Description | Doc | Status |
|-----------|-------------|-----|--------|
| <!-- e.g. Solving Pipeline --> | <!-- e.g. Multi-strategy order solver --> | [solving-pipeline.md](solving-pipeline.md) | <!-- active / planned / deprecated --> |
| <!-- e.g. Dashboard --> | <!-- e.g. Web UI for monitoring --> | [dashboard.md](dashboard.md) | |

<!-- Add a row for each component doc. Create docs from _TEMPLATE.md -->

## Cross-Cutting Concerns

<!-- Things that span multiple components -->

- **Observability:** <!-- e.g. tracing + Prometheus metrics -->
- **Auth:** <!-- e.g. Supabase Auth, JWT -->
- **Error Handling:** <!-- e.g. structured errors, retry policies -->

## Key Data Flows

<!-- Describe 1-3 critical paths through the system -->

### <!-- e.g. Order Processing Flow -->

```
1. <!-- Step -->
2. <!-- Step -->
3. <!-- Step -->
```
