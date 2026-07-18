---
name: agency-brand
description: White-label the workstation with the agency's own logo and name by fetching their logo from their website URL. Use when the user says "set my branding", "add my agency logo", "white-label", "use our logo on the reports", or shares their agency website to brand the deliverables. Fetches the logo, saves it, and writes branding.json so every report (matrix board, citation audit, task board) carries the agency's brand with a small "Powered by RankPrompt".
---

# agency-brand

Put the **agency's** logo on every client-facing deliverable, so the reports an agency sends its own clients are branded as theirs. One setup from a website URL brands everything.

## Usage

```
/agency-brand youragency.com
/agency-brand youragency.com --name "Acme Digital"
```

## Steps

1. **Agency name + domain.** Clean the URL to a domain. Name from `--name`, else derive from the domain (`acme-digital.com` → "Acme Digital").

2. **Fetch the logo** (same waterfall as the service-side `client-logo`, stop at the first good result — prefer a transparent **PNG/SVG wordmark**):
   - Fetch the homepage and pull `<img>`/SVG with "logo" in class/alt/src; try common paths (`/logo.svg`, `/logo.png`, `/assets/logo.*`, `/wp-content/uploads/*logo*`), and `apple-touch-icon.png`.
   - **Clearbit:** `https://logo.clearbit.com/{domain}` (square PNG, works for most).
   - **Favicon fallback:** `https://www.google.com/s2/favicons?domain={domain}&sz=256`.
   - Verify it's a real image (`file` → PNG/SVG). Prefer transparent (RGBA) and ≥200px. Save to **`logos/agency-logo.png`** (or `.svg`).

3. **(Optional) accent color.** If easy to read a primary brand color from the site (a prominent header/CTA color), capture it; else default `#6b4eff`. Don't overwork this.

4. **Write `branding.json`** at repo root:
   ```json
   {
     "agency_name": "Acme Digital",
     "website": "acmedigital.com",
     "logo": "logos/agency-logo.png",
     "accent": "#6b4eff",
     "show_powered_by": true
   }
   ```

5. **Confirm.** Tell the user their brand is set and every deliverable now carries it, with RankPrompt shown small as "Powered by". To go fully unbranded of RankPrompt, set `show_powered_by` to false.

## How deliverables use it

When any deliverable skill renders a template (`matrix-board`, `citation-audit`, `task-board`), it reads `branding.json` and fills the template's `BRANDING` block:
- **`agencyName`** ← `agency_name`
- **`logo`** ← the logo **base64-encoded as a `data:` URI** (embed it, so the HTML/PDF is self-contained and portable — never a bare relative path that breaks when the file moves). On dark covers (citation-audit) the template inverts it to white automatically.
- **`accent`** ← `accent` — re-themes the report's primary color: it overrides the `--purple` CSS variable, so labels, markers, chips, and lines pick up the agency's brand color and the report visually matches their site.
- **`poweredBy`** ← `show_powered_by`

If `branding.json` doesn't exist, the templates fall back to RankPrompt branding automatically — so nothing breaks before an agency sets it. (This is documented as a house rule in `CLAUDE.md`.)

## Guardrails

- Only fetch the agency's own logo from the URL they gave. If no good logo is found, save nothing and tell them to drop a transparent PNG at `logos/agency-logo.png` manually.
- `branding.json` and `logos/agency-logo.png` are the agency's own — gitignored, never shipped in the template.
- Keep "Powered by RankPrompt" unless the agency explicitly turns it off.
