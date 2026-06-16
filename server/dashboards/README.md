# Dashboards (Public Notes)

This directory includes example dashboards for observability use cases.

## Claude dashboard

The `claude-code-usage.json` dashboard is a **hybrid** layout:

### Row labels

Every section title states **product scope** and **data source**:

| Prefix | Scope |
| --- | --- |
| `Claude Code · … (Prometheus)` | OTLP metrics, Claude Code only |
| `Code + Cowork · … (Loki)` | OTLP log events, both products |

### Row 1 — Claude Code (Prometheus)

Fast KPIs from OTLP **metrics** (`service_name="claude-code"`):

- sessions, cost, input/output tokens, cache read/write, active time
- cost and token trends, top users, cache hit rate

### Row 2 — Organization (Loki)

Combined **Code + Cowork** KPIs from OTLP **log events** (`service_name=~"claude-code|cowork"`):

- API requests, cost, tokens, cache read/write

Use this row when Cowork is configured via Anthropic admin OTLP (no local env vars).

### Loki drill-down

Tools, tool decisions, request log stream, heatmap, duration and cost per request.

### Event schema (Loki)

- `service_name`: `claude-code` or `cowork`
- `body`: e.g. `claude_code.api_request`, `claude_code.tool_decision`
- `attributes_*`: model, tokens, cost, effort, cache, user email, etc.

### Metric schema (Prometheus)

- `claude_code_cost_usage_USD_total`, `claude_code_token_usage_tokens_total`, etc.
- Labels: `user_email`, `model`, `effort`, `query_source`, `terminal_type`, `type` (for tokens)

## Portability note

This repository provisions a Loki datasource with UID `ffd8h30nfuxhcd` and Prometheus with UID `prometheus` so the dashboard JSON imports without manual edits.
