# Karpathy Guidelines

Behavioral coding guidelines for LLM-assisted development, packaged for both Codex and Claude.

This plugin is maintained under the GitHub owner `pyaichatbot` and is inspired by Andrej Karpathy's observations on common LLM coding pitfalls: hidden assumptions, overcomplication, unrelated edits, and weak verification criteria.

## What It Adds

The included `karpathy-guidelines` skill asks coding agents to:

- Surface assumptions before coding.
- Prefer the simplest implementation that solves the request.
- Keep changes surgical and avoid unrelated refactors.
- Define verifiable success criteria and check the result.

## Codex Usage

This repository includes Codex plugin metadata:

```text
.codex-plugin/plugin.json
skills/karpathy-guidelines/SKILL.md
```

For this workspace, the plugin is also listed in:

```text
.agents/plugins/marketplace.json
```

Marketplace:

```text
name: spytrix-ai
displayName: Spytrix AI
```

## Claude Usage

This plugin package includes Claude plugin metadata, and the marketplace repository includes the root Claude marketplace manifest:

```text
plugins/andrej-karpathy-skills/.claude-plugin/plugin.json
.claude-plugin/marketplace.json
plugins/andrej-karpathy-skills/skills/karpathy-guidelines/SKILL.md
```

From Claude Code, add the marketplace from your GitHub repository:

```text
/plugin marketplace add pyaichatbot/spytrix-plugins-mp
```

Then install the plugin:

```text
/plugin install andrej-karpathy-skills@spytrix-ai
```

## Repository

Expected GitHub repository:

```text
https://github.com/pyaichatbot/spytrix-plugins-mp
```

## License

MIT
