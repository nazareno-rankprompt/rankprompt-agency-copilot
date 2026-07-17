---
name: matrix-diagnose
description: Plot a brand on the AI Visibility Matrix and produce a prioritized action plan. Use when the user wants to know where their (or their client's) brand stands in AI search, which of the four squares each category/location is in, why, and what to do next. Segments a RankPrompt report, computes Visibility Score and Citation Share per segment, names the square, and lays out a per-segment strategy map.
---

# matrix-diagnose

Turn a RankPrompt report into a plotted position on the AI Visibility Matrix plus a per-segment action plan. This is the copilot's core diagnosis. Read `knowledge/matrix.md` and `knowledge/brain.md` before you start; only ever reason over real MCP data.

## Inputs

- A brand (`rankprompt_list_brands` → pick, store in `profile.md`).
- A report to diagnose (`rankprompt_list_reports` → `rankprompt_get_report` for full prompts/results/citations; `rankprompt_get_report_summary` for the rollup). Citations: `rankprompt_list_citations`.

## Steps

1. **Segment first.** Split the report by `category`, and by region/location when there are several. Never diagnose the blended whole (`matrix.md` → "Segment before you plot"). If there are many segments, offer parallel analysis (one subagent per segment) for speed.

2. **Compute the two numbers per segment — keep them separate and labeled:**
   - **Visibility Score** = share of the segment's prompts where the brand appears (`brand_appears` rate).
   - **Citation Share** = brand's own-domain citations ÷ all citations for the segment.
   - Compute citation frequency yourself from `citations[]` grouped by the prompt's `category`. **Do not** use `rankprompt_score` for the diagnosis — it's listicle-biased and belongs only to outreach.

3. **Name the square** using the thresholds (Visibility HIGH ≥25% / Citation HIGH ≥5%; 4–5% is a soft edge — call it, flag borderline):
   - High × High → **Winning** · High × Low → **Recommended, not sourced** · Low × High → **Cited, not chosen** · Low × Low → **Invisible**

4. **Read the citations** — run `citation-map` (or inline its logic): rank cited sources by frequency, categorize (listicles / location pages / blog / social / directories), name the dominant type and the play it implies.

5. **Deep diagnosis** (`brain.md`): own-source autopsy + sitemap reconciliation (improve vs. create), then commit to one root-cause pattern per segment and state its mechanism in one sentence.

6. **Present.** Lead with a per-segment table (segment · Visibility Score · Citation Share · square · dominant citation type). Then, per segment, the four action buckets (omit empty ones):
   - **Content** — improve an existing page (exact URL) or create a new one (name + format), and why.
   - **External mentions** — the specific listicles (full URLs) / directories to get into.
   - **Social** — the exact subreddits/platforms, if the data shows it.
   - **Technical** — only on a real finding (blocked AI bots, noindex, missing schema, not in sitemap, stale dates).

   Recommend a starting segment (a foothold you can grow, or highest-value intent) as a recommendation among options — don't railroad. Offer to write the full map to `out/<brand>-matrix-strategy.md` and to render it with `matrix-board`.

## Output

- A plotted position (square) per segment + the per-segment action plan.
- Everything sourced to real data, every source a full clickable `https://…` URL.
- Feeds `matrix-board` (the visual) and `templates/action-plan.template.md` (the written plan).

## Guardrails

- Never swap Visibility Score and Citation Share. They are different numbers and different problems.
- Never invent a number, citation, competitor, or URL. Pull it or say you don't have it.
- One prioritized plan per segment, not a laundry list.
