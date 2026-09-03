---
title: "JSON-LD for documentation: schema types that matter"
description: "Which JSON-LD schema types are worth adding to documentation pages, which no longer earn rich results, and copy-paste examples you can validate today."
---

# JSON-LD for documentation: schema types that matter

JSON-LD is structured data embedded in your HTML that tells search engines and AI agents what type of content is on the page. For documentation, the right schema types make the page's type, steps, breadcrumbs and product identity machine-readable instead of leaving them implied by layout.

This post lists the schema types worth adding, names the one whose rich result Google has since restricted, and gives working examples. It does not promise a ranking or a citation: no reviewed technique has a stable, cross-platform causal effect on either.

## TL;DR

| Schema | Used on | Why it matters |
|---|---|---|
| `TechArticle` | How-to and tutorial pages | Tells Google "this is technical content" |
| `FAQPage` | Any page with Q&A | Machine-readable Q&A pairs — but no rich result for most sites, see below |
| `HowTo` | Step-by-step guides | Step-by-step rich results in Google |
| `SoftwareApplication` | Product overview page | Pricing, ratings, OS surfaced |
| `Article` | Blog posts and announcements | Standard article rich results |
| `BreadcrumbList` | Every doc page | Breadcrumb in search results |
| `WebSite` | Site root | SiteSearchAction enables Google search box |

If you only do one, do `TechArticle` and `BreadcrumbList`. Docsbook adds these automatically.

## Why JSON-LD over Microdata or RDFa

JSON-LD wins because:

1. It is a separate `<script>` block, decoupled from your HTML markup
2. Google explicitly prefers it ("recommended" in their docs)
3. Easier to maintain — change schema without touching layout
4. AI agents parse it more reliably than inline markup

Microdata and RDFa still work but are legacy in 2026.

## TechArticle: the default for docs

For most documentation pages, `TechArticle` is the right schema:

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "TechArticle",
  "headline": "How to authenticate with OAuth",
  "description": "Step-by-step guide to authenticating users with OAuth 2.0",
  "author": {
    "@type": "Organization",
    "name": "Acme",
    "url": "https://acme.com"
  },
  "datePublished": "2026-01-15",
  "dateModified": "2026-03-20",
  "publisher": {
    "@type": "Organization",
    "name": "Acme",
    "logo": {
      "@type": "ImageObject",
      "url": "https://acme.com/logo.png"
    }
  },
  "mainEntityOfPage": "https://docs.acme.com/auth/oauth"
}
</script>
```

What this gives you:

- Google flags the page as authoritative technical content
- AI agents tend to weight `TechArticle`-tagged pages higher in citations
- `dateModified` tells crawlers the page is fresh

## FAQPage: rich snippets gold

If your page has Q&A structure, `FAQPage` schema makes Google show those Q&As directly in search results.

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [{
    "@type": "Question",
    "name": "How do I revoke an API key?",
    "acceptedAnswer": {
      "@type": "Answer",
      "text": "Open the dashboard, navigate to API Keys, find the key, click Revoke. Revocation is immediate."
    }
  }, {
    "@type": "Question",
    "name": "Can I have multiple API keys?",
    "acceptedAnswer": {
      "@type": "Answer",
      "text": "Yes. Replace this answer with the real limit from your own product."
    }
  }]
}
</script>
```

### Does FAQPage markup still produce a rich result in Google?

For almost all documentation sites, no. Google restricted the FAQ rich result in 2023, and its own documentation now states that the feature "is only shown for well-known, authoritative government and health websites" ([Google Search Central, FAQPage structured data](https://developers.google.com/search/docs/appearance/structured-data/faqpage), read 2026-09-03). Any guide promising a click-through lift from FAQ snippets on a product docs site is describing the pre-2023 world.

That is not a reason to delete the markup. `FAQPage` still does one thing well: it states, in a form a parser cannot misread, that this block is a question and that block is its answer. Keep it where the page genuinely is a list of questions and answers, and expect no visual change in Google.

## HowTo: step-by-step guides

If you have a numbered step-by-step guide, use `HowTo`:

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "HowTo",
  "name": "Set up a custom domain for documentation",
  "step": [{
    "@type": "HowToStep",
    "text": "Open the dashboard and go to Settings → Domain"
  }, {
    "@type": "HowToStep",
    "text": "Enter your subdomain (docs.yourcompany.com)"
  }, {
    "@type": "HowToStep",
    "text": "Add a CNAME record in DNS pointing to cname.vercel-dns.com"
  }, {
    "@type": "HowToStep",
    "text": "Wait for SSL to provision (under 5 minutes)"
  }]
}
</script>
```

Result: Google may show step-by-step rich results with each step expanded.

## SoftwareApplication: product page

Your product overview page should be tagged as `SoftwareApplication`:

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "SoftwareApplication",
  "name": "Acme",
  "applicationCategory": "DeveloperApplication",
  "operatingSystem": "Web",
  "offers": {
    "@type": "Offer",
    "price": "150",
    "priceCurrency": "USD"
  },
  "aggregateRating": {
    "@type": "AggregateRating",
    "ratingValue": "4.8",
    "ratingCount": "247"
  }
}
</script>
```

This surfaces pricing and ratings in Google rich results. Be honest about ratings — Google penalizes inflated `aggregateRating`.

## BreadcrumbList: every page

Every page should have breadcrumbs in JSON-LD. Google shows them in search results, AI agents use them to understand hierarchy:

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "BreadcrumbList",
  "itemListElement": [{
    "@type": "ListItem",
    "position": 1,
    "name": "Docs",
    "item": "https://docs.acme.com"
  }, {
    "@type": "ListItem",
    "position": 2,
    "name": "Authentication",
    "item": "https://docs.acme.com/auth"
  }, {
    "@type": "ListItem",
    "position": 3,
    "name": "OAuth",
    "item": "https://docs.acme.com/auth/oauth"
  }]
}
</script>
```

## WebSite: site search box

On your home page, declare site search:

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "WebSite",
  "url": "https://docs.acme.com",
  "potentialAction": {
    "@type": "SearchAction",
    "target": "https://docs.acme.com/search?q={search_term_string}",
    "query-input": "required name=search_term_string"
  }
}
</script>
```

This unlocks the search box directly under your result in Google.

## Multiple schemas on one page

You can stack schemas. A doc page might have:

- `TechArticle` for the content type
- `BreadcrumbList` for navigation
- `FAQPage` if there is a Q&A section

All three in three separate `<script type="application/ld+json">` blocks. Google reads all of them.

## What AI agents do with JSON-LD

Three observed behaviors:

1. **Type filtering** — agents looking for tutorials prefer `TechArticle` and `HowTo` over `Article`
2. **Extraction shortcuts** — `FAQPage` schema gets extracted nearly verbatim
3. **Trust signals** — schemas with proper `Organization` and `publisher` get weighted higher

## How Docsbook ships JSON-LD

Docsbook automatically adds:

- `TechArticle` to every docs page
- `BreadcrumbList` to every page
- `FAQPage` to pages where it detects Q&A patterns
- `SoftwareApplication` to your home page if metadata is provided
- `WebSite` with SearchAction to the site root

No configuration. The schema is built from your existing markdown and frontmatter.

## Validation

Two tools:

- **Google Rich Results Test** — `https://search.google.com/test/rich-results`
- **Schema.org validator** — `https://validator.schema.org/`

Run both on your docs pages. Fix any warnings. Errors are blocking; warnings are not.

## Related reading

- [Documentation SEO guide](./documentation-seo-guide.md)
- [How to get docs cited by ChatGPT](./how-to-get-docs-cited-by-chatgpt.md)
- [llms.txt: the complete guide](./llms-txt-guide.md)

---

Docsbook adds JSON-LD automatically on every page. [Publish your docs →](https://docsbook.io/start)
