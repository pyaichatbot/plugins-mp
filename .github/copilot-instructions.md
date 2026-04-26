# Spytrix Plugins Marketplace Instructions

This repository stores reusable AI coding-agent plugins. Preserve compatibility across Codex and Claude whenever adding or editing plugins.

For each plugin package:

- Keep it under `plugins/<plugin-name>/`.
- Maintain `plugins/<plugin-name>/.codex-plugin/plugin.json` for Codex.
- Maintain `plugins/<plugin-name>/.claude-plugin/plugin.json` for Claude.
- Keep skill files under `plugins/<plugin-name>/skills/<skill-name>/SKILL.md`.
- Update `.agents/plugins/marketplace.json` for Codex marketplace discovery.
- Update `.claude-plugin/marketplace.json` for Claude marketplace discovery.
- Validate JSON manifests after edits.
- Avoid unrelated formatting or refactors.

GitHub Copilot does not use Claude or Codex plugin manifests directly. Treat this file, `.github/instructions/*.instructions.md`, and `AGENTS.md` as the Copilot-compatible instruction layer.

For DESIGN.md files, also follow `.github/instructions/design-md.instructions.md` and prefer the packaged `design-md` plugin guidance.

For Text-to-SQL work, also follow `.github/instructions/text2sql-framework.instructions.md` and prefer the packaged `text2sql-framework` plugin guidance.

For OpenRouter terminal agent TUI work, also follow `.github/instructions/create-agent-tui.instructions.md` and prefer the packaged `create-agent-tui` plugin guidance.

For Hyperbrowser browser automation apps, also follow `.github/instructions/hyperbrowser-app-patterns.instructions.md` and prefer the packaged `hyperbrowser-app-patterns` plugin guidance.

For Gas Town multi-agent orchestration work, also follow `.github/instructions/gastown-agent-orchestration.instructions.md` and prefer the packaged `gastown-agent-orchestration` plugin guidance. Use `glab` instead of `gh` when the rig remote is GitLab.com or a self-managed GitLab org instance.
