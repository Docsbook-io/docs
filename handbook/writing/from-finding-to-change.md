---
title: "From a finding to a change: which fix answers which defect"
description: "Each class of audit finding mapped to the change that answers it, and the fixes that make things worse — like rewriting a body when the title was wrong."
tldr: "Diagnosis and treatment are different jobs. Every finding is one of three failure modes — missing, unhelpful, or unfindable — and the mode decides the fix: a missing page is a page-set decision, an unhelpful page is a rewrite, and an unfindable one is fixed by a title, a link or the navigation, never by a body rewrite. Ship one change per page per pass, or the next measurement cannot say which change worked."
---

# From a finding to a change

An audit produces findings. This page maps each class of finding to the change that answers it — which is the whole reason diagnosis and treatment are kept apart: they are different jobs, and a process that does both can be trusted at neither. What the findings themselves look like, and how they are graded, belongs to [Auditing](../auditing/README.md).

**Before any of this:** the apply route must already be settled — pull request, approve in chat, or direct update. That is the audit's gate, and nothing below runs before it is answered.

**One change per page per pass.** If a page needs a title rewrite, a restructure and a merge, ship the title and let it be measured. Bundled changes make the next measurement unable to say which one worked.

## Which of the three failure modes is it?

The mode decides who acts, and mislabelling it is expensive in one direction specifically: writing a new page when the real problem was the title costs a week and does not work.

| Finding says | Meaning | Who acts |
|---|---|---|
| **Missing** | No page answers the question | A page-set decision, not a writing one — see [The page set](../planning/page-set.md). Never write it as part of a fix. |
| **Unhelpful** | The page exists and does not answer | A rewrite, per the playbooks below |
| **Unfindable** | The answer exists and readers never reach it | A title, a link or the navigation — **not** a body rewrite |

## Playbooks

<!-- widget:accordion -->

### A title ranks for a query it shares no words with

The page already earns impressions; only the click is missing. Rewrite the title into the query's own phrasing, write a real description, and open the first paragraph with a one-sentence direct answer. Ship all three verbatim and paste-ready — never "improve the title".

Keep the URL and keep the subject. Both forfeit the ranking this fix exists to exploit.

### Readers searched, saw the page listed, and opened nothing

The reader's own rejected queries are the vocabulary. Use their words, not the product's. Feature names are decided by people who already know what the feature does; queries are typed by people who do not, and when the two disagree the reader is right by definition. [The reader's own words](../lenses/user-language.md) covers where that vocabulary comes from; [`get_search_zero_click`](../../mcp/analytics/get-search-zero-click.md) is where this finding is visible.

Rewrite the title **and** the first line — the first line is what the result snippet shows, and where the reader confirms the guess the title made. A title that over-promises turns a non-click into a dead end, which is worse than the original; if the proposed title promises something the page does not deliver, the diagnosis was wrong.

Never rewrite a body here. If the body is also wrong, that is a separate and more expensive finding — note it and move on. Mixing the two destroys the one thing that made this fix worth doing.

### A page ranks for a query it genuinely does not answer

No rewrite saves this. Record it as a content gap for whoever decides the page set, and let the page stop competing for that query. If its queries split across both cases, the page is trying to be two pages — say so instead of averaging it into one recommendation.

### Readers give up on the page

Read the journeys before touching the text ([`get_page_journeys`](../../mcp/analytics/get-page-journeys.md)). The step *before* the exit is usually the real problem. Then, depending on what the journeys show: rewrite the section they give up in, add the missing next step, or fix the page that should have sent them somewhere else.

Never recommend a rewrite on exit rate alone, and never rewrite a page readers leave from *after succeeding* — that is a terminal success page, and rewriting it makes the documentation worse.

### Readers stay a long time and dislike it

High dwell with negative feedback is confusion, not interest ([`get_negative_feedback`](../../mcp/analytics/get-negative-feedback.md)). It is a correctness or clarity problem: an accuracy pass on the specific section, and usually a structure problem underneath — a section answering three questions at once, or an answer arriving after three paragraphs of background. See [Writing rules](./writing-rules.md#3-write-so-a-single-section-can-be-quoted) and [answer in the first 60 words](./retrieval.md#how-much-of-the-answer-belongs-in-the-first-60-words).

### A page has traffic and no outgoing clicks

Either the action is buried, badly worded, or wrong for that reader — a signup prompt on a page whose readers already signed up ([`get_dead_end_pages`](../../mcp/analytics/get-dead-end-pages.md)). Fix the wording and the placement first; the placement rule is one primary action per page, at the point where the reader has just got what they came for. If the page is genuinely terminal, give it related links instead.

### An assistant cannot answer from a page that covers the topic

This is retrieval, not content. Apply [Writing for retrieval](./retrieval.md): name the subject in full inside the section, answer in the first 60 words, split a section that answers three questions. If the page is not server-rendered or the crawlers are blocked, no rewriting will help — that is a configuration fix, covered in [Site capabilities](../automation/site-capabilities.md).

If the assistant's own retrieval or instructions are the problem rather than the page, that is a tuning loop rather than a rewrite — see [Automation](../automation/README.md) and [AI chat](../../ai-chat/README.md).

### The documentation supports but does not sell

A pre-purchase minority means the highest-intent page space is spent on people who already paid. Add the evaluation layer per [Conversion](./conversion.md): what it costs, what it replaces, what to do next. Where a specific objection survives a correct answer, the fact is documented and the reassurance is not — promote it into an FAQ objection-killer.

### The documentation quotes a price that is no longer true

**Do not edit it.** A wrong number may mean the pricing page changed without a decision anyone signed off, and an automatic rewrite erases the evidence. Propose the corrected line with both sources quoted, and let a human apply it.

The same holds for any claim about another company: propose the corrected sentence, never assert it on their behalf.

### A page states something a partner's documentation contradicts

Propose the correction with the source URL and the date it was read. Where the linked page is simply gone, the page needs a new destination or an archived note, not a patched sentence. Where a product was discontinued, the page is archived with a migration note rather than corrected.

### Content is stale

A page carrying "coming soon" past its date, a past date presented as a future promise, a leftover TODO, an old version referenced prominently: fix the sentence, and where the underlying thing shipped, replace the promise with the link.

**Deprecated content gets a banner and a specific migration path — never deletion.** "Use `newMethod()`, see [guide]", never "use the new API". It stays for at least one major release, and current pages linking to it note the deprecation.

### A translation has fallen behind

Re-translate from the current source. Until it is current, the page carries an outdated-content banner: a stale translation is worse than none, because it is trusted. Code is never translated — only the surrounding prose and the code comments — and a translated string value, or a comment that breaks the syntax, is a defect to fix rather than a style choice. See [Translations](../../translation/README.md).

### Two pages compete for the same query

Flag it. Neither wins while they split the signal, but the merge decision belongs to a human — it changes what the documentation contains, not just how it reads.

### Structure, accessibility and link defects

These are mechanical and safe to batch, and they are the one exception to "one change per page": a heading-level fix, an added code-block language, an added alt text and a fixed anchor can ship together, because none of them is a hypothesis about reader behaviour and none needs measuring.

Broken internal links and orphan pages are the exception's exception: a link added to fix an orphan changes the graph, so say which page it was added from and why that page is the right parent.

<!-- /widget -->

## After the change

Record the baseline the audit asked for — the numbers today, the window, the date, and the one number expected to move, with a horizon. Then stop. Measuring it is the next run's job, and the loop only closes if this run wrote the baseline down. [Did it work?](../auditing/did-it-work.md) is that next run.

## Related

<!-- widget:cards plain cols=2 -->

- [Writing rules](./writing-rules.md) — the rules a rewrite has to satisfy once you know which rewrite it is. {file-text}
- [Writing for retrieval](./retrieval.md) — the fix for every finding that is really about passages rather than pages. {sparkles}
- [Conversion](./conversion.md) — the fix for documentation that explains and never asks. {target}
- [Auditing](../auditing/README.md) — where the findings come from, and how they are graded before they reach this page. {chart-line}

<!-- /widget -->
