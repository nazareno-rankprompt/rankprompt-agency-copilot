# Technical & on-page checklist

A page can't be cited if AI can't crawl it, can't tell what it's about, or finds nothing worth quoting. Before any clever strategy, run the boring fundamentals — most "why aren't we cited" cases have a basic miss underneath.

## On-page basics (the page itself)

- **One clear H1** that states what the page is, with a logical H2/H3 hierarchy that matches how buyers phrase the question.
- **Unique, substantive content** — not a thin or near-duplicate template. Enough real, on-intent material to actually answer the query, in the buyer's vocabulary.
- **Title tag + meta description** that match the page's intent and read like the query.
- **Answer-first structure** and the citable-format rules in `citable-content.md`.
- **Internal links** from related pages so the page isn't an orphan.

## Technical (can AI reach and trust it)

- **Crawlable and indexed** — check `site:yourdomain.com/your-page` in Google; no accidental `noindex` or robots block.
- **AI crawlers allowed** in `robots.txt` — GPTBot, PerplexityBot, ClaudeBot, Google-Extended, and the rest. If these are blocked, the page is invisible to those models no matter how good it is.
- **In the sitemap** — your regular sitemap *and* the AI/agentic sitemap if your platform exposes one (e.g. Shopify's `sitemap_agentic_discovery.xml`).
- **Right structured data (JSON-LD)** for the page type — LocalBusiness / Service / FAQ / Product as fits — so AI can parse the entities.
- **Core Web Vitals and mobile** — slow or broken-on-mobile pages get discounted.
- **llms.txt and the LLM-info page** published and current (`llms-txt.md`).

## How to confirm

- Open `yourdomain.com/your-page` and view source: is there a real H1? Is the JSON-LD present?
- Open `yourdomain.com/robots.txt`: are AI bots allowed?
- Open `yourdomain.com/sitemap.xml`: is the page listed?
- `site:` search it: is it indexed?

Run this as a checklist on every page you're trying to win. Fix the fundamentals first; then the content and strategy have something to stand on. How to actually apply each fix depends on your CMS — see `cms-notes.md`.
