---
name: reddit
description: Build a client's Reddit plan from RankPrompt data — the subreddits and threads AI already cites for their category, ranked, as a working sheet, plus optional survive-worthy brand-mention comments. Use when the user wants a Reddit strategy, the threads to comment on, or drafted Reddit comments for a client. Outputs a Google Sheet if a Drive/Sheets connector is available, otherwise a branded HTML + CSV.
---

# reddit

Get a client's brand into the Reddit threads AI actually cites. This fuses the two service-side Reddit skills into one: find + rank the target subreddits/threads (from real citation data) and, optionally, draft the comments. Keep it simple — produce a solid working artifact the agency runs with.

## 1. Pull the threads (real data)

Use the RankPrompt MCP: `rankprompt_list_citations` for the brand, filter to `reddit.com` URLs. For each thread capture: URL, subreddit (`r/...` from the path), thread title (from the slug), citation count, which AI platforms cited it. Dedupe by base URL. Rank **top-cited first**, and group by subreddit (High/Medium/Low by total citations).

## 2. Output — Sheet if connected, else HTML

- **If a Google Sheets / Drive connector is available in the session** → create a Google Sheet with two tabs:
  - **Client Info** — brand name, positioning, differentiators, market.
  - **Threads** — one row per thread, top-cited first: `URL | Subreddit | # Citations | Cited By | Status | Comment | Notes`.
- **If not** → render a branded **HTML** plan (subreddit table with priority badges + the top 5–8 cited threads as clickable links) per `deliverable-design-rules`, and write a **CSV** with the same Threads columns so they can import it into a sheet themselves.

Either way the artifact is the same data; the Sheet is just the nicer home when Drive's connected.

## 3. Comments (optional)

If the user wants the comments drafted, write one per thread into the Comment column (or the HTML), following the **safe-comment style**:

- Value-first, lowercase, native Reddit voice; answer the OP's actual question with specific, lived detail.
- Name the client brand **once, softly, earned** (inside a list of options / mid-paragraph with a real reason — never "X is the best"). Sometimes name a real competitor too; it reads more genuine.
- Include one honest caveat. End with a genuine question back (vary it — not every comment).
- **Fit-triage first:** if the thread isn't a category + intent match, or the sub is hostile/rules-heavy, or it's >~1yr old (necro risk), write `⚠ RECOMMEND SKIP — <reason>` instead of a comment.
- If a browser connector (Chrome DevTools) is available, read the live thread first (reddit.com 403s plain fetches — navigate once, then same-origin fetch the `.json`). Otherwise work from the title + citation context and note it wasn't live-scanned.
- **Run the `humanizer` skill on every comment**, and vary the brand phrasing across the batch so it doesn't look like one template. Never add a "Disclosure:" line.

## Guardrails

- Real citation data only — never invent a thread, subreddit, or citation count.
- Check `content-rules.md` if the client has one and obey it (British English, approved naming, banned claims).
- A top-cited thread is not automatically a fit — skip mismatches rather than forcing the brand in.
