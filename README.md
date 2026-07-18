# RankPrompt Agency Copilot

Clone-and-go **AI-visibility workstation** for agencies. It carries RankPrompt's brain — the full GEO/AEO methodology, organized around the **AI Visibility Matrix** — and connects to your RankPrompt account over the hosted MCP so it reasons over *real* client data: reports, citations, competitors, movement over time.

Point it at a client and it will: plot them on the Matrix (per category and location), read what AI actually cites for them, name the one play that moves them toward Winning, and render a branded, interactive matrix board you can show the client. It **does not** publish for you — it produces ready-to-apply deliverables and tells you how to use them.

> This is the workstation used in the **RankPrompt GEO Agency Sprint** (see `rankprompt-claude/context/agency-program/sprint-outline.md`), set up in Session 1 and used every session after.

## What you need

- **Claude Code** installed (or Claude Desktop — see `docs/desktop-setup.md`).
- A **RankPrompt account**, Starter plan or higher.

## Setup (Claude Code)

1. Clone this repo and open it in Claude Code.
2. Connect the RankPrompt MCP (already declared in `.mcp.json`):
   ```bash
   claude mcp add --transport http --scope user rankprompt https://mcp.rankprompt.com/mcp
   ```
3. Run `/mcp` and authenticate in the browser (OAuth — no key to paste). Prefer a key? Copy `.env.example` → `.env` and set `RANKPROMPT_API_KEY` (create one at [app.rankprompt.com/developers](https://app.rankprompt.com/developers)).
4. Say *"prime RankPrompt and list my brands"* — the copilot runs `rankprompt_prime`, confirms auth, and you're live.

## Quickstart

- *"Diagnose <brand> on the Matrix"* → runs **matrix-diagnose** (segments, plots each square, per-segment action plan).
- *"What does AI cite for <brand>?"* → runs **citation-map** (categorizes citations, names the highest-leverage lane).
- *"Build the matrix board for <brand>"* → runs **matrix-board** (branded interactive HTML + PDF; filter by platform/location; animate movement over time).

## What's in here

```
CLAUDE.md              operating brief — the Matrix model, the MCP tools, the workflow
.mcp.json              RankPrompt MCP wiring (https://mcp.rankprompt.com/mcp)
.claude/skills/
  matrix-diagnose/     plot on the Matrix + action plan
  citation-map/        quick citation read → the play each type implies
  citation-audit/      deep: crawl top cited URLs → branded audit + rebuild plan  ← template.html
  matrix-board/        branded interactive matrix board (HTML + PDF)  ← template.html
  reddit/              subreddits/threads AI cites → Google Sheet or HTML + comments
  listicle/ how-to-guide/ comparison/ faq-page/   create owned, citable content (Markdown + schema)
  content-calendar/    sequence the content plays into a monthly plan
  humanizer/           strip AI-writing tells — run on every client-facing piece
knowledge/             the methodology the copilot reasons with
  matrix.md            the AI Visibility Matrix (the spine) + citation taxonomy
  brain.md             deep diagnostic mechanics (root causes, own-source autopsy)
  reading-reports.md · citable-content.md · llms-txt.md · outreach.md
  reddit-social.md · technical-seo.md · measuring.md · prompt-discovery.md · cms-notes.md · geo-101.md
templates/             profile (session memory) + action-plan shells
logos/                 RankPrompt logos for branded deliverables
docs/desktop-setup.md  how to run the same brain in Claude Desktop
```

## The one rule

The copilot only ever reasons over **real** RankPrompt data. It never invents a visibility score, a citation, a competitor, or a URL. If it doesn't have something, it pulls it or tells you — it never guesses.

## Credits

Built on the methodology from `rankprompt-geo-copilot`, reframed around the AI Visibility Matrix for the agency program.
