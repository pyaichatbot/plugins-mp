---
applyTo: "**/*agent*tui*,**/src/cli.ts,**/src/agent.ts,**/src/tools/**"
---

When scaffolding OpenRouter agent TUIs:

- Use `@openrouter/agent` for model calls, tool execution, streaming, and stop conditions.
- Keep tool implementations in `src/tools/` with Zod schemas.
- Do not hardcode `OPENROUTER_API_KEY`; load it from environment/config.
- Support explicit choices for input style, tool display, loader, slash commands, and harness modules.
- Verify generated TypeScript with `npx tsc --noEmit` when dependencies are available.
