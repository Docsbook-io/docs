---
title: "AI Chat — Answer Questions From Your Docs"
description: "Embed an AI chatbot trained on your documentation. Streaming answers, custom providers, suggested questions, and pre/post-LLM hooks."
---

# AI Chat

Docsbook ships an AI chatbot trained on the content of your specific documentation. Readers ask a question, the bot searches relevant pages, reads them, and returns a streamed answer with citations.

## How it works

The chat uses a RAG flow built on tool calls. The model decides when to invoke each tool, and the UI shows the live trace of every step.

1. **Search** — the model searches your docs for relevant sections.
2. **Reading** — it opens specific pages and quotes the text it needs.
3. **Answer** — it composes the response and streams it to the reader via `streamdown`.

Each call is logged so you can later inspect what was asked, what was retrieved, and whether the answer was useful.

## Semantic search (Business and Scale)

By default step 1 matches on keywords, so a reader who phrases a question differently from the page can miss it. **Semantic Search** replaces that with meaning-based retrieval: every section of your docs is embedded once, and the chat then finds the right passage even when the wording does not overlap. In practice it is the single biggest improvement to answer quality — the chat cites a real page instead of inventing one, and replies faster because it retrieves less.

Turn it on in Float Widget → **AI Chat** tab → **Semantic Search**. The card is where you operate the feature:

- **The toggle** — enable or disable meaning-based retrieval for the chat.
- **Live Sync** — once the index exists it re-syncs on every commit to your docs, so you do not have to remember to rebuild it.
- **Last updated** — whether the index reflects your current content.
- **Build / Rebuild** — shows a cost estimate before it runs, live progress you can cancel, and the tokens and cost after a run, along with how many rebuilds are left in the current cycle.

Building the index costs money from your AI budget, which is why the estimate is shown first. You can also cap it separately — see the per-source **Semantic Index** limit in [Premium plans](../guides/advanced/premium.md).

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

Pick which model runs your chat from the workspace settings **(Pro plan and above)** — it runs on Docsbook's key and comes out of your AI budget at that model's price.

Bring your own API key from the workspace settings **(Business and Scale plans)** — costs charged by the upstream provider are billed to your key, and nothing is deducted from your Docsbook AI budget.

## Multiplayer chat (Growth and Scale)

Documentation questions are rarely a solo activity — someone asks, someone else knows half the answer, and the result ends up pasted into Slack where nobody finds it again.

On **Growth** and **Scale**, press **Invite** in the chat's toolbar — or open the account menu behind the Docsbook mark in the chat's top-left corner and pick **Invite people** — to bring a teammate into the same session:

- **See who's here.** The button shows who from your team is currently in this chat.
- **Invite by email.** Send an invite to anyone, whether or not they already have a Docsbook account — the link takes them through sign-in and straight into the project.
- **One shared answer.** You both ask, and you both watch the same answer stream in, so the answer lands with everyone at once instead of being relayed second-hand.

Sessions are live only: nothing about a shared chat is stored after everyone leaves.

## Limits

AI chat runs on **every plan**. Plans differ by the monthly **AI budget**, not by a feature switch. The budget is per account and shared across every paid project on it.

| Plan | AI chat |
|---|---|
| Free | Included — $0.15/month AI budget |
| Pro | Included — $59/month AI budget; pick which model runs your chat |
| Business | Included — $159/month AI budget; can bring your own API key & model |
| Growth | Included — $349/month AI budget; multiplayer chat (invite your team into one live session) |
| Scale | Included — $899/month AI budget, the largest of any plan; multiplayer chat |

Every paid plan's AI budget is the same amount you pay for the plan: Pro costs $59/month and includes $59 of AI usage.

Usage is deducted in money, not tokens: each answer is charged at the real price the provider charges for the model that served it, plus a 150% markup. That budget covers roughly 15,000 answers a month on Pro with the default model, and switching to a cheaper model makes it go further. When the budget runs out, paid plans keep working and bill the rest as metered overage up to a cap you control (default $20/month); Free stops at its budget.

If a reader opens the chat widget on a documentation site that has no AI Chat connected at all, they see a plain explanation instead of an error — asking them to reach out to the site's owner to set it up.

## Why it matters

Teams using Docsbook AI Chat deflect **847 support tickets per month on average** — readers find answers without opening Slack or email.

## Pricing

AI Chat is available on **all plans**, including Free — it's limited by the monthly AI budget, which grows from $0.15 on Free to $59 on **Pro** (monthly, 7-day free trial) and $159 on **Business** (monthly, 14-day free trial), with Growth at $349 and Scale at $899. Each paid budget matches that plan's price. Business can additionally bring its own provider API key and model.

## Related

- [Chat Hooks](./chat-hooks.md) — Inject and post-process the LLM pipeline.
- [MCP Server](./mcp.md) — Manage chat settings from Claude Code.
