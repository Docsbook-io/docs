---
title: "AI Chat — Answer Questions From Your Docs"
description: "Embed an AI chatbot trained on your documentation. Streaming answers, custom providers, suggested questions, and pre/post-LLM hooks."
---

# AI Chat

Docsbook ships an AI chatbot trained on the content of your specific documentation. Readers ask a question, the bot searches relevant pages, reads them, and returns a streamed answer with citations.

## How it works

The chat uses a RAG flow built on tool calls. The model decides when to invoke each tool, and the UI shows the live trace of every step.

1. **Search** — the model queries the indexed graph of your docs for relevant sections.
2. **Reading** — it opens specific pages and quotes the text it needs.
3. **Answer** — it composes the response and streams it to the reader via `streamdown`.

Each call is logged so you can later inspect what was asked, what was retrieved, and whether the answer was useful.

## Customization

You control how the bot behaves without writing backend code:

- **Suggested questions** — seed the empty state with 3–5 starter prompts.
- **System prompt** — replace the default instruction set with your own voice and rules.
- **Pre/post-LLM hooks** (PRO) — transform the prompt before the LLM sees it and post-process the response before the reader sees it. See [Chat Hooks](./chat-hooks.md).

## Providers

The default provider is OpenRouter with `openai/gpt-4o-mini`. You can switch to any of:

```yaml
providers:
  - openrouter
  - openai
  - gemini
  - anthropic
```

Bring your own API key from the workspace settings **(Business plan)** — this also lets you pick a custom model for the provider, not just supply a key. Costs charged by the upstream provider are billed to your key, not to Docsbook.

## Limits

AI chat runs on **every plan**. Plans differ by the monthly AI **token budget**, not by a feature switch.

| Plan | AI chat |
|---|---|
| Free | Included — smaller monthly token budget |
| Pro | Included — larger monthly token budget |
| Business | Included — largest budget; can bring your own API key & model |

## Why it matters

Teams using Docsbook AI Chat deflect **847 support tickets per month on average** — readers find answers without opening Slack or email.

## Pricing

AI Chat is available on **all plans**, including Free — it's limited by the monthly AI token budget, which grows on **Pro** (monthly, 7-day free trial) and **Business** (monthly, 14-day free trial, largest budget). Business can additionally bring its own provider API key and model.

## Related

- [Chat Hooks](./chat-hooks.md) — Inject and post-process the LLM pipeline.
- [MCP Server](./mcp.md) — Manage chat settings from Claude Code.
