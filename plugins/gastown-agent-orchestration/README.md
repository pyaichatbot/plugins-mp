# Gas Town Agent Orchestration Plugin

Agent guidance for operating Gas Town multi-agent orchestration: towns, rigs, crew, polecats, convoys, Beads, mail, nudges, runtime providers, and merge queues.

This plugin packages high-signal guidance from `gastownhall/gastown` without vendoring the Go runtime.

## Included Skills

- `gastown-agent-orchestration` - Core Gas Town operating model and workflow guidance.
- `convoy` - Convoy system guide for batch work tracking and dispatch.
- `crew-commit` - Canonical Gas Town crew commit workflow.
- `pr-list` - Formatted GitHub PR listing workflow.
- `ghi-list` - Formatted GitHub issue listing workflow.
- `gitlab-org-integration` - Gas Town guidance for GitLab.com and self-managed GitLab org instances.
- `crew-commit-gitlab` - Gas Town commit, push, and GitLab merge request workflow.
- `mr-list` - Formatted GitLab merge request listing workflow.
- `gli-list` - Formatted GitLab issue listing workflow.
- `gas-town-cursor` - Cursor runtime preset guidance.

## Compatibility

- Codex: `.codex-plugin/plugin.json` and `skills/*/SKILL.md`
- Claude: `.claude-plugin/plugin.json` and `skills/*/SKILL.md`
- GitHub Copilot: `.github/instructions/gastown-agent-orchestration.instructions.md`
- GitLab org instances: supported through `glab`-based skills for merge requests, issues, and self-managed hosts

## Source

Upstream: https://github.com/gastownhall/gastown

License: MIT
