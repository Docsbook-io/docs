---
title: "Update branding"
description: "Update visual branding: colors, fonts, logo, theme, the site's call-to-action URL, and the Site source URL the AI reads facts from."
---

# Update branding

<!-- widget:mcp access=write -->

## update_branding

Update visual branding: colors, fonts, logo, theme, the site's call-to-action URL, and the Site source URL the AI reads facts from. Available on all plans including FREE. Pass the values the user stated. To copy another site's look, get its values first — fetch_url returns the page's prose, not its CSS, so use colours and fonts stated on the page, or ask the user for them; never invent hex values. BEFORE CHANGING THIS, call `docsbook_expert` with what you are trying to achieve: it names the reading that should decide the value, so the setting is a conclusion rather than a guess. One call, changes nothing.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped to a workspace). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `cta_url` | string | no | Call To Action URL — the ONE page this documentation should drive readers to (pricing, demo booking, signup). https:// only. Treat it as the project's conversion goal: reference it where a page naturally ends in a next step, and surface it as a header button via update_navigation header_links with an accent `color` so it reads as a button rather than a plain link. Pass an empty string to clear it. |
| `average_product_price_cents` | integer | no | What ONE conversion is worth, in CENTS (29900 = $299) — the average revenue from a reader who clicks through to cta_url. The analytics card multiplies it by those readers to report Revenue and Revenue per visitor; without it both stay switched off rather than being guessed. Save it whenever the owner states an average price, order value or plan price. Pass 0 to clear it and switch revenue reporting back off. |
| `site_source_url` | string | no | Site source — the product's OWN website, the place to read real facts from (pricing, plan names, limits, contacts) instead of inventing them. http(s). Save it as soon as the owner names their website or you fetch one for this project, so later sessions can look facts up there. NOT the same as cta_url (that is a destination for readers; this is an origin for facts). Pass an empty string to clear it. |
| `logo_url` | string | no | URL for site logo |
| `icon_url` | string | no | URL for favicon |
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
| `background_style` | string | no | Visual background style: clean (no effect), muted (soft neutral wash), bold (stronger accent treatment), or gradient (soft radiant glow tied to the accent color — the old background_glow toggle). One of: `clean`, `muted`, `bold`, `gradient`. |
| `background_glow` | boolean | no | Legacy on/off toggle — prefer background_style. true sets it to 'gradient'. |
| `search_button_color` | string | no | Custom background color (hex) for the header search bar button. Pass an empty string to clear it back to the default muted background. |
| `ask_ai_button_color` | string | no | Custom background color (hex) for the header Ask AI button. Pass an empty string to clear it back to the default muted background. |

<!-- /widget -->

## Call it

<!-- widget:code-group -->

### MCP

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "update_branding",
    "arguments": {
      "default_theme": "light",
      "background_style": "clean"
    }
  }
}
```

### curl

```bash
curl -X POST 'https://docsbook.io/api/mcp/server' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"update_branding","arguments":{"default_theme":"light","background_style":"clean"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/tools/update_branding

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | no | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/update_branding' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{"default_theme":"light","background_style":"clean"}}'
```

<!-- /widget -->
