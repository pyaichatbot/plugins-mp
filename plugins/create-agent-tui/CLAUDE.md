# Create Agent TUI Plugin Instructions

Use this plugin when scaffolding or modifying a TypeScript terminal UI for an OpenRouter agent.

- Use `@openrouter/agent` for the model/tool loop instead of hand-rolling it.
- Present the tool, module, slash command, input style, tool display, and loader choices before generation.
- Generate strict TypeScript and verify with `npx tsc --noEmit` when dependencies are available.
- Require `OPENROUTER_API_KEY` through environment/config, not hardcoded secrets.
