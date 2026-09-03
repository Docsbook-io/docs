---
title: "AI Chat: answer reader questions from your own docs"
description: "Embed an AI chat trained on your documentation — streamed answers with citations, your choice of model, semantic retrieval and pre/post-LLM hooks."
---

# AI Chat

Docsbook AI Chat is a chat widget on your documentation site that answers from the content of that documentation, not from the model's memory. A reader asks a question, the assistant searches your pages, opens the relevant ones, and streams back an answer that cites the pages it used.

## How does Docsbook AI Chat answer a question?

Docsbook AI Chat answers with a retrieval-augmented generation (RAG) flow built on tool calls. The model decides when to call each tool, and the widget shows the live trace of every step, so a reader can see which page an answer came from.

1. **Search** — the assistant searches your documentation for relevant sections.
2. **Read** — it opens specific pages and quotes the text it needs.
3. **Answer** — it composes the response and streams it to the reader through `streamdown`.

Every call is logged, so you can later inspect what was asked, what was retrieved, and whether the reader found the answer useful. Because the assistant answers out of your indexed pages, a reader who would otherwise have opened a support ticket gets the answer on the page — and a question the assistant could not answer shows up as a documented gap rather than as an email.

## What does Docsbook AI Chat cost to run?

Every answer Docsbook AI Chat streams draws on the balance of the project it answered for. Nothing else in the chat does: hosting the widget, serving the page, and the reader's search are not metered.

Three things in the chat spend the balance, and they are the three that call a model:

- An answer to a reader.
- Building or rebuilding the semantic index.
- An agent run started from the chat.

The current prices, and what a plan includes, are on the [Docsbook pricing page](https://docsbook.io/pricing) — it is generated from the live billing constants on every request, so it is the only figure worth quoting. When a project's balance runs out, AI chat pauses instead of billing you further, and the widget says so.

## Semantic search

Semantic search replaces keyword matching in step 1 with meaning-based retrieval: every section of your documentation is embedded once, and Docsbook AI Chat then finds the right passage even when the reader's wording does not overlap the page's wording. A reader who asks "why is my site blank after a push" reaches the build-failure page that never uses the word "blank".

Turn it on in Float Widget → **AI Chat** tab → **Semantic Search**. The card is where you operate it:

- **The toggle** — enable or disable meaning-based retrieval for the chat.
- **Live Sync** — once the index exists it re-syncs on every commit to your docs, so you do not have to remember to rebuild it.
- **Last updated** — whether the index reflects your current content.
- **Build / Rebuild** — shows a cost estimate before it runs, live progress you can cancel, and the tokens and cost after a run.

Building the index calls an embedding model over your whole corpus, which is why the estimate is shown before the run rather than after it. You can cap the spend per source — see the **Semantic Index** limit in [Premium plans](../guides/advanced/premium.md).

## Customization

You control how the chatbot behaves without writing backend code:

- **Suggested questions** — seed the empty state with 3–5 starter prompts. These are the highest-leverage text in the widget: they tell a reader what the assistant is for.
- **System prompt** — replace the default instruction set with your own voice and rules.
- **Pre/post-LLM hooks** — transform the prompt before the model sees it, and post-process the response before the reader sees it. See [Chat Hooks](./chat-hooks.md).

## Which model runs the chat?

Docsbook runs the chat through OpenRouter by default, on `openai/gpt-4o-mini`, and you pick a different model in the workspace settings. The provider can be any of:

```yaml
providers:
  - openrouter
  - openai
  - gemini
  - anthropic
```

There are two model settings under **Settings ▸ Chat**, because two different models are at work:

- **AI Visitors Chat Model** — what answers your readers in the docs chat.
- **Admin & AI Agent Model** — what runs the assistant inside your dashboard: the one that reads your analytics, calls tools and edits your docs.

Each setting lists its own models with the price per 1M tokens next to them, so a cheap reader chat and a stronger admin assistant — or the reverse — is one choice each. A cheaper model makes the same balance go further. Translations have a model setting of their own under **Settings ▸ Translations**.

You can also bring your own provider API key from the workspace settings. Usage then goes to your key at the provider's own price and is not deducted from your Docsbook balance.

## Multiplayer chat

Press **Invite** in the chat's toolbar to bring a teammate into the same live session. Documentation questions are rarely solo work: someone asks, someone else knows half the answer, and the result ends up pasted into Slack where nobody finds it again.

- **See who's here.** The button shows who from your team is currently in this chat.
- **Invite by email.** The invite works whether or not the recipient already has a Docsbook account — the link takes them through sign-in and straight into the project.
- **One shared answer.** You both ask, and you both watch the same answer stream in, so it lands with everyone at once instead of being relayed second-hand.

Sessions are live only. Nothing about a shared chat is stored after everyone leaves.

## What a reader sees when no chat is connected

If a reader opens the chat widget on a documentation site that has no AI Chat connected, they see a plain explanation instead of an error, asking them to contact the site's owner to set it up. The widget never fails silently and never shows a stack trace to a reader.

## Related

- [Chat Hooks](./chat-hooks.md) — intercept the prompt and the answer.
- [Sources](./sources.md) — what the assistant reads before it answers.
- [MCP Server](./mcp.md) — manage chat settings from Claude Code.
- [Pricing](https://docsbook.io/pricing) — what an answer draws on.
