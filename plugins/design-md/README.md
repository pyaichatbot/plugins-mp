# DESIGN.md Plugin

Agent guidance for creating, validating, reviewing, and applying DESIGN.md visual identity specifications.

This plugin packages guidance from `google-labs-code/design.md` for use in the Spytrix AI marketplace. It includes a primary `design-md` skill, the upstream DESIGN.md spec as reference material, upstream examples, and the upstream agent skills shipped by the source repository.

## Included Skills

- `design-md` - Create, validate, review, and apply DESIGN.md files.
- `agent-dx-cli-scale` - Evaluate CLIs for agent-first design.
- `ink` - Guidance for `@json-render/ink` terminal UIs.
- `tdd-red-green-refactor` - TypeScript red-green-refactor workflow.
- `typed-service-contracts` - Type-safe service contract architecture.

## Codex

Codex metadata is in:

```text
.codex-plugin/plugin.json
skills/*/SKILL.md
```

The marketplace entry is at repository root:

```text
.agents/plugins/marketplace.json
```

## Claude

Claude metadata is in:

```text
.claude-plugin/plugin.json
```

The marketplace entry is at repository root:

```text
.claude-plugin/marketplace.json
```

## GitHub Copilot

GitHub Copilot does not consume Claude or Codex plugin manifests directly. Copilot support is provided through repository instructions:

```text
.github/copilot-instructions.md
.github/instructions/design-md.instructions.md
.github/instructions/plugins.instructions.md
AGENTS.md
CLAUDE.md
```

## Source

Upstream: https://github.com/google-labs-code/design.md

License: Apache-2.0
