---
title: "Collect ai citability"
description: "Measure whether answer engines and AI assistants can FETCH this documentation at all, and whether there is anything in it worth quoting."
---

# Collect ai citability

<!-- widget:mcp access=read price-millicents=12000 -->

## collect_ai_citability

Measure whether answer engines and AI assistants can FETCH this documentation at all, and whether there is anything in it worth quoting. Finds what no traffic-based check can see: the reader who asked an assistant, got their answer from your page, and never visited — and the page that cannot be cited however well it is written, because it renders client-side, sits behind a robots rule nobody remembers adding, or serves a challenge to a named crawler while a browser gets 200. Returns scores out of 100 on five separate axes — crawler_access, machine_surfaces, atom_citability, answer_shape, version_freshness — each with the evidence it rests on, plus ranked findings. Scores are computed from the observations, not written by the model, so two runs are comparable. Use it for 'why does ChatGPT never cite us', 'is our GEO/AEO set up', 'can AI crawlers read our docs', 'do we need llms.txt', 'are we invisible to answer engines', «почему нас не цитирует ИИ», «видят ли нас ассистенты». This is the fetchability and citability probe; it does not judge writing quality or search rankings, and it does not say which of its findings to fix first — that is `docsbook_expert`, which ranks them against what you are actually trying to achieve. Returns the finished result — a validated `collect_ai_citability.v1` payload: an `evidence` map every claim cites, scores computed by code rather than written by the model, and ranked findings. Numbers that trace to no evidence fail the contract rather than shipping, so an invented figure is not a risk you have to check for. Changes nothing; safe on a read-only token. Typical wait 5–60 s: this call crawls the site itself, one fetch after another, and a slow or unreachable host is what stretches it. Nothing is returned until it finishes. Evidence, not a verdict — nothing here says what the gap MEANS. If you have not already asked `docsbook_expert` how to read it, ask: it says what this evidence is worth against, and what to do with it. One call, changes nothing.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `pages` | string[] | no | Page paths to probe, e.g. ["/", "/docs/quickstart"]. Defaults to the site root and two common docs paths. Each page costs two fetches. |

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
    "name": "collect_ai_citability",
    "arguments": {}
  }
}
```

### curl

```bash
curl -X POST 'https://docsbook.io/api/mcp/server' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"collect_ai_citability","arguments":{}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/tools/collect_ai_citability

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | no | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/collect_ai_citability' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{}}'
```

<!-- /widget -->
