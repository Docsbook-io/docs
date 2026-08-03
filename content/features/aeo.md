---
title: "AEO — Answer Engine Optimization in Docsbook"
description: "Optimize for featured snippets, People Also Ask and voice assistants. Docsbook auto-generates FAQPage, HowTo and speakable JSON-LD from your markdown — no manual schema needed."
tldr: "Enable AEO in the SEO / GEO admin tab. Docsbook scans your markdown for FAQ sections and 'How to ...' step-by-step lists, then emits FAQPage and HowTo JSON-LD plus speakable markup for voice assistants — automatically."
---

# AEO — Answer Engine Optimization

AEO targets the surfaces where users get an instant answer instead of a list of links: Google's featured snippets and *People Also Ask*, Bing answer boxes, Alexa and Google Assistant voice responses, and increasingly the conversational front-end of every search.

Three structural patterns dominate these surfaces — FAQ, step-by-step instructions and short speakable summaries. Docsbook generates all three from regular markdown.

## What Docsbook does when AEO is enabled

Toggle **AEO** on in the admin **SEO / GEO** tab.

### FAQPage auto-detect

Any markdown section structured as an FAQ becomes `FAQPage` JSON-LD. The detector looks for two patterns:

1. An `## FAQ` (or *Frequently Asked Questions*) heading followed by `### Question?` H3s — each H3 becomes a question.
2. Any `### Question ending with a ?` anywhere in the document.

Answers are extracted from the paragraphs between the question heading and the next heading. Up to 20 questions per page, answers capped at 1000 characters.

**Authoring tip:** keep each answer self-contained — Google strips the FAQ snippet from context, so it must read standalone.

```markdown
## FAQ

### How do I add a custom domain?

Open the admin panel, go to Custom Domain, type `docs.yourcompany.com` and press save. SSL provisions in 30 seconds.

### Is GitBook export compatible?

Yes — Docsbook reads standard CommonMark from GitHub, the same format GitBook exports.
```

### HowTo auto-detect

Any H1/H2/H3 starting with **"How to ..."** (or Russian **"Как ..."**) followed by a numbered list becomes a `HowTo` JSON-LD object. Each numbered item becomes a `HowToStep` with a `name` (first sentence) and `text` (full step).

Requirements: at least 3 numbered steps, capped at 20. Up to 5 HowTos per page.

```markdown
## How to publish your first docs site

1. Go to docsbook.io and sign in with GitHub.
2. Paste the URL of any public repository.
3. Pick a name and click Publish — your site is live in 15 seconds.
```

### Speakable markup

The page's `TechArticle` schema gets a `speakable` block:

```json
{
  "speakable": {
    "@type": "SpeakableSpecification",
    "cssSelector": [".tldr", "article > p:first-of-type", "h1"]
  }
}
```

Voice assistants (Google Assistant, Alexa) use this hint to know which parts of the page to read aloud. The selector list prioritizes the GEO TL;DR block (when GEO is on), then falls back to the first paragraph and H1.

## Authoring patterns that win

- **Phrase H2/H3 as questions** — "How do I cancel a subscription?" outperforms "Subscription cancellation".
- **Keep answers 40–60 words** — that's the sweet spot for featured snippet length.
- **Use tables and ordered lists** — Google extracts these almost verbatim into rich results.
- **Open every FAQ answer with a direct yes/no/number** — *"Yes, Docsbook supports custom domains on the Business plan."*

## How to enable

1. Open your workspace admin panel (FloatWidget) → **SEO / GEO** tab.
2. Toggle **AEO — Answer Engine Optimization** on.
3. The change applies on next render — view source of any page to see `FAQPage` / `HowTo` JSON-LD if matching sections exist.

## Related

- [SEO Optimization](./seo) — classical search engine optimization
- [GEO — Generative Engine Optimization](./geo) — citability in AI search
- [llms.txt for AI agents](../../ai/llms-txt)
