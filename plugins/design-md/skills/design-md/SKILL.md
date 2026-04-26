---
name: design-md
description: Use when creating, editing, validating, reviewing, or applying DESIGN.md visual identity specifications with YAML design tokens and Markdown design rationale.
license: Apache-2.0
---

# DESIGN.md

Use this skill for DESIGN.md files: structured visual identity specifications that combine machine-readable YAML front matter with human-readable Markdown rationale.

## Core Format

A DESIGN.md file has two layers:

1. YAML front matter at the top of the file, delimited by `---` fences.
2. Markdown body with design rationale organized under `##` sections.

The token values are normative. The prose explains intent and usage.

## Required Agent Behavior

When creating or editing a DESIGN.md file:

- Define concrete tokens before writing broad design prose.
- Keep token names stable, semantic, and kebab-case where possible.
- Use valid hex colors, valid dimensions, and explicit typography objects.
- Use token references like `{colors.primary}` for component values.
- Preserve unknown sections unless the user asks to remove them.
- Keep `##` sections in canonical order when present.
- Validate with `npx @google/design.md lint DESIGN.md` when Node/npm access is available.

When applying a DESIGN.md to UI implementation:

- Treat YAML tokens as the source of truth.
- Use Markdown prose to resolve intent, hierarchy, and interaction tone.
- Do not invent unrelated colors, radii, or typography when tokens exist.
- If a needed token is missing, choose the smallest addition and document it.
- Check contrast for foreground/background component pairs.

## Canonical Section Order

Use this order for `##` sections when they are present:

1. Overview
2. Colors
3. Typography
4. Layout
5. Elevation & Depth
6. Shapes
7. Components
8. Do's and Don'ts

Accepted aliases are described in `references/spec.md`.

## Common CLI Commands

```bash
npx @google/design.md lint DESIGN.md
npx @google/design.md diff DESIGN.md DESIGN-v2.md
npx @google/design.md export --format tailwind DESIGN.md
npx @google/design.md export --format dtcg DESIGN.md
npx @google/design.md spec --rules
```

## Validation Checklist

Before claiming a DESIGN.md is ready:

- YAML front matter parses.
- Required `name` token exists.
- Color values are valid sRGB hex values.
- Token references resolve.
- Component foreground/background pairs have acceptable contrast.
- Markdown sections are not duplicated.
- Present sections follow canonical order.
- CLI lint passes, or unavailable tooling is stated clearly.

## References

- Full upstream specification: `references/spec.md`
- Upstream examples: `../../examples/upstream/`
- Upstream project: https://github.com/google-labs-code/design.md
