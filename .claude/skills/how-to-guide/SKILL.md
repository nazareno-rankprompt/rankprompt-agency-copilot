---
name: how-to-guide
description: Write a how-to / step-by-step guide the brand can publish that AI will cite for informational queries in its category. Use when the citation read shows how-to / guide content wins, or to answer the "how do I …" prompts a brand is losing. Produces a clean, citable guide.
---

# how-to-guide

Create an owned how-to / step-by-step guide built for AI citation — the format that wins informational and "how do I …" queries. Keep it simple and genuinely useful; a guide only gets cited if it actually answers the question.

## Inputs

- The target question/topic (ideally a losing informational prompt from `matrix-diagnose` / `citation-audit`).
- The brand's real expertise/context (so the guide is specific, not generic).
- `content-rules.md` if the client has one (obey verbatim).

## How to write it

1. **Answer the question directly, up top.** Lead with a 1–2 sentence direct answer, then the steps. AI extracts the direct answer first; burying it loses the citation.
2. **Numbered steps, one action each.** Each step: what to do + why it matters + any specific detail (settings, amounts, timing). Concrete beats comprehensive-sounding.
3. **Cover the sub-questions the topic raises** — the "but what about…" a real person would ask. Those are often their own cited snippets.
4. **Add a short FAQ** at the end (3–5 real questions) — good for long-tail + FAQ rich results.
5. **Mention the brand only where it's genuinely the tool for a step** — earned, not shoehorned. A helpful guide that name-drops naturally gets cited; an ad doesn't.
6. **Paragraphs: 2 sentences max** (~150–160 chars); real transitions, prose cut not just split.
7. **Run the `humanizer` skill** before finalizing. No "Disclosure:" line.

## Output

- A clean **Markdown** guide (CMS-ready) + optional simple branded HTML.
- **Apply notes:** title/meta, where it lives, and to add `HowTo` + `FAQPage` schema.

## Guardrails

- Steps must be correct and real — never invent a procedure, setting, or spec.
- Direct answer first; keep the brand mention earned and light.
- Obey `content-rules.md` where present.
