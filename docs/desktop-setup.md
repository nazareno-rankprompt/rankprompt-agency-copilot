# Running the copilot in Claude Desktop

The workstation is built as a Claude Code repo, but the same brain runs in **Claude Desktop** for agencies that prefer the chat UI over a CLI. The difference: in Desktop the `.claude/skills/` don't auto-run as slash-skills, so you load the methodology as **Project knowledge** and drive it conversationally. The RankPrompt MCP and all reasoning work the same.

## 1. Connect the RankPrompt MCP

Edit your `claude_desktop_config.json` (Settings → Developer → Edit Config):

```json
{
  "mcpServers": {
    "rankprompt": {
      "url": "https://mcp.rankprompt.com/mcp"
    }
  }
}
```

Restart Claude Desktop. You'll be prompted to authenticate RankPrompt in the browser (OAuth). Needs a Starter plan or higher.

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
