---
title: "Read linkedin company"
description: "Company size (as the source's own STRING field, never its unreliable numeric twin), industry, founding year and follower count for up to 5 LinkedIn company pages."
---

# Read linkedin company

<!-- widget:mcp access=read price-millicents=3000 -->

## read_linkedin_company

Company size (as the source's own STRING field, never its unreliable numeric twin), industry, founding year and follower count for up to 5 LinkedIn company pages. GitHub's Organization type has no size field at all; this is the read that tells a soloist and a funded team apart before a lead is written to. Routes from questions like: how big is this company · check their linkedin company page · «насколько большая эта компания» · «проверь их страницу компании в linkedin». Not: It reads a /company/ page only. A person's own /in/ profile is not supported by this tool at all, and is not attempted. Example: Look up company size and industry for https://linkedin.com/company/vercel. Pass `workspace_id` whenever the answer will be quoted later: it is what files the reading in that project's history with a `call_id`, and only a `call_id` (or a URL) is accepted as the source of a figure on an audit finding — the tool's own name is not a source. One call fetches at most 5 results and costs $0.0300.

| Field | Type | Required | Description |
|---|---|---|---|
| `company_urls` | string[] | yes | LinkedIn COMPANY page URLs only, e.g. ["https://linkedin.com/company/vercel"] — /in/ personal profiles are not supported by this tool. |
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
    "name": "read_linkedin_company",
    "arguments": {
      "company_urls": []
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"read_linkedin_company","arguments":{"company_urls":[]}}}'
```

<!-- /widget -->
