---
applyTo: "**/*gastown*,**/.beads/**,**/CLAUDE.md,**/AGENTS.md"
---

When working with Gas Town workflows:

- Treat `gt` as the orchestration CLI and `bd` as the issue/work ledger.
- Use `gt prime` after compaction, restart, or context loss.
- Use `gt mail` for persistent inter-agent messages and `gt nudge` for immediate delivery.
- Prefer convoys for batched work tracking.
- Keep runtime-provider guidance explicit for Claude, Codex, Cursor, OpenCode, Gemini, and GitHub Copilot.
- For GitLab repos, use `glab` for issues, merge requests, pipelines, and self-managed host authentication; do not use `gh` commands at GitLab boundaries.
- Do not vendor the full Gas Town Go runtime into marketplace plugins; package focused guidance and references.
