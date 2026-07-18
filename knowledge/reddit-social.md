# Reddit & community — the external play AI rewards

Reddit is consistently one of the most-cited sources in AI answers. If your report's citation-source mix is heavy on Reddit/forums or social, AI is sourcing your category from communities — and the play is to be *in* those communities and to *out-answer* the threads.

## Pick the right rooms

Don't guess subreddits. From your citations, filter to `reddit.com` and see **which subreddits and threads AI already pulls from** for your prompts. Note the ones citing competitors but not you — those are the exact rooms to be in. Rank them by how often AI cites each.

## Warm up before you post

Never promote from a brand-new account — it gets ignored or removed.
- Join 5–10 relevant subreddits.
- Comment naturally, upvote, reply, take part for **2–4 weeks**.
- Build some karma (50–200+) before any brand mention.
- Mix business and non-business activity so you read as a real person.

## The 80/20 rule

**80% genuine value, 20% contextual brand mention.** Answer questions, share real insight, and only mention your brand where it honestly helps — with a light disclosure ("full disclosure, I'm on the team at {brand}"). Drop-a-link-and-run gets downvoted and does nothing for AI visibility. The 80/20 is measured across your *whole account history*, not per comment.

## Read the thread first — never draft from the title

The single biggest mistake when drafting comments is writing from the thread's **title or the citation URL** instead of the **actual discussion**. A comment that ignores what people said reads as an ad and gets downvoted or removed — and it won't earn a citation. Before drafting *any* comment:

1. **Read the real thread — actually open it in a browser.** Plain WebFetch is blocked on Reddit (returns 403), so load the page with a **browser MCP** and read the actual comments. This repo ships one: `chrome-devtools-mcp` is declared in `.mcp.json` (`npx -y chrome-devtools-mcp@latest`; needs Node LTS + Chrome, and a Claude Code restart to load) — use it, or Claude-in-Chrome, to open the thread URL and pull the top comments. Fallbacks when no browser is available: the RankPrompt citation **snippet** (`citations[].snippet` / `cited_text` — the exact text AI pulled, real but partial), or ask the user to paste the thread. Read public threads only, respect Reddit's rate limits and ToS (this is for reading the handful of cited threads, not mass-scraping), and do **not** route around the fetch block with raw curl/JSON endpoints.
2. **Note what's actually there:** the specific places and prices people name, the *vibe* (budget/casual vs premium; community vs feature-list), and any single commenter whose exact need the brand fits.
3. **Draft to that.** Validate the answers already given, then add the brand where it genuinely fits — referencing the real thread, not a generic category pitch. (A "cheapest coworking" thread that already names the budget spots is the wrong place to claim you're the best; the right move there is an *honest-caveat mention* — see below.)

## Mention the brand every time — but adapt, and vary the format

Be present as a **citable, credible source**. Mention the brand in each comment (with disclosure), but change the *type* of comment to fit the thread so nothing reads as copy-paste. Pick the type that matches the thread:

- **Value-first list-add** *(default)* — answer the question well, validate the options already named, then add the brand as *one* honest option with disclosure. Works almost anywhere.
- **Specific-need reply** *(safest)* — reply to the one commenter whose exact need the brand solves (podcast/video/private day office/etc.). You're helping a person, not broadcasting — lowest removal risk, best fit.
- **Honest-caveat mention** — when the brand isn't the thread's best answer, say so plainly and reframe to where it *does* fit. Admitting the mismatch builds credibility.
- **"I work here, ask me"** — transparent and low-key: offer to answer pricing / what's-included. Invites questions instead of pitching.

**Always avoid:** link-drops (don't paste a URL unless asked), the same comment pasted across threads, mentioning the brand where it's irrelevant, arguing, and first-comment-on-a-fresh-account. These are what get removed and shadowbanned.

**Disclosure is required** (FTC + most subreddit rules). Keep it short and human ("I'm on the team at {brand}"); done lightly it builds trust rather than killing the comment. Never post an undisclosed brand mention.

## A weekly cadence that compounds

- A few **authority comments** on existing threads that already rank (double value: Reddit + Google + AI).
- A couple of **helpful posts** that invite the kind of questions you can answer well.
- Several **soft recommendation** comments where your brand genuinely fits.

Results compound: threads age, get cited by AI, and keep working long after you post.

## Pair it with content

Community engagement is strongest next to content. Publish answer-first pages that answer the same questions the threads do (`citable-content.md`), so AI starts citing *your page* alongside the thread. Engagement + a citable page is the full community play.

## Social authority layer (when it fits)

If your report shows LinkedIn or YouTube in the cited mix, the category rewards a social layer:
- **LinkedIn** — publish your listicles/comparisons as articles from a founder or company page. High authority, gets indexed, strong for B2B.
- **YouTube** — video versions of "best X" / "A vs B" content. AI increasingly pulls from transcripts, and there's less competition.
- **Instagram** — if the cited mix shows Instagram (common for visual/creative categories), the plays are (1) post from the brand's own handle so it becomes a citable source — including Reels, which AI Overviews cites individually — and (2) get *featured/tagged* by the curator accounts AI already pulls from.

Only invest here if the citations show the category rewards it — otherwise put the effort into content and outreach first.
