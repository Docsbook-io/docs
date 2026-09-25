---
title: "Ask the documentation a question"
description: "Ask this workspace's documentation a question and get one grounded answer back, with the pages it was drawn from."
---

# Ask the documentation a question

<!-- widget:api -->

## POST /api/v1/chat

Ask this workspace's documentation a question and get one grounded answer back, with the pages it was drawn from. This is the same retrieval and the same model call the Ask AI widget on the published docs site makes — not a second engine — so an answer here and an answer there agree, and a fix to one is a fix to both.

The call spends from the project owner's account balance — for a project in a team, the team owner's — the same balance the widget spends from. There is no separate API quota.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `question` | string | yes | What to ask the documentation. |
| `currentPath` | string | no | The page the reader is on, so the answer can prefer nearby context. |
| `lang` | string | no | Answer in this language. Defaults to the workspace's default language. |
| `sessionId` | string | no | Groups several calls as one conversation, the way a multi-turn chat is. |
| `mentionedPages` | string[] | no | Page paths to put in front of the model regardless of what retrieval finds. |

### Returns

| Field | Type | Description |
|---|---|---|
| `answer` | string | The answer, in markdown. |
| `refs` | object[] | The pages the answer was drawn from. |
| `follow_up_questions` | string[] | — |

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/chat' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"question":"How do I connect a custom domain?","currentPath":"guides/advanced/custom-domain"}'
```

### Response

```json
{
  "answer": "<answer>",
  "refs": [],
  "follow_up_questions": []
}
```

### Responses

| Status | Meaning |
|---|---|
| `200` | The grounded answer, its sources, and suggested follow-up questions. |
| `400` | `question` was missing or empty. |
| `401` | Missing or invalid API key. |
| `403` | AI chat is switched off for this workspace. |
| `429` | The balance this workspace spends from is used up. |

<!-- /widget -->
