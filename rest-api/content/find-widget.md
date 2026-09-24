---
title: "Find widget"
description: "Search the Docsbook widget catalog for an interactive UI widget matching the user's request."
---

# Find widget

<!-- widget:api -->

## GET /api/v1/find_widget

Search the Docsbook widget catalog for an interactive UI widget matching the user's request. Returns matching widget ids and summaries. Use this to discover available widgets (e.g. 'dark mode toggle', 'analytics chart', 'search bar'). After finding a widget, use the returned resourceUri to read its HTML bundle via the ui:// resource.

**Price** — free, never metered.

Also reachable without a token on this workspace's public MCP endpoint.

Also reachable by name at `POST /api/v1/tools/find_widget`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `query` | string | yes | Free-text description of what the user wants, e.g. 'dark mode toggle' or 'analytics dashboard'. |
| `mode` | string | no | Restrict matches to widgets available in this mode (admin or user). |

### Request

```bash
curl -X GET 'https://docsbook.io/api/v1/find_widget?query=%3Cquery%3E' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

<!-- /widget -->

## Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |
