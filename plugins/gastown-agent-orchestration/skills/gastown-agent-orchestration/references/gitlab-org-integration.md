# GitLab Org Integration

Gas Town can coordinate work against GitLab repositories because its core orchestration is local and git-based. GitLab-specific behavior lives at the source-control boundary: authentication, issue listing, merge request creation, approvals, and pipelines.

## Supported Shape

- GitLab.com repositories.
- Self-managed GitLab instances with SSH or HTTPS remotes.
- `glab`-based issue, merge request, and pipeline operations.
- Claude, Codex, and other Gastown-managed workers operating on branches.

## Required Local Tools

```bash
git --version
glab --version
gt --help
bd --help
```

Authenticate with the right host:

```bash
glab auth login
# or
glab auth login --hostname gitlab.company.com
```

## Recommended Agent Pattern

Use one Mayor/coordinator and multiple worker agents. Keep task state in Beads unless the team explicitly wants GitLab issues as the canonical backlog.

```bash
gt rig add app git@gitlab.company.com:group/app.git
gt mayor attach
gt convoy create "MR cleanup" gt-abc12 gt-def34 --notify
gt sling gt-abc12 app --agent codex
gt sling gt-def34 app --agent claude
```

## GitLab Boundary Commands

```bash
glab issue list --state opened
glab issue view <iid>
glab mr list --state opened
glab mr create --target-branch main
glab mr checks <iid>
glab pipeline list
```

## Self-Managed Instance Notes

- Prefer SSH remotes when possible: `git@gitlab.company.com:group/project.git`.
- Use `--hostname gitlab.company.com` when `glab` cannot infer the host.
- Ensure tokens have the minimum scopes needed for project, issue, MR, and pipeline reads/writes.
- Respect project-level protected branch, approval, CODEOWNERS, and CI rules.

## Current Limitations

This plugin adds operational guidance and skills; it does not modify the upstream `gt` Go runtime. If an upstream Gastown command assumes GitHub-specific APIs, use the GitLab companion skills and `glab` commands at that boundary.
