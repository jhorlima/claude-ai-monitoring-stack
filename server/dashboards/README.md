# Dashboards (Public Notes)

This directory includes example dashboards for observability use cases.

## Claude dashboard

The `claude-code-usage.json` dashboard is designed around structured usage events stored in Loki, especially events where:

- `service_name` is `claude-code` or `cowork`
- `body` includes values such as `claude_code.api_request` and `claude_code.tool_decision`
- `attributes_*` fields include model, token, cost, effort, cache, and tool data

## Portability note

This repository provisions a Loki datasource with UID `ffd8h30nfuxhcd` so existing dashboard JSON imports work without manual edits.

If you prefer a stricter portable pattern, you can replace hardcoded datasource UIDs in dashboard JSON with a datasource variable (for example, `loki_datasource`) and keep provisioning consistent.
