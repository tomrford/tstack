---
name: reflect
description: Spawn three parallel review subagents over the active transcript, surface learnings, and route each to a concrete edit on an existing skill. Use when the user says reflect.
---

# Reflect

Mine the current conversation for durable learnings, then route them into skill edits.

Invoke when the user says "reflect" or "$reflect". Skip when the conversation is trivial, off-topic, or already covered by an existing skill the parent followed correctly. One-offs are not learnings.

## 1. Locate the active transcript

Use the current conversation as the primary record. For an identified earlier chat, use `read_thread` with pagination and `includeOutputs` when supported. Summaries and truncated outputs cannot prove every historical tool call. If raw evidence is unavailable, pass a labelled digest and flag the resulting gaps. Follow `../workflow/references/codex-agent-tools.md` and confine lookups to the requested project and topic.

## 2. Spawn three reviewers in parallel

Spawn three independent read-only reviewers with `collaboration.spawn_agent` and `fork_turns: "none"`. Use Astra high for judgement and divergent review, and Sol 6.1 high for tooling, per `../workflow/references/model-defaults.md`. Give each its lens and template: `references/judgment-reviewer.md`, `references/tooling-reviewer.md`, or `references/divergent-reviewer.md`. They may use available MCP tools for contextual reads, but must not edit files or external state.

Pass each template verbatim, substituting the scoped evidence path or labelled digest where marked. Reviewers return findings to the parent through collaboration results.

## 3. Synthesize

Spawn a fresh synthesizer using the judgement default. Pass `references/synthesizer.md` with the reviewers' complete results. It verifies citations with available read tools and returns Accepted / Rejected / Backlog without applying edits.

## 4. Structural enforcement check

Move any Accepted item that a lint rule, script, metadata flag, or runtime check would enforce more reliably to Backlog. See the **encode-lessons-in-structure** principle skill.

## 5. Apply

Present the synthesizer's full Accepted / Rejected / Backlog output and wait for explicit approval before applying any Accepted edit. The user picks the subset and may redirect routings. Skill changes affect every future agent in the org. Do not auto-apply.

Report Backlog items to the user. File them externally only when requested.

Follow each approved row's Routing exactly:

- Trivial existing-skill edit (a one-line bullet, a tightened sentence, a stale fact corrected): the parent does it directly.
- Substantive existing-skill edit (a new section, a new pattern table, more than ~10 lines): hand to Codex's `skill-creator` skill and run its draft / test / iterate loop.
- `tune description: <skill path>` (the skill exists but didn't trigger when it should have): hand to `skill-creator` and run its description-optimization loop.
- `new skill via skill-creator: <kebab-name>`: hand creation to `skill-creator`. Do not invent the shape ad hoc.

If your environment ships a SKILL.md validator, run it on every touched skill before declaring done.

## 6. Summarize for the user

Short list, no preamble:

- Edits applied: `<skill path>`. What changed, one line each.
- New skills created: `<skill path>`. One line each (rare).
- Backlog filed to the devex tracker: `<issue title>` (`<tags>`). One line each.
- Dropped: one line per rejected finding + reason from the synthesizer.
