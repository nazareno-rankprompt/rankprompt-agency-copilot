---
name: content-calendar
description: Plan a month of citable content for a brand, mapped to its losing prompts and Matrix square. Use when the user wants a content plan / calendar that sequences which listicle, how-to, comparison, or FAQ to make and when. Produces a simple, prioritized calendar.
---

# content-calendar

Sequence the content plays into a simple monthly plan, driven by where the brand is actually losing. This is the planning layer over `listicle` / `how-to-guide` / `comparison` / `faq-page` — it decides what to make and in what order. Keep it lightweight.

## Inputs

- The brand's diagnosis (`matrix-diagnose`): the square per segment and the losing prompts.
- The citation read (`citation-map` / `citation-audit`): which content format wins each losing prompt.
- Capacity (how many pieces/month — ask; default ~4).

## How to build it

1. **Start from the losing prompts, not topics.** Each planned piece should target a real prompt where the brand is invisible or cited-not-chosen.
2. **Match format to what AI cites** for that prompt: listicle where roundups win, how-to for informational, comparison for "vs" queries, FAQ for long-tail, location page for local intent.
3. **Prioritize by leverage:** highest-value buyer intent + fastest path to a citation first. Front-load the zero-citation gaps.
4. **Lay out the month** as a simple table: week · piece · format · target prompt(s) · which skill produces it · priority. Note the one internal-GEO fix that should ship alongside (llms.txt, schema) if relevant.
5. Keep it to what the capacity can actually ship — a real 4-piece plan beats a 20-item wishlist.

## Output

- A clean **Markdown** calendar (table) the agency can work straight from, each row pointing to the skill that produces it.
- Optional simple branded HTML if they want to send it to the client.

## Guardrails

- Every piece maps to a real losing prompt from RankPrompt data — no generic content ideas.
- Don't over-plan; match the plan to stated capacity.
- Re-plan monthly off a fresh diagnosis (movement changes priorities).
