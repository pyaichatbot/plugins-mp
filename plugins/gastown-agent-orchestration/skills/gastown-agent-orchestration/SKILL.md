---
name: gastown-agent-orchestration
description: Use when installing, configuring, operating, debugging, or explaining Gas Town multi-agent orchestration with gt, Beads, towns, rigs, crew, polecats, convoys, mail, nudges, runtime providers, and merge queues.
license: MIT
---

# Gas Town Agent Orchestration

Use this skill for Gas Town, a multi-agent orchestration system for coordinating coding agents across projects with persistent work tracking.

## Core Mental Model

- **Town**: workspace root, usually `~/gt`.
- **Mayor**: primary AI coordinator for the town.
- **Rig**: project container wrapping a git repository.
- **Crew**: long-lived user-managed worker workspace.
- **Polecat**: supervised worker agent with persistent identity and ephemeral sessions.
- **Convoy**: tracked batch of work items.
- **Beads**: git-backed issue/work ledger, accessed with `bd`.
- **Witness / Deacon / Refinery**: monitoring, supervision, and merge queue roles.

## Common Setup

```bash
gt install ~/gt --git
cd ~/gt
gt rig add myproject https://github.com/you/repo.git
gt crew add yourname --rig myproject
gt mayor attach
```

Use `gt doctor`, `gt status`, and `gt config agent list` when diagnosing setup.

## Operating Workflow

For multi-agent work:

1. Start from the Mayor for coordination.
2. Create or identify Beads issues.
3. Group related work into a convoy.
4. Sling discrete work items to a rig or worker.
5. Monitor with `gt convoy list`, `gt agents`, and `gt feed`.
6. Use `gt mail` for persistent messages and `gt nudge` for immediate delivery.
7. Use `gt prime` after compaction, restart, or context loss.

Useful commands:

```bash
gt mayor attach
gt convoy create "Feature X" gt-abc12 gt-def34 --notify
gt sling gt-abc12 myproject
gt convoy list
gt agents
gt feed
gt prime
gt mail inbox
gt nudge mayor "Status update"
```

## Runtime Providers

Gas Town supports multiple runtime presets, including Claude, Codex, Cursor, OpenCode, Gemini, GitHub Copilot, and others.

For Codex rigs, ensure Codex can read role instructions. The upstream README recommends configuring Codex with a project doc fallback for `CLAUDE.md`.

For GitHub Copilot, Gas Town uses lifecycle hooks and requires a Copilot seat and suitable CLI/org policy.

For GitLab.com or self-managed GitLab org instances, keep Gas Town orchestration in `gt`/`bd` and use `glab` for GitLab issues, merge requests, pipelines, and host authentication.

## Agent Rules

- If assigned work is on the hook, execute it instead of waiting for confirmation.
- Use `gt nudge` to wake another active agent; terminal output is not inter-agent communication.
- Use `gt mail` for persistent messages that must survive session restarts.
- Use `bd` for task tracking in Gas Town-managed repos.
- Run `gt prime` after compaction or new sessions.
- Avoid raw tmux text injection unless upstream docs explicitly require it.

## When To Use Included Skills

- `convoy`: convoy creation, staged launch, dispatch, stranded work, and feeding behavior.
- `crew-commit`: Gas Town crew commit, branch, push, and PR workflow.
- `pr-list` and `ghi-list`: formatted GitHub PR/issue listing workflows.
- `gitlab-org-integration`: GitLab.com and self-managed GitLab org setup and operating rules.
- `crew-commit-gitlab`: Gas Town commit, branch, push, and GitLab MR workflow.
- `mr-list` and `gli-list`: formatted GitLab merge request/issue listing workflows.
- `gas-town-cursor`: Cursor runtime preset details.

## References

- Overview: `references/overview.md`
- Install guide: `references/installing.md`
- Technical reference: `references/reference.md`
- Agent provider integration: `references/agent-provider-integration.md`
- GitLab org integration: `references/gitlab-org-integration.md`
- Upstream README: `../../references-upstream-README.md`
- Upstream repository: https://github.com/gastownhall/gastown
