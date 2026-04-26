---
name: gitlab-org-integration
description: >
  Use when operating Gas Town against GitLab.com or self-managed GitLab org instances, including glab authentication, GitLab remotes, merge requests, issues, and CI-aware review workflows.
allowed-tools: "Bash(gt *), Bash(bd *), Bash(git *), Bash(glab *)"
version: "1.0.0"
author: "pyaichatbot"
---

# GitLab Org Integration for Gas Town

Use this skill when a Gas Town rig points at GitLab instead of GitHub. Keep Gas Town as the local orchestration layer and GitLab as the source-control, issue, merge request, and CI host.

## Compatibility Model

- Gas Town orchestration stays provider-neutral: `gt`, `bd`, tmux sessions, convoys, mail, nudges, rigs, and workers.
- GitLab handles remotes, protected branches, merge requests, approvals, and pipelines.
- Prefer Beads for internal multi-agent task state unless the team has asked to mirror GitLab issues.
- Use `glab` for GitLab operations; use `gh` only for GitHub repositories.

## Setup

Install and authenticate `glab` before asking agents to create issues or merge requests.

```bash
# GitLab.com
glab auth login

# Self-managed GitLab
glab auth login --hostname gitlab.company.com
```

For CI or non-interactive shells, prefer scoped tokens and explicit host config:

```bash
export GITLAB_HOST=gitlab.company.com
export GITLAB_TOKEN="<token>"
glab auth status --hostname gitlab.company.com
```

## Add A GitLab Rig

Use SSH or HTTPS GitLab URLs the same way as any git remote.

```bash
gt rig add myrepo git@gitlab.company.com:group/subgroup/myrepo.git
# or
gt rig add myrepo https://gitlab.company.com/group/subgroup/myrepo.git
```

After adding the rig, verify default branch detection and access:

```bash
cd ~/gt/myrepo/mayor/rig
git remote -v
git fetch origin
git branch -r
glab repo view
```

If the default branch is not `main`, set or confirm the rig's `default_branch` so Refinery and workers target the right merge base.

## Worker Flow

1. Start from the Mayor/coordinator.
2. Track work in Beads or accepted GitLab issues.
3. Use convoys for parallel batches.
4. Dispatch workers to feature branches.
5. Push branches to GitLab.
6. Create merge requests with `glab mr create`.
7. Use GitLab pipelines and approvals as the review gate.

```bash
gt mayor attach
gt convoy create "GitLab hardening" gt-abc12 gt-def34 --notify
gt sling gt-abc12 myrepo --agent codex
gt sling gt-def34 myrepo --agent claude
```

## GitLab-Specific Rules

- Never push directly to protected branches such as `main`, `master`, `develop`, or release branches.
- Check `glab auth status` and `git remote -v` before creating issues or MRs.
- Use `glab mr create` for GitLab merge requests, not `gh pr create`.
- Use `glab issue list` for GitLab issues, not `gh issue list`.
- Include the Bead ID in MR descriptions when work came from Gas Town.
- Respect GitLab approval rules, CODEOWNERS, protected branches, and required pipelines.

## Common Commands

```bash
# Issues
glab issue list --state opened
glab issue view <iid>

# Merge requests
glab mr list --state opened
glab mr create --fill --target-branch main
glab mr view <iid>
glab mr checks <iid>

# CI
glab pipeline list
glab pipeline ci view
```

## Troubleshooting

- Authentication failures: run `glab auth status --hostname <host>` and verify token scopes.
- Wrong host: confirm `git remote -v` and `GITLAB_HOST` match the self-managed instance.
- MR targets wrong branch: pass `--target-branch <branch>` explicitly.
- CI not visible: ensure the token can read pipelines and the project is selected by the current git remote.
