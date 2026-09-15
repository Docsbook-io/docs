---
title: "Content detectors: what is actually wrong with the page itself"
description: "Nine detectors with severity ladders — page type, structure, style, audience, links, accessibility, media, freshness, translations — and when to run each."
tldr: "A number says a page is failing; a detector says what is wrong with it. Run only the detectors that can explain the failure mode you established, classify the page type before checking anything else, and run graph-wide checks after the graph is built. Detectors report; they never edit."
---

# Content detectors

A number tells you a page is failing. It does not tell you why, and the detectors below are how you find out. Each one reads the page rather than the reader, and each has a severity ladder so that two people auditing the same corpus produce the same priority order.

Three rules govern all of them.

- **Run only the detectors that can explain the failure mode.** Running all nine over every page produces a report nobody reads and a queue nobody can act on. [Choosing a lens](./choosing-a-lens.md) covers the routing; these detectors answer the **unhelpful** case — the page exists and does not answer — and nothing else. A page nobody can find is a title or a link problem, and a page that does not exist has nothing to detect on.
- **Independent detectors run in parallel; graph-wide ones run after the graph is built.** Orphans, broken links, duplicate titles and translation parity all need the whole corpus, and running them page by page produces false findings on every page.
- **Deduplicate across detectors.** A line flagged twice is reported once, at the higher severity, naming both detectors that found it. Two severities for one line is how a reader learns to trust neither.

None of these detectors edits a file. They report. What the replacement text says is a separate decision with its own rules — see [writing rules](../writing/writing-rules.md).

## Which kind of page is this? Page type

Classify first, then check. Never flag a page for violating the rules of a type it is not: a reference page is supposed to be a flat list of entries, and "improving" it into a tutorial breaks it for everyone who arrived to look one thing up. Confirm any naming convention the project uses — `/guides/` meaning how-to, `/concepts/` meaning explanation — before flagging navigation.

There are four kinds of page serving four different needs, and a page that mixes them serves none of them well ([Diátaxis](https://diataxis.fr/)).

**Tutorial** — learning-oriented, one guaranteed path, imperative, hands-on. Breaks on: alternatives ("alternatively, you can…"), theory mid-task, full parameter tables, undeclared assumed knowledge, an open-ended outcome.

**How-to** — task-oriented, assumes competence, handles variation ("if X, do Y"). Breaks on: teaching foundations mid-task, listing every option without guiding a choice, a rigid single path.

**Reference** — information-oriented, consulted rather than read, machine-like consistency, neutral, complete. Breaks on: narrative prose between entries, missing entries, inconsistent format, opinions about which option to prefer.

**Explanation** — understanding-oriented, discusses rather than instructs, may be opinionated about trade-offs. Breaks on: step-by-step instructions, complete parameter lists, runnable code, no conceptual depth.

One page covering the same topic in all four modes is a defect. One topic across four pages, one per type, is correct.

| Severity | Problem |
|---|---|
| Critical | No identifiable type — no consistent goal or audience |
| High | Tutorial offers alternative paths; reference reads as narrative; how-to teaches foundations; tutorial assumes undeclared knowledge |
| Medium | Tutorial title is a noun; explanation carries numbered instructions; how-to has no variation handling |
| Low | One large page serving two distinct audiences; tutorial missing prerequisites or a "what you'll learn" line |

## Structure and frontmatter

Cheap, deterministic, and worth running on every page.

- **Frontmatter** — `title` present, 50 to 60 characters, unique across the corpus, search-intent shaped (starts with a verb or a question), keyword near the start, not stuffed. `description` present, 130 to 160 characters, active voice, a complete sentence, outcome-focused. Optionally `last_reviewed`.
- **Headings** — one H1, generated from the title rather than typed as `# Title` in the body. H2 → H3 → H4 in sequence, never skipping a level. Siblings unique. Descriptive when read out of context. Never used for visual sizing. Question-style H2s where the section answers a question — which is also what makes a passage liftable ([writing for retrieval](../writing/retrieval.md)).
- **Prerequisites** — tutorials declare them before step 1, with specific versions ("Node.js 18+", never "some experience"), plus a "what you'll learn" line at the top rather than buried.
- **Code blocks** — language tagged on every fence. Output separated from input. Lines short enough not to scroll. Commands complete and copy-pasteable. Placeholders obviously fake (`YOUR_API_KEY`, never `key123`). No real secrets, ever.
- **Density** — reference pages complete; tutorials split beyond roughly 2,000 words; every H2 carrying real content; paragraphs of four to five sentences at most; comparisons in tables rather than prose.
- **Callouts** — warnings precede the action they warn about. More than three callouts on a page is noise. The type matches the content. No "Note:" typed as plain prose.

| Severity | Problem |
|---|---|
| Critical | Missing `title`; duplicate title across pages; multiple H1 in the body |
| High | Missing `description`; heading level skip; untagged code block; tutorial with no prerequisites |
| Medium | Title over 60 or under 30 characters; description over 160; title is a label with no verb; warning placed after its action |
| Low | No `last_reviewed`; a placeholder that does not look like a placeholder |

## Style and register

Ask whether the project has a style guide and audit against that; use these defaults otherwise. Sample pages of different types first, to calibrate before flagging specifics — a corpus with a deliberate house voice should not be rewritten into a generic one.

- **Voice** — active by default. Second person. Imperative for instructions. Present tense. First person plural only for opinions, and only in explanation pages.
- **Filler and marketing** — flag for review, never for automatic removal: "simply", "just", "easily" (condescending to a stuck reader); "powerful", "robust", "flexible", "seamlessly", "effortlessly" (empty); "of course", "obviously", "naturally" (excluding); "please note that", "in order to", "utilize", "leverage", "make sure to" (verbose).
- **Sentences** — under 25 words on average, one idea each, main clause first. Paragraphs of two to four sentences. Three or more parallel items become a list.
- **Headings** — sentence case, descriptive rather than clever, parallel structure among siblings.
- **Terminology** — one term per concept, matching the product's own interface label. Defined at first use. Product names exact. Precise technical synonyms used in their proper contexts are not inconsistency.

Expected register by type: a tutorial is encouraging; a how-to is efficient and preamble-free; a reference is neutral and precise; an explanation is conversational but authoritative.

| Severity | Problem |
|---|---|
| High | The same concept under different names; passive voice in an instruction; "simply"/"just"/"easily" in a tutorial or how-to |
| Medium | Sentence over 40 words; marketing adjective with no specifics; mixed "you" and "the user"; heading not in sentence case |
| Low | "Please note that"; "utilize"; an undefined abbreviation at first use |

## Audience fit

Read the page's stated prerequisites and its type *before* flagging vocabulary. Jargon is only a finding when it is undefined **and** the stated prerequisites do not cover it — an expert reference page is allowed to assume the words it was written for.

- Every page states who it is for, explicitly or by its type. Prerequisites are specific. Assumed knowledge matches what was declared.
- Technical terms are defined at first use; abbreviations expanded; product-specific terms explained on beginner pages.
- Beginner pages: every command explained, expected output shown, error handling included, no "just".
- Expert pages: no hand-holding, no re-explaining the product, dense is fine, edge cases documented.
- A page may serve two levels if the sections are clearly separated by headers. Without that separation, it is a mixed-audience page and both audiences lose.

[Know the reader](../planning/know-the-reader.md) is where the audience is decided; this detector only checks that the page kept to it.

| Severity | Problem |
|---|---|
| Critical | Beginner tutorial uses expert terms with no definition |
| High | Prerequisites claim no experience while the content assumes coding; one page serves beginner and expert with no break; abbreviation unexpanded at first use |
| Medium | Product term undefined on a beginner page; reference page over-explains basics; tutorial assumes an unlinked prior tutorial |
| Low | No "who this is for" on an ambiguous page; examples too complex for the stated level |

## Links and navigation

Never run this on a single page — it needs the whole graph. The root index is expected to have no inbound links, so exclude it from orphan detection. Ask before making outbound HTTP requests to check external links.

Orphan detection is a subtraction: `all_pages − linked_pages − {homepage}`.

- Every referenced page exists; anchor links resolve to real headings; relative paths used consistently.
- Every page has at least one inbound link.
- Anchor text describes the destination — never "click here", "read more", "here", "this link", and never a bare URL.
- Hierarchy at most three levels for most content. Tier 1 pages reachable in one click.
- Tutorials end with "Next steps". How-tos link to the reference for the commands they use. Reference pages link back to a guide that demonstrates them. Concept pages link to the tutorial that applies them.
- External links prefer official sources over blog posts that disappear.

**Anchors deserve their own check, because nothing fails when they break.** A link built by generating an anchor from a heading will drift from the anchor the renderer actually emits, and the reader simply lands at the top of the page instead of at the section. Measured across 21,827 headings in one repository, 6.3% of generated anchors did not match the id on the rendered page and 263 collapsed to nothing but hyphens; on a clean English corpus of 2,968 headings the rate was 1.7%, concentrated on the most-used page, where every step of a quick start missed because of an em dash. Punctuation and non-ASCII characters are where two slug generators part company first.

[Internal linking](../lenses/internal-linking.md) is the reading that works on topology — islands, sinks, missing edges — rather than on individual broken links.

| Severity | Problem |
|---|---|
| Critical | Broken internal link; broken anchor |
| High | Orphan page; "click here" anchor text; hierarchy deeper than four levels |
| Medium | Tier 1 page not in the top navigation; tutorial with no "Next steps"; bare URL as anchor text |
| Low | External link to an unstable source; thematically adjacent pages never cross-linked |

## Accessibility

Audited against WCAG 2.1 AA, from the Markdown source. Contrast ratios and keyboard behaviour depend on the rendered theme and are out of scope here — note them, do not flag them. Empty alt text is correct for decorative images; flag it only when the context implies the image is informative.

- **Images** — informative images have alt text; decorative ones have empty alt; alt never starts with "image of" or "screenshot of"; alt describes content rather than filename; 125 characters or fewer; complex diagrams get a text alternative in the body; no critical information exists only inside an image.
- **Headings** — one H1, sequential levels, unique siblings, descriptive out of context, never used for sizing.
- **Links** — meaningful out of context; identical anchor text always goes to the same place; links that open a new tab are labelled as such.
- **Lists** — numbered for sequences, bulleted for sets, parallel grammar throughout.
- **Tables** — header row present, never used for layout, no merged cells, a caption or a preceding sentence explaining what they show.
- **Code** — language tagged; output separated; inline code in backticks rather than distinguished by colour.
- **Media** — captions or subtitles, audio description for important visuals, no autoplay, a transcript or written summary.
- **Prose** — sentences under 25 words, paragraphs of two to four sentences, abbreviations expanded, no meaning conveyed by colour alone.
- **Markup hygiene** — Markdown in preference to raw HTML; correct ARIA where HTML is unavoidable; emoji never used as functional status indicators, because a screen reader reads their names aloud.

| Severity | Problem |
|---|---|
| Critical | Informative image with no alt text; multiple H1 |
| High | Alt text starting "image of"; "click here"; heading skip; untagged code block; video with no captions or transcript |
| Medium | Generic alt text ("Screenshot", "Diagram"); paragraphs over six sentences; colour-only meaning; table with no header row |
| Low | Raw HTML where Markdown exists; emoji as a functional indicator |

## Media

Skip this entirely if the pages reference no media. The physical checks — byte size, dimensions, file age — need local access to the files; note them as skipped when you do not have it.

**Formats:** PNG or WebP for interface screenshots, never JPG, which degrades text. WebP or JPG for photographs. GIF or MP4 under five seconds for short animation, an external embed for longer video. Mermaid in Markdown for diagrams. SVG for logos.

**Sizes:** PNG under 500 KB, GIF under 2 MB, total media per page under 5 MB, no video files committed to the repository.

**Filenames:** kebab-case, descriptive of the content rather than its position on the page, no spaces, no capture timestamps.

**Screenshots:** cropped to the relevant area, no personal data, no visible timestamps, the important area highlighted, one consistent theme across the set. A screenshot on a page untouched for 180 days or more, in an actively developed product, is very likely stale.

**Diagrams:** prefer Mermaid. It renders automatically, versions in git, and updates inside a pull request without design software. Keep the editable source next to any exported image. Converting an existing PNG diagram is a recommendation rather than a defect — ask before flagging it as an issue.

| Severity | Problem |
|---|---|
| Critical | Informative image with no alt text |
| High | PNG over 1 MB; generic filename; committed video file; JPG used for an interface screenshot; uncropped full-browser screenshot |
| Medium | GIF over 2 MB; screenshot on a page untouched for 180+ days; static diagram that could be Mermaid; video with no caption note |
| Low | Timestamp in a filename; screenshot with no highlight |

## Freshness and maintenance

Whole-tree work rather than a single-page review. Confirm the staleness threshold before applying it — the default is 90 days for Tier 1 pages and 365 for the rest — and confirm which pages are Tier 1.

- No "coming soon" older than 30 days. No past date presented as a future promise. No TODO, FIXME or XXX markers in published documentation. No "in beta" on something that shipped. Version numbers current.
- Deprecated pages carry a banner at the top, not buried halfway down, plus a **specific** migration path: "use `newMethod()`, see [guide]", never "use the new API". Deprecated content stays for at least one major release. Internal links to it note the deprecation. Old URLs redirect.
- Ownership: `last_reviewed` on technical pages, an owner recorded somewhere (CODEOWNERS, frontmatter, a registry), Tier 1 reviewed within 90 days.
- Code and documentation consistency, where local access exists: endpoints in the documentation exist in the routes, command-line examples work on the current version, code examples are at least syntactically valid.

With the repository on disk, three of these are nearly free:

```bash
# stale pages
find docs -name '*.md' -mtime +90 -printf '%T@ %p\n' | sort -n | head -20
# leftover markers
grep -rnE '\b(TODO|FIXME|XXX|HACK)\b' docs/
# deprecated with no migration path
grep -rln -i "deprecated\|no longer supported" docs/ | while read f; do
  grep -qiE "use instead|replaced by|migration|migrate|see \[" "$f" || echo "$f — no migration path"
done
```

Without local files, read the same signals from the page content and whatever `last_updated` metadata the source provides, and say which file-age checks were skipped. Anything you find here that keeps coming back is a monitor rather than an audit finding — see [drift](../automation/drift.md).

| Severity | Problem |
|---|---|
| Critical | TODO/FIXME in published documentation; "coming soon" older than 90 days; Tier 1 page untouched for 180+ days |
| High | Past date presented as a future promise; an old version referenced prominently; deprecated with no migration path |
| Medium | No `last_reviewed`; any page untouched for 365+ days; a documented endpoint that does not exist |
| Low | "Beta" on a generally available feature; no owner attribution anywhere |

Deprecated content is flagged for a banner and a migration path — **never** for immediate deletion.

## Translations

Skip this entirely when one language is in scope. Confirm which language is the source of truth before flagging parity.

- Language codes are ISO 639-1 (`en`, `ru`, `zh`), with regional variants in IETF form (`zh-CN`, `pt-BR`). A default is explicitly set.
- Parity is priority-based. Tier 1 — home, quick start, pricing, authentication, privacy and terms — is always translated and never more than 30 days behind the source. Tier 2 — top pages by traffic, onboarding, troubleshooting — when possible. Tier 3 — deep reference, edge-case guides, changelog — may stay in one language.
- A missing translation falls back to the source language with a banner, never a 404.
- Navigation, buttons and interface strings are translated; a non-source sidebar showing source-language labels is a defect. The language switcher is reachable from any page.
- **Code is never translated** — only the surrounding prose and the code comments. A translated string value, or a comment that breaks JSON, is a high-severity error. Brand and product names are never translated.
- Dates, numbers and currency follow the locale. Right-to-left languages set direction and mirror directional imagery.
- A stale translation is worse than no translation. Anything more than 90 days behind the source carries a "may be outdated" banner.
- Multilingual discovery: `hreflang` per version, self-referential, `x-default` on the fallback, canonical pointing at the page itself rather than at the source language, and every version present in the sitemap.

| Severity | Problem |
|---|---|
| Critical | Tier 1 page missing in an enabled language; source-language labels in a translated sidebar |
| High | Non-ISO language code; Tier 1 translation 90+ days behind; translated code breaking syntax; missing translation returning 404 |
| Medium | `hreflang` missing; date format not localised; interface screenshot in another language with no note |
| Low | Brand name translated; register too formal or informal for the language |

[Translations](../../translation/README.md) covers how they are produced and kept in step.

## Related

- [Reading the numbers](./metrics.md) — what put this page in front of you, and how far the number can be trusted
- [Reader behaviour](./behaviour.md) — the readings that answer unfindable rather than unhelpful
- [Choosing a lens](./choosing-a-lens.md) — when detectors are the right instrument and when they are not
- [Writing rules](../writing/writing-rules.md) — what the replacement text says once a detector has fired
- [Presentation](../writing/presentation.md) — tables, callouts, code blocks and media as the reader sees them
- [External checks](./external-checks.md) — the claims that rot without anyone touching the page
