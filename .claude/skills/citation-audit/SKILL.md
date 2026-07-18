---
name: citation-audit
description: Deep citation analysis for a category or location — crawls the top cited URLs, categorizes every cited source by type and page type, compares the winning pages against the brand's own pages signal-by-signal, and produces a branded HTML/PDF audit with a concrete rebuild plan. Use when the user wants to understand exactly why a brand is or isn't cited in a market, what to fix on their own pages vs what to create, and get a client-ready citation/location audit deliverable.
---

# citation-audit

The deep version of citation analysis. Where `citation-map` gives a quick read of the citation mix, `citation-audit` **fetches the actual top-cited URLs** — the winners and the brand's own pages — pulls them apart, and produces a client-ready audit with a specific rebuild plan per segment. It operationalizes the own-source autopsy + sitemap reconciliation in `knowledge/brain.md` §3.5 and the citation taxonomy in `knowledge/matrix.md`.

**Gold-standard references** (read them to match depth + structure before building):
- `examples/quiet-events-city-audit/` (`report.html` + PDF) — city audit; mechanism = page-quality/intent (city pages existed but were thin, duplicate, disco-framed → discounted).
- `examples/owings-auto-location-audit/` (`report.html` + PDF) — location audit; mechanism = footprint (on-page fine; too few third-party profiles cited Owings in the lagging market).

The point of the analysis is to land on **the mechanism** — the one real reason — and prove it with fetched evidence, not to list generic tips.

## Inputs

- Report + citations via MCP: `rankprompt_get_report` / `rankprompt_get_report_summary`, `rankprompt_list_citations`, `rankprompt_list_competitors`.
- On-page signals: `rankprompt_audit_pages` for the brand's own pages; **web fetch** for the top competitor/third-party pages (you must actually open them).
- The brand's **sitemap** (`/robots.txt` → `Sitemap:`, `/sitemap.xml`, and any `llms.txt` / `sitemap_agentic_discovery.xml`) via web fetch — never `rankprompt_*` for this.

## Steps

1. **Scope & segment.** Pick the category and/or location set. Compute per segment (see `matrix-diagnose`): **Visibility Score** (appear rate) and **Citation Share** (own-domain ÷ all cited links). Show a per-segment table; flag the winning and lagging segments.

2. **Field position.** Rank brands by mentions across all answers (share of voice) — where does the brand sit, and who are the real rivals to compare against?

3. **Categorize every cited URL — two axes** (this is the heart; compute by frequency, not `rankprompt_score`):
   - **Source type:** brand-owned · competitor site · directory/review · social/community · AV/event vendor (or the vertical's equivalent) · other/local · Google/Maps.
   - **Page type:** homepage · location/city page · listicle/"best of" roundup · blog/editorial · product/service page · directory listing · social · top-level · other deep page.
   - Report the **% mix** per segment. The dominant page type = the format AI rewards here (e.g. "51% of cited URLs are location/city pages"). The source-type mix = where trust is coming from (own vs third-party vs directories vs social — the answer to "is it citing homepages? listicles? directories? social? our page?").

4. **Per-segment cards.** For each location/category: the source-mix line + the **actual top cited URLs** (full clickable `https://…`), each tagged with source + page type, the brand's own pages highlighted, with citation counts. This is the surface you fetch from next.

5. **Own-source surface + sitemap reconciliation.** List which of the brand's *own* pages AI cites and how often. Then fetch the sitemap and check, per losing segment: **does a matching page already exist?** Is it cited or ignored? Is it even in the AI sitemap / `llms.txt`? (Quiet Events had all 10 city pages — existence wasn't the problem.) This decides improve-vs-create.

6. **The autopsy — fetch and compare.** For each priority segment, open the **top-cited winning page** (usually a competitor location or listicle page) and the brand's **matching own page**, and compare signal-by-signal in a table:
   - **Content** — word count, uniqueness, and **duplication across the brand's own pages** (are the city pages byte-for-byte templates? that's fatal).
   - **Intent framing** — keyword density for the real query intent vs the wrong one (QE's pages were "disco"-framed while the queries were "conference").
   - **Title / meta** — do they carry the commercial + local + intent keywords, or a dead line like "No events yet in your city"?
   - **Schema** — LocalBusiness / Service / Event / FAQPage present, or just Organization/Image?
   - **In the AI sitemap?** — is the page discoverable to AI crawlers at all?
   Conclude the **mechanism** for the segment in one sentence, mapped to a `brain.md` root-cause pattern: *page-existence* (no page) · *page-quality/intent* (thin/duplicate/mis-framed) · *footprint* (fine on-page, too few third-party citations) · *off-site/community* · *cold-start*.

7. **Recommendations — the rebuild.** Turn the mechanism into a concrete plan:
   - **Page blueprint** — the exact sections the page needs, each written so it doubles as a heading AI extracts, made specific to the segment (cover every intent the market serves, not one).
   - **Technical must-dos** — uniqueness per page (kill duplication), title/meta tuned to intent, the schema types to add, internal links + add the page to the AI sitemap/llms.txt.
   - **Prioritized rollout** — start with zero-citation segments, then the weak cluster; note the reports already exist so it can be re-run monthly.
   - **The measurable target** — own citation share now → goal (e.g. 5.6% → 15–20%), tracked by re-running this audit.

8. **Render.** Fill the `DATA` block in `template.html` → `out/<brand>-citation-audit.html`. Review, then print to PDF per `deliverable-design-rules` (`--virtual-time-budget=5000`, A4, no gradient text). Final files also copied to the client folder per the Final Output Rule.

## Output

- A branded, multi-section HTML + PDF citation/location audit matching the reference examples.
- Per segment: the citation mix (both axes), the top cited URLs, the fetched-evidence autopsy, and the rebuild plan — every claim tied to real data and every source a clickable URL.

## Guardrails

- **Actually fetch the pages.** The autopsy's whole value is real evidence — never characterize a page (word count, schema, duplication, framing) you didn't open. If a fetch fails, say so and mark it unverified; don't guess.
- Categorize by **frequency**, never `rankprompt_score`.
- Land on ONE mechanism per segment and prove it. Don't hand over a generic checklist.
- Keep Visibility Score and Citation Share correctly labeled and never swapped.
- Real data only — no invented URLs, counts, competitors, or page attributes.
