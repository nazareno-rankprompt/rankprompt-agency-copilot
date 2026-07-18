---
name: task-board
description: Turn the copilot's recommendations into a tracked list of concrete GEO tasks for a client — adapt a page, create a page, find author emails and pitch listicle inclusion, claim/improve directories, get reviews, write a blog/listicle/how-to, engage or post on Reddit, make a YouTube/LinkedIn/Instagram post, optimize a page, tear down a competitor's cited page. Use when the user wants the action plan captured as tasks, wants to add/update tasks, or asks "what's on the board." Persists as a Google Sheet if a Drive connector is available, else a Markdown file (+ optional branded HTML board).
---

# task-board

The execution tracker. Everything the diagnosis/audit skills surface becomes a **typed, trackable task** the agency works through. This is where "here's what to do" turns into "here's the list, here's what's done." Keep it simple: one board per client, easy to update.

## Where tasks come from

- **From a diagnosis/audit** — ingest the action plan from `matrix-diagnose`, `citation-audit`, `citation-map`, or `content-calendar` and generate one task per recommended action, tagged to the segment and the mechanism that justifies it.
- **From the user** — "add a task to …", dictated directly.
- Each task should trace back to a real reason (a losing prompt / square / citation gap) — no busywork.

## Task schema

Every task has:

| Field | Meaning |
|---|---|
| **title** | The action, imperative — "Rebuild the Dallas location page", "Pitch inclusion in {listicle}" |
| **lane** | `content` · `on-page` · `outreach` · `directories` · `reviews` · `reddit` · `social` · `competitive` |
| **target** | the page URL / directory / subreddit / competitor URL / prompt it acts on |
| **why** | the diagnosis reason — square + citation gap / mechanism |
| **segment** | category / location it serves |
| **priority** | High / Med / Low (by leverage) |
| **effort** | S / M / L |
| **produced_by** | the skill that executes it (`listicle`, `citation-outreach`, `reddit`, …) or `manual` |
| **status** | Todo / In progress / Blocked / Done |
| **link** | the deliverable/output once done |

## Standard task types (map recommendations to these)

- **on-page:** adapt/optimize an existing page · optimize a landing page (→ `technical-seo` / `quick-wins`)
- **content:** create a new page — listicle / how-to / comparison / FAQ / location page / blog post (→ the matching content skill)
- **outreach:** find author emails in RankPrompt and pitch listicle/article inclusion (pull contacts from the citation data — `author`, `author_email`, `has_contact` — via `rankprompt_list_citations`; → `citation-outreach`)
- **directories:** create/claim a profile in a cited directory · improve ranking within a directory
- **reviews:** get N reviews on {directory/review site} the AI cites
- **reddit:** engage in {subreddit} · create a Reddit post in {subreddit} about {topic} (→ `reddit`)
- **social:** create a YouTube video about {X} · LinkedIn post about {X} · Instagram post about {X}
- **competitive:** scan a competitor's top-cited page and improve our matching cited page (→ `citation-audit`)

## Steps

1. **Gather** the actions (from a diagnosis/audit, or the user).
2. **Write each as a well-formed task** using the schema — imperative title, correct lane, real target, the why, priority by leverage, and which skill produces it. Front-load the zero-citation / highest-value gaps.
3. **Persist:**
   - **If a Google Sheets / Drive connector is available** → create/update a **Google Sheet**, one "Tasks" tab, columns = the schema, Status as the working column (Todo/In progress/Blocked/Done). This is the live, shareable board.
   - **Else** → write/update `out/<client>-tasks.md` — grouped by lane, `- [ ]` / `- [x]` checkboxes, each task with its fields on one line. This is the in-repo source of truth.
   - **Optional** → render the branded **HTML board** (`template.html`, columns by status, cards colored by lane) for a client-facing snapshot.
4. **Update, don't duplicate.** When re-run, match existing tasks by title/target and update status/links rather than adding duplicates. Mark done tasks done; add new ones from a fresh diagnosis.

## Guardrails

- Every task traces to a real reason from RankPrompt data — never invent targets, directories, author emails, or competitor URLs.
- Keep titles concrete and doable (one action each), not vague themes.
- Match the plan to capacity — a tight, prioritized board beats a 50-item dump.
