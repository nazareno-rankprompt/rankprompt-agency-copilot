# Applying fixes on your CMS

Every fix — a new page, schema, an llms.txt file — has to actually land on your site. How depends on your stack. Find out where their website is built — ask in plain terms (*"Is your site on WordPress, Shopify, Webflow, Squarespace, Framer, or something custom? Not sure is fine."*), not by saying "CMS" — and store it in `profile.md`, then give them the matching steps. When in doubt, or if they don't know, fall back to the generic version at the bottom.

## WordPress
- **New content/pages:** create as normal Pages/Posts. Keep one H1, clean H2/H3.
- **Schema (JSON-LD):** use Yoast SEO or Rank Math (both add FAQ/Article/LocalBusiness schema), or a custom-HTML block / a header-footer-code plugin for hand-written JSON-LD.
- **llms.txt:** place the file at the site root (`/llms.txt`) via your host's file manager or SFTP, or a plugin that serves a custom route. Build `/llm-info/` as a normal Page.
- **robots/sitemap:** Yoast/Rank Math manage the sitemap; confirm AI bots aren't blocked in `robots.txt`.

## Webflow
- **New content/pages:** build as CMS items or static pages; use the heading elements (don't fake headings with styled text).
- **Schema:** add JSON-LD via an embed/custom-code element on the page, or in page settings → custom code (before `</body>`).
- **llms.txt:** Webflow can't easily serve an arbitrary root `.txt`. Serve it via a domain-level redirect/reverse proxy or your CDN (e.g. Cloudflare Worker) so `/llms.txt` resolves. Build `/llm-info` as a normal Webflow page.

## Shopify
- **New content/pages:** blog posts and Pages via the admin; product/collection content in the theme.
- **Schema:** add JSON-LD in the theme (`theme.liquid` or section files), or via an SEO app.
- **llms.txt:** serve via an app, a theme template, or a redirect; confirm the agentic sitemap (`sitemap_agentic_discovery.xml`) exposes your pages to AI crawlers.
- **robots:** editable via `robots.txt.liquid` — make sure AI bots are allowed.

## Framer
- **New content/pages:** build pages/CMS collections normally with real heading elements.
- **Schema:** add JSON-LD via a custom-code component or the site's custom `<head>` code.
- **llms.txt:** serve via a redirect/proxy at the domain level (similar to Webflow); build `/llm-info` as a page.

## Custom / Next.js / static
- **New content/pages:** as routes/MDX/markdown in your codebase.
- **Schema:** render JSON-LD in a `<script type="application/ld+json">` in the page head (a small reusable component).
- **llms.txt:** drop `llms.txt` in `public/` (Next.js) or your web root so it serves at `/llms.txt`. Deploy.
- **robots/sitemap:** ensure `robots.txt`/`sitemap.xml` allow and list the pages; add AI user-agents to the allow list.

## Generic / other CMS
- Create the page with one real H1 and clean headings.
- Add JSON-LD anywhere you can inject `<head>` or body HTML.
- Get `llms.txt` reachable at `yourdomain.com/llms.txt` — via file upload to web root, a redirect, or your CDN.
- Confirm everything is live by opening the URL in a browser and running a `site:` search. If it 404s or isn't indexed, AI can't use it.
