---
applyTo: "plugins/**"
---

Plugin packages must stay host-compatible:

- Codex metadata belongs in `.codex-plugin/plugin.json`.
- Claude metadata belongs in `.claude-plugin/plugin.json`.
- Skills belong under `skills/<skill-name>/SKILL.md`.
- Do not put Codex marketplace files inside a plugin package; Codex marketplace metadata belongs at repository root `.agents/plugins/marketplace.json`.
- Keep plugin names stable and kebab-case.
- Validate every edited JSON file before claiming completion.
