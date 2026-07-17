# Running the copilot in Claude Desktop

The workstation is built as a Claude Code repo, but the same brain runs in **Claude Desktop** for agencies that prefer the chat UI over a CLI. The difference: in Desktop the `.claude/skills/` don't auto-run as slash-skills, so you load the methodology as **Project knowledge** and drive it conversationally. The RankPrompt MCP and all reasoning work the same.

## 1. Connect the RankPrompt MCP

**RankPrompt is a custom server — it is NOT in Claude's connector directory.** Searching the directory or "connector search" will never find it. You must add it by hand as a *custom connector* with its URL. This is the step people get stuck on.

1. In Claude Desktop, click the **+** next to the message box → **Connectors** (or **Settings → Connectors**).
2. Click **Add custom connector** (at the bottom; may sit under an "Advanced" heading).
3. **Name:** `RankPrompt` · **URL:** `https://mcp.rankprompt.com/mcp`. Leave it as a remote/HTTP connector. Click **Add / Connect**.
4. A browser window opens for **OAuth** — sign into RankPrompt and approve. (If it asks for a key instead, create one at [app.rankprompt.com/developers?tab=keys](https://app.rankprompt.com/developers?tab=keys) and paste it.) Needs a Starter plan or higher.
5. Back in the app, make sure RankPrompt's tools are enabled for the chat via the **Search and tools** control by the message box.

No "developer mode" toggle is required. If the connector shows offline with no error, the cause is almost always that the server URL isn't publicly reachable from your machine (VPN/firewall) — `https://mcp.rankprompt.com/mcp` is public, so if it fails, retry the OAuth step.

> **Simpler alternative — Claude Code:** if the agency is even a little technical, the CLI is a genuinely smoother one-liner: `claude mcp add --transport http --scope user rankprompt https://mcp.rankprompt.com/mcp`, then `/mcp` → select `rankprompt` → Authenticate. See the main `README.md`.

**Old manual method (only if the UI lacks "Add custom connector"):** Settings → Developer → Edit Config, add to `claude_desktop_config.json`:
```json
{ "mcpServers": { "rankprompt": { "url": "https://mcp.rankprompt.com/mcp" } } }
```
then restart Claude Desktop.

## 2. Create a Project and load the brain

1. New Project → name it e.g. *"<Client> — AI Visibility."*
2. Add these files as Project knowledge (drag them in):
   - `CLAUDE.md` (paste its contents into the Project's **custom instructions** — this is the operating brief)
   - `knowledge/matrix.md`, `knowledge/brain.md`, `knowledge/reading-reports.md`
   - Any play file you'll use that session (`citable-content.md`, `outreach.md`, `reddit-social.md`, `llms-txt.md`, `technical-seo.md`, `measuring.md`)
3. Keep a `profile.md` per client (copy `templates/profile.template.md`) in the Project as the running memory.

## 3. Drive it

Start with *"Prime RankPrompt and list my brands,"* then *"Diagnose <brand> on the Matrix."* The skill files under `.claude/skills/` double as step-by-step recipes — paste a skill's steps in if you want the model to follow that exact flow.

## The board

`matrix-board/template.html` is a self-contained file — open it in a browser, replace the `DATA` block with the real values the copilot computed, and print to PDF. This works identically whether you drove the diagnosis from Code or Desktop.

## When to graduate to Claude Code

If an agency wants the skills to run automatically and the MCP write-actions (create/run/schedule reports) wired end-to-end, move them to the Claude Code setup in the main `README.md`. Same repo, fuller automation.
