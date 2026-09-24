---
title: "Update branding"
description: "Update visual branding: colors, fonts, logo, theme, the site's call-to-action URL, and the Site source URL the AI reads facts from."
---

# Update branding

<!-- widget:api -->

## POST /api/v1/update_branding

Update visual branding: colors, fonts, logo, theme, the site's call-to-action URL, and the Site source URL the AI reads facts from. Available on all plans including FREE. Pass the values the user stated. To copy another site's look, get its values first: fetch_url with `assets: true` returns that page's logo, favicon, theme colour, the brand colours it declares in CSS and the fonts it asks for. Use what it reports, or ask the user; never invent hex values.

**Price** — $0.00001 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/update_branding`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `cta_url` | string | no | Call To Action URL — the ONE page this documentation should drive readers to (pricing, demo booking, signup). https:// only. Treat it as the project's conversion goal: reference it where a page naturally ends in a next step, and surface it as a header button via update_navigation header_links with an accent `color` so it reads as a button rather than a plain link. Pass an empty string to clear it. |
| `average_product_price_cents` | integer | no | What ONE conversion is worth, in CENTS (29900 = $299) — the average revenue from a reader who clicks through to cta_url. The analytics card multiplies it by those readers to report Revenue and Revenue per visitor; without it both stay switched off rather than being guessed. Save it whenever the owner states an average price, order value or plan price. Pass 0 to clear it and switch revenue reporting back off. |
| `product_description` | string | no | The owner's OWN description of their product — what it is, who it is for, what it does. Briefing for the AGENT only: it is never rendered on the docs site and never shown to readers. Save it whenever the owner explains their product in their own words; it is the one fact about them no crawl can produce. Not a substitute for site_source_url — a price or limit mentioned here is still confirmed there before it reaches a page. Pass an empty string to clear it. |
| `agent_instructions` | string | no | Standing instructions the owner wants the agent to follow on this project — house style, what never to touch, who to ask. Read on every admin turn, under (never over) the safety and tool rules. Save it when the owner states a durable preference about HOW work is done here, as opposed to a one-off request. Pass an empty string to clear it. |
| `support_email` | string | no | Support email — the address the PUBLIC docs chat gives a reader whose question the documentation does not answer. The assistant says plainly that it does not know the answer, then points them here. Save it whenever the owner names a support/contact inbox. Leave it unset rather than guessing: with no address the chat still admits it does not know and still tells the reader to contact support, whereas a made-up support@<domain> sends them somewhere nobody reads. Pass an empty string to clear it. |
| `site_source_url` | string | no | Site source — the product's OWN website, the place to read real facts from (pricing, plan names, limits, contacts) instead of inventing them. http(s). Save it as soon as the owner names their website or you fetch one for this project, so later sessions can look facts up there. NOT the same as cta_url (that is a destination for readers; this is an origin for facts). Pass an empty string to clear it. |
| `logo_url` | string | no | URL for site logo |
| `icon_url` | string | no | URL for favicon |
| `icon_url_dark` | string | no | URL for an alternate icon shown only when the site is in dark theme (e.g. a dark/near-monochrome icon that would otherwise sink into a dark header). Optional — unset means icon_url renders unchanged in dark mode too. |
| `custom_name` | string | no | Display name for the docs site |
| `accent_color` | string | no | Primary accent color as hex (#3b82f6) |
| `accent_color_dark` | string | no | Accent color for dark mode |
| `muted_color` | string | no | Muted/secondary color as hex |
| `muted_color_dark` | string | no | — |
| `base_foreground` | string | no | Main text color as hex |
| `base_foreground_dark` | string | no | — |
| `base_background` | string | no | Background color as hex |
| `base_background_dark` | string | no | — |
| `font_family` | string | no | Google Font name for HEADINGS (e.g. 'Inter') |
| `content_font_family` | string | no | Google Font name for BODY/CONTENT text; falls back to font_family when unset |
| `default_theme` | string | no | One of: `light`, `dark`, `system`. |
| `theme_toggle` | boolean | no | Show theme toggle to visitors |
| `background_style` | string | no | Visual background style: clean (no effect), muted (soft neutral wash), bold (shown as 'Premium': an accent haze across the top of the page — a full hero haze on a front page with the sidebar hidden — and an accent-framed Ask docs chat; the most upscale option), or gradient (soft radiant glow tied to the accent color — the old background_glow toggle). One of: `clean`, `muted`, `bold`, `gradient`. |
| `background_glow` | boolean | no | Legacy on/off toggle — prefer background_style. true sets it to 'gradient'. |
| `search_button_color` | string | no | Custom background color (hex) for the header search bar button. Pass an empty string to clear it back to the default muted background. |
| `ask_ai_button_color` | string | no | Custom background color (hex) for the header Ask AI button. Pass an empty string to clear it back to the default muted background. |

### Returns

| Field | Type | Description |
|---|---|---|
| `ok` | boolean | Whether the tool itself succeeded. A tool that ran and refused — an exhausted balance, a plan restriction, a bad argument — answers `200` with `ok: false`: the call was made and billed, and that refusal is its answer. |
| `result` | object | The tool's own JSON answer, already parsed — not a string to parse a second time. |
| `duration_ms` | integer | Server-side wall time for the call. |

### `result` fields

| Field | Type | Description |
|---|---|---|
| `id` | number | — |
| `repoFullName` | string | 'owner/repo', or a Docsbook-hosted placeholder when the site was created from scratch. |
| `customName` | string | null | — |
| `site_url` | string | The live docs URL — report this verbatim, never build one from repoFullName. |
| `customDomain` | string | null | — |
| `plan` | string | free \| pro \| business |
| `visibility` | string | public \| private |
| `not_discoverable` | string | Present ONLY when `visibility` is private, i.e. when no crawler and no answer engine can open this site. Says what that rules out — keyword work, SERP meta, crawler-facing sitemap/llms.txt tuning, backlinks, ranking readings, being cited by ChatGPT or Perplexity — and what is worth the run instead. A private SOURCE REPOSITORY is NOT this and does not rule anything out: Docsbook serves indexed public sites from private repositories. |
| `discoverability_blocked_by` | string | Alongside `not_discoverable`: "private" (the owner's choice) or "plan_locked" (the plan lapsed and Docsbook made it private — tell the owner before doing any work). |
| `aiEnabled` | boolean | — |
| `hasApiKey` | boolean | Whether a REST bearer exists — never the key itself. |
| `hasCustomAiKey` | boolean | — |
| `hasCustomTranslationKey` | boolean | — |
| `hasPassword` | boolean | — |
| `hasSourceOfTruthGraph` | boolean | Whether the semantic index has ever been built. |
| `sso` | object | { configured: false } or { issuer, clientId, allowedDomain, configured: true }. |
| `plan_capabilities` | object | What this plan unlocks. |
| `upgrade_hint` | string | null | — |
| `cta_url` | string | null | The one page readers should end up on. |
| `cta_hint` | string | — |
| `average_product_price_cents` | number | null | — |
| `revenue_hint` | string | — |
| `site_source_url` | string | null | Where facts about the product are read from. |
| `site_source_hint` | string | — |
| `subheaderFolders` | object[] | Top-level folder placements, each carrying the `placement` it resolves to — "subheader_tab" (a tab in the category strip, its pages kept out of the root sidebar tree), "sidebar_tree" (an ordinary folder in the sidebar), "subheader_tab_and_sidebar_tree" (both) or "hidden". Read `placement` rather than re-deriving it from inSubheader / showInSidebar / hiddenInSidebar. |
| `navigation_placement_hint` | string | Present when the project has folder placements: what each one resolves to and why a tab's hiddenInSidebar is not a defect to fix. |
| `publish_mismatch_warning` | string | Present only when the live site does not show what was published. |
| `…` | … | Plus every other project setting on this row — branding colors/fonts, navigation, UI toggles, SEO/GEO/AEO flags, access rules, domain, languages — minus secrets. |

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/update_branding' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"default_theme":"light","background_style":"clean"}'
```

### Response

```json
{
  "ok": true,
  "result": {
    "id": 0,
    "repoFullName": "<repoFullName>",
    "customName": "<customName>",
    "site_url": "<site_url>",
    "customDomain": "<customDomain>",
    "plan": "<plan>",
    "visibility": "<visibility>",
    "not_discoverable": "<not_discoverable>",
    "discoverability_blocked_by": "<discoverability_blocked_by>",
    "aiEnabled": true,
    "hasApiKey": true,
    "hasCustomAiKey": true,
    "hasCustomTranslationKey": true,
    "hasPassword": true,
    "hasSourceOfTruthGraph": true,
    "sso": {},
    "plan_capabilities": {},
    "upgrade_hint": "<upgrade_hint>",
    "cta_url": "<cta_url>",
    "cta_hint": "<cta_hint>",
    "average_product_price_cents": "<average_product_price_cents>",
    "revenue_hint": "<revenue_hint>",
    "site_source_url": "<site_source_url>",
    "site_source_hint": "<site_source_hint>",
    "subheaderFolders": [],
    "navigation_placement_hint": "<navigation_placement_hint>",
    "publish_mismatch_warning": "<publish_mismatch_warning>",
    "…": "<…>"
  },
  "duration_ms": 0
}
```

### Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |

<!-- /widget -->
