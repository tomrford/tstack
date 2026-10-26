# pstack provenance

Imported on 10 October 2026 in commit `9fef6d15c69ff1269532b0c4704bf47b3b9eed32` from [Cursor's pstack](https://github.com/cursor/plugins/tree/ccb5507cec1546dc88135c1139c811e6c59115ba/pstack), revision `ccb5507cec1546dc88135c1139c811e6c59115ba`.

## Imported material

- [create-verification-skill](../../skills/create-verification-skill/SKILL.md)
- [maintain-verification-skill](../../skills/maintain-verification-skill/SKILL.md)
- The creation skill's [references/feature-map-example/](../../skills/create-verification-skill/references/feature-map-example/) directory, including `README.md`, `create-note.md` and `search.md`.

The adaptations replace `.cursor/skills/` with `.agents/skills/` and use Codex's `$skill-name` invocation syntax. Explicit-only invocation is preserved through `agents/openai.yaml`. The reference files are unchanged. These skills require no other pstack skills or principles. The reference commands describe an illustrative Notes app, not tools to install.

## Condensed investigation skills

- [how](../../skills/how/SKILL.md)
- [why](../../skills/why/SKILL.md)
- [blast-radius](../../skills/blast-radius/SKILL.md)

Adapted from the PStack skills and supporting prompts retained in tstack at revision `9ca1aed20d6cffea67420ffce1992db8fc9f5830`, originally based on [PStack revision `11713c6`](https://github.com/cursor/plugins/tree/11713c683fe4add4fd403ea880580abbc9e0875f/pstack).

These versions retain the original invocation cues and core investigation goals while condensing the guidance into self-contained skills. They replace prescribed fan-out, model choices, prompt templates, and cross-skill dependencies with proportionate investigation and independent assessment where useful.

## Licence

The imported material is copyright 2026 Lauren Tan and retains its [upstream MIT notice](LICENSE).
