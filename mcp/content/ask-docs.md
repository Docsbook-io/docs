---
title: "Ask docs"
description: "Answer a question from a project's own published docs — the same retrieval and model call the project's public 'Ask AI' widget runs, scoped to your own workspace, returning the synthesized answer a reader would see instead of a page to read yourself."
status: generated
version: "0.1"
---

# Ask docs

<!-- widget:mcp access=read -->

## ask_docs

Answer a question from this project's own published documentation — the same retrieval and model call the project's public 'Ask AI' chat widget runs for a real reader, scoped to your own workspace instead of a page search. Where `search` / `search_docs` / `read_doc` hand back snippets or a whole page for you to read yourself, `ask_docs` hands back the synthesized, cited answer a reader would actually see. Available on your own token — it does not need to be handed to `docsbook_agent`.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). |
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
    "name": "ask_docs",
    "arguments": {
      "question": "<question>"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"ask_docs","arguments":{"question":"<question>"}}}'
```

<!-- /widget -->
