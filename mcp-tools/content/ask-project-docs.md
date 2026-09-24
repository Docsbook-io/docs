---
title: "Ask project docs"
description: "Ask a question about THIS project's own documentation and get back a synthesized, cited answer — the SAME retrieval and model call the project's public 'Ask AI' widget runs for a…"
---

# Ask project docs

<!-- widget:mcp access=read price-millicents=800 -->

## ask_project_docs

Ask a question about THIS project's own documentation and get back a synthesized, cited answer — the SAME retrieval and model call the project's public 'Ask AI' widget runs for a real reader on its docs site, run here instead for the ADMIN of this documentation. Use it when you want the ANSWER, not a page to go read yourself: 'what does our docs say the rate limit is', 'would a reader asking about refunds be told the right thing right now', «что у нас написано про...». Comes back with `refs`, the pages the answer actually drew on — quotable and checkable, not a guess. NOT for browsing the content yourself — that is `search_project_docs` (by meaning), `search_docs` (literal string), `read_project_doc` (one page in full) or `get_project_doc_outline` (what exists). Use those when you already know, or want to find, the page; use this when you want the finished answer a reader would get. NOT `docsbook_assistant` — that tool answers CRAFT questions ('how should a comparison page be structured') from Docsbook's OWN published corpus about documentation practice. This one answers from THIS project's OWN published pages, about what THIS project's documentation actually says. Booked to this project's own AI usage the way the admin's other questions here are (see `get_ai_usage`) — works on every plan, including Free, and does not require the visitor-facing AI Chat capability to be turned on. `session_id` is optional: reuse the same one across calls to keep them grouped as one conversation; omit it and each call reads as a separate one. Any language — the answer comes back in whichever language the question was asked in.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `question` | string | yes | The question, in plain language, any language — the whole question, not a keyword: this is what the corpus is searched by. |
| `context` | string | no | Optional: what sharpens the answer — which section or audience you mean, why you're asking. Read as the asker's situation and never cited back as a documented fact; keep it out of `question`, which is what retrieval embeds. |
| `session_id` | string | no | Optional: reuse the same id across calls to group them as one conversation. |

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
    "name": "ask_project_docs",
    "arguments": {
      "question": "<question>"
    }
  }
}
```

### curl

```bash
curl -X POST 'https://docsbook.io/api/mcp/server' \
  -H 'Authorization: Bearer YOUR_MCP_OAUTH_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"ask_project_docs","arguments":{"question":"<question>"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

<!-- widget:api -->

### GET /api/v1/ask_project_docs

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `question` | string | yes | The question, in plain language, any language — the whole question, not a keyword: this is what the corpus is searched by. |
| `context` | string | no | Optional: what sharpens the answer — which section or audience you mean, why you're asking. Read as the asker's situation and never cited back as a documented fact; keep it out of `question`, which is what retrieval embeds. |
| `session_id` | string | no | Optional: reuse the same id across calls to group them as one conversation. |

#### Request

```bash
curl 'https://docsbook.io/api/v1/ask_project_docs?question=%3Cquestion%3E' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

<!-- /widget -->
