# Spytrix Plugins Marketplace

A marketplace repository for Spytrix AI plugins. Plugins in this repo should be compatible with Codex and Claude, and should include GitHub Copilot instruction support where Copilot has an equivalent mechanism.

## Layout

```text
.agents/plugins/marketplace.json      # Codex marketplace manifest
.claude-plugin/marketplace.json       # Claude marketplace manifest
.github/copilot-instructions.md       # GitHub Copilot repository instructions
.github/instructions/*.instructions.md# GitHub Copilot path-specific instructions
AGENTS.md                             # Agent instructions for tools that read AGENTS.md
plugins/<plugin-name>/                # Individual plugin packages
```

## Included Plugins

- `andrej-karpathy-skills` - Behavioral coding guidelines for simpler, more deliberate LLM-assisted code changes.
- `design-md` - Agent guidance for creating, validating, reviewing, and applying DESIGN.md visual identity specifications.
- `create-agent-tui` - Scaffold customizable TypeScript terminal UIs for OpenRouter agents.
- `text2sql-framework` - Guidance for Text-to-SQL agents that explore schemas, verify SQL, and improve with scenarios.
- `hyperbrowser-app-patterns` - Curated Hyperbrowser browser automation, scraping, crawl, research, and web-to-agent app patterns.


## Categories

- Coding: `andrej-karpathy-skills`, `create-agent-tui`
- Design: `design-md`
- Data: `text2sql-framework`
- Browser Automation: `hyperbrowser-app-patterns`

## Codex

Codex marketplace metadata lives at `.agents/plugins/marketplace.json`. Each plugin package must include `.codex-plugin/plugin.json` and any referenced skills under its own folder.

For local testing, register this repository root as marketplace source `spytrix-ai` and enable plugins by `<plugin>@spytrix-ai`.

## Claude

Claude marketplace metadata lives at `.claude-plugin/marketplace.json`. Each plugin package should include `.claude-plugin/plugin.json` and use paths relative to the plugin package.

Claude Code marketplace install target after publishing to GitHub:

```text
/plugin marketplace add pyaichatbot/spytrix-plugins-mp
/plugin install andrej-karpathy-skills@spytrix-ai
```

## GitHub Copilot

GitHub Copilot does not currently consume Claude/Codex plugin manifests as plugins. This repository provides Copilot-compatible guidance through:

- `.github/copilot-instructions.md` for repository-wide instructions.
- `.github/instructions/plugins.instructions.md` for plugin package files.
- `AGENTS.md` for agent instruction compatibility.

## Adding A Plugin

Each new plugin should include:

```text
plugins/<plugin-name>/.codex-plugin/plugin.json
plugins/<plugin-name>/.claude-plugin/plugin.json
plugins/<plugin-name>/skills/<skill-name>/SKILL.md
```

Then add matching entries to both marketplace manifests. If the plugin includes behavior that Copilot should follow, update `.github/copilot-instructions.md`, `.github/instructions/plugins.instructions.md`, or `AGENTS.md`.
