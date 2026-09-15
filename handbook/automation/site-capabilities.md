---
title: "Site capabilities: what each setting gives a reader, and when to turn it on"
description: "The order to apply site configuration in, how to derive a visual identity instead of inventing one, the contrast floors that are not negotiable, and how to verify a setting on the rendered page."
tldr: "Configuration is not a checklist of switches — approach every setting by what it does for a reader who has not decided yet, and apply it in order: navigation, identity, reading affordances, discovery, assistant, reach. Never invent a brand colour; derive it from signals that already exist, check contrast, and offer a choice. A write that succeeded is not a setting a reader can see, so verify on the rendered page."
---

# Site capabilities

Configuration is what turns a published folder into a site that feels like the product's own documentation. Approach every setting by its **purpose** — what it does for a reader who has not decided yet — and apply the maximum the platform and the plan allow.

Deciding what a setting should be is this page. Keeping it that way once it is set is [automation](./setting-it-up.md).

## Read this before naming a single field

- **Read the platform's live settings and its live catalogue of what it offers.** Match by purpose, never by a field name recalled from memory. A field name written down in a handbook is wrong the week the platform renames it, and worse than wrong: it sends you looking for something that no longer exists while a better-fitting capability sits unused because nothing here mentions it.
- **A capability the platform does not have is not a finding.** Say it is unavailable and move on. Where no platform is connected at all, most of this becomes ordinary edits to the docs config or theme files in the repository, and the purposes below still decide what is worth doing.
- **Read the current state first.** Anything a human already set is a decision. Build around it; never overwrite it unprompted.

## In what order should these be applied?

In this one, because each layer makes the next one worth having:

1. **Navigation** — a site with dead ends does not benefit from anything else.
2. **Identity** — the site must read as the product's, not as a sandbox.
3. **Reading affordances** — what separates a docs site from a rendered README.
4. **Discovery** — indexing and answer markup, once there is content worth finding.
5. **Assistant** — a live answer surface over content that is now worth answering from.
6. **Reach** — languages, custom domain, access.

The first three are usually available on any plan and are the minimum that makes a site feel real. **Never stop after identity.** A branded site with no sub-header, no on-page contents and no feedback affordance still reads as a raw README with a nicer colour.

## The capability catalogue

| Capability | What it gives a reader | When it is worth it |
|---|---|---|
| **Navigation structure** | A sub-header built from the top-level folders, so the site reads as documentation rather than a file listing. Social links in the header. A link back to the product site. The one conversion action as a filled button | Always. It is usually free, and it is the single largest visual difference between a docs site and a dump |
| **Visual identity** | Accent and muted colours in light and dark, a font, a theme default, a logo, an icon, a display name — so the docs read as a continuation of the product | Always, once real brand signals exist. Never with invented values |
| **Conversion destination** | The one page the docs exist to drive readers to, rendered as a header button and used as the default action on every evaluation page | Whenever the product has one. [Conversion](../writing/conversion.md) decides what it should be |
| **Reading affordances** | Copy-page, a feedback control, breadcrumbs, on-page contents, search | Always. These are what make a site feel professional; each is small and their absence is conspicuous |
| **Indexing** | Base indexing signals, sitemap inclusion, meta reinforcement | Always, for public docs. Without it the pages do not appear in search at all |
| **Authorship signals** | A real person as author rather than the organisation | Where the content is genuinely authored and the author is known. It is an expertise signal engines weight |
| **Answer markup** | Q&A and numbered procedures promoted into machine-readable question and procedure markup, plus speakable regions | **Only where the content genuinely has Q&A and procedures.** The easiest layer of all to misapply |
| **Assistant over the docs** | A reader who cannot find something asks instead of leaving. The strongest single affordance for an unsold reader | Whenever available and the content is indexed. Derive its suggested questions from the pages that actually exist, never generic ones |
| **Languages** | Reach into markets the source language does not serve | When someone will keep the translations current. A stale translation is worse than none. Enabling several languages at once surprises people: confirm before applying |
| **Custom domain** | The docs live under the product's own brand, and the domain's search authority is shared | As soon as the site is real |
| **Access control** | Private or gated documentation | Only when asked. Gating removes the pages from search and from assistant retrieval entirely — that is the trade, and it should be stated |
| **Agent context file** | A file at the repository root telling every coding agent where the docs live, what languages exist and what conventions apply, so each session starts with the same context | Whenever the docs have a repository. It is cheap, and it stops agents from guessing |

### Where these live in Docsbook

Docsbook's own surfaces for the rows above, with their gates — read them as an example of the shape rather than as the list to memorise, since the platform owns this catalogue and it moves:

| Layer | Tool | Gate |
|---|---|---|
| Navigation, header and footer links, sidebar labels | [`update_navigation`](../../mcp/settings/update-navigation.md) | All plans |
| Colours, fonts, logo, icon, display name, the call-to-action URL | [`update_branding`](../../mcp/settings/update-branding.md) | All plans |
| Reading affordances — search, breadcrumbs, feedback, copy-page, the footer itself | [`update_ui_settings`](../../mcp/settings/update-ui-settings.md) | All plans |
| The assistant over the docs | [`update_ai_settings`](../../mcp/settings/update-ai-settings.md) | PRO |
| Languages | [`update_languages`](../../mcp/settings/update-languages.md) | PRO |
| Private or gated docs | [`update_access`](../../mcp/settings/update-access.md) | PRO |
| Custom domain | [`update_domain`](../../mcp/settings/update-domain.md) | BUSINESS |

Two rows of the catalogue have no switch in Docsbook at all, which is worth knowing before you go looking for one: **indexing** is automatic — every owner gets a sitemap advertised from `robots.txt`, and changes published through Docsbook are pushed to indexing endpoints as they happen ([how a page gets discovered](../../seo/indexing.md)) — and **answer markup** is emitted on every page of every project from the content that qualifies ([AEO](../../aeo/README.md)), alongside the [GEO](../../geo/README.md) page signals. There is nothing to enable and nothing to forget to enable.

### The answer-markup trap

Enabling answer markup on prose with no genuine Q&A and no numbered procedure produces nothing at best — and at worst produces invalid or irrelevant markup, which search engines can penalise. **The switch and the content go together.** If the pages have no FAQ, write one first ([writing rules](../writing/writing-rules.md), [deciding the page set](../planning/page-set.md)) and then enable the layer.

Two things sharpen this. First, the markup itself buys less in Google than it used to: the FAQ rich result "was removed from Google Search in May 2026", and from August 2023 it was already shown only for "well-known, authoritative government and health websites" ([Google Search Central, FAQPage structured data](https://developers.google.com/search/docs/appearance/structured-data/faqpage)). What the markup still does is make the question-and-answer structure machine-readable for everything that is not a Google rich result. Second, where a platform *does* gate this behind a switch, the inverse is the highest-value finding available: a site getting real assistant-crawler traffic with its answer layer switched off is being read while its most quotable structure is withheld.

## Deriving a visual identity without inventing one

The reflex when branding comes up is a default blue and a default font. The whole discipline here is the opposite: **derive, advise, then ask.**

### Derive: collect the signals that already exist

| Signal | Where it comes from |
|---|---|
| Anchor colour | The source site's theme-colour meta tag, then `:root` custom properties (`--accent`, `--primary`), then the dominant non-neutral hue of the logo, then an explicit hex in the README |
| Colour scheme | Background luminance; a theme-toggle element on the source site means prefer following the reader's system rather than pinning one |
| Logo and icon | **Different slots.** See below |
| Font | Only when the source CSS explicitly names a web font |
| Display name | The site brand, then the repository name |
| Social links | Usually in the footer markup, not the header |
| Existing configuration | Whatever a human already set — this outranks anything you would derive |

Record each signal with its source. Record a missing one as missing. **If there is no signal at all, the job is to ask for one** — a reference URL, a screenshot, a hex — not to make one up.

### Build the palette from one anchor colour

The goal is a complete, balanced palette from a single colour, not a rainbow.

1. **Anchor.** The strongest signal above. This becomes the light-mode accent.
2. **Sanity-check it for interface use.** It will carry links and buttons. If it is too light to read on the background, darken it until it passes. **Keep the hue; move only the lightness.**
3. **Muted companion.** The accent's hue with saturation dropped hard toward a grey-tinted neutral and lightness nudged toward the background. It should read as "the same brand, turned down", never as a second accent competing for attention.
4. **Foreground and background.** Near-black on white, or near-white for light mode, unless the brand explicitly runs a tinted surface.
5. **Dark mode is derived, not invented.** Lighten the accent so it stays vivid on a dark surface. Use a near-black background rather than pure black, which crushes shadows, and an off-white foreground rather than pure white, which halates on near-black. The muted companion follows the same logic, tuned for the dark surface.
6. **Font only if you are changing it.** Never swap an existing font without being asked.

### Contrast is not negotiable

Compute the ratio for each pair and report the number:

| Pair | Minimum |
|---|---|
| Body foreground on background, light scheme | 4.5:1 |
| Body foreground on background, dark scheme | 4.5:1 |
| Accent where it carries normal text, both schemes | 4.5:1 |
| Accent on large text and interface elements, both schemes | 3:1 |
| Muted colour carrying readable secondary text | 4.5:1 |
| Muted colour used only for borders and decoration | 3:1 |

If the brand's literal colour fails, keep the hue, shift the lightness until it passes, and tell the owner the exact shade you moved to and why. **Never offer or apply a palette whose body text fails.**

### Logo and icon are different slots

They look interchangeable and are not, and getting it wrong quietly breaks the header.

- The **logo** is the horizontal wordmark in the header, usually a mark plus the product name as text.
- The **icon** is the square favicon for the browser tab and the small header glyph.

**Never put a square favicon into the logo slot.** The square image takes the logo's place and the product name disappears from the header, so the site reads as *less* branded than if no logo had been set at all. When the source has only a square mark: leave the logo empty, set the icon, set the display name — the header then renders the name as text beside the small icon, which is the correct look.

Two checks before writing any image URL. **Verify it is publicly fetchable and actually an image**: a path behind a framework's on-the-fly optimiser, or one returning an HTML shell, renders as nothing. And **match the theme to the source**: a light product site whose docs open dark reads as someone else's site.

### Ask, then apply

Never present a single take-it-or-leave-it value. Every identity question offers three routes: **pick** one of two or three derived palettes with their real hex values and contrast ratios shown; **type your own** value, which you then build the full light-and-dark palette around; or **send a reference** — a URL or a screenshot — which you run back through the derivation.

```
I derived your brand from real signals:
  • Source site theme colour: #1E40AF (strongest signal)
  • Logo dominant colour:     #2547C0 (same blue family)
  • Currently set:            nothing

Two contrast-checked palettes built from that blue. Pick one, type your own,
or send a reference and I'll derive from it.

(a) PICK
    1) "Brand blue"  accent #1E40AF / dark #3B82F6 · muted #64748B / dark #475569
                     fg #111827 on #FFFFFF (7.0:1) · dark #E5E7EB on #0B0D10 (12.6:1)
    2) "Calm slate"  accent #2547C0 / dark #5B7CFA · muted #6B7280 / dark #4B5563
                     fg #111827 on #FAFAFA (6.8:1) · dark #ECECEC on #141414 (12.1:1)

(b) TYPE YOUR OWN — give me a hex and I'll build the full palette and check contrast.
(c) SEND A REFERENCE — a URL or a screenshot whose look you want.

Nothing is applied until you choose.
```

Apply only the fields the owner confirmed, and echo back what was written with its source signal and its contrast ratios. The same shape works for the font and theme questions.

There is one exception: during the **initial** generation of a site, applying the best available derived palette silently is correct — the owner sees the result immediately and can refine it. That exception never extends to re-branding a site whose branding a human already set.

## Segment fit is a tie-breaker, never an override

Use the segment only to choose between otherwise-valid palettes:

| Segment | Tendency |
|---|---|
| Fintech, enterprise | Restrained blue-greys, navy, low saturation. Trust over flash; the muted companion does a lot of work |
| Developer tools, infrastructure | High contrast, often dark-first. Engineers default to dark themes — make dark mode first-class |
| Consumer, creator | Warmer, a touch more saturated. Personality is allowed; contrast still has to pass |
| Healthcare, reference-heavy | Soft, high-legibility, generous neutrals. Readability beats brand expression |

Font follows the same logic: a geometric sans for product and developer surfaces, a humanist sans for consumer warmth, a serif only where the brand already signals editorial. Propose; do not impose.

## Plan gates

Catch each gated failure individually and record it — **never abort the whole run on one.** The freely available layers still apply, and they are the ones that matter most.

When a capability is gated, say once what it would add, in a sentence the owner can act on. Do not sprinkle upgrade prompts through the report.

A gate that refuses while reporting the current plan as already sufficient is a platform bug, not a grant failure. Do not retry it — skip the field, note it, and continue.

## Verify on the rendered page

A write that succeeds tells you the store accepted the value. It does not tell you a reader sees it. **A settings call returning success while the page renders defaults is the normal failure mode here, and it is invisible from the configuration side.**

If you can open a browser, open the public URL and confirm what you are about to claim: colours and logo present, navigation present, and — if you enabled an assistant — **ask it one real question and read the answer.** With no browsing available, re-read the stored configuration, compare it against what you sent, and report the site as **unverified**. Never imply a visual confirmation you did not make.

| Symptom on the live page | What it means | What to do |
|---|---|---|
| **Every** branded field is default, not one but all | The page is not resolving to the site you configured — usually an identifier-normalisation mismatch, where the public URL resolves a lowercased owner and repository while the record stored the original casing | Compare the casing in the URL against the stored record before suspecting cache. Retrying the write cannot fix this |
| One field is stale, the rest applied | Edge cache on a public page | Wait briefly, hard-reload once. Do not re-send the write with different values |
| A field is correct in the stored config and wrong on the page | A render-layer bug, not a configuration problem | Stop. Report it plainly and move on — blind retries with other values will not help, and shipping a silent mismatch is worse |
| The assistant is enabled but refuses or reports no budget | Enabling and **funding** are separate concerns. A plan grant can set the flag while leaving the usage balance at zero | Check the balance, not just the enabled flag. Verify with a real question before claiming it works |
| The assistant answers, but generically | The index is fresh or thin, so the model leans on priors | Say the assistant is live. Do not claim answer accuracy you have not checked |
| The default landing tab lists root-level files — build config, agent instructions, internal notes | The entry point is the repository root rather than the documentation | Point the entry at the documentation folder if the platform supports it, and say which tab is the clean one. This reads as careless to whoever you are showing it to |

If the site was created moments ago and is not indexed yet, wait briefly and retry once before reporting failure.

## Reporting

Say which capabilities were applied, which were gated and what enabling them would add, which were **verified on the live page**, and what warnings came up. When you tell an owner a feature is on, that claim must come from the rendered page — not from the write that enabled it.

## Related

- [Setting up automation](./setting-it-up.md) — keeping a configuration correct once it is set, and the consent rules for changing anything readers see.
- [Monitors and alerts](./monitoring.md) — watching for an indexing or answer-markup switch turning off.
- [Conversion](../writing/conversion.md) — deciding what the one conversion destination should be.
- [AEO](../../aeo/README.md) and [GEO](../../geo/README.md) — what Docsbook emits for answer engines without being asked.
- [How a page gets discovered](../../seo/indexing.md) — sitemaps, push notifications and the caches in between.
- [Translations](../../translation/README.md) — what enabling a language actually commits you to.
