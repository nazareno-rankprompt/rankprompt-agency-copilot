# The AI Visibility Matrix

This is the organizing model for the whole copilot. Every brand, in every category and location, gets plotted here. Two numbers → one of four squares → one clear play. Re-plot over time to prove movement.

`brain.md` holds the deep diagnostic mechanics (root-cause patterns, the own-source autopsy, sitemap reconciliation). **The Matrix is the frame that sits on top of it:** it tells you *which square* a segment is in and *which play* that implies; `brain.md` tells you *exactly how* to run the play. Always use both.

---

## The two axes

Both numbers come straight from RankPrompt report data. **Never swap them — they are different numbers and different problems.**

- **Visibility Score** (vertical) — how often AI *mentions/recommends* the brand when people ask questions in its space. This is the `brand_appears` rate across the segment's prompts.
  - **HIGH ≥ 25%** · **LOW < 25%**
- **Citation Share** (horizontal) — the brand's own domain's share of cited sources. **RankPrompt computes this in the frontend (the Citation Share pie / Citation Rank panel) but does *not* store it in the database — so you must reproduce the exact formula yourself, and your result must match the dashboard.** You cannot "just read the number"; there isn't one to read.
  - **The formula** (ground truth: `app/frontend/src/components/AIVisibilityPage/CitationSharePie.tsx`): over the citations of **the report(s) you're scoring**, count each citation occurrence and aggregate by domain. `total` = the summed count across **all** domains (the brand plus everyone else). **`Citation Share = brand-domain count ÷ total × 100`.** **Citation Rank** = the brand domain's position when all cited domains are sorted by count (Coast to Coast = 3.8%, rank #6).
  - **HIGH ≥ 5%** · **LOW < 4%** (the 4–5% band is a soft edge — call it, but note it's borderline)
  - **The denominator trap (this burned us — do not repeat it):** the denominator is the citations **within the report/segment you're scoring**, **never the brand's entire all-time pool of every source across every report.** Dividing 28 own-domain citations by the 4,030 all-time-everything pool gave a fake ~0.7% and a false "their site is uncited" story — the correct, report-scoped figure was 3.8%. **If your number is far below the client's dashboard, you widened the denominator — rescope it and recompute before you ship.**
  - **Not the same as share-of-voice-among-competitors.** "Citation Share" is the brand's share of *all* cited domains (the formula above). "Share of voice among competitors" (own domain vs *rival* domains only — e.g. dealer vs dealer) uses a *different, smaller* denominator, so it's a higher number (~5.9% for Coast to Coast among dealers). Both are useful; label each distinctly and never report one as the other.

> Visibility = *are you recommended.* Citation = *are your own pages the reason.* A brand can be recommended without being cited (AI trusts third parties about you) or cited without being chosen (AI quotes your page but picks a competitor). One number hides that; two reveal it.

## Segment before you plot (non-negotiable)

A report blends categories and — for multi-region setups — locations. They have different scores, different cited sources, different winning page types. **Never plot the blended whole.** Split by `category` (and by region/location when there are several), compute Visibility Score *and* Citation Share per segment, and plot each one. A brand is routinely in different squares across its categories — that's the point, and it's what drives a per-segment action plan. (See `brain.md` §3.0.)

---

## The four squares

| Square | Visibility × Citation | What it means | The play |
|---|---|---|---|
| **Winning** | High × High | AI recommends you **and** cites your pages | Hold **and grow** the lead: keep top pages fresh + schema, watch competitors, expand into nearby prompts — and **broaden which of your own page types get cited.** If the win rests on 1–2 assets of one type (e.g. two listicles) while rivals get their location/home/entity pages cited, strengthen or build those owned pages so the position isn't fragile |
| **Recommended, not sourced** | High × Low | AI recommends you but cites third parties | Publish owned content answering those prompts; make the site crawlable + structured; convert earned mentions into owned pages |
| **Cited, not chosen** | Low × High | AI quotes your pages but recommends someone else | Sharpen positioning; earn reviews + reputation; get named inside comparisons and "best of" lists |
| **Invisible** | Low × Low | Not recommended, not cited — a foundation problem | Build citable assets (guides, comparisons, FAQs); get into the listicles + directories AI reads; publish where models already look |

Colors used across deliverables (match `deliverable-design-rules.md`):
- Winning = green `#22C55E` · Recommended-not-sourced = blue `#3B82F6` · Cited-not-chosen = amber `#E8A838` · Invisible = red `#EF6461` · **YOU** marker = brand purple `#6b4eff`.

---

## Reading citations — what AI cites tells you what to build

Once you know the square, read *which type of source* is winning the segment's prompts. Rank the actual cited sources by **frequency** (how often AI cites each — compute it yourself from `citations[]`, do **not** sort by `rankprompt_score`; that score is listicle-biased and belongs only to outreach). Each dominant type points to a specific play:

| Citation type | What it signals | The play it implies |
|---|---|---|
| **Listicles / "best of" roundups** | AI leans on third-party roundups for the category | Get named in more of them + publish your own listicles/comparisons |
| **Location pages** (local intent) | Local buyers, page-per-market matters | Benchmark the top-cited local page and close gaps; build one strong page per market if none exists |
| **Blog / editorial** | A specific content format is winning | Identify the format (how-to, step-by-step, ultimate guide, comparison, FAQ) and make more of exactly that |
| **Social / community** (Reddit, LinkedIn, YouTube) | Community consensus feeds the answers | Find the dominant platform and engage where it lives — presence in the threads AI cites |
| **Directories & review sites** | Trust signals decide it | Claim + complete the cited profiles, then build reviews + organic trust. **This is the reputation lane** — maps to Cited-not-chosen |

The citation-type read is what turns a square into a concrete to-do list. `citation-map` skill automates this read; `matrix-diagnose` turns it into the plotted position + action plan.

---

## Movement over time

Re-plotting on a schedule is the proof of work. A scheduled report series gives snapshots; each snapshot is a (Visibility, Citation) point, so a segment traces a **path** across the squares over time. The goal is always the same direction: **toward Winning** (up and to the right). `matrix-board` renders this path. Movement — not a static score — is what you show the client on the monthly readout.

---

## How this maps to the sprint

Session 0 teaches this model. Session 1 plots the baseline. Session 2 reads the square + citation types and picks the one play. Sessions 3–4 run the play (internal + external GEO). Session 5 re-plots to prove movement. This copilot is the engine for all of it. (See `rankprompt-claude/context/agency-program/sprint-outline.md`.)
