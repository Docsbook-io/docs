---
title: "Get project doc outline"
description: "List every markdown page in the workspace with a short summary (title, heading count, char count) plus its lifecycle — `status`, `version` and `agentMayBuildFrom`."
---

# Get project doc outline

<!-- widget:api -->

## GET /api/v1/get_project_doc_outline

List every markdown page in the workspace with a short summary (title, heading count, char count) plus its lifecycle — `status`, `version` and `agentMayBuildFrom`. An INVENTORY, not a search: NOT the way to answer a question or find the page about something — that is `search_project_docs`. Building this list downloads and parses every page of the site (slow on a large one), and a list of titles answers nothing by itself. Use it for 'what does this documentation cover', to pick a folder for a NEW page, or after `search_project_docs` found nothing. It is also the REVIEW BOARD for documentation that is governed by status: `status: 'review'` lists what is waiting on a human, `status: 'generated'` what a machine wrote that nobody has read. `counts` always describes the whole prefix, not the filtered rows, so 'four of ninety pages are approved' is one call. Statuses: generated (A machine wrote this page and no human has read it yet.) · draft (Someone is still writing it. Not ready to be read as settled.) · review (Waiting for a human to read it and decide.) · approved (A human read this version and signed off. Safe to build work from.) · locked (Frozen on purpose. Agents may read it and build from it, but may not rewrite it.) · deprecated (Superseded. Kept so its links keep working, not to be relied on.) · archived (History. Neither built from nor edited.)

**Price** — $0.00003 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/get_project_doc_outline`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `path_prefix` | string | no | Optional: restrict to pages under this path prefix. |
| `status` | string | no | Optional: only pages at this lifecycle status. `counts` still covers them all. |

### Request

```bash
curl -X GET 'https://docsbook.io/api/v1/get_project_doc_outline' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

<!-- /widget -->

## Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |
