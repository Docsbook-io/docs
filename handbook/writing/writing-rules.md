---
title: "Writing rules: get the page right while you write it"
description: "The rules that decide a documentation page before anyone reviews it: one page type, quotable sections, plain style, a named reader, and no dead end."
tldr: "Pick exactly one page type before writing a word — tutorial, how-to, reference or explanation — because the type decides structure, tone and what is off-limits. Then write so every section survives being quoted alone, answer in the first 60 words, cut filler and marketing adjectives on sight, invent no fact, and close the page with somewhere to go."
---

# Writing rules

Read this before the first line of a new page, and before any rewrite. These are rules for writing, not for auditing: noticing a defect on a neighbouring page while writing means noting it and moving on. Repairing it is a separate job with its own justification, covered in [From a finding to a change](./from-finding-to-change.md).

## The five rules everything else is detail for

1. **One page, one type, one reader.** Decide the page's type before writing a word; it decides structure, tone, and what is off-limits.
2. **Every section must survive being quoted alone.** Paste it into an empty file: does it still say what it is about and answer completely? Assistants score passages, not pages, and so do readers who land mid-page from a search.
3. **Never invent a fact.** Not a price, a limit, an SLA, a statistic, a quotation, a competitor, a customer, or a route like `/signup` that nobody observed. A missing number is "contact sales" or an omission — never a plausible guess.
4. **Never end in a dead end.** Every page closes with a next step or a related link. Evaluation pages carry exactly one conversion action; reference pages carry none.
5. **Cut the filler and the marketing adjectives on sight.** "Simply", "just", "easily" read as contempt to a stuck reader. "Powerful", "robust", "seamless" carry no information. Replace with a number, or delete.

## Are you writing a new page or changing an old one?

These are two jobs, and they do not blur. Decide which one you are doing before you open the file.

| What you are doing | What it may do | What it must never do |
|---|---|---|
| **Writing a new page** | Produce a page that is already correct | Repair an old one on the way past |
| **Changing an existing page** | Rewrite preserving meaning and the URL | Invent a new page |

Mixing them is how "write one page" becomes a rewrite nobody asked for, and how an audit quietly starts editing. Deciding that a page *should exist* is a different decision again — see [The page set](../planning/page-set.md).

## 1. Decide the page type first

Pick exactly one type before writing a word. The type decides structure, tone, and what is off-limits. The four are the ones named by Diátaxis, and the split matters because the four serve genuinely different needs ([Diátaxis, a systematic framework for technical documentation](https://diataxis.fr/)).

- **Tutorial** (learning) — one guaranteed path, imperative steps, a stated start and end state. No alternatives: "you can also use the CLI" belongs in a how-to.
- **How-to** (task) — one real goal, a competent reader, may branch ("if X, do Y"). No teaching foundations mid-task; link out instead.
- **Reference** (information) — the same shape for every entry, complete, neutral. No narrative, no "which one should I pick".
- **Explanation** (understanding) — why and how it works, trade-offs, opinions allowed. No numbered procedures, no full parameter tables.

**One page, one type.** Four pages on one topic — one per type — is correct. One page covering the topic four ways is the defect audits flag most.

**The title matches the type.** A how-to starts with a verb ("Set up a custom domain"). An explanation reads "How authentication works". A reference is a noun label ("API endpoints").

## 2. Structure

- **Frontmatter carries `title` and `description`.** Title 50–60 characters, unique across the docs, phrased as intent — not `Authentication` but `How to authenticate API requests`. Description 130–160 characters, a complete active sentence naming the outcome.
- **One H1, and it comes from `title`.** Do not open the body with `# Title`.
- **Never skip a heading level.** H2 → H3 → H4. A jump to H4 breaks screen-reader and keyboard navigation.
- **Headings make sense out of context** and are sentence case: "Set up a custom domain", not "Set Up A Custom Domain" and not "Getting fancy". Sibling headings are unique and parallel in structure.
- **Tutorials open with prerequisites**, versioned and specific — "Node.js 18+", not "Node.js installed" — above step 1, never mid-page, with a "what you'll learn" line before them.
- **Every fenced code block declares a language.** Separate the command from its output into two blocks. Placeholders look fake by design: `YOUR_API_KEY`, never `key123`, and never a real token.
- **Keep it scannable.** Paragraphs 2–4 sentences. A table for any comparison of three or more columns. At most about three callouts per page, and a warning always *before* the action it warns about. Split a tutorial past roughly 2000 words.

## 3. Write so a single section can be quoted

An assistant retrieves and ranks **passages**, not pages. A section that only makes sense after the three above it loses before the reader ever sees it.

- **Name the subject in full inside each section.** "To rotate it, call…" is unretrievable — nothing in it says which product, or that it is an API key.
- **Answer in the first 60 words after the heading**, then elaborate. "Before we get into rotation, it's worth understanding…" is the answer arriving too late.
- **One question per section.** A section answering three competes weakly for all three — split it.
- **Apply the quote test.** Paste the section into an empty file. Does it still say what it is about and answer completely? If not, rewrite it now.
- **Give one extractable fact where you honestly have it** — a limit, a timeout, a price, or a one-sentence definition ("A *workspace* is a documentation site with its own domain, members and billing").
- **Never invent a number, limit, price, quotation or source** to make a passage quotable. Omit it and say it is not stated — a wrong limit repeated by an assistant is worse than silence.
- **Keep natural synonym variety** ("API key", "token", "credentials"). Writing as a human would is the point; cramming query strings scores *below* it.

This is the minimum. [Writing for retrieval](./retrieval.md) goes deeper when a page needs more than it — including the tactics that measurably backfire.

## 4. Style

- **Active voice, second person, present tense.** "The service returns an error", not "an error is returned". "You" — not "the user", and not "we" except for an explicit recommendation on an explanation page.
- **Imperative for every instruction.** "Click Save", not "You should click Save".
- **Cut the fillers on sight:** *simply, just, easily, of course, obviously, naturally, please note that*. They read as contempt to a reader who is stuck.
- **Cut the marketing adjectives:** *powerful, robust, flexible, seamless, effortless, revolutionary*. Replace with a number or delete. "A powerful indexing engine" becomes "indexes a 500-page repo in under 30 seconds".
- **Shorten the verbose:** "in order to" to "to", "utilize" to "use", "leverage" to "use", "make sure to" to "ensure".
- **One idea per sentence, under 25 words.** Three or more parallel items become a list, not an "and" chain. Lead with the main clause.
- **One name per concept**, for the page and for the whole docs set. If the interface says "workspace", never write "project". Product names are spelled exactly.
- **Match tone to type:** tutorial encouraging, how-to efficient and preamble-free, reference neutral, explanation conversational but authoritative.

## 5. Audience

- **Name the reader before writing**, explicitly or through the page type, and write to that one reader for the whole page.
- **Declare prerequisites, then honour them.** If the page says "no experience needed", every term in it must be introduced. Unstated assumed knowledge is the most expensive defect on a getting-started page.
- **Expand every abbreviation at first use** — "CLI (command line interface)" — and define product-specific terms the first time they appear.
- **Do not mix levels on one page.** "Open your terminal for the first time" and "configure the idempotency key" cannot share a reader. Split, or separate with explicit per-audience headings.
- **Do not over-explain in reference.** A reader in the API table already knows what an API is; starting with basics wastes their scan.
- **Beginner pages** explain every command, show expected output, and include error handling ("if you see X, it means Y, do Z").
- **Expert pages** get to the information fast, assume product knowledge, and document the edge cases.

Writing in the reader's vocabulary rather than the product's is a discipline of its own — [The reader's own words](../lenses/user-language.md) covers where to get that vocabulary.

## 6. Do not end in a dead end

Every page owes the reader somewhere to go. The minimum costs one section.

- **Close every page with `## Next steps` or `## Related`** and at least one internal link. A page ending on its last instruction is a page readers leave.
- **Point forward by type:** tutorial to how-to, how-to to reference, reference to the guide that demonstrates it, explanation to the tutorial that applies it.
- **Evaluation pages** (hero, features, use-cases, pricing, FAQ) carry **exactly one** conversion action. Competing calls to action convert worse than one clear one; secondary links go in "Next steps", not as buttons.
- **No call to action on reference pages.** A reader in a parameter table wants related links, not a pitch. A tutorial converts by working, not by selling.
- **Never state a price, plan, limit or SLA you did not read from the source.** An unknown price is "contact sales" or a link — never a plausible guess.
- **Link to a route that exists.** Do not invent `/signup`; use a URL observed on the product or an internal doc path. A root-relative product path copied into docs served from another domain is a 404 — rewrite it onto the source's origin, and leave internal links and anchors alone.

[Asking for the sale](./conversion.md) decides *which* action a page closes with, from how the product actually makes money.

## 7. Links and accessibility

- **Every new page gets at least one inbound link** from an existing page, added in the same change. A page nobody links to is an orphan the moment you save it.
- **Anchor text describes the destination:** "see the authentication guide", never "click here", "read more", or a bare URL. Screen readers list links out of context, and so do readers who scan. Identical anchor text must go to the same place.
- **Link targets resolve** — the file and the `#anchor` both exist when you commit. Check the anchor against the rendered page rather than guessing it from the heading text: an anchor guessed from a heading fails silently, because a link to a missing anchor still loads the page, just at the top of it.
- **Alt text on every informative image**, describing content rather than the file: "Workspace settings with the API key field highlighted", 125 characters or fewer, never starting with "image of". Decorative images take empty alt.
- **No information lives only inside an image**, and no meaning is carried by colour alone — "the red fields" needs "the required fields (shown in red)".
- **Numbered lists for sequences, bullets for sets, a header row on every table.** Tables are for tabular data, never for layout, and carry a caption or a preceding sentence saying what they show.
- **Videos carry captions and a transcript or written summary**, and never autoplay.
- **Emoji are never functional indicators.** Screen readers read their names aloud, which turns a checkmark into noise.

## What a rewrite must never do

A rewrite is the riskier half of this job, because the page already works for somebody.

- **Preserve meaning and preserve the URL.** A title change implying a slug change means flagging the redirect, not silently breaking links.
- **Never fabricate a commercial fact**, and never state a price you did not read from the source in this run.
- **Never rewrite a claim about another company.** Propose the corrected sentence; a human decides what to assert about a partner or a rival.
- **Never overwrite human-authored prose or human-set configuration.** Additive edits go in marked blocks, and a re-run replaces its own block rather than stacking a second one beside it.
- **Do not rewrite a page that already earns assistant traffic** without checking first. Body-only rewrites measurably cost retrieval — see [Writing for retrieval](./retrieval.md#how-do-i-avoid-wrecking-retrieval-while-polishing-for-citation).
- **Do not bundle changes.** One coherent change per page per pass, so its effect stays measurable.

## The 60-second self-check before committing

- [ ] I can name this page's type, and nothing on it belongs to another type.
- [ ] `title` and `description` exist, are unique, sized, and read as reader intent.
- [ ] Headings descend without skipping; exactly one H1, from frontmatter.
- [ ] Every code block has a language; prerequisites are versioned, if a tutorial.
- [ ] Each section passes the quote test standalone and answers in its first 60 words.
- [ ] No filler, no marketing adjective, no passive instruction, one term per concept.
- [ ] Every term is either defined here or covered by the stated prerequisites.
- [ ] Every commercial or third-party fact traces to a source read in this run, or is absent.
- [ ] The page ends with a next step; evaluation pages carry exactly one conversion action and reference pages carry none.
- [ ] Something links **to** this page, and every link **from** it resolves.
- [ ] Every informative image has alt text; nothing is conveyed by colour alone.

Any unchecked box is a defect being born. Fixing it here is an order of magnitude cheaper than fixing it in a queue three months from now.

<!-- widget:cards plain cols=2 -->

## Next steps

- [Writing for retrieval](./retrieval.md) — the passage-level rules, what the evidence supports, and the popular tactic that backfires. {search}
- [Asking for the sale](./conversion.md) — which closing action a page gets, derived from the product's monetisation model. {credit-card}
- [Presentation](./presentation.md) — turning a flat section into a rendered block, and the rules for images and diagrams. {image}
- [From a finding to a change](./from-finding-to-change.md) — what to do when an audit has already told you what is wrong. {wrench}

<!-- /widget -->
