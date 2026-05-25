---
title: "How to Get Your Documentation Cited by ChatGPT (2026)"
description: "A practical checklist for making documentation discoverable and quotable by ChatGPT, Claude, Perplexity, and Gemini — llms.txt, structure, factual prose, and the JSON-LD that matters."
---

# How to Get Your Documentation Cited by ChatGPT

When a developer asks ChatGPT "how do I use feature X in product Y", one of two things happens. Either ChatGPT cites your docs and quotes you correctly, or it hallucinates an API surface that does not exist. Which one happens depends on the work you have done.

This is the working checklist we use at Docsbook for our own docs and for customers.

## TL;DR

1. Publish a clean `llms.txt` at your root
2. Serve clean HTML with content visible without JavaScript
3. Write factual, declarative prose — not marketing copy
4. Add a TL;DR or summary block at the top of every page
5. Use JSON-LD: `TechArticle`, `FAQPage`, `SoftwareApplication`
6. Keep page response under 1 second
7. Make sure your robots.txt allows the right AI crawlers

The rest of this post is the why and how for each.

## 1. llms.txt is the new robots.txt

ChatGPT, Claude, and Perplexity now look for `/llms.txt` on first contact with a domain. A well-formed `llms.txt` cuts hallucination rates dramatically because the agent uses your shortlist instead of guessing URLs.

See [the complete llms.txt guide](./llms-txt-guide.md). Docsbook generates one automatically per workspace.

## 2. Render content without JavaScript

AI crawlers run lightweight HTML parsers. Most do not execute JavaScript. If your docs are a single-page app that fetches content after `DOMContentLoaded`, AI sees a blank page.

Three checks:

```bash
curl -s https://yourdomain.com/docs/page | grep -c "your unique phrase"
```

If the count is 0, you are invisible to AI.

- Use server-side rendering or static generation
- Avoid hydration-only patterns for primary content
- Test with `curl` and `lynx`, not just Chrome

## 3. Write factual prose, not marketing

AI models prefer declarative sentences over hedged marketing language. Compare:

> "Docsbook is a leading platform that empowers teams to revolutionize their documentation workflows."

versus

> "Docsbook publishes a documentation site from a GitHub repository in five seconds. PRO is $150 one-time. Translations support 15 languages."

The second sentence is quotable. The first is filler. Quotable sentences end up in answers; filler does not.

## 4. TL;DR at the top of every page

AI agents are extraction machines. Give them an obvious extraction target.

A useful pattern: a `## TL;DR` heading followed by 3–5 bullet points containing the most important facts. AI models lift these almost verbatim into answers.

Docsbook does this on every blog post. So does every well-cited Stripe documentation page.

## 5. JSON-LD that AI actually uses

Three types matter for documentation:

- **`TechArticle`** — for how-to and tutorial pages
- **`FAQPage`** — for any page with Q&A blocks
- **`SoftwareApplication`** — for your product overview page (price, OS, ratings)

Docsbook adds these automatically. If you are on a self-built site, the [Documentation SEO guide](./documentation-seo-guide.md) covers implementation.

## 6. Speed matters for crawlers too

AI crawlers have stricter timeouts than Googlebot. A page that takes 3 seconds to first byte gets dropped.

- Run PageSpeed Insights, aim for 90+
- Avoid blocking analytics scripts in the head
- Cache aggressively at the CDN

Docsbook pages score 95+ on PageSpeed Insights by default. Static generation, minimal JavaScript, Vercel edge.

## 7. Robots.txt for AI crawlers

The major AI crawlers in 2026:

| Crawler | User-agent | Used by |
|---|---|---|
| GPTBot | `GPTBot` | ChatGPT browsing and training |
| OAI-SearchBot | `OAI-SearchBot` | ChatGPT Search |
| ClaudeBot | `ClaudeBot` | Claude.ai and Anthropic search |
| PerplexityBot | `PerplexityBot` | Perplexity |
| Google-Extended | `Google-Extended` | Gemini, Google AI Overviews |
| CCBot | `CCBot` | Common Crawl (training data for many models) |

For documentation, you generally want to allow all of them. The default `robots.txt` Docsbook ships does. If you are blocking some — check whether that is intentional.

## 8. Bonus: get cited as the canonical source

ChatGPT prefers to cite a URL that other sites already link to. If your docs are linked from your homepage, your changelog, your blog, and your GitHub README, AI models gain confidence that you are the canonical source for your own product.

Internal linking is undervalued. So is putting `docs.yourcompany.com` in your GitHub repo's About link.

## Common mistakes

- **Cloaking** — Showing different content to crawlers than to users. AI models test this; they downrank inconsistencies.
- **Excessive marketing copy at the top** — Anything above the first H2 is heavily weighted. Put facts there.
- **Hidden prerequisites** — A page that assumes "you have set up X" without linking to X traps the AI into half-answers.
- **No code samples** — Developer queries are heavily code-shaped. Pages without code get cited less.

## How to measure citation

Three signals worth tracking:

1. **Direct referrals from `chat.openai.com`, `perplexity.ai`, `claude.ai`** — visible in your analytics
2. **AI question logs** — if you run a docs AI chat, the questions tell you what people expect to find
3. **Mention monitoring** — Google your product name + "ChatGPT" once a month to see anecdotal citations

Docsbook ships AI usage analytics (`get_ai_questions`, `get_ai_unanswered`, `get_failed_searches`) so you can see what people are asking that you do not answer well.

## Related reading

- [llms.txt: the complete guide](./llms-txt-guide.md)
- [Perplexity citations for docs](./perplexity-citations-for-docs.md)
- [Documentation SEO guide](./documentation-seo-guide.md)
- [JSON-LD for documentation](./json-ld-for-documentation.md)

---

Docsbook handles `llms.txt`, JSON-LD, server-side rendering, and AI crawler robots.txt automatically. [Publish your docs →](https://docsbook.io/start)
