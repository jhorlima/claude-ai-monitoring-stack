# AI Monitoring Stack (Public Template)

Public, self-hosted monitoring template for AI tooling usage analysis.

This template focuses on operational observability for tools like Claude Code and Claude Cowork, with a practical business angle: understanding cost versus outcomes.

## What is included

- Grafana (dashboards and analysis)
- Loki (log storage/query)
- Prometheus (metrics and remote write receiver)
- Grafana Alloy (OTLP ingestion and forwarding)
- Example dashboard: `claude-code-usage.json`

## Why this exists

Teams often adopt AI tooling quickly but struggle to answer:

- Which models are driving cost?
- How much input/output token volume are we generating?
- Is cache reducing spend?
- Are tool decisions indicating productive usage?
- Are we improving cost-efficiency over time?

This stack gives a concrete starting point for those questions.

## Quick start

```bash
cd server
cp .env.example .env
docker compose --env-file .env -f docker-compose.yml up -d
```

Then open:

- Grafana: <http://localhost:3000>
- Loki: <http://localhost:3100>
- Prometheus: <http://localhost:9090>
- Alloy UI: <http://localhost:12345>

## Telemetry ingest endpoints

- OTLP gRPC: `localhost:4317`
- OTLP HTTP: `localhost:4318`

## How to read value signals

The dashboard is not a full business KPI system by itself. It provides strong operational evidence (usage, cost, efficiency proxies) that should be interpreted together with product and delivery metrics.

Use this baseline framing:

- cost trend by model/user/team
- token efficiency and cache behavior
- tool decision outcomes as utility proxy
- stable or improving cost per useful outcome over time

## Traces roadmap

This public template starts with logs + metrics.
If trace telemetry is available and useful in your environment, add Tempo in a next phase.
