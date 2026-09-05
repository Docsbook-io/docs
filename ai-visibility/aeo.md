---
title: "AEO: get your docs into answer boxes and voice replies"
description: "Docsbook detects FAQ sections and How-to procedures in your Markdown and emits FAQPage, HowTo and speakable JSON-LD — with the shapes the detector needs."
tldr: "Turn AEO on in the admin SEO / GEO tab. Docsbook scans your Markdown for FAQ sections and 'How to …' numbered procedures, then emits FAQPage and HowTo JSON-LD plus speakable markup for voice assistants."
---

# AEO — Answer Engine Optimization

Docsbook AEO generates the structured data that answer surfaces read: Google's featured snippets and *People Also Ask*, Bing answer boxes, and the voice replies of Google Assistant and Alexa. Toggle **AEO** on in the admin **SEO / GEO** tab, and Docsbook emits `FAQPage`, `HowTo` and `speakable` JSON-LD from the Markdown you already wrote.

AEO is markup: it describes content a page already has. Its neighbours cover the other two surfaces — [SEO](./seo.md) for ranking in the result list, and [GEO](./geo.md) for being quoted by an AI assistant.

Docsbook emits each object **only when the page genuinely contains the matching content**. A page with no FAQ gets no `FAQPage`. Structured data describing content a reader cannot find is a manual-action risk, not an optimisation.

## What shape must an FAQ have to be detected?

Docsbook turns a Markdown section into `FAQPage` JSON-LD when it matches one of two patterns:

1. An `## FAQ` heading (or *Frequently Asked Questions*, or the Russian equivalents) followed by `### Question?` H3s — each H3 becomes a question.
2. Any `### heading ending with a question mark`, anywhere in the document.

The answer is the paragraphs between the question heading and the next heading. Docsbook takes **up to 20 questions per page** and truncates each answer at **1,000 characters**.

```markdown
## FAQ

### How do I add a custom domain?

Open the admin panel, go to Custom Domain, enter `docs.yourcompany.com` and save. Docsbook then provisions the certificate.

### Is a GitBook export compatible?

Yes — Docsbook reads standard CommonMark from GitHub, the same format GitBook exports.
```

**Authoring rule:** keep each answer self-contained. Google strips the FAQ snippet out of its context, so an answer that starts "As mentioned above…" is an answer nobody can use. Open with a direct yes, no, or number.

## What shape must a procedure have to become a HowTo?

Docsbook turns a heading into `HowTo` JSON-LD when three conditions hold together:

1. An H1, H2 or H3 begins with **"How to …"** (or the Russian **"Как …"**).
2. A numbered list follows it.
3. That list has **at least 3 steps**.

Each numbered item becomes a `HowToStep`, with its first sentence as the step `name` and the full item as its `text`. Docsbook caps a procedure at **20 steps** and a page at **5 HowTo objects**. A stepper widget counts too: a numbered procedure written as a Docsbook stepper region is read the same way as a numbered list.

```markdown
## How to publish your first docs site

1. Sign in at docsbook.io with your GitHub account.
2. Paste the URL of any public repository.
3. Pick a name and publish.
```

A two-step procedure produces nothing. If the steps are genuinely two, that is the right outcome — do not pad a list to reach the threshold.

## What does speakable markup do?

With AEO on, the page's `TechArticle` schema gains a `speakable` block naming the parts a voice assistant should read aloud:

```json
{
  "speakable": {
    "@type": "SpeakableSpecification",
    "cssSelector": [".tldr", "article > p:first-of-type", "h1"]
  }
}
```

The selector list prefers the [GEO](./geo.md) TL;DR block when GEO is on, then falls back to the first paragraph, then to the H1. The practical consequence: whatever a reader sees first is also what a voice assistant says first, so a page opening with background rather than an answer reads badly out loud.

## Authoring patterns for answer surfaces

- **Phrase a heading as the question a reader would ask** — "How do I cancel a subscription?" is matched by more queries than "Subscription cancellation". This also feeds the H3-ending-in-a-question-mark detector above.
- **Open every FAQ answer with a direct yes, no, or number**, then explain.
- **Use tables and ordered lists** for anything enumerable; answer surfaces extract them close to verbatim.
- **Keep each answer readable alone** — it will be displayed without the paragraph before it.
- **Do not add FAQ markup to prose that is not a FAQ.** Exhaustive FAQ markup on non-FAQ pages is a weak-tier tactic at best, and misdescribing your page is the way to lose rich results entirely.

Docsbook does not promise a snippet. Whether a page wins one depends on the query, the competition and the engine — markup makes a page *eligible*, and that is the honest claim.

## How to enable AEO

1. Open your workspace admin panel (FloatWidget) → **SEO / GEO** tab.
2. Toggle **AEO — Answer Engine Optimization** on.
3. The change applies on the next render. View source on any page to confirm the `FAQPage` and `HowTo` JSON-LD, if matching sections exist.

## Next steps

Turn AEO on, then check one page with a FAQ and one with a "How to" procedure — the JSON-LD in the page source tells you immediately whether the detector matched what you wrote.

## Related

- [SEO](./seo.md) — meta tags, sitemap, canonical URLs and `noindex`.
- [GEO](./geo.md) — the TL;DR block the speakable selector prefers, and citation by assistants.
- [llms.txt](./llms-txt.md) — the site-level index for AI crawlers.
- [Search options](../ai-chat/search.md) — on-site search for readers who are already on the page.
