---
name: mr-list
description: >
  List GitLab merge requests in a compact table for GitLab.com or self-managed GitLab org repositories. Use for Gas Town review, sheriff, and merge queue workflows.
allowed-tools: "Bash(glab mr list:*)"
version: "1.0.0"
author: "pyaichatbot"
---

# MR List - Formatted GitLab Merge Requests

Display GitLab merge requests in a compact terminal table.

## Usage

```text
/mr-list [options]
```

## Options

Pass supported options through to `glab mr list`.

Common options:

- `--state opened|closed|merged|all` - Filter by state.
- `--author <user>` - Filter by author.
- `--assignee <user>` - Filter by assignee.
- `--label <label>` - Filter by label.
- `--milestone <name>` - Filter by milestone.
- `--target-branch <branch>` - Filter by target branch.
- `--source-branch <branch>` - Filter by source branch.
- `--hostname <host>` - Use a self-managed GitLab host when needed.

## Execution Steps

1. Run `glab mr list` with the requested filters.
2. Include enough fields to show IID, author, title, source branch, target branch, and state when `glab` output supports formatting.
3. Format results as a compact table suitable for terminal review.
4. If the repo is on a self-managed instance, verify `glab auth status --hostname <host>` before retrying.

## Example Commands

```bash
# Default open MRs for the current GitLab repo
glab mr list --state opened

# Self-managed host
glab mr list --hostname gitlab.company.com --state opened

# Filter review queue
glab mr list --state opened --target-branch main --label ready-for-review
```

## Output Guidance

Show these columns when available:

```text
IID   Author        Source -> Target        State    Title
123   alice         feat/a -> main          opened   feat: add auth retry
122   bot-user      fix/b -> release/1.2    opened   fix: patch release flow
```

Prefer GitLab IID references (`!123`) in follow-up messages.
