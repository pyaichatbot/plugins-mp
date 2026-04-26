# Spytrix Plugins Marketplace Claude Instructions

This repository is a marketplace for reusable AI coding-agent plugins maintained by `pyaichatbot`.

## Repository Purpose

Keep this repo organized as a multi-plugin marketplace. New plugins should be added under `plugins/<plugin-name>/` and registered in the root marketplace manifests.

## Compatibility Requirements

Every plugin should be compatible with Codex and Claude unless its README explicitly documents why one host is unsupported.

For each plugin package, maintain:

- `plugins/<plugin-name>/.codex-plugin/plugin.json` for Codex.
- `plugins/<plugin-name>/.claude-plugin/plugin.json` for Claude.
- `plugins/<plugin-name>/skills/<skill-name>/SKILL.md` for shared skill content.

For marketplace registration, maintain:

- `.agents/plugins/marketplace.json` for Codex.
- `.claude-plugin/marketplace.json` for Claude.

## GitHub Copilot

GitHub Copilot does not consume Claude or Codex plugin manifests directly. For Copilot compatibility, update repository instruction files instead:

- `.github/copilot-instructions.md`
- `.github/instructions/*.instructions.md`
- `AGENTS.md`

## Change Discipline

When editing this repo:

- Keep plugin names kebab-case and stable.
- Do not put Codex marketplace files inside individual plugin folders.
- Do not put Claude marketplace files inside individual plugin folders unless intentionally creating a standalone plugin repo.
- Validate every changed JSON manifest before finishing.
- Keep edits scoped to the requested plugin or marketplace metadata.

When working with DESIGN.md files, follow the `design-md` plugin guidance and validate with `npx @google/design.md lint DESIGN.md` when available.

When working with Text-to-SQL systems, follow the `text2sql-framework` plugin guidance and prefer read-only credentials plus verified SQL execution.

When scaffolding OpenRouter terminal agents, follow the `create-agent-tui` plugin guidance and verify TypeScript with `npx tsc --noEmit` when available.

When building Hyperbrowser web automation apps, follow the `hyperbrowser-app-patterns` plugin guidance and keep API keys server-side.
