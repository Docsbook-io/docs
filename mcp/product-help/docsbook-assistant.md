---
title: "Docsbook assistant"
description: "🔴 THE SPECIALIST — the second of this server's two agents, and the one that answers HOW."
---

# Docsbook assistant

<!-- widget:mcp access=read price-millicents=30000 -->

## docsbook_assistant

🔴 THE SPECIALIST — the second of this server's two agents, and the one that answers HOW. Ask it before you write anything. `docsbook_expert` tells you WHAT to do and WHY, in what order, and what to measure; it holds no craft and runs no model. THIS one holds the craft: how a documentation surface should actually be built so it does the job. It answers from Docsbook's published corpus, searched by MEANING rather than by keyword, and comes back with the pages it drew on — so the guidance is quotable to whoever asks why the page is shaped that way. ASK IT ABOUT THE WORK: how to structure a page for a search intent, what a quickstart owes a reader in its first screen, how to write a passage an answer engine will lift whole, what makes a comparison page win the query it is about, how to shape an API reference, what information architecture a growing set of pages needs, how to write for a reader who arrived from a competitor's name, what a translated page needs beyond translation, how to make a page convert without the assistant becoming an advert. Documentation practice, technical writing, readability, information architecture, tutorials and how-tos, reference, examples, FAQs, internal linking, semantic structure, SEO, semantic SEO, search intent, programmatic SEO, GEO, AEO, AI citation, answerable blocks, entity clarity. 🔴 PASS `context`. It is the difference between an answer about documentation and an answer about YOUR page: what the product is and who it is for, the intent the surface has to answer in the words a reader would type, what already exists on the subject, the evidence that made this worth doing, and what it is expected to move. This agent cannot see your repository, your analytics or your project — the Expert names those slots on its `consult` block and you fill them here. Context is read as the asker's situation, never as a source: it is never cited back at you as a documented fact. IT ALSO ANSWERS ABOUT DOCSBOOK ITSELF — how a feature works, how to set something up, what a plan includes, why the product behaves a certain way, 'can Docsbook do X' — because it is the SAME answer, from the same retrieval and the same model call, that a reader gets from the public 'Ask AI' chat on https://docsbook.io/docs. IT ADVISES; IT DOES NOT WRITE. Nothing here edits a file or commits anything — take the structure and the principles into the step that writes, which is yours. NOT for a customer's OWN documentation — that is `search` / `search_docs` / `read_doc` against their workspace. NOT a planner: if you do not yet know whether this work is the right work, `docsbook_expert` first. `session_id` is optional: reuse the same one across calls to keep them grouped as one conversation in this project's own chat analytics, the way a real visitor's multi-turn chat is; omit it and each call reads as a separate visitor. Any language — answers come back in whichever language the question was asked in. This answers HOW, not whether. It is the specialist — the craft, from the published corpus — and it does not know what this project is owed. If you have not already got the direction from `docsbook_expert`, get it first: it says whether this is the work, and hands you the question to ask here. One call, changes nothing.

| Field | Type | Required | Description |
|---|---|---|---|
| `question` | string | yes | The craft question, in plain language, any language — the whole question, not a keyword. This is what the corpus is searched by, so ask what you actually want to know: "how should a page targeting a comparison intent be structured so an answer engine quotes it?" beats "page structure". When `docsbook_expert` returned a `consult` block, send its `question` verbatim. |
| `context` | string | no | 🔴 What YOU know and this corpus cannot: the product and its audience, the intent this surface answers, what already exists on the subject, the evidence behind the work, and what it is expected to move, with the figure. Without it the answer is about documentation in general. It is supplied to the answering model as the asker's situation and is never quoted back as a documented fact — and it is NOT part of what the corpus is searched by, so pasting your product into `question` instead makes retrieval worse, not better. |
| `session_id` | string | no | Optional: reuse the same id across calls to group them as one visitor's conversation. |

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
    "name": "docsbook_assistant",
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"docsbook_assistant","arguments":{"question":"<question>"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/tools/docsbook_assistant

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | yes | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/docsbook_assistant' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{"question":"<question>"}}'
```

<!-- /widget -->
