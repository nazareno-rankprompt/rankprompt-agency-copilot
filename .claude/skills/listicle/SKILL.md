---
name: listicle
description: Write a "best of" / listicle article the brand can publish that AI will cite for its category. Use when the citation read shows listicles/roundups win the category and the play is to publish your own. Produces a clean, citable article the agency can put on the client's site.
---

# listicle

Create an owned listicle ("best X in {city/category}", "top N tools for Y") built to get cited by AI — because roundups are one of the formats AI leans on most. Keep it simple: a strong, honest, citable article they can publish as-is.

## Inputs

- The target query/category (ideally from `matrix-diagnose` / `citation-audit`: a prompt where listicles win and the brand is losing).
- The brand + a real sense of the competitor set (from RankPrompt: who AI names in that category).
- `content-rules.md` if the client has one (obey verbatim — naming, banned claims, market/spelling).

## How to write it

1. **Frame the list honestly.** A roundup that only exists to crown the client reads as an ad and won't survive as a citable source. Include the real players AI already names; place the client where it genuinely fits and say why. Credibility is what gets a listicle cited.
2. **Structure for extraction.** Clear H2 per entry (the entry name), a 2–3 line description, and a consistent mini-rubric across entries (who it's best for, notable strength, a real caveat). AI extracts clean, parallel structure.
3. **Lead with a short, specific intro** that states what the list covers and how entries were chosen — no throat-clearing.
4. **Be concrete.** Real differentiators, real use-cases, real numbers where you have them. Vague praise doesn't get cited.
5. **Paragraphs: 2 sentences max** (~150–160 chars). Cut, don't just split — real conversational transitions between them.
6. **Run the `humanizer` skill** on the whole piece before finalizing. **Never** include a "Disclosure:" / "this list is published by X" line — a byline is enough.

## Output

- A clean **Markdown** article by default (paste into any CMS), plus optional simple branded HTML.
- **Apply notes:** suggested title/meta, where it should live on the site, and to add `ItemList` / `Article` schema. Note that AI-cited roundups compound — it's worth keeping fresh.

## Guardrails

- Real competitors and real facts only — no invented entrants, stats, or quotes.
- Honest placement of the client; keep at least one genuine caveat per entry.
- Obey `content-rules.md` where present.
