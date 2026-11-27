# Working on tarkle-mcp-server

The same rule as the main Tarkle repository: one branch for everyone, people, coding agents and bots alike.

## One branch: `develop` (owner, 2026-11-24)

- Every change goes to **`develop`**. Never create another branch and never open another pull request.
- How to push: `git fetch origin`, start from `origin/develop`, commit, then `git push origin HEAD:develop`. Never force-push. If the push is refused because someone pushed first, fetch, rebase and push again.
- `develop` reaches `main` through one open pull request (`develop` into `main`). Only the owner merges it.
- Merge that pull request with **"Create a merge commit"**, never squash or rebase. Listings pin exact commits of this repository (the Hermes Agent catalog pins a commit SHA), and a squash or rebase would drop those commits from `main`.
- After a merge, keep working on `develop`. The owner opens the next `develop` into `main` pull request when there is something new.

## What lives here

Listing files for directories and agent marketplaces: `.claude-plugin/` and `.mcp.json` (Claude Code and Cowork plugin, Anthropic's plugin directory), `gemini-extension.json` and `GEMINI.md` (Gemini CLI), `plugin.json` and `mcp.json` (Hermes Agent, and the ChatGPT and Codex plugin directory through `extensions.com.openai`), `after-install.md` (Hermes Agent), `skills/tarkle/SKILL.md` and `skills/tarkle-get-started/SKILL.md` (skills.sh, Hermes, Claude and ChatGPT), `openclaw.plugin.json`, `package.json` and `assets/icon.png` (OpenClaw, published on ClawHub as `@tarklehq/tarkle`), `server.json` (official MCP Registry), `lhm.plugin.json` (LobeHub), and the logos in `assets/`. The MCP server itself is hosted at `https://mcp.tarkle.tech/mcp`; its code is not in this repository.

## Copy

- Lead with what people do: upload, manage and share business files, and request documents. Tagline: "Upload, manage and share your business files".
- Never claim a feature the server does not have. Check tool names and inputs against the live tool list before writing them.
- Mark Pro-only tools as Pro (for example restoring an earlier version).
- Never put secrets, tokens or access codes in this repository.
