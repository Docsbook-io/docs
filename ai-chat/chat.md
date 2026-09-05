---
title: "AI chat: what the assistant on your docs can and cannot do"
description: "The contract for Docsbook AI chat — what it answers from, what it refuses, which model runs it, what it costs, and what a reader sees when it fails."
tldr: "AI chat answers reader questions from pages Docsbook fetched for that question and cites them. It refuses rather than guessing when retrieval finds nothing, and every refusal becomes a report line. It is a Pro capability for readers; the owner's own chat stays open on every plan."
---

# AI chat

Docsbook AI chat is a widget on your documentation site that answers a reader's question from the content of that documentation. A reader asks, the server searches your pages, fetches the ones that matched, and streams back an answer that cites them.

The thing worth checking about any docs assistant is not that it answers — it is what it does when it *cannot*. This page is the contract on both sides. The pipeline itself is on [Answer quality](./answer-quality.md).

## What you get

- **An answer in the page, not a ticket.** A reader who phrases the question differently from your heading still reaches the page that answers it.
- **A visible trace.** The widget prints `Found N results`, then one `Reading <page>` line per page opened. Each line is a link, so a sceptical reader can go and check the source themselves.
- **Citations under the answer.** A citation survives only if the server really fetched that page for this question, or the answer quoted its path inline. A path the model neither read nor quoted is dropped before the reader sees it.
- **Follow-up questions.** Three short next questions are generated from the answer and offered as buttons.
- **A record of what failed.** Questions the assistant could not answer become an Unanswered questions report and a `chat.no_answer` webhook, which is the list of pages you have not written yet.

## What the assistant will not do

| It will not | Why |
|---|---|
| Answer from the model's own pretrained knowledge | The instruction block forbids falling back on general knowledge to define a term or fill a gap your docs do not cover |
| Cite a page it neither read nor quoted | A citation survives only if the path was quoted inline in the answer **or** is a page the server actually fetched. The fetched half is grounded by construction; the inline half is not — see [Answer quality](./answer-quality.md#limits) |
| Invent a setup flow | For "how do I set up X", it must point at a sentence in your content naming a concrete menu path, button or step. A passing mention of X is not a setup flow, and it is instructed to say so |
| Omit a stated precondition | If a page states a required plan, role, prior step, version or quota, the answer must carry it — including when that requirement is stated only in the page intro |
| Blend a free feature with its paid upgrade | Pages describing related-but-different things are kept distinct on purpose |
| Guess an anchor | The link target for a cited heading is computed by the server with the same slugifier that renders your page, never taken from the model |

## How does an answer get produced?

Short version; the detail is on [Answer quality](./answer-quality.md).

1. **Optional pre-hook.** If you registered one, your endpoint sees the question first and can block it or inject context. See [Chat hooks](./chat-hooks.md).
2. **Retrieval.** Vector search and Postgres full-text search both run, and their results are merged — capped at five pages total. Two lexical fallbacks cover corpora with no vector index.
3. **Fetch.** Each selected page is read from your repository at its default branch and clipped to 12,000 characters, keeping the head *and* the tail.
4. **Generation.** The pages, your system prompt, and the grounding rules go to the model; the answer streams back as markdown plus a citation array.
5. **Citation filtering.** Refs are checked against the pages actually read, and anchors are recomputed server-side.
6. **Recording.** Token counts and provider cost are written to your usage ledger; `chat.question_asked` fires, and `chat.no_answer` too when the answer admitted it did not know.

## What you can configure

| Control | What it changes | Where |
|---|---|---|
| **System prompt** | Replaces the default instruction with your voice and rules. It is added *alongside* the grounding rules, not instead of them | Chat settings |
| **Suggested questions** | The starter prompts in the empty state — the highest-leverage text in the widget, because they tell a reader what the assistant is for | Chat settings |
| **Call-to-action URL** | The assistant answers the question first, then points at that link in one sentence — only when the reader is evaluating, comparing, or asking about limits, pricing or plans, and never more than once per reply | Chat settings |
| **Model** | Which model answers readers. Free on every plan | Chat settings |
| **Pre / post / streaming hooks** | Your own HTTPS endpoints around each answer | [Chat hooks](./chat-hooks.md) |
| **Semantic index** | Meaning-based retrieval on top of keyword matching | Float Widget → AI Chat → Semantic Search |

An assistant that ends every answer with a pricing link stops being trusted, which costs more conversions than it wins — that is why the call-to-action is worded as a constraint on *when* to offer it rather than as a standing instruction to advertise.

## Which model runs the chat?

The reader chat's managed default is **`openai/gpt-4o-mini`** through OpenRouter: a 128,000-token context window and a 16,384-token output cap, per [OpenAI's model reference](https://developers.openai.com/api/docs/models/gpt-4o-mini). You can pick any model from the chat catalog instead, on every plan, and the picker prints each model's price per million tokens next to it.

Two model settings exist because two different assistants are at work, and they are measured separately:

- **AI Visitors Chat Model** — what answers your readers.
- **Admin & AI Agent Model** — what runs the assistant inside your dashboard, which calls tools and edits your docs.

They are deliberately not one setting. Docsbook once shipped a release where the admin loop silently ran on the reader chat's default because one parameter was not passed through, and both surfaces looked identical from the outside for weeks. A model measured for tool-calling is not automatically the right model for reader Q&A, and vice versa; keeping the constants apart is what makes each choice checkable.

Only models in the published catalog are honoured on Docsbook's key, because spend is billed at the model's real price — an unrecognised model would be charged at a rate you were never shown. If you [bring your own provider key](../guides/advanced/premium.md), you can name any model your provider offers, and usage goes to your key at your provider's price instead of your Docsbook balance.

## Availability and cost

**AI chat for readers is a Pro capability.** On a Free project a visitor's question is refused before any model is called, whatever key the project holds — the gate is a tier decision, not a cost decision, so bringing your own key does not re-open it. The owner's own questions in the admin chat stay open on every plan. Current plans are on the [pricing page](https://docsbook.io/pricing).

Three things in the chat are metered against the project balance: an answer to a reader, building or rebuilding the semantic index (and the embedding of each incoming question), and an agent run started from the chat. Hosting the widget, serving the page, keyword search, page feedback and hook calls are not metered.

Metered and *calls a model* are not the same list, and it is worth knowing which way each one falls. Two model calls on the reader path are **not** billed today: the three follow-up questions under an answer, and the agentic search loop that only runs when every retriever came back empty. One model call that is not part of the reader path **is** billed: the judge that fills the **Answered** column on your Chat tab, charged as owner-side AI work.

When the balance is exhausted, the chat stops rather than billing further. The server's own response distinguishes a plan limit from a cap you set yourself, and only the first is counted as a paywall hit — so a self-imposed source limit never shows up in your funnel as demand for an upgrade. The reader is told the chat has paused either way.

## What a reader sees when something fails

| Situation | What the reader gets |
|---|---|
| No AI chat connected for this site | A plain explanation asking them to contact the site owner. Never a stack trace |
| Project on Free | Nothing. The chat surface is not rendered at all, so there is no button and no message — the reader sees a documentation site without an assistant |
| Balance exhausted | The chat pauses and says so |
| Retrieval found nothing | An answer that says plainly the docs do not cover it — and a row in your Unanswered questions report |
| Your pre-hook blocked the question | A generic error message. See the limit below |
| Model or network failure | "Something went wrong. Please try again.", in the reader's language |

## Limits

- **A blocked question does not show your reason to the reader.** The pre-hook's `reason` string is sent in the response stream, but the docs-site widget renders the generic error message instead. Under question: the field is delivered and a custom front-end can read it, but the shipped widget does not. Treat `reason` as a value for your own logs until this is fixed.
- **Multiplayer chat is built but not switched on.** The invite UI, presence button and API routes exist; the transport does not, so activating a shared session returns "Temporarily unavailable". Do not plan around it.
- **The no-answer detector is an English pattern match.** A refusal written in another language is not recognised, so `chat.no_answer` and the Unanswered questions report under-count on non-English sites.
- **Answer feedback and page feedback are different series.** A thumbs-down on an *answer* is not the same event as a thumbs-down on a *page*; see [Page feedback](./feedback.md) for what each one reaches.
- **No published accuracy figure.** Docsbook does not claim an answer-accuracy percentage. [Answer quality](./answer-quality.md) explains what is measured instead and why we do not quote a number.
- **The default reader model is the provider's to change.** Context window, refusal behaviour and price are theirs; the retrieval and citation mechanism is ours.

## Related

- [Answer quality](./answer-quality.md) — the retrieval and grounding pipeline in full, with sources.
- [Sources](./sources.md) — what the assistant may read beyond your own pages.
- [Chat hooks](./chat-hooks.md) — block, enrich, or mirror every answer.
- [Search](./search.md) — the keyword index the chat shares with your search box.
- [MCP server](../agent-ready/mcp.md) — manage chat settings from Claude Code or Cursor.
- [Pricing](https://docsbook.io/pricing) — what an answer draws on.
