---
title: "Routing the input: what you start from decides the whole run"
description: "Documentation gets created from a site, a repository, another docs platform, or nothing at all. How to tell which, and what the rest of the pipeline does once you know."
tldr: "The four ways documentation comes into existence differ only in where the truth comes from. Classify the input, name the project from a real signal, then run one pipeline: audit the product, decide the page set, write, publish."
---

# Routing the input

Documentation that did not exist before gets created in one of four ways: from a live product site, from a code repository, from another documentation platform you are migrating off, or from nothing but a product name. They differ in exactly one respect — **where the truth comes from**. Everything after that is the same work: understand the product, decide the page set, write the pages, publish and configure the site.

So the first decision is the cheapest one to get wrong and the most expensive one to discover late. A run that read a JavaScript shell and called it "the site content" produces a full documentation set that is quietly invented, and nothing downstream will catch it.

## What are you actually starting from?

| Input | Route | What that route reads |
|---|---|---|
| A product or marketing URL | **site** | The rendered pages, their real content |
| `github.com/<owner>/<repo>`, or a local code path | **code** | README, the file tree, the exported API, the examples |
| A repository or URL carrying a docs-platform marker | **migration** | The existing structure, mirrored and normalised |
| A product name or a one-liner, with no source | **idea** | Nothing — invent the pages, never the facts |

[The four routes into creation](./sources.md) has the detection table, the platform marker files, and the full method for each route.

Three rules keep the classification honest:

- **One ambiguous signal is not a detection.** Route to **migration** only on a platform-specific config file or meta tag — not on a phrase in the footer, not on a CDN domain.
- **When nothing is conclusive, default to site** rather than stopping to ask. A site read is the recoverable mistake; a blocked run is not.
- **A populated `<head>` does not mean the content is there.** Most product sites are JavaScript shells, so detection may use a plain fetch, but reading must render first.

## What is the project called?

Take the name from a real signal, in this order:

1. The site brand — `<title>` or `og:site_name`, with taglines stripped.
2. The repository name, the part after `owner/`.
3. The title declared in the documentation platform's own config.

If none of the three is readable, ask. **A placeholder name is not an acceptable fallback** — it propagates into the hero, the repository name, the site title and every page's frontmatter, and renaming afterwards means rewriting all of them.

## What happens after the route is chosen?

Four stages, in this order, and the order is load-bearing: each one produces the input the next one cannot work without.

<!-- widget:stepper -->

### 1. Understand the product and the source

Before deciding a single page, establish who the documentation is for and what the product actually claims. This is the stage most generation skips, and it is why generated documentation reads like a file dump. You are after four things: who enters and how, who the product is measured against, how it makes money, and where its call to action points.

Full method: [Know the reader before you write the page](./know-the-reader.md). Ask a discovery question only when the source cannot answer it — one question at a time, skipping anything already answered.

A run with a person steering it stops here for confirmation. A run without one states its inference in a single line — "treating this as a self-serve developer tool, correct me if I am off" — and continues.

### 2. Decide the structure

Derive the outline from what you found, then group leaf pages into **folders by meaning**. Folders are not cosmetic: they become the site's navigation sub-header, which is the difference between real documentation and a flat file list.

Aim for **10–18 substantive leaf pages** where the source supports it. A well-scoped 8-page site beats 15 stubs; three solid pages beat five thin ones. Never create a placeholder page "for later". An FAQ of 6–10 genuine questions and at least one use-case page are effectively mandatory — they kill an evaluating reader's objections and they are the shape an answer engine can lift.

Full method: [Deciding the page set](./page-set.md). Print the proposed tree before writing anything; a reader who is going to edit the structure should edit it while it is still a list.

### 3. Write the pages

Decide the full page list **before** writing the first page, so every page knows its real neighbours and can link to them accurately. Then write to the rules rather than restating them — [writing rules](../writing/writing-rules.md) for page types, frontmatter and voice, [writing for retrieval](../writing/retrieval.md) for passages an assistant can lift, and [conversion](../writing/conversion.md) for the action pattern that matches the monetisation model you classified in stage 1.

Non-negotiable on every page: frontmatter `title` (50–60 characters, matching a real search intent) and `description` (130–160 characters, active voice, stating the outcome); benefit-first headings; active voice and second person; no filler — "simply", "just", "easily", "powerful", "robust", "seamless"; and real product facts only, never `example.com`, never a capability the source did not show.

**Everything must trace to something you read.** A source too thin to support a page means skip the page and record why. It never means invent.

### 4. Preview, publish, configure

Print the tree and excerpts from up to three representative pages plus the FAQ, then ask before publishing. Publish every page in one atomic commit, configure the live site, and declare the goals and funnel the stage-1 audit already named. Full method: [Publishing what you wrote](./publishing.md).

<!-- /widget -->

## What is each stage allowed to change?

A run crosses these boundaries only deliberately, and only at the points below. Mixing them is how a creation run quietly edits somebody's existing documentation.

| Stage | May it write? |
|---|---|
| 1. Product and source audit | Reports only. May write the plan file, and additive marked blocks in a private source-of-truth. |
| 2. Structure decision | Nothing on disk except the plan. |
| 3. Generation | Writes new pages. Never repairs pages it did not create. |
| 4. Preview and publish | Publishes what stage 3 wrote. Changes no content. |

Documentation that already exists is a different job with a different method: audit it with the [auditing](../auditing/README.md) section rather than regenerating it, and do not point a creation run at your own fresh output.

## What makes a run wrong

These are the failures that produce output which looks finished and is not.

- **Inventing.** Not brand colours, not competitors, not glossary terms, not capabilities, not metrics, not a project name. A missing signal is recorded as missing and the field that depended on it is skipped.
- **Overwriting a human.** Human-set branding and human-authored prose are never replaced. Enrichment is additive: writes into a private source-of-truth go inside marked blocks, and a re-run replaces its own previous block rather than stacking duplicates.
- **Wrapping a fresh repository in a new top-level `docs/` folder.** Write to the repository root, or into an existing `docs/` folder if the repository already has one.
- **Committing secrets.** Skip `.env`, `*.key`, `*.pem`, and anything matching a token pattern — `sk-`, `ghp_`, `AKIA`.
- **Losing content in a migration.** A component that cannot be normalised keeps its inner text verbatim plus a `> **TODO:**` note. Heading hierarchy is preserved and slugs stay URL-stable.
- **Treating GitHub as a precondition.** When a platform that hosts documentation is connected, "we have no repository" is a supported starting point, not a blocker. Asking the reader to go and make a repository first, when the connected platform could have hosted it, is a failed run rather than a careful one.
- **Filling a thin JavaScript shell with invented content.** Skip the page and note why.
- **Reading forever.** Cap the read at roughly 50 pages. Past that a site is mostly blog noise, and a repository should be grouped by package rather than walked file by file.
- **Interviewing instead of deriving.** At most two questions before starting — which source, and which optional sections. Everything else comes from what you read. Runs a person is steering are the exception: there, every checkpoint waits.

## When you want control at every step

The same pipeline pauses at six checkpoints: source detection, structure, enrichment sections, branding palette, repository name, and which site features to enable. One question per turn, each waiting for an explicit answer, each applied before the next stage runs. Never skip a checkpoint, and never enable an extra nobody picked. [Publishing what you wrote](./publishing.md#interactive-checkpoints) lists what each checkpoint has to confirm.

## How you know the run was good

- The route came from real signals, and the project name came from the brand, the repository or the platform config — or was asked for.
- The product audit ran: segments, entry paths, competitors, monetisation model, call-to-action destination and brand signals each recorded with a source, or noted as absent.
- The structure is foldered and multi-section — 10–18 real pages where the source supports it, zero stubs, an FAQ and at least one use-case page present.
- Every page carries `title` and `description` frontmatter, and the writing rules that were applied were named out loud.
- The link graph is wired: the index links to every section, every leaf links to the hero and to a sibling, zero orphans, descriptive anchor text.
- A preview — tree plus excerpts including the FAQ — was printed before anything was published.
- All pages went out in one atomic commit, or the run ended cleanly as crawl-only with the local path and the follow-up command.
- The site was configured, or the connection instructions were printed without failing the run.
- The goals and funnel named in the audit were declared against the live site, or their absence was reported with a reason.
- The final report lists the local path, repository URL, live URL, page count by folder, and every section skipped with its reason.

## Related

<!-- widget:cards plain cols=2 -->

- [The four routes into creation](./sources.md) — detection, platform markers, and the method for site, code, migration and idea. {plug}
- [Know the reader before you write the page](./know-the-reader.md) — segments, entry paths, competitors, monetisation, brand signals. {search}
- [Deciding the page set](./page-set.md) — which pages exist, what each type must contain, and the link graph. {list}
- [Publishing what you wrote](./publishing.md) — preview, transports, site configuration, the final report. {rocket}
- [Writing rules](../writing/writing-rules.md) — the rulebook the generation stage writes to. {file-text}
- [Automation](../automation/setting-it-up.md) — the drift guards and monitors to wire once the documentation is live. {settings}

<!-- /widget -->
