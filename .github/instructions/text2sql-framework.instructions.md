---
applyTo: "**/*text2sql*,**/scenarios.md,**/traces.jsonl"
---

When working on Text-to-SQL systems:

- Prefer read-only database credentials.
- Require generated SQL to be executed before calling it verified.
- Use `scenarios.md` for business rules, ambiguous terms, and corrective examples.
- Keep scenario entries under `##` headings and retrieve only relevant examples.
- Log traces for schema exploration, attempted SQL, errors, and final answers.
- Enforce row limits and avoid exposing sensitive data unnecessarily.
