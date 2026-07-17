# RankPrompt Agency Copilot — Prompt Library

Copy-paste prompts by situation. Replace `<client>` / `<prompt>` / `<URL>` etc. with real values. Prompts marked **(write)** need a write-scoped key/OAuth; on read-only the copilot hands you the steps to do it in the RankPrompt app.

## 1. Connect & warm up
- `Prime RankPrompt and list my brands.`
- `Which of my brands already have reports, and when were they last run?`
- `What can you actually do with my RankPrompt data? Give me the short version.`

## 2. Baseline a client (Sprint Session 1)
- `Set up brand context for <client> — category, who buys, markets — then help me build a 25-prompt map covering their whole category.`
- `Create a baseline report for <client> tracking ChatGPT, Perplexity, AI Overviews and Claude.` **(write)**
- `Pull the latest report for <client> and give me the shareable link to send them.`

## 3. Diagnose — plot on the Matrix (Session 2)
- `Diagnose <client> on the AI Visibility Matrix. Segment by category and location, and show me each square with the two numbers.`
- `What's <client>'s Visibility Score vs Citation Share per category? Put it in a table.`
- `Which square is <client> in for "<category>", and what's the one-sentence reason they're losing?`
- `Analyze <client>'s segments in parallel so this is faster.`

## 4. Read the citations
- `What does AI actually cite for <client>? Categorize the top sources and name the highest-leverage lane.`
- `Show me the listicles ChatGPT pulls from for <client>'s category that we're NOT in yet.`
- `For <client>, how much of what AI cites is their own domain vs third parties?`
- `Rank <client>'s cited sources by how often AI uses them — not by RankPrompt score.`

## 5. Build the client-facing board (matrix-board)
- `Build the matrix board for <client> — plot them and their competitors.`
- `Make the matrix board filtered to ChatGPT only.` / `...filtered to <location>.`
- `Show <client>'s movement on the matrix across the last 3 scheduled reports.`
- `Export the matrix board to PDF for the client readout.`

## 6. Turn diagnosis into a plan
- `Give me the single play that moves <client> from <square> toward Winning.`
- `Write the full per-category action plan for <client> and save it to out/.`
- `For <client>'s "<category>", should we improve an existing page or create a new one? Check their sitemap.`

## 7. Run the plays
**Content / Internal GEO (Session 3)**
- `Draft a citable comparison page for <client> targeting "<prompt>", in the format AI already cites for that category.`
- `Build <client>'s llms.txt + an AI-info page, and tell me exactly where to put it for <CMS>.`
- `Write a listicle <client> can publish that AI will cite for "<category>".`

**External GEO — listicles, reviews, Reddit (Session 4)**
- `Build a citation-outreach target list for <client> from the listicles AI cites, with a pitch email for each.`
- `Find articles where <competitor> is named but <client> isn't, for "<category>".`
- `Which review/directory sites does AI cite for <client>'s category, and how do we build trust there?`
- `AI recommends <client> but the sentiment is weak — what's the reputation play?`
- `Which subreddits does AI pull from for <client>'s category? Give me a Reddit plan and 3 comments that get them named naturally.`

**Technical**
- `Is <client>'s site crawlable by AI bots? Check for blocked bots, noindex, missing schema, stale dates.`
- `Run the on-page GEO checklist against <URL>.`

## 8. Prove movement (Session 5)
- `Schedule and isolate the prompts we just worked for <client> so we can watch that set move.` **(write)**
- `Did <client>'s "<category>" visibility move since last month? Re-diagnose and show the delta.`
- `Re-plot <client> on the matrix and tell me if we moved toward Winning.`

## 9. Report to the client (Session 5)
- `Write the monthly readout for <client>: baseline vs now, what we did, what moved, what's next.`
- `Give me <client>'s latest report share link and a 3-bullet summary I can paste into an email.`

## 10. Sell & land more clients (Session 5 / growth)
- `Run a quick AI-visibility audit on <prospect> I can use to open a pitch.`
- `Turn <prospect>'s baseline into a one-page sales asset.`
- `Help me package and price a GEO retainer for a client like <X> — give me the conversion math.`

## 11. Manage a book of clients
- `Give me a portfolio view: every client's current square, one line each.`
- `Which of my clients slipped in AI visibility since last check?`
- `Which client has the fastest path to a visible win this month, and why?`

---

**Tips**
- The copilot only reasons over real RankPrompt data — if it doesn't have something it'll pull it or ask, never invent.
- Lead with a client name and it'll pull the right report; say "segment by category and location" when a client spans several.
- Ask for a file (`save to out/…`) whenever you want a plan/deliverable you can keep or send.
