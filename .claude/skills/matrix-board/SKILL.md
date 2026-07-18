---
name: matrix-board
description: Render the AI Visibility Matrix as a branded, interactive HTML board (and PDF) with the brand and its competitors plotted from real RankPrompt data. Use when the user wants a client-facing visual of where a brand sits on the Matrix, wants to filter by AI platform, location or category, drill into a single prompt, see report history over time, or rank competitors and cited sources. Produces the deliverable that matches the RankPrompt matrix design.
---

# matrix-board

Generate the branded AI Visibility Matrix visual — the client-facing centerpiece. Self-contained interactive HTML (filters + over-time animation + drill-downs) plus a print-to-PDF static snapshot. Follows `deliverable-design-rules` (brand colors, Inter, logos, PDF gotchas) and the model in `knowledge/matrix.md`.

## What it shows

- The brand (**YOU**, purple marker) and its competitors plotted on Visibility Score (vertical) × Citation Share (horizontal), in the four squares (Winning green / Recommended-not-sourced blue / Cited-not-chosen amber / Invisible red).
- **Filter by location AND by category** — re-plots live. With both set to *All*, every location×category **segment** is plotted at once (each as its own labelled purple marker) so the client sees the whole strategy on one board: a brand is routinely in different squares across its categories.
- **Show / hide competitors** — a toggle that removes competitor markers from the plot for a clean brand-only view.
- **Over-time mode** — when a single location is selected (categories = All), a slider/animation traces the brand's weekly path across the squares (the movement trail), proving direction toward Winning.
- **Trends over time** — a line chart (like RankPrompt's own dashboard) directly under the plot, with two controls: **Metric** (Citation Share ↔ Visibility Score) and **Compare** (Competitors / By platform / By category). Competitors plots the brand vs its top cited-domain rivals; By platform splits the brand's Visibility across ChatGPT/Perplexity/AI Overviews (visibility-only — per-platform citation isn't tracked); By category splits the brand across its categories. Respects the Location filter (with Location=All it shows the brand's line per market) and, in Competitors mode, the Category filter (the brand line follows the selected category; competitor lines stay market-level and say so). A dashed threshold line marks the square cutoff.
- The four play-cards beneath, each auto-tagged with the segments currently sitting in that square.
- A tabbed panel under the plot with four views, all respecting the active location/category filter:
  - **Prompts** — a drill-down: click a prompt to see, per engine (ChatGPT / Perplexity / AI Overviews), whether the brand appeared, at what rank, and the exact sources it cited (own pages highlighted).
  - **Report history** — every scheduled report, newest first, with its Visibility, Citation, computed square, and a link straight to the live RankPrompt report.
  - **Competitor leaderboard** — share of voice: who AI recommends most in each market.
  - **Citation leaderboard** — the most-cited domains per market, with the brand's own domain highlighted.

## How to build it

1. **Get the data (real only).** Pull via MCP:
   - Snapshot: `rankprompt_get_report` / `rankprompt_get_report_summary` + `rankprompt_list_citations`.
   - Per-segment: compute Visibility Score (`brand_appears` rate) and Citation Share (own-domain ÷ all citations) **per category, and per location** — this is `matrix-diagnose` logic. Classify each prompt into the report's `category` values.
   - Competitors: visibility = share of prompts they appear in; citation = their domain's share of citations. Competitor visibility is reliable; citation share can be partial — omit a competitor rather than fake a position.
   - Over time: `rankprompt_list_reports` for the scheduled series → one `{date, visibility, citation, id}` snapshot per run, per location.
   - Leaderboards: rank cited domains by frequency from `citations[]` (not `rankprompt_score`); rank competitors by `rankprompt_list_competitors` / per-report appearance.
   - Sample prompts: pick a few illustrative prompts (a win and a gap per segment) and capture each engine's appearance/rank + top cited sources.
2. **Fill the `DATA` block** in `template.html` (copy to `out/<brand>-matrix-board.html`). Every number must come from MCP data. The block is fully documented inline; see the contract below.
3. **Write the STORY notes** — one short per-view narrative, keyed `"<Location>|<Category>"`, calling the square and the one play. Unmatched keys render no note.
4. **Render / export.** Open the HTML to review. For the client PDF, print with headless Chrome per `deliverable-design-rules` (`--virtual-time-budget=5000`, no gradient text, A4). The `@media print` rules hide the controls/tabs and expand all prompt drill-downs so nothing is lost in the static export.

## The DATA contract (template.html)

Top-level keys:

- `brand`, `domain` — name + own domain (used to highlight "your page" in prompts + leaderboards).
- `thresholds` — Matrix cutoffs `{visibility:25, citation:5}` (4–5% citation is the soft edge). The board computes each square from these; don't hardcode squares.
- `axisMax` — `{visibility, citation}` top of each axis's HIGH range, for scaling the plot only (does not move the threshold, which always sits on the centre gridline).
- `locations`, `categories` — dropdown values; keep `"All"` first. Categories should match the report's `category` values.
- `reportBase` — URL prefix; the report `id` is appended for the history-tab link. **Swap for tokenized client share links before sending to a client.**
- `segments[]` — one row per `{loc, cat, prompts, visibility, citation}`. The heart of the board: every location×category segment, each plotted on its own.
- `competitorsByLocation{}` — per location, `[{id, name, visibility, citation}]` for the plot markers + competitor leaderboard.
- `timelineByLocation{}` — per location, weekly `[{date, visibility, citation, id}]` for the movement trail and the report-history tab.
- `citationLeaderboard{}` — per location `{total, rows:[{domain, count}]}`.
- `prompts[]` — drill-down samples: `{text, loc, cat, outcome:"win"|"gap", platforms:[{platform, appeared, rank, sources:[{n,u}]}]}`.
- `trendCompetitors{}` — per location, the ordered list of competitor domains to draw as lines in the trends chart (exclude search-viewer noise like `google.com/searchviewer` links — those are not competitors).
- `trends{}` — per location, the weekly series powering the trends chart: `[{date, you:{vis, cit, visByPlatform:{chatgpt, perplexity, ai_overviews}, byCategory:{<cat>:{vis, cit}}}, competitors:{<domain>:{cit, vis}}}]`. Keep the competitor domains consistent across all weeks (0 when absent) so lines are continuous. `byCategory` keys must be the report's **real** `category` values.

Two correctness rules learned the hard way:
- **Use the report's real `category` values** (from each prompt's `category` field) — do NOT invent or merge buckets. Fetch them from the report data.
- **`visibility` must equal the report's `visibility_score`** = cell-level `brand_appears` rate (brand-appearing platform×prompt cells ÷ total cells), NOT a prompt-level "appears in any platform" rate. Per-category visibility uses the same cell-level method within the category's cells. `citation` = own-domain citation URLs ÷ all citation URLs. The **report-history tab always shows these report-level numbers** (it does not split by category) so it matches RankPrompt exactly.

The board derives everything else (squares, per-square play-card tags, percentages, trail geometry, which locations to show in the leaderboards) from these — so populating DATA fully is the whole job.

## Output

- A plotted board per segment + interactive drill-downs, PDF-ready.
- Everything sourced to real data, every source a full clickable `https://…` URL.
- Feeds the client readout (interactive HTML) and the leave-behind (PDF).

## Guardrails

- Only plot real data. No invented scores, competitors, trail points, or URLs. If a competitor's citation share is unknown, omit it. If a report has no share URL, link with `reportBase`+id and flag that it should be swapped for a tokenized share link.
- Keep Visibility Score (vertical) and Citation Share (horizontal) correctly assigned — never swap the axes.
- Match `deliverable-design-rules`: solid `#a855f7` for the title accent (NOT gradient-clip — breaks in PDF), Inter, RankPrompt + client logos, the square colors from `knowledge/matrix.md`.

## Files

- `template.html` — the self-contained board (CSS + JS + a documented `DATA` block with sample data so it renders standalone; replace `DATA` + `STORY` with real values).
