# tstack

Tom's personal skills for testing and maintaining software projects.

- [test-authoring](./skills/test-authoring/SKILL.md): write meaningful tests through consumer interfaces.
- [feature-grounding](./skills/feature-grounding/SKILL.md): assess whether a proposed change fits the project.
- [reality-check](./skills/reality-check/SKILL.md): assess practical risk and whether a proposed response is proportional.
- [ping-pong](./skills/ping-pong/SKILL.md): agree on a concrete target before implementation.
- [work-summary](./skills/work-summary/SKILL.md): brief a reader on a change or stretch of work.
- [pr-authoring](./skills/pr-authoring/SKILL.md): write a PR title and description from a work summary.
- [lgtm](./skills/lgtm/SKILL.md): review, verify, and merge an accepted change.
- [nightly-review](./skills/nightly-review/SKILL.md): review the day's merged changes and prepare focused fixes for review.
- [how](./skills/how/SKILL.md): explain architecture, runtime flow, and ownership.
- [why](./skills/why/SKILL.md): investigate design rationale and whether its constraints still apply.
- [blast-radius](./skills/blast-radius/SKILL.md): assess consequences beyond the diff and substantiate safety assumptions.
- [create-verification-skill](./skills/create-verification-skill/SKILL.md): build a project-specific verification skill and feature map.
- [maintain-verification-skill](./skills/maintain-verification-skill/SKILL.md): keep that verification skill aligned with the real app.

## Install and update

### Claude Code

```
/plugin marketplace add tomrford/tstack
/plugin install tstack@tstack
```

Run `/plugin marketplace update tstack` to pick up pushed changes.

### Codex

Ask **@Plugin Creator** to import `tomrford/tstack` from GitHub as a private plugin in your account. Open the returned plugin link and select **Install/+**.

Start a new chat and select **@tstack** to use the skills. GitHub is the source of truth; the account plugin contains a snapshot of `main`.

After pushing changes, ask **@Plugin Creator** to sync the existing tstack plugin from `tomrford/tstack`. Start a new chat after updating to load the latest skills.

### Releases

Bump `version` in both [plugin.json](./plugin.json) and [.claude-plugin/plugin.json](./.claude-plugin/plugin.json) together.

The verification skills and condensed how, why, and blast-radius skills come from Lauren Tan's PStack. See [provenance](./provenance/pstack/README.md) and its [MIT licence](./provenance/pstack/LICENSE). The personal skills use the [project MIT licence](./LICENSE).
