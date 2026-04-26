---
name: crew-commit-gitlab
description: >
  Use when a Gas Town crew member is ready to commit, push, and open a GitLab merge request from a GitLab.com or self-managed GitLab org repository.
allowed-tools: "Bash(git *), Bash(gt *), Bash(glab *)"
version: "1.0.0"
author: "pyaichatbot"
---

# Crew Commit - GitLab Merge Request Workflow

Use this workflow for Gas Town work in GitLab-backed rigs. It mirrors the standard crew commit flow, but creates GitLab merge requests with `glab`.

## Preconditions

Verify the repository and GitLab auth before staging or pushing.

```bash
git remote -v
glab auth status
# For self-managed GitLab:
glab auth status --hostname gitlab.company.com
```

If the repo uses a non-`main` default branch, use that branch consistently in fetch, rebase, and MR target commands.

## Step 1: Sync

```bash
git fetch origin
git status
git branch --show-current
```

If you are behind the target branch, rebase before continuing:

```bash
git rebase origin/main
```

## Step 2: Create Or Confirm Feature Branch

Never commit directly on a protected branch.

```bash
git checkout -b feat/short-description
# or
git checkout -b crew/<name>/short-description
```

Common branch prefixes: `feat/`, `fix/`, `refactor/`, `docs/`, `test/`, `chore/`, `crew/<name>/`.

## Step 3: Check Submodules And Secrets

```bash
cat .gitmodules 2>/dev/null || echo "(no submodules)"
git submodule status 2>/dev/null
git diff
git status
```

Do not stage `.env` files, credentials, generated secrets, or accidental submodule pointer changes.

## Step 4: Stage Intentionally

```bash
git add path/to/file path/to/test
# or review hunks interactively
git add -p
```

## Step 5: Commit With Gas Town Identity

Use `gt commit` so Gas Town applies the correct agent identity.

```bash
gt commit -m "fix: concise description"
```

For non-obvious work, include a body with context, test evidence, and the Bead ID.

## Step 6: Push Branch

```bash
git push -u origin HEAD
```

## Step 7: Create GitLab Merge Request

```bash
glab mr create   --title "fix: concise description"   --description "$(cat <<'EOF'
## Summary

- <what changed and why>

## Test plan

- [ ] <command or manual check>

## Gas Town

Bead: <gt-abc12 or n/a>
Agent: <claude|codex|other>
EOF
)"   --target-branch main
```

For self-managed GitLab, add `--hostname gitlab.company.com` when the current remote does not resolve the host automatically.

If the project supports `--fill`, use it only after confirming the generated title and description include review context.

## Step 8: Check Pipeline And Notify

```bash
glab mr view
glab mr checks
```

If the MR is high-priority or blocks a convoy, notify through Gas Town:

```bash
gt mail send mayor "GitLab MR ready for <bead-id>: !<iid>"
```

## Completion Checklist

- [ ] Synced with the target branch.
- [ ] On a feature branch, not a protected branch.
- [ ] Staged only intentional files.
- [ ] Used `gt commit`.
- [ ] Pushed the branch to GitLab.
- [ ] Created MR with `glab mr create`.
- [ ] Included Bead ID or context in the MR description.
- [ ] Checked pipeline status or documented why it is unavailable.

## Anti-Patterns

| Do not | Do instead |
|--------|------------|
| `git push origin main` | Push a feature branch and open an MR |
| `gh pr create` in GitLab repos | Use `glab mr create` |
| Ignore protected branch rules | Target the configured default branch |
| Hide Bead context | Add Bead ID and agent context to the MR |
| Assume GitLab.com | Verify `glab auth status --hostname <host>` for org instances |
