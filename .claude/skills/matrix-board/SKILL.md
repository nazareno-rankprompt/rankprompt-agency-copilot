---
name: matrix-board
description: Render the AI Visibility Matrix as a branded, interactive HTML board (and PDF) with the brand and its competitors plotted from real RankPrompt data. Use when the user wants a client-facing visual of where a brand sits on the Matrix, wants to filter by AI platform or location, or wants to show how the brand moved across the squares over time from a scheduled report. Produces the deliverable that matches the RankPrompt matrix design.
---

# matrix-board

Generate the branded AI Visibility Matrix visual — the client-facing centerpiece. Self-contained interactive HTML (filters + over-time animation) plus a print-to-PDF static snapshot. Follows `deliverable-design-rules` (brand colors, Inter, logos, PDF gotchas) and the model in `knowledge/matrix.md`.

## What it shows

- The brand (**YOU**, purple marker) and its competitors plotted on Visibility Score (vertical) × Citation Share (horizontal), in the four squares (Winning green / Recommended-not-sourced blue / Cited-not-chosen amber / Invisible red).
- **Filter by platform** (ChatGPT / Perplexity / AI Overviews / Claude / …) and **by location** — re-plots live.
- **Over-time mode** — when a scheduled report series is available, a slider/animation traces the brand's path across the squares (the movement trail), proving direction toward Winning.
- The four play-cards beneath, one per square.

## How to build it

1. **Get the data (real only).** Pull the report(s) via MCP:
   - Single snapshot: `rankprompt_get_report` / `rankprompt_get_report_summary` + `rankprompt_list_citations`.
   - Per-platform: report results carry the platform, so compute Visibility Score per platform (share of that platform's prompts where the brand appears) and Citation Share per platform.
   - Per-location: segment by region/location (or parse location from the prompt set).
   - Over time: `rankprompt_list_reports` for the scheduled series → one snapshot per run.
2. **Compute positions per segment/filter** using `matrix-diagnose` logic: Visibility Score (`brand_appears` rate) and Citation Share (own-domain ÷ all citations). Do this for YOU and for each competitor the report tracks. Competitor **visibility** is reliable; competitor **citation share** is often partial — if you don't have it for a competitor, plot them by visibility with citation marked estimated, or omit rather than fake a position.
3. **Fill the `DATA` block** in `template.html` (copy the template to `out/<brand>-matrix-board.html`): brand name, thresholds, `points` (default = All/All), optional `byPlatform` / `byLocation` overrides, optional `timeline` (snapshots for the trail), and the play-card copy. Every number must come from the MCP data.
4. **Render / export.** Open the HTML to review. For the client PDF, print with headless Chrome per `deliverable-design-rules` (`--virtual-time-budget=5000`, no gradient text, A4). Save the static PDF for sending; keep the interactive HTML for the readout call.

## Guardrails

- Only plot real data. No invented scores, competitors, or trail points. If a competitor's citation share is unknown, don't fabricate one.
- Keep Visibility Score (vertical) and Citation Share (horizontal) correctly assigned — never swap the axes.
- Match `deliverable-design-rules`: solid `#a855f7` for the title accent (NOT gradient-clip — breaks in PDF), Inter, RankPrompt + client logos, the square colors from `knowledge/matrix.md`.

## Files

- `template.html` — the self-contained board (CSS + JS + a `DATA` block with sample data so it renders standalone; replace `DATA` with real values).
