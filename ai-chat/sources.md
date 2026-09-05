---
title: "Sources: what your docs assistant is allowed to go and read"
description: "Connect a repository, a site or a single page as a source, and the Docsbook assistant and your own MCP agents fetch it before answering instead of recalling your facts from training data."
tldr: "A connected source is an address the assistant is allowed to fetch. With one registered, \"is this still true?\" becomes a read of your repository or your pricing page rather than a guess from a model whose knowledge stopped months ago. Sources are ungated, they are never crawled on a timer, and a failed read is reported rather than filled in."
---

# Sources

A **Docsbook source** is a repository, a website or a single page that this project's assistant and agents are allowed to fetch. Connect one, and "update the documentation" or "is this page still true" starts with a read instead of a recollection.

Open the **Sources** section of your project's admin panel, directly under MCP and Agents.

## What you get

- **An address the assistant can go to.** Ask what your product costs, and it fetches your pricing page for this question rather than answering from what it absorbed in training.
- **The same registration in your own tools.** The two tools that are the feature, `list_sources` and `read_source`, are served over your project's [MCP endpoint](../agent-ready/mcp.md), so a source you connect here means the same thing in Claude Code or Cursor.
- **A sentence of yours attached to each one.** The note you write ("the API server the reference pages describe") is read as instruction by everything that later reads that source.
- **A read that fails loudly.** An unreachable repository comes back as an error with a hint, never as an empty list that reads like an empty repository.
- **No plan gate.** Sources are on every plan, deliberately: a paywall here would be selling the ability to tell the truth.

## What can I connect as a source?

Four kinds exist under the covers — **Website**, **Page**, **Repository** and **Repository folder** — and the table presents them as a catalogue of the *named* things owners actually ask about, in five groups: *Your project*, *Documentation platforms*, *Knowledge bases*, *Code and APIs* and *Community*. A published documentation site is a website whoever built it, so Mintlify, GitBook, ReadMe, Docusaurus, Read the Docs, MkDocs, Nextra, VitePress, Starlight, Redocly, Stoplight, Scalar and the rest need nothing built per vendor.

The table lists every kind Docsbook knows about, connected or not, narrowed through a **Filters** menu rather than split into sections. Each connection is its own row: two connected websites are two rows.

Grey means two different things, and the row says which:

- **Not connected** — the row offers a **Connect**. Reading it works today, through the same public fetch every other `url` row uses.
- **Not available yet** — the row offers no button and prints what it would need: an authorisation you grant once (Notion workspace, Confluence, Coda), a bot token (Telegram, Discord, Slack), or a reader for a repository host Docsbook does not read yet (GitLab, Bitbucket). Where a workaround exists the row names it — a public help centre connects as a Website today.

A row without a button is deliberate. A row is only allowed to offer **Connect** if `read_source` can genuinely read it as it stands; a Connect that cannot connect makes every other row on the screen untrustworthy.

## How do I connect a source?

Press **Connect** on a row, or **New Source** above the table. Either way there is one field, and the **address** decides what the source is — not the row you pressed. The row you clicked only sets the placeholder and the heading, and when the two disagree the dialog says so before you commit.

| What you paste | What it becomes | What a read returns |
|---|---|---|
| `github.com/acme/api` | Repository | Its readable files, README and docs first; any path by name |
| `github.com/acme/api/tree/main/docs` | Repository folder | Only that subtree — and only commits inside it |
| `acme.com` or `acme.com/docs` | Website | Several of its pages, found from its own `sitemap.xml` |
| `acme.com/pricing.html` | Page | That one page, read whole |
| `acme.mintlify.app`, `acme.gitbook.io`, `acme.notion.site`… | Filed under that vendor's row | The same as a website, filed where you would look for it |

A file extension in the path is what separates a *page* from a *website*. A link pasted from an issue or a pull request connects the **repository**, not the issue — storing `/issues` as a subtree would produce a source that reads back empty forever. Tracking parameters (`utm_*`, `fbclid`, `gclid`, `ref`, `si`…) are stripped, so the same page pasted from a tweet and from your address bar is one source rather than two. A bare host gets `https://`; an `http://` you typed on purpose is left alone, because silently upgrading it produces a source that 404s for a site with no TLS and no way to see why from the row.

**A private repository needs the picker, not a paste.** GitHub answers the same 404 for "private" and for "does not exist", so a pasted address cannot tell Docsbook which it is, and a hand-typed private address connects as public and reads nothing. Use **Or pick one of your GitHub repositories** in the dialog: the picker knows, and a source marked private stores the connecting account's GitHub authorisation, encrypted at rest, so a scheduled run with no browser session behind it can still read the repository. That authorisation never leaves the server — the API answers `has_token`, never the token — and a token GitHub has since rejected is reported as "reconnect this repository" rather than retried in silence.

Two entries appear without you adding them, and neither can be renamed, paused or removed here:

- **This site's repo** — the repository your documentation is built from. It is already being read; making you "connect" it would imply it was not.
- **From Branding** — the Site source URL, if your workspace set one. It still lives on the Branding card.

Re-pasting an address you already connected **updates** that row rather than failing or duplicating it, and a re-paste with no note does not wipe the note you typed the first time.

## What reads a connected source?

Three things, and nothing else. A connected source is not crawled on a timer, is not added to your published documentation, and is not searched by the reader-facing chat on your docs site — that one answers only from your own pages ([Answer quality](./answer-quality.md) is the pipeline it uses).

**The assistant in your admin panel.** `list_sources` and `read_source` sit in its base toolbox rather than behind a lookup, because a capability that costs an extra round trip to discover is one the model answers from memory instead — the exact failure sources exist to prevent.

**Your own MCP agents.** The same two tools over your project's MCP endpoint, plus `connect_source` and `configure_source` for setting one up without opening a browser. Those two need a read-write MCP token.

**Background runs.** Scheduled prompts and agent runs read them too, which is where it matters most: there is nobody sitting there to paste a link.

Not every automated run reaches a source, so the panel says which do rather than implying they all can. Wherever runs are listed, the chips are drawn in three states:

- **Lit** — this run fetches the source: your site's pages, your repository's files.
- **Unlit** — this run knows the source is connected and will name it, but never declared that it leaves the property, so it will not fetch it. Ask the assistant instead; it has no such fence.
- **Nothing at all** — this run reaches no source. A settings write has no business reading your repository, and a chip there would say otherwise.

## How is a source fetched, and how fresh is what comes back?

Nothing is pre-fetched and nothing is mirrored. A read happens when a tool asks for one, against the live address, and these are its edges:

| | Repository | Website / page |
|---|---|---|
| Read without a path | The readable file list, ranked README → prose under `docs/`, `guides/`, `specs/` → other prose → root-level config → everything else, first **300** paths | Up to **10** pages, discovered from `sitemap.xml` |
| Read with a path | That file, from the default branch | That one page, resolved against the source's own URL |
| Size cap | **25,000** characters per file, truncation reported | **25,000** characters for a single page; **8,000** per page in a multi-page read |
| Also available | The last **10** commits — sha, subject, author, date, and the repository's default branch; path-scoped for a repository folder | — |
| Freshness | Default branch cached 1 hour, file tree 5 minutes; file contents and commits are fetched with no cache | Fetched live, every call |
| Timeout | GitHub's own | **15s** per page, **8s** for the sitemap |

Code, lockfiles and build output are filtered out of the *listing* (`node_modules`, `dist`, `build`, `.next`, `coverage` and friends), not out of the reads: `read_source` with a path fetches any file, the filter only decides what gets named without being asked for.

Sitemap scoping is matched at a path **boundary**, not as a string prefix. Connect `acme.com/docs` and `/docs-for-fintech` stays out of it. A section the sitemap lists nothing under falls back to the entry page alone — never to the whole site — and the result says which of the three things happened: pages came from the sitemap, the site has a sitemap but nothing under your section, or there is no sitemap at all. A thin read is never allowed to read as a thin site.

Every outbound fetch goes through the same guard the rest of Docsbook's web reading uses: `robots.txt` is honoured, redirects are followed manually with the address re-validated at each of at most five hops, and private and link-local ranges are refused, so a public URL cannot bounce into a cloud metadata endpoint. Pages that render their content with JavaScript come back with a note saying no readable text was found, rather than as an empty page.

## Online, paused, and what the green dot means

Every connected source shows a green dot and the word **Online**. A paused one shows a grey dot and **Paused**.

> **Online means the source is connected and your agents may read it. It is not a health check.** Nothing pings the host and nothing checks the repository still exists. The honest signal is the **Last used** column, written only when a tool actually fetched the source *successfully* — a failed fetch never stamps it.

**Disconnect** keeps the row and stops everything reading it; press it again (it reads **Connect**) to resume. **Remove** deletes the connection outright, along with any GitHub authorisation attached to it. **Open** visits the address. The two ways to stop reading a source are different on purpose: "stop reading this for now" should not make you retype the address later.

## What happens when a source cannot be read

Every failure is a sentence with a next step, and none of them is an empty result:

| Situation | What the tool returns |
|---|---|
| The source is paused | Names the source and says it is switched off in this workspace's Sources tab |
| A repository tree will not load | "The repository may be private, renamed or deleted. Say so plainly rather than answering from memory about what it contains." |
| A file path is wrong | Suggests listing the repository first — the file may live under a different folder |
| A private repo's stored authorisation stopped working | "GitHub refused … with the authorisation stored for it. Reconnect the repository from Sources." — never an empty commit list |
| A site is down, blocks server-side fetches, or disallows the path in `robots.txt` | Says which, and says to report that rather than describing the site from memory |
| Nothing is connected at all | `NO_SOURCES`, with "Do not invent one" |

That last row is the point of the whole design. The failure mode a source prevents is not an error message — it is a confident paragraph about a repository nobody read.

## What does reading a source cost?

Sources themselves are free to connect and free to keep. Two of the four tools are metered when called over MCP, and they are priced by what serving them actually costs:

- **`list_sources`** reads rows Docsbook already stores, and is priced as an ordinary read.
- **`read_source`** leaves the Docsbook network for GitHub or for somebody's website — and a website source fetches several pages in one call — so it is priced as an outbound call, the same class as `fetch_url`.

Both come off the balance of the project the call is about. Amounts are on the [pricing page](https://docsbook.io/pricing).

## Why this is the right way (evidence)

| Rule in Docsbook | Why it works | Source |
|---|---|---|
| Fetch the source instead of asking the model to recall it | Across a benchmark built for current-world-knowledge questions, "all models (regardless of model size) struggle on questions that involve fast-changing knowledge and false premises" — your prices, limits and endpoints are exactly that class of fact | Vu et al., 2023 — [FreshLLMs](https://arxiv.org/abs/2310.03214) (Findings of ACL 2024) |
| Treat the assistant's own knowledge as dated, whatever the model | The model behind Docsbook's admin assistant publishes a "Knowledge Cutoff" of "Feb 2026". Anything your product changed after its provider's cutoff exists for it only if something fetched it | OpenRouter — [gpt-5.6-luna model page](https://openrouter.ai/openai/gpt-5.6-luna) (vendor-reported) |
| Discover a site's pages from its own sitemap rather than guessing paths | `<loc>` carries the "URL of the page", and the protocol exists so a site can "provide details about your pages to search engines" — it is the site's own answer to "what pages do I have" | [sitemaps.org protocol](https://www.sitemaps.org/protocol.html) (spec) |
| Honour `robots.txt` on every source fetch | RFC 9309 standardises how "service owners \[can\] control how content served by their services may be accessed… by automatic clients known as crawlers" | [RFC 9309](https://www.rfc-editor.org/rfc/rfc9309.html) (IETF standard) |
| Label a fetched source as data to quote, never as instructions to follow | "Indirect prompt injections occur when an LLM accepts input from external sources, such as websites or files" — content the model reads can carry instructions aimed at the model | OWASP GenAI — [LLM01:2025 Prompt Injection](https://genai.owasp.org/llmrisk/llm01-prompt-injection/) (industry standard) |
| Re-validate the address at every redirect hop, and refuse link-local ranges | Cloud instance metadata is served on a link-local address — AWS documents `http://169.254.169.254/latest/meta-data/`, "valid only from the instance" — so a redirect that lands there turns a page fetch into a credential read | AWS — [Access instance metadata for an EC2 instance](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/instancedata-data-retrieval.html) (vendor documentation) |

## Limits

- **A source is read on demand, not indexed.** There is no background crawl, no stored copy and no freshness guarantee between calls. What a tool saw is what the address served at that moment.
- **The green dot is not a reachability check.** See above. A repository deleted this morning shows Online until something tries to read it.
- **A hand-typed private repository connects as public and reads nothing.** Docsbook cannot tell a private repo from a missing one by its address. Use the repository picker, which can.
- **Only GitHub repositories are read as repositories.** GitLab and Bitbucket rows exist and offer no Connect; a public project page on either can be connected as a Website, which reads the rendered pages and not the tree.
- **A website source is not a crawler.** At most ten pages per call, from the sitemap only, no recursion, no link-following. A large documentation site is better connected as its repository.
- **JavaScript-rendered pages come back empty.** The fetcher does not execute scripts. The result says so, so the emptiness is never reported as an absence of content — but you still have no content.
- **Notes are instructions, and they are yours to keep honest.** Everything that reads a source reads your note as guidance. A stale note ("the v1 API, deprecated") steers an agent as effectively as a correct one.
- **We publish no measurement of how much sources reduce wrong answers.** The mechanism is above and the evidence for it is external; a before-and-after number over customer corpora is not something Docsbook has run. Treat "sources improve accuracy on your docs" as a well-supported expectation, not as a figure we have measured.

## Related

- [AI chat](./chat.md) — the assistant on your docs site, and what it may answer from.
- [Answer quality](./answer-quality.md) — the retrieval and grounding pipeline, in full.
- [Chat hooks](./chat-hooks.md) — the other way to hand a model a fact it cannot read.
- [MCP server](../agent-ready/mcp.md) — the same tools, for your own agents.
- [MCP tools reference](../reference/mcp-tools.md) — `list_sources`, `read_source`, `connect_source`, `configure_source` in full.
- [Source of Truth](../agent-ready/source-of-truth.md) — a different feature with a similar name: a local graph of *your own* pages, built on the agent's machine.
- [Pricing](https://docsbook.io/pricing) — what a source read draws on.
