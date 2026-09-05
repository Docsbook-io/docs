---
title: "Answer readers with AI chat"
description: "Give readers an assistant that answers from your indexed pages instead of opening a ticket — what it can read, how to configure it, and how readers rate the answer."
---

# Answer readers with AI chat

This is the job from ["Support answers the same five questions every week"](../use-cases.md#support-answers-the-same-five-questions-every-week): the answer already exists in your documentation, but a reader who phrases it differently from your heading gets nothing and opens a ticket instead.

| Surface | What it does | Page |
|---|---|---|
| AI chat | Answers from your indexed pages and cites the page it answered from | [AI chat](./chat.md) |
| Full-text search | A keyword fallback in the header, the sidebar, or both | [Search](./search.md) |
| Connected sources | Repositories and sites the assistant reads as fact instead of recalling them | [Sources](./sources.md) |
| Chat hooks | Your own HTTPS endpoint, run before and after the model | [Chat hooks](./chat-hooks.md) |
| Docs skills | `SKILL.md` files that teach any agent how to do documentation work | [Skills](./skills.md) |
| Page feedback | Thumbs up and down on every page, so you see which answers land | [Page feedback](./feedback.md) |

What the chat could not answer is recorded — unanswered questions and searches that returned nothing tell you which page to write next. Assistant answers are AI work and draw on the project balance; search, feedback, sources and hooks do not.

## Where should I start?

Connect your [Sources](./sources.md) first. A connected source is what stops the assistant answering from memory: with a repository or a site registered, "what does this cost" begins by reading it, rather than by guessing. Then turn on [AI chat](./chat.md) itself.

## Related

- [Get cited by AI and found by search](../ai-visibility/README.md) — the other half of the AI layer: being read and quoted OFF your own site
- [Use cases](../use-cases.md) — the situations teams bring to Docsbook
