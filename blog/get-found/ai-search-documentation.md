---
title: "AI search for documentation: why keyword search fails"
description: "Why documentation search returns nothing for the questions readers type, how AI search answers by meaning, and how to turn every failed search into a page."
layout: landing
---

<!-- widget:story share -->

[All posts](../README.md)

**Get found**

# AI search for documentation

[Start free](https://docsbook.io/?start=1)

**AI search** {bg:navy}

Keyword search fails when a reader describes the problem in their own words and your page uses different ones; AI search answers by meaning, and the lasting fix is to write the page the failed searches were asking for.

- **Category** — Get found
- **Reading time** — 4 min

[Get discovered](../../get-discovered.md)

<!-- /widget -->

## Why does keyword search return nothing?

Keyword search matches the words in the query against the words on the page. A reader who types "reset my password" gets nothing when the page is called "Account recovery".

Readers rarely type your headings. They type the symptom or the question:

- "why does my webhook keep failing"
- "can I use this without an API key"
- "what is the difference between the two plans"

When the words don't match the page that answers them, a keyword index comes back empty and the reader leaves or opens a ticket.

## How does AI search work?

AI search compares meaning instead of words. Most implementations follow the same three steps:

1. **Your pages are split into passages**, and each passage is turned into an embedding: a vector that stands for what it means.
2. **The reader's question is embedded the same way.**
3. **The closest passages are retrieved**, and a language model writes the answer from them, citing the pages they came from.

Because retrieval works on passages, a section that names its own subject retrieves better than one that leans on the heading above it.

## What does Docsbook do with search?

Every Docsbook site gets a search box, and the misses become work for the agent:

- **Search box** — full-text search over every page, with titles weighted above body text.
- **Ask AI** — with the [AI chat](../../ai-chat/README.md) on (Pro), the search box offers to ask the question instead. The chat answers with the pages it used, cited; with **Semantic Search** on in **Settings ▸ Agent**, it finds those pages by meaning.
- **Every miss is recorded** — a search that returns nothing is logged once the reader stops typing; the agent reads those misses, and the **Write the pages readers wanted** [trigger](../../agent/triggers.md) wakes on them.
- **The agent writes the missing page** — the **Write the pages readers wanted** trigger wakes on a search with no results; **File the search gaps** files the misses as a ranked issue every day.

<!-- widget:callout type=tip -->

A better search engine finds the page you have. Only a new page answers the question you don't cover yet, which is why Docsbook routes every miss to the agent ([Find wins fast](../../find-wins-fast.md)).

<!-- /widget -->

## What should you measure?

Three numbers show whether readers find their answers:

- **Searches with no results** — each one names a page or a section that is missing.
- **Chat questions nobody answered** — the **Answer what the chat could not** trigger works from these.
- **Tickets the docs already answer** — tag them for a month; if the count stays high, the answer exists but readers can't find it.

In Docsbook the first two are collected for you. You can also ask your agent in one sentence ([Get discovered](../../get-discovered.md)):

```text
Read last month's failed searches and unanswered chat questions, and write the three pages that would answer most of them.
```

## FAQ

<!-- widget:accordion -->

### Is AI search the same as an AI chat?

No. AI search finds the passages that mean what the reader asked; an AI chat also writes the answer from them, and Docsbook's cites the pages it used.

### Does AI search replace good headings?

No. Retrieval works on passages, and a passage whose heading and first sentence name the subject is easier to find by keyword and by meaning.

### Do I have to build a vector database?

Not on Docsbook: turn on **Semantic Search** in **Settings ▸ Agent** and the index is built from your repository and kept current, billed as AI usage. Building your own means owning the embeddings, the index updates and the answer model.

<!-- /widget -->

## Next steps

<!-- widget:cards plain cols=2 arrow=hover -->

- [AI chat](../../ai-chat/README.md) — Answers for your readers, with the pages cited {messages-square}
- [Find wins fast](../../find-wins-fast.md) — How failed searches become the next page {zap}
- [Analytics](../../analytics/README.md) — What readers searched, asked and rated {chart-line}
- [Get cited by ChatGPT](./how-to-get-docs-cited-by-chatgpt.md) — When the search happens inside an AI engine {quote}

<!-- /widget -->
