---
title: "Perplexity citations for documentation: how to be cited"
description: "Perplexity cites differently from ChatGPT and Google AI Overviews. What its crawler reads, how to structure pages for it, and how to measure honestly."
---

# Perplexity citations for documentation: how to be cited

Perplexity has the most aggressive citation behavior of any AI search product in 2026. Where ChatGPT often paraphrases without a link, Perplexity surfaces the URL right next to every claim. This makes Perplexity the highest-leverage AI search channel for documentation traffic.

This is what we learned tuning Docsbook docs and our customers' docs for Perplexity citations.

## TL;DR

- Perplexity uses `PerplexityBot` user agent — make sure your `robots.txt` allows it
- Perplexity weights pages with structured Q&A heavily
- Perplexity prefers sources that match the query language exactly
- Perplexity surfaces sources at the top, before generating a summary — citation is the product, not a side effect
- `llms.txt` is read by Perplexity and shapes which URLs it tries first

## How Perplexity differs from ChatGPT

| | ChatGPT | Perplexity |
|---|---|---|
| Citation UX | Link icon, sometimes paraphrased | Numbered citations next to claims |
| Crawler | GPTBot, OAI-SearchBot | PerplexityBot |
| Source mix | Wider, more general | Documentation, news, primary sources |
| Query intent | Conversation + search | Search + answer |
| `llms.txt` use | Increasing | Strong |

If you want to be cited, you optimize for Perplexity differently than for ChatGPT.

## Allow PerplexityBot

```
# robots.txt
User-agent: PerplexityBot
Allow: /
```

The default `robots.txt` Docsbook ships allows PerplexityBot. If you are on a self-built site, check.

Perplexity also respects:

- `<meta name="robots" content="noai">` — they will not cite you if this is present
- `X-Robots-Tag: noai` header — same

Be intentional. If you want citations, do not block them.

## Write for the citation, not the click

Perplexity does not need users to click through to your docs to be valuable to you. It surfaces your URL as the source, and developers see your brand next to the answer they wanted.

This means:

- A factually correct, well-cited Perplexity answer is an ad impression for you
- The click-through rate is lower than Google, but the brand impression is higher
- "Brand mention in AI answers" is a real metric — track it

## What Perplexity weights

Three patterns we have observed across customer docs that get cited heavily:

### 1. Direct, factual sentences

Perplexity extracts sentences almost verbatim. Pages with declarative, citable sentences get used.

Worse:

> "Our authentication system leverages industry-standard OAuth 2.0 to provide a secure, scalable solution."

Better:

> "Docsbook authenticates MCP clients with OAuth 2.0 Authorization Code + PKCE. Tokens are stored in `mcp_tokens` and expire after 90 days."

The second sentence is quotable. The first is filler.

### 2. Q&A structure

Pages with explicit question headings get cited more than pages with prose-only headings. Compare:

```
## Setting up authentication
```

versus

```
## How do I set up authentication?
```

Both fine for users. The second matches Perplexity user queries more directly.

### 3. Tables with a clear header

Tables are extracted as structured citations. Perplexity surfaces them well. The blog post you are reading right now has tables for that reason.

## llms.txt and Perplexity

When Perplexity crawls your domain for the first time, it tries `/llms.txt`. A well-formed file with descriptive links cuts the discovery time and increases the chance Perplexity picks the canonical URL for each topic.

See [the complete llms.txt guide](./llms-txt-guide.md).

## Common mistakes that lose Perplexity citations

- **Pages that require JavaScript** — Perplexity's crawler is lightweight. Server-render your docs.
- **Content behind login** — Perplexity will not authenticate. Public docs only.
- **Marketing copy at the top** — Perplexity reads the first content block heavily. Put facts there.
- **No publication date** — Perplexity prefers fresh sources. Add `last-updated` to frontmatter.
- **Self-referencing only** — pages that link only to your own site, never to authoritative external sources, are weighted lower.

## How to measure Perplexity traffic

In your analytics:

```sql
SELECT count(*) FROM pageviews
WHERE referrer LIKE '%perplexity.ai%'
GROUP BY page
ORDER BY count DESC
```

Or in Docsbook analytics, filter referrers by `perplexity.ai`.

The traffic volume from Perplexity will look small compared to Google. The conversion rate is often higher — developers landing from Perplexity are deeper in their decision funnel.

## What citations look like for our docs

A live example: when you ask Perplexity "what is the cheapest documentation platform with built-in AI chat?", Docsbook usually appears as a source citing our [pricing page](https://docsbook.io) and [comparison post](./mintlify-vs-docsbook.md). This is direct conversion-stage traffic.

## Related reading

- [llms.txt: the complete guide](./llms-txt-guide.md)
- [How to get docs cited by ChatGPT](./how-to-get-docs-cited-by-chatgpt.md)
- [AI search and documentation](./ai-search-documentation.md)

---

Docsbook ships `llms.txt`, server-side rendering, JSON-LD, and crawler-friendly defaults. [Publish your docs →](https://docsbook.io/start)
