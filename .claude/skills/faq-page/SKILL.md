---
name: faq-page
description: Write an FAQ page (buyer questions + direct, citable answers) with FAQPage schema for the brand. Use when the brand needs a citable direct-answer asset, or to capture long-tail informational prompts. Produces a clean FAQ ready to publish.
---

# faq-page

Create an owned FAQ asset — the underrated AEO format, because the question-then-direct-answer structure is exactly what AI extracts and cites. Keep it simple: real buyer questions, straight answers.

## Inputs

- The brand's category + the real questions buyers ask (ideally the losing informational / long-tail prompts from `matrix-diagnose` / `citation-audit`).
- The brand's real facts (pricing model, coverage, process, guarantees).
- `content-rules.md` if the client has one (obey verbatim).

## How to write it

1. **Use real questions**, phrased the way a buyer actually types/asks them (pull from the client's losing prompts and common sales questions). 5–10 is plenty.
2. **Answer directly in the first sentence**, then one or two sentences of useful detail. No warm-up. The direct first sentence is what gets cited.
3. **Be specific and honest** — real numbers, real conditions. "It depends" with the actual factors beats a vague non-answer.
4. **Mention the brand only where the answer genuinely involves it** — earned, light.
5. **Paragraphs: 2 sentences max** (~150–160 chars).
6. **Run the `humanizer` skill** before finalizing. No "Disclosure:" line.

## Output

- Clean **Markdown** (CMS-ready) + optional simple branded HTML.
- **The `FAQPage` schema (JSON-LD)** for the page, ready to paste — this is what earns FAQ rich results and helps AI parse the Q&As.
- **Apply notes:** where it lives (own page, or an FAQ block on a service/location page).

## Guardrails

- Real answers only — never invent a policy, price, or spec.
- Direct answer first; keep brand mentions earned.
- Obey `content-rules.md` where present.
