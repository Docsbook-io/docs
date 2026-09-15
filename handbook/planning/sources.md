---
title: "The four routes into creation: site, code, migration, idea"
description: "How to detect whether documentation is being built from a live site, a code repository, another docs platform or nothing — and the method each of those four routes runs."
tldr: "Four routes into creating documentation, differing only in where the truth comes from: a rendered product site, a code repository, a migration from another platform, or an idea with no source. One ambiguous signal is never a detection."
---

# The four routes into creation

This page is about where the **content** comes from when documentation is created — not about which sources you are allowed to cite in it. For evidence and citation, see [sources of evidence](../evidence/sources.md).

Detection is read-only and never mutates the source. All four routes end in the same place: a set of files on disk, plus a record of what could not be read and why.

## Which route is this?

| Input shape | What to check | Route |
|---|---|---|
| A plain URL | HTML meta tags, CDN links, the domain | **site**, unless a platform marker appears |
| `github.com/<owner>/<repo>` | Root contents, for marker files | **code** if only a README and source directories; **migration** on a marker |
| A local path | The same marker files, on disk | As above |
| A product name only | — | **idea** |

Platform markers, and only these, are conclusive:

| Marker file | Platform |
|---|---|
| `mint.json` / `docs.json` | Mintlify |
| `SUMMARY.md` at the root | GitBook |
| `docusaurus.config.js` / `.ts` | Docusaurus |
| `theme.config.tsx` alongside Next.js | Nextra |
| `.vitepress/config.*` | VitePress |
| `astro.config.*` with `@astrojs/starlight` | Starlight |

A single ambiguous signal is not a detection. Inconclusive input defaults to **site**.

## Route: site

### Why the naive crawl fails

Most modern product sites are JavaScript single-page applications. A plain HTTP fetch of `/`, `/docs`, `/features` or `/blog/<slug>` returns an empty shell or a 404 — the real content is behind the render. A process that fetches flat HTML, finds a thin `<main>` and carries on will silently fall back to **inventing** generic content. That is the single failure mode that produces a bland, plausible, worthless site.

**Render first.** Load each page in a real browser and read the rendered `<main>` or `<article>`; the [`read_rendered_page`](../../mcp/research/read-rendered-page.md) tool does this for one URL at a time. Fall back to a plain fetch only for pages that are already server-rendered. Never write a page from a shell you could not read — skip it and note why.

Detection is the exception: platform signals live in the HTML shell, so a plain fetch is enough to *route*. It is never enough to *read*.

### Steps

1. **Map the site.** Try `/sitemap.xml` first. If it is missing, discover links from the rendered homepage and from the header and footer navigation.
2. **Find their existing documentation — it is the best source you will get.** Check `/docs`, `/documentation`, `/help`, `/guides`, `/api`, `/faq`, product-relevant `/blog` paths, and the `docs.*` and `help.*` subdomains. If a documentation site already exists, walk *its* structure: that sidebar is a ready-made folder skeleton, and mirroring it turns "invent documentation" into "reproduce their documentation, better".
3. **Read the real content.** Prioritise documentation-relevant paths over marketing copy. Cap at roughly 50 pages. Hard-exclude `/login`, `/signup`, `/auth`, `/checkout` and `/cart`. Take the rendered `<main>` or `<article>` text, stripping `<header>`, `<footer>`, `<nav>` and `<aside>`. Keep explanatory images as absolute-URL `![alt](url)`; skip decorative ones.
4. **Collect the brand signals** — the table in [know the reader](./know-the-reader.md#brand-signals) says which ones and where each lives.

Every claim, feature and example in the output must come from something you actually read.

## Route: code

1. **Resolve the repository.** Shallow-clone a remote URL into a temporary directory; work in place for a local path. The project name is the `<repo>` part after `owner/`.
2. **Detect the project type** from root files: `package.json` (Node/TypeScript), `pyproject.toml` or `setup.py` (Python), `go.mod` (Go), `Cargo.toml` (Rust), `*.csproj` (.NET). When signals conflict, prefer the one whose `lib`, `src` or `pkg` directory actually exists.
3. **Turn the README into a benefit-first hero.** Lead with what the project does, who it is for and the outcome — not with "Installation". Split long top-level sections (`## Installation`, `## Usage`, `## API`) into dedicated pages under `getting-started/`, `guides/` and `api/`.
4. **Enumerate the public API surface.** Node and TypeScript: `package.json#exports` plus the entry files. Python: `__all__` of the top-level package. Go: the exported identifiers per top-level package. One Markdown file per module or package, under `api/`.
5. **Pull in the examples.** `examples/`, `samples/` and `demo/` become `guides/<example>.md`, using each subfolder's README or a generated one.
6. **Read the configuration.** `.env.example`, `config/*.example.*` and `docker-compose.yml` become `guides/configuration.md`, with descriptions taken from the comments next to each setting.
7. **Add a concepts page** when the project has a non-trivial mental model, and an FAQ of 6–10 questions synthesised from the README and the issue tracker: how it compares, what its limits are, what it requires.

Do not invent API documentation. A function with no docstring gets its signature plus `TODO: describe what this does`. Group by package, never one page per file. Never commit secrets.

## Route: migration

The folder structure already exists — reproduce it faithfully. Its navigation becomes the sub-header. The one piece of enrichment worth adding is an FAQ or a use-case page when the source has neither.

1. **Identify the platform** from the marker table above.
2. **Read the navigation** — `mint.json#navigation`, `SUMMARY.md`, `docusaurus.config.js#sidebars`, `.vitepress/config.ts#themeConfig.sidebar` — and build a flat ordered list of `{label, sourcePath}`.
3. **Copy and normalise.** Keep `title`, `description` and `slug`; drop frontmatter keys that do not translate. Convert:
   - Mintlify `<Card>`, `<CardGroup>`, `<Accordion>`, `<Note>` into headings and lists; callouts become `> **Note:** …`
   - Docusaurus `<Tabs>` and `<TabItem>` into `### Tab name` headings with the content underneath
   - GitBook `{% hint %}` into `> **Hint:** …`, and `{% tabs %}` into headings
   - Nextra `<Callout>` into `> **Note:** …`
   - Strip every `import` line at the top of `.mdx` files
4. **Rewrite internal links** to relative paths between the output files. Leave external `https://` links alone.
5. **Carry over the assets.** `static/`, `public/` and `images/` referenced by imported pages go to `_assets/`, with the image sources updated to match.
6. **Record the platform's accent colour** if its config declares one; omit the field otherwise.

**Never lose content.** A component that cannot be normalised keeps its inner text verbatim, plus `> **TODO:** original used <ComponentName>, may need styling tweak.` Preserve the heading hierarchy — do not flatten H3s into H2s to look tidier. Keep slugs URL-stable: `/docs/getting-started/installation` becomes `getting-started/installation.md`, not `installation.md`, because every inbound link and every search result points at the old address. Pure-React `.mdx` files with no prose are recorded as warnings and skipped, not treated as errors. Imported prose stays as it was written; the active-voice rules apply only to sentences you add.

## Route: idea

No source exists, so the constraint inverts: invent the **pages**, never the **facts**.

1. **One question maximum.** If the request already carries a product name or concept, use it. Otherwise ask exactly one: "What is your product? (name plus one line)". Infer the category, audience and tone, state what you inferred, and proceed. Do not ask about colour, page count, structure or tone.
2. **Compose the page set inline** — no separate plan file. A hero, a getting-started page, three to five benefit-first feature pages, one to three use-cases, an FAQ of 6–10 objection-killing questions, and optionally one educational or comparison piece where the category rewards it.
3. **Write conversion-grade from the first draft.** Marketing-grade language, not placeholder copy. Every page ends with a next step.

Never invent competitor names or real-world facts. If a comparison or migration section is wanted and no names were given, ask once or omit the section. Never fall back to a default accent colour — omit the field when no colour is deterministic for the domain.

This route does not hand off to a planning interview. It generates.

## Related

- [Routing the input](./route-the-input.md) — the decision that picks between these four, and the pipeline they all feed.
- [Deciding the page set](./page-set.md) — the starting page set each route implies.
- [Know the reader before you write the page](./know-the-reader.md) — what to establish about the product once the source is readable.
- [Publishing what you wrote](./publishing.md) — where the files go afterwards.
- [Sources of evidence](../evidence/sources.md) — the other meaning of "sources": what you are allowed to cite.
