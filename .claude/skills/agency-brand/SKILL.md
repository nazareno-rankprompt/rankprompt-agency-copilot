---
name: agency-brand
description: White-label the workstation with the agency's own name, brand color, and logo — just share the agency website. Use when the user says "set my branding", "add my agency logo", "white-label", "brand the reports", or shares their agency URL. Writes branding.json so every report (matrix board, citation audit, task board) carries the agency's brand, with a small "Powered by RankPrompt".
---

# agency-brand

Put the **agency's** brand on every client-facing deliverable. One setup from a website URL brands everything.

## The rule: brand first, logo second

**Branding works immediately with just the agency name + accent color — the logo is an enhancement, never a blocker.** The templates render the agency *name* (styled) and re-theme to the agency *color* with no logo at all. So always get name + color working first and confirm the reports are branded; then add the logo when you can. Never leave the user stuck at "I couldn't download your logo."

## Steps

1. **Name + website.** Clean the URL to a domain. Name from `--name`, else derive from the domain (`acme-digital.com` → "Acme Digital").

2. **Read the site's HTML (text — this works even in locked-down sandboxes).** Fetch the homepage source and pull:
   - **Logo URL(s):** `<img>` with "logo" in class/alt/src, `data-site-logo`, `og:image`, and `apple-touch-icon`. Prefer an SVG or transparent-PNG **wordmark**. Note the best URL — you'll need it whether you download it or the user does.
   - **Brand color:** a `theme-color` meta, or the most prominent brand hex in the CSS/markup. Use it as the accent; if unsure, tell the user your best estimate and invite the exact hex.

3. **Write `branding.json` NOW** (with what you have — name + accent + the intended logo path). The reports are branded from this moment:
   ```json
   {
     "agency_name": "Acme Digital",
     "website": "acmedigital.com",
     "logo": "logos/agency-logo.png",
     "accent": "#2d8e5c",
     "show_powered_by": true
   }
   ```
   Confirm to the user: "Your reports now carry {name} in {color}. Adding the logo next makes it complete."

4. **Get the logo — try to fetch, but fall back gracefully (this is expected, not an error).**
   - **If the environment can download images** (shell `curl`, WebFetch, a connected browser, or `https://logo.clearbit.com/{domain}`): download the best logo → save to **`logos/agency-logo.png`** (or `.svg`). Verify it's a real image.
   - **If image download is blocked** (Claude Desktop's cloud sandbox blocks non-allowlisted hosts; no browser connector; proxy) — **don't stall.** The branding already works from step 3. Give the user the three universal ways to add the logo, and say the reports are branded meanwhile:
     1. **Attach the logo in this chat** (drag in a transparent PNG or SVG wordmark) — you'll save it to `logos/agency-logo.png`. *(Works in Desktop and Code — the simplest path.)*
     2. **Drop the file yourself** at `logos/agency-logo.png` in the repo.
     3. **Paste the direct image URL** (e.g. the logo URL you found in step 2) — you'll retry the fetch; it often works even when the homepage scrape didn't.

5. **When the logo arrives**, save it to `logos/agency-logo.png`, confirm it renders on a quick sample, and (optionally) refine the accent from the logo's dominant color. Done.

## How deliverables use it

When any deliverable skill renders a template (`matrix-board`, `citation-audit`, `task-board`), it reads `branding.json` and fills the template's `BRANDING` block:
- **`agencyName`** ← `agency_name` (shown as styled text when there's no logo — so branding never depends on the logo)
- **`logo`** ← the logo **base64-encoded as a `data:` URI** (embed it so the HTML/PDF is self-contained; on dark covers the template inverts it to white). If no logo file exists, leave `logo` null and the agency name is shown instead.
- **`accent`** ← `accent` — re-themes the report's primary color (overrides the `--purple` CSS variable) so it visually matches the agency's site.
- **`poweredBy`** ← `show_powered_by`

If `branding.json` doesn't exist at all, the templates fall back to RankPrompt branding automatically — nothing breaks before an agency sets it. (House rule in `CLAUDE.md`.)

## Guardrails

- Never block on the logo. Ship name + color first; add the logo when available.
- Only fetch/accept the agency's own logo. If none can be obtained, that's fine — the name-and-color branding still looks clean and complete.
- `branding.json` and `logos/agency-logo.*` are the agency's own — gitignored, never shipped in the template.
- Keep "Powered by RankPrompt" unless the agency explicitly turns it off.
