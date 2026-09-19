---
title: "Search job postings"
description: "Up to 30 current LinkedIn job postings matching a keyword and location, with the full description, seniority and posting date — the company's own dated statement of what it is…"
---

# Search job postings

<!-- widget:mcp access=read price-millicents=3000 -->

## search_job_postings

Up to 30 current LinkedIn job postings matching a keyword and location, with the full description, seniority and posting date — the company's own dated statement of what it is hiring for. A job posting naming a stack or a pain ("own our documentation migration") is a company-stated trigger event no GitHub field or marketing page will say this plainly, or this recently. Routes from questions like: is this company hiring for docs or dev relations · what stack is this company building with, per their job posts · «ищет ли эта компания людей в доку» · «что за стек у компании судя по вакансиям». Not: It returns current postings for a keyword/location pair. Historical hiring trends or an org chart are not something this tool, or Docsbook, produces. Example: Search LinkedIn for "technical writer" jobs at companies in the San Francisco Bay Area. Pass `workspace_id` whenever the answer will be quoted later: it is what files the reading in that project's history with a `call_id`, and only a `call_id` (or a URL) is accepted as the source of a figure on an audit finding — the tool's own name is not a source. One call fetches at most 30 results and costs $0.0300.

| Field | Type | Required | Description |
|---|---|---|---|
| `keywords` | string | yes | Job title or skill to search for, e.g. "developer relations" or the company's own name. |
| `location` | string | no | City, region or country to scope the search to, as typed on LinkedIn. |
| `workspace_id` | string | no | The project this reading is FOR. 🔴 Pass it whenever the answer will be QUOTED later: it is what files the call in that project's history with a `call_id`, and a `call_id` is the only thing an opportunity accepts as the source of a demand figure (`demand_source`). Nothing about the project is sent to the site being read. Omitted, the reading still comes back — it simply lands in no history, so nothing afterwards can point at it. Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |

<!-- /widget -->

## Call it

<!-- widget:code-group -->

### MCP

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "search_job_postings",
    "arguments": {
      "keywords": "<keywords>"
    }
  }
}
```

### curl

```bash
curl -X POST 'https://docsbook.io/api/mcp/server' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"search_job_postings","arguments":{"keywords":"<keywords>"}}}'
```

<!-- /widget -->
