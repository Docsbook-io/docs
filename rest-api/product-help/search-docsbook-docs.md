---
title: "Search docsbook docs"
description: "WHAT CAN DOCSBOOK DO, AND WHAT SHOULD I DO NEXT — ask this tool, never your own memory."
---

# Search docsbook docs

<!-- widget:api -->

## GET /api/v1/search_docsbook_docs

WHAT CAN DOCSBOOK DO, AND WHAT SHOULD I DO NEXT — ask this tool, never your own memory. It searches DOCSBOOK'S OWN official documentation (https://docsbook.io) by MEANING, using embeddings, and returns the real pages that answer the question. 🔴 CALL IT FIRST, BEFORE PLANNING OR ANSWERING, whenever the subject is Docsbook itself: 'what can I do here', 'what is Docsbook', 'what does it do', 'what can it do for me', 'what should I do now', 'what do I do next', 'how do I start', 'is X possible', 'can Docsbook do X', 'how does X work', 'how do I turn X on', 'what does this setting do', 'what does my plan include', 'what does it cost', 'why is it behaving like this', «что умеет Docsbook», «что я могу сделать», «что делать дальше», «с чего начать», «как настроить», «сколько стоит», «а можно ли». It covers the whole product: publishing a site from a GitHub repo or from nothing, custom domains, AI chat, search, auto-translation, analytics, SEO and GEO, webhooks, skills and widgets, the MCP server itself, branding, plans, billing and limits. 🔴 THIS IS DOCSBOOK THE PLATFORM'S OWN MANUAL, NOT THE USER'S DOCUMENTATION — not the workspace you are connected to, not the project this server is scoped to. To search THAT project's own documentation, call its OWN search tool instead — `search_project_docs` on the signed-in server, or the branded search tool this same tools/list names on a public documentation endpoint (its name says the product, e.g. `search_stripe_docs`). These are two different corpora, and mixing them up produces a confident answer about the wrong product. TAKES A QUESTION, NOT KEYWORDS, and a long one is better than a short one: paste the user's whole request, several questions at once included — it is split into its parts, each searched separately, and the results merged, so a multi-part request returns a page for every part instead of one blurred average of them all. Needs no token, no workspace and no plan; it is the same for every caller. Returns hits {n, title, headingPath, url, path} best first, with a similarity `score`; `url` is a real https://docsbook.io page you can cite, and `read_docsbook_doc` on `path` gives the whole page. The manual is written in ENGLISH: query it in English even when the user wrote in another language, and answer them in theirs.

**Price** — $0.00003 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable without a token on this workspace's public MCP endpoint.

Also reachable by name at `POST /api/v1/tools/search_docsbook_docs`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `query` | string | yes | The question, in English, in natural language — not keywords. Long is good: paste the user's whole request if it has several parts, each part is searched separately and the results merged. |
| `limit` | integer | no | Max results (default 8). |

### Request

```bash
curl -X GET 'https://docsbook.io/api/v1/search_docsbook_docs?query=%3Cquery%3E' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

<!-- /widget -->

## Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |
