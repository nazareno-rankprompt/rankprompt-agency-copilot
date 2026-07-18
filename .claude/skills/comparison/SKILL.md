---
name: comparison
description: Write an "X vs Y" / "alternatives to X" comparison page the brand can publish to own comparison queries in AI answers. Use when the citation read shows comparison content wins, or the brand is losing "X vs Y" / "best alternative to X" prompts. Produces a clean, citable comparison page.
---

# comparison

Create an owned comparison page ("{Brand} vs {Competitor}", "alternatives to {Competitor}", "{Brand} vs {Competitor} vs {Competitor}") built for AI citation — comparison pages are a format AI leans on heavily for buying-decision queries. Keep it simple, fair, and genuinely useful.

## Inputs

- The comparison to own (ideally a losing "vs" / "alternatives" prompt from `matrix-diagnose` / `citation-audit`).
- The real competitor(s) AI names in the category, and the brand's honest differentiators.
- `content-rules.md` if the client has one (obey verbatim).

## How to write it

1. **Be genuinely fair.** A comparison that trashes every competitor won't get cited (or trusted). State where each option actually wins — including where a competitor beats the client. Fairness is what makes it a citable source.
2. **Lead with a one-paragraph verdict** ("best for X → {Brand}; best for Y → {Competitor}") so AI can extract the summary.
3. **A comparison table** on the dimensions buyers actually weigh (price model, best-for, key strength, main limitation, support, etc.) — clean, parallel rows AI can lift.
4. **A short section per option** with its real best-fit case and an honest caveat.
5. **Close with "which should you choose"** by use-case, not a blanket "pick us."
6. **Paragraphs: 2 sentences max** (~150–160 chars), real transitions.
7. **Run the `humanizer` skill** before finalizing. No "Disclosure:" line.

## Output

- Clean **Markdown** (CMS-ready) + optional simple branded HTML with the table.
- **Apply notes:** title/meta ("{Brand} vs {Competitor}: {year} comparison"), where it lives, and to add `Article` / `FAQPage` schema.

## Guardrails

- Real competitors, real facts, real pricing/feature claims — never invent a spec or misstate a rival.
- Keep it fair: at least one honest point where a competitor wins.
- Obey `content-rules.md` where present.
