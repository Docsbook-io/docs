---
title: "Structured answers: every schema.org type Docsbook emits"
description: "The exact JSON-LD Docsbook puts on a documentation page, what triggers each object, the Markdown shape that produces it, and what happens when the markup comes out wrong."
tldr: "Every docs page carries one JSON-LD @graph with Organization, TechArticle and BreadcrumbList. AEO adds speakable, plus FAQPage and HowTo when the Markdown genuinely contains a question section or a numbered How-to of at least three steps."
---

# Structured answers

Docsbook writes one `<script type="application/ld+json">` element per documentation page. It holds a schema.org `@graph` — a single array of linked objects — rather than several separate script tags, so every object on the page shares one context and can reference the others by `@id`.

This page lists exactly what goes into that graph, what has to be true of your Markdown for each object to appear, and what a failure looks like.

## What is in the graph, and what turns it on

| Object | Appears | Condition |
|---|---|---|
| `Organization` | Always | The project owner, with `sameAs` pointing at the GitHub account and `logo` when the workspace has one |
| `TechArticle` | Always | The page itself: `headline`, `name`, `description`, `url`, `inLanguage`, `datePublished`, `dateModified`, `author`, `publisher`, `mainEntityOfPage` |
| `BreadcrumbList` | Always | The trail from workspace home to the page |
| `Person` as `author` | GEO on | `author:` in frontmatter, else the last commit author of that file. With GEO off, `author` is an `@id` reference to the `Organization` |
| `speakable` | AEO on | Added inside the `TechArticle`, unconditionally |
| `FAQPage` | AEO on | The page yields at least one question and answer |
| `HowTo` | AEO on | The page yields at least one procedure of three or more steps |

`SoftwareApplication` is **not** part of this graph. Docsbook emits it on its own marketing pages, not on customer documentation — if you have read a competitor comparison saying otherwise about us, that is where the type actually lives.

Dates come from the file's Git history, not from the front matter: `datePublished` and `dateModified` are read from the latest commit that touched that file. A page with no commit history yet carries neither key rather than an invented date.

## What Markdown shape produces a `FAQPage`?

A section becomes questions when either condition holds:

1. An **H2 whose text matches** `FAQ`, `Frequently asked questions`, or the Russian `Частые вопросы` / `Вопросы и ответы` / `Часто задаваемые` — case-insensitively. Every H3 under it becomes a question, whether or not it ends in a question mark.
2. **Any H3 ending in `?`**, anywhere in the document, regardless of the section it sits in.

The answer is every non-empty line between that H3 and the next heading. Inline `*`, `_` and backtick characters are stripped. Content-widget markers (`<!-- widget:accordion -->` and its closing marker) are skipped rather than swallowed into the answer, because an accordion is how an FAQ is usually authored.

Then the bounds apply, in this order: a trailing `?` is appended to every question that lacks one; each answer is cut to **1,000 characters**; a pair is dropped if the question is 3 characters or shorter or the answer is 10 characters or shorter; and the page keeps at most **20 questions**.

```markdown
## FAQ

### Does a custom domain change my page URLs

Yes. Every canonical URL, sitemap entry and breadcrumb item moves to the new host on the next render.

### How long does the certificate take

Usually under a minute after the CNAME resolves.
```

An H3 that is not a question and is not inside an FAQ section produces nothing. `### Install the CLI` under `## Setup` is correctly ignored.

## What Markdown shape produces a `HowTo`?

Three conditions must hold together:

1. An **H1, H2 or H3 beginning with `How to`** — or the Russian `Как`, where the next character must not be a letter or digit, so `Каким образом` does not match.
2. A **numbered list follows it** — `1.` or `1)` both count.
3. The list has **at least 3 steps**.

Each numbered item becomes a `HowToStep`. Its `name` is the first sentence, truncated at 80 characters on a word boundary with an ellipsis; its `text` is the whole item, capped at 1,000 characters. Links are flattened to their anchor text and inline emphasis is stripped. Content inside fenced code blocks is ignored entirely, so a numbered list in an example does not become a procedure.

A procedure is capped at **20 steps** and a page at **5 `HowTo` objects**.

A [stepper widget](../content/features/widgets.md) counts as the numbered list. Inside a `<!-- widget:stepper -->` region every heading opens the next step, whatever its level — but the region only becomes a `HowTo` if a `How to` / `Как` heading introduced it. A stepper under `# Quick start` yields nothing.

```markdown
## How to move your docs to a custom domain

1. Open the admin panel and select **Custom Domain**.
2. Enter `docs.example.com` and save.
3. Add the CNAME record the panel shows to your DNS provider.
```

Two steps produce nothing. If the procedure genuinely has two steps, that is the correct outcome — do not pad the list to reach the threshold.

## What the emitted JSON-LD actually looks like

This is the output of Docsbook's own extractors, run over the two Markdown blocks above:

```json
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": "FAQPage",
      "mainEntity": [
        {
          "@type": "Question",
          "name": "Does a custom domain change my page URLs?",
          "acceptedAnswer": {
            "@type": "Answer",
            "text": "Yes. Every canonical URL, sitemap entry and breadcrumb item moves to the new host on the next render."
          }
        },
        {
          "@type": "Question",
          "name": "How long does the certificate take?",
          "acceptedAnswer": { "@type": "Answer", "text": "Usually under a minute after the CNAME resolves." }
        }
      ]
    },
    {
      "@type": "HowTo",
      "name": "How to move your docs to a custom domain",
      "step": [
        { "@type": "HowToStep", "position": 1, "name": "Open the admin panel and select Custom Domain.", "text": "Open the admin panel and select Custom Domain." },
        { "@type": "HowToStep", "position": 2, "name": "Enter docs.example.com and save.", "text": "Enter docs.example.com and save." },
        { "@type": "HowToStep", "position": 3, "name": "Add the CNAME record the panel shows to your DNS provider.", "text": "Add the CNAME record the panel shows to your DNS provider." }
      ]
    }
  ]
}
```

Note what the extractor did to the question headings: it appended the `?` that the Markdown omitted. That is why an H3 phrased as a question reads correctly in the markup even when you wrote it as a statement.

## What the breadcrumb trail contains

The trail is workspace home → project home → one item per path segment. Each segment's `name` is humanised — the `.md` extension dropped, dashes and underscores turned into spaces, each word capitalised — while its `item` URL is built from the same canonical-URL builder the page's `<link rel="canonical">` uses, so the two can never name different hosts. In a translated locale the trail's URLs are expressed inside that locale.

```json
{
  "@type": "BreadcrumbList",
  "itemListElement": [
    { "@type": "ListItem", "position": 1, "name": "acme", "item": "https://acme.docsbook.io" },
    { "@type": "ListItem", "position": 2, "name": "Acme Handbook", "item": "https://acme.docsbook.io/handbook" },
    { "@type": "ListItem", "position": 3, "name": "Guides", "item": "https://acme.docsbook.io/handbook/guides" },
    { "@type": "ListItem", "position": 4, "name": "Custom Domains", "item": "https://acme.docsbook.io/handbook/guides/custom-domains" }
  ]
}
```

Google requires `position`, `name` and `item` on each `ListItem` and at least two items in the list ([Google, breadcrumb](https://developers.google.com/search/docs/appearance/structured-data/breadcrumb)); a page at the project root produces exactly the two home items, which is the documented minimum.

## What `speakable` says

With AEO on, the `TechArticle` gains:

```json
"speakable": {
  "@type": "SpeakableSpecification",
  "cssSelector": [".tldr", "article > p:first-of-type", "h1"]
}
```

schema.org defines `SpeakableSpecification` as indicating "sections of a document that are highlighted as particularly speakable" ([schema.org](https://schema.org/SpeakableSpecification)). The selector list is a preference order: the [GEO TL;DR block](../geo/README.md) if GEO is on, then the article's first paragraph, then the H1. The practical consequence is that whatever a reader sees first is also what a machine treats as the summary — a page opening with background rather than an answer declares the background as its summary.

## What happens when the markup is wrong

Nothing in Docsbook validates the graph before it ships. There is no schema linter in the render path, and `audit_geo` — the tool that checks crawler access, server-rendering and `llms.txt` — does not inspect JSON-LD at all. Whatever the extractors produced is what goes on the page. Four failure modes are worth knowing:

- **The detector matched nothing.** The commonest outcome and the least visible one: AEO is on, the page has an FAQ-looking section, and no `FAQPage` appears. Almost always the heading level — the detector reads H2 sections and H3 questions, so an FAQ written with H3 sections and H4 questions yields nothing.
- **The detector matched too much.** Any H3 ending in `?` becomes an FAQ question anywhere in the document, including a rhetorical heading in prose. The result is valid markup describing a page that is not an FAQ, which is a policy problem rather than a syntax one — Google's guidelines require that "Your structured data must be a true representation of the page content" ([Google](https://developers.google.com/search/docs/appearance/structured-data/sd-policies)). Rephrase the heading as a statement and it stops matching.
- **Raw HTML in an answer breaks the block.** Answer text is copied into the JSON verbatim. A literal `</script>` sequence inside an FAQ answer ends the JSON-LD element early, and every object after that point is lost. Keep raw HTML out of FAQ answers; use the Markdown the rest of the page uses.
- **The page is served on a custom domain.** A workspace on its own domain renders through a different path that emits a bare `TechArticle` and nothing else — no breadcrumb, no `FAQPage`, no `HowTo`, no `speakable`, whatever the AEO toggle says. Verify on the `*.docsbook.io` address before concluding the detector failed.

Verify with Google's [Rich Results Test](https://search.google.com/test/rich-results) or the [Schema Markup Validator](https://validator.schema.org/). Note what a green result does and does not mean today: `BreadcrumbList` is still a supported rich result, while `FAQPage` and `HowTo` are valid schema.org that Google no longer renders — see the limits on [AEO](./README.md).

## Limits and open questions

- **`TechArticle` is not one of the three types Google names for the article rich result.** Google's documentation says "Article objects must be based on one of the following schema.org types: `Article`, `NewsArticle`, `BlogPosting`" ([Google, article](https://developers.google.com/search/docs/appearance/structured-data/article)). `TechArticle` is a schema.org subtype of `Article` — "A technical article - Example: How-to (task) topics, step-by-step, procedural troubleshooting, specifications" ([schema.org](https://schema.org/TechArticle)) — and it is the honest description of a documentation page. Whether Google treats a subtype as eligible for the article rich result is not stated in that documentation either way. We chose accuracy over guessing.
- **The FAQ and How-to detectors recognise English and Russian only.** The section headings and the procedure verb are matched against those two languages. A German or Japanese FAQ page produces no `FAQPage` unless its H3 headings end in `?`.
- **Answers are prose only.** Everything between a question heading and the next heading is joined and cut at 1,000 characters — tables, code blocks and images end up as their raw source inside the answer text, or are truncated mid-way. Keep FAQ answers to a few sentences.
- **No count of what was emitted is reported anywhere.** There is no panel, log or API that tells you how many `FAQPage` questions or `HowTo` objects a given page produced. View source, or use a validator.

## Related

- [AEO](./README.md) — what an answer engine needs and what the markup can still buy
- [Content rules for answer engines](./content-rules.md) — the prose rules that decide whether the passage gets picked
- [GEO](../geo/README.md) — the TL;DR block the `speakable` selector prefers
- [SEO](../seo/README.md) — meta tags, sitemap and canonical URLs
- [Content widgets](../content/features/widgets.md) — the stepper and accordion regions the detectors understand
