# DESIGN.md Plugin Instructions

Use this plugin when working with DESIGN.md visual identity specifications.

- Treat YAML front matter tokens as the source of truth.
- Use Markdown prose for intent, tone, and application guidance.
- Preserve unknown sections unless the user asks for removal.
- Keep known `##` sections in canonical order.
- Validate with `npx @google/design.md lint DESIGN.md` when available.
- State clearly when CLI validation cannot be run.
