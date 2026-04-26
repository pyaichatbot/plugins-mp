# Spytrix Plugins Marketplace Agent Instructions

This repository contains reusable coding-agent plugins. Keep every plugin compatible with Codex and Claude unless a plugin explicitly documents why one host is unsupported.

When adding or changing a plugin:

- Keep the plugin package under `plugins/<plugin-name>/`.
- Include `.codex-plugin/plugin.json` for Codex.
- Include `.claude-plugin/plugin.json` for Claude.
- Keep Codex marketplace entries in `.agents/plugins/marketplace.json`.
- Keep Claude marketplace entries in `.claude-plugin/marketplace.json`.
- Prefer simple, surgical changes and verify JSON manifests parse before finishing.
- For GitHub Copilot compatibility, update repository instructions instead of inventing plugin manifests Copilot does not consume.

When working with DESIGN.md files, follow the `design-md` plugin guidance and validate with `npx @google/design.md lint DESIGN.md` when available.

When working with Text-to-SQL systems, follow the `text2sql-framework` plugin guidance and prefer read-only credentials plus verified SQL execution.

When scaffolding OpenRouter terminal agents, follow the `create-agent-tui` plugin guidance and verify TypeScript with `npx tsc --noEmit` when available.

When building Hyperbrowser web automation apps, follow the `hyperbrowser-app-patterns` plugin guidance and keep API keys server-side.
