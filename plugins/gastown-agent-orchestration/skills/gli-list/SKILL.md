---
name: gli-list
description: >
  List GitLab issues in a compact table for GitLab.com or self-managed GitLab org repositories. Use for issue triage and Gas Town task-mapping workflows.
allowed-tools: "Bash(glab issue list:*)"
version: "1.0.0"
author: "pyaichatbot"
---

# GLI List - Formatted GitLab Issues

Display GitLab issues in a compact terminal table.

## Usage

```text
/gli-list [options]
```

## Options

Pass supported options through to `glab issue list`.

Common options:

- `--state opened|closed|all` - Filter by state.
- `--assignee <user>` - Filter by assignee.
- `--author <user>` - Filter by author.
- `--label <label>` - Filter by label.
- `--milestone <name>` - Filter by milestone.
- `--search <text>` - Search issue titles/descriptions.
- `--hostname <host>` - Use a self-managed GitLab host when needed.

## Execution Steps

1. Run `glab issue list` with the requested filters.
2. Format results as a compact table with IID, assignee, labels, state, and title when available.
3. Prefer GitLab issue IID references (`#123`) in summaries.
4. When mapping GitLab issues into Beads, include the GitLab URL or IID in the Bead description.

## Example Commands

```bash
# Default open issues for the current GitLab repo
glab issue list --state opened

# Self-managed host
glab issue list --hostname gitlab.company.com --state opened

# Triage queue
glab issue list --state opened --label bug --assignee @me
```

## Output Guidance

Show these columns when available:

```text
IID   Assignee      Labels             State    Title
372   max           bug, backend       opened   fix auth timeout
371   -             docs               opened   update deployment notes
```

If the team uses Beads as the primary work ledger, do not create or mutate GitLab issues unless asked. Summarize and map them to Beads first.
