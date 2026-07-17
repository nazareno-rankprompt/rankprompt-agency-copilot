---
name: citation-map
description: Categorize a brand's AI citations and name the highest-leverage play. Use when you want to understand what kind of sources AI pulls from for a brand (listicles, location pages, blog/editorial, social/community, directories/reviews), how much is owned vs third-party, and what each dominant source type tells you to build. Reads RankPrompt citation data and maps it to the AI Visibility Matrix citation taxonomy.
---

# citation-map

Read what AI actually cites for a brand and turn it into a lane-by-lane play. This is the "read the citations" step of the Matrix (`knowledge/matrix.md` → "Reading citations"). Runs standalone or as step 4 of `matrix-diagnose`.

## Inputs

- Brand + report (`rankprompt_get_report` for the embedded `citations[]`; `rankprompt_list_citations` / the by-domain rollup for scored, categorized citation metadata: `rankprompt_score`, `is_actionable`, `has_contact`, `domain_category`, per-platform counts).

## Steps

1. **Rank by frequency, per segment.** Count how often each source is cited (`citations[]` occurrences grouped by the prompt's `category`). Read the real top 10–20. **Do not sort by `rankprompt_score`** for this — it's listicle-biased (it flags outreach opportunities), so a score-sorted list is circular. `rankprompt_score` is used only in the outreach step.

2. **Categorize each top source** into the taxonomy:
   - **Listicles / "best of" roundups** — third-party category roundups.
   - **Location pages** — local-intent pages (city/region).
   - **Blog / editorial** — how-to, guide, comparison, FAQ content.
   - **Social / community** — Reddit, LinkedIn, YouTube, forums.
   - **Directories & review sites** — G2, Clutch, Trustpilot, Capterra, GMB, etc.
   - **Owned vs third-party** — is the cited page the brand's own domain or someone else's? (This is what Citation Share measures.)

3. **Roll up the mix.** For each segment: the % share of citations by type, the owned-vs-third-party split, and which type dominates.

4. **Name the play per dominant type** (`matrix.md` table):
   - Listicles → get named in more + publish your own.
   - Location pages → benchmark the top-cited local page; one strong page per market.
   - Blog/editorial → identify the winning format and make more of exactly that.
   - Social → engage where the citations live.
   - Directories/reviews → claim + complete the cited profiles, build reviews (the reputation lane).

## Output

- A citation map per segment: ranked top sources (full `https://…` URLs), each tagged with its type and owned/third-party, the type-mix rollup, and the single highest-leverage lane with its play.
- Feeds `matrix-diagnose`'s action plan and, for a client-facing view, `matrix-board`.

## Guardrails

- Frequency, not `rankprompt_score`, drives the read.
- Every source a full clickable URL, not a bare domain or `/path`.
- Never invent a citation or its category — categorize only what's in the data; mark "uncertain" when the type isn't clear.
