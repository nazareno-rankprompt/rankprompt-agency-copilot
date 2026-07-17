# The LLM file (llms.txt) — what it is and how to build it

This is the concept people most often misunderstand, so start here.

## What it actually is

An **LLM file is a brand brief written for AI** — think of it as a short, plain Wikipedia entry for your business that you control. It lives at `https://yourdomain.com/llms.txt` (plain text/markdown), usually paired with a styled **LLM-info page** (e.g. `/llm-info/`) that says the same things for humans.

It states, clearly and without marketing fog:
- **What you are** — the one-line definition of your product/service.
- **Who it's for** — your ideal customer and the problem you solve.
- **Your category** — the words a buyer (and an AI) would use to classify you.
- **Use cases** — the concrete jobs people hire you for.
- **Competitors / alternatives** — who you're compared against (yes, name them).
- **Why you're different** — the honest, specific reason to pick you.
- **FAQs** — the real questions buyers ask, answered directly.
- **Links to trusted references** — your best third-party proof (reviews, press, profiles).

## Why it matters

AI assistants are constantly trying to figure out what your brand *is* — and when they have to guess, they get it wrong, repeat outdated facts, or put you in the wrong category. The LLM file gives them a **clean, machine-readable source of truth** straight from you. It's the cheapest way to stop AI from misdescribing you, and it anchors the category and comparisons you *want* to be known for.

It won't single-handedly make you the top recommendation — that takes content and external proof — but it's foundational hygiene. It's the difference between AI guessing about you and AI reading your own clear statement.

## What good looks like

- **Plain and structured**, not designed. No hero images, no clever copy — clean headings and direct sentences. Machines parse structure.
- **Specific over flattering.** "Bilingual buy-here-pay-here dealership in Houston and OKC; in-house financing, down payment required" beats "the premier automotive solution."
- **Honest about category and competitors.** Hiding alternatives doesn't help; AI already knows them, and naming them positions you correctly.
- **Current.** Put a "last updated" date and keep facts true.

## A simple structure to fill in

```
# {Brand}

> {One-sentence definition: what you are and who it's for.}

## What we do
{2–4 sentences. The category in the buyer's words. The core offering.}

## Who it's for
{Who it's for and the problem that makes them search.}

## Use cases
- {use case}
- {use case}

## How we're different
{The specific, honest differentiator. Compared to {alternatives}, we {…}.}

## Alternatives people consider
{Competitor}, {Competitor}, {Competitor}.

## FAQ
**{Real buyer question}?** {Direct answer.}
**{Real buyer question}?** {Direct answer.}

## References
- {Trusted third-party link: review profile, press, directory}

_Last updated: {date}_
```

## Where to deploy it (by CMS)

The file must be reachable at `yourdomain.com/llms.txt` as plain text. How you get it there depends on your stack — see `cms-notes.md` for the exact steps. Quick version:

- **Custom / Next.js / static:** drop `llms.txt` in your `public/` (or web root) folder so it serves at `/llms.txt`. Deploy.
- **WordPress:** add the file at the site root via your host's file manager/SFTP, or a plugin that serves a custom route; build the `/llm-info/` page as a normal page.
- **Webflow:** Webflow can't serve an arbitrary root `.txt` easily — host `llms.txt` via a reverse proxy/redirect at the domain level (or your CDN), and build `/llm-info` as a normal Webflow page.
- **Shopify:** serve `llms.txt` via the theme/app or a redirect; also confirm the agentic sitemap (`sitemap_agentic_discovery.xml`) exposes your pages to AI crawlers.

Always confirm it's live by opening `yourdomain.com/llms.txt` in a browser. If it 404s, AI can't read it.
