---
applyTo: "**/DESIGN.md,**/design.md"
---

When editing DESIGN.md files:

- Keep YAML front matter at the top of the file between `---` fences.
- Treat tokens as normative and prose as rationale.
- Use valid hex colors and valid CSS dimensions.
- Use token references like `{colors.primary}` for component values.
- Preserve unknown sections and avoid unrelated rewrites.
- Keep known `##` sections in this order: Overview, Colors, Typography, Layout, Elevation & Depth, Shapes, Components, Do's and Don'ts.
- Validate with `npx @google/design.md lint DESIGN.md` when tooling is available.
