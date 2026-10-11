---
name: help
description: Guides users through tstack setup, $workflow, and picking the skill, playbook, or principle for a task. Type $help with a question.
---

# tstack help

Answer the user's question about tstack, hand them a prompt they can send, and link the file the answer came from. For a help question, don't start the work. The user asked how, and a tstack run spends real tokens, so let them send the prompt.

A message that asks for work, such as "use tstack to fix this bug", is not a help question. Read [`workflow`](../workflow/SKILL.md), do the work under it, and route the task through it.

This file maps questions to the skills that hold the answers. Read the relevant file before quoting it. Use available workspace or published plugin links; do not invent a public URL for unpushed files.

## Find out what they need

Infer the need from the message and the conversation. A named situation, such as "which skill reviews a PR?", goes straight to its section. If the need is still unclear, ask one multiple-choice question with these options, then answer only the section they pick:

- Get set up
- Start a task with `$workflow`
- Pick a skill for a situation
- Fix a run that went wrong
- Make tstack my own

Use the README for the entry point and [`references/recipes.md`](references/recipes.md) for examples. Model defaults live in `../workflow/references/model-defaults.md`; there is no model setup command. Mention `@tstack` with a goal, or invoke `workflow` directly. A plugin mention selects available capabilities for this task, not a persistent Custom Mode. Before delegates or schedules, read `../workflow/references/codex-agent-tools.md`.

## Pick a skill

The default answer is `$workflow`, which runs most of the others when its steps need them. Name a skill directly when the user wants more or less of something than the playbook gives. Read the skill before you recommend it, and give one example prompt.

| The user wants to | Skill |
|---|---|
| Do any non-trivial task with rigor | [`$workflow`](../workflow/SKILL.md) |
| Know how code works now, or where new code should live | [`$how`](../how/SKILL.md) |
| Know why code is shaped this way, or where a number came from | [`$why`](../why/SKILL.md) |
| Understand a change or subsystem, explained plainly | [`$teach`](../teach/SKILL.md) |
| Catch up on their own recent work on a topic | [`$recall`](../recall/SKILL.md) |
| Catch up on everything in this chat since their last message, with enough context to decide each action item | [`$ketchup`](../ketchup/SKILL.md) |
| Know what a small diff could break outside itself | [`$blast-radius`](../blast-radius/SKILL.md) |
| Settle types and module shape before code that crosses a function boundary | [`$architect`](../architect/SKILL.md) |
| Get several attempts at one brief, merged into the best one | [`$arena`](../arena/SKILL.md) |
| Run parallel checks over slices, or race workers, as isolated subagents | [`$swarm`](../swarm/SKILL.md) |
| Have independent reviewers review a diff and try to break it | [`$interrogate`](../interrogate/SKILL.md) |
| Fix a bug test-first when a cheap local test exists | [`$tdd`](../tdd/SKILL.md) |
| Apply TypeScript rules to `.ts` or `.tsx` work | [`$typescript-best-practices`](../typescript-best-practices/SKILL.md) |
| Strip comments before review, using a reviewer that didn't write them | [`$no-comments`](../no-comments/SKILL.md) |
| Clean AI tells out of prose | [`$unslop`](../unslop/SKILL.md) |
| Write docs, an RFC, a README, a PR description, or a commit message to a standard | [`$technical-writing`](../technical-writing/SKILL.md) |
| Hear the last reply again in plain words | [`$bro`](../bro/SKILL.md) |
| Give agents a scripted way to drive the app and prove behavior | [`$create-verification-skill`](../create-verification-skill/SKILL.md) |
| Bring a verification skill and its feature map back in line with the app | [`$maintain-verification-skill`](../maintain-verification-skill/SKILL.md) |
| Vet a performance number before reporting or acting on it | [`$benchmark-checklist`](../benchmark-checklist/SKILL.md) |
| Run a large or cross-cutting change, or one to review after stepping away | [`$figure-it-out`](../figure-it-out/SKILL.md) |
| Keep a decision log during a run, and review it afterward | [`$show-me-your-work`](../show-me-your-work/SKILL.md) |
| Turn their own working habits into a personal mode skill | [`$automate-me`](../automate-me/SKILL.md) |
| Turn what a finished task taught into skill edits | [`$reflect`](../reflect/SKILL.md) |
| Stop agents from repeating the same mistakes in this repo | [`$correct`](../correct/SKILL.md) |
| Find their way around tstack | `$help` |

If a skill directory next to this one is missing from the table, read its frontmatter and route by its description. The `principle-*` directories are covered under principles below.

Close calls:

- `$how` explains what the code does. `$why` explains the reasons. `$teach` runs one or both and explains the result plainly.
- `$arena` gives every worker the same brief and merges the best parts. `$swarm` splits work into slices or a race and returns one report.
- `$architect` implements right after it settles the design. Add "with checkpoint" to review the design before it writes code.
- `$interrogate` reviews the diff. `$blast-radius` looks for breakage outside the diff and proves the one fact that makes the change safe.
- `$recall` rebuilds context across recent chats. `$ketchup` covers only this chat since the user's last message. Resuming one specific chat or branch is the Session pickup playbook.
- `$figure-it-out` designs one rigorous run. The Orchestrate playbook runs a program that spans days and many PRs. The Autonomous run playbook drives one task to a finish condition.

Codex's `skill-creator` authors skills. Orchestrate is a workflow playbook, not a separate skill. Goals and heartbeat automations are documented in the agent-tools reference.

## Playbooks and principles

Playbooks are step lists inside `$workflow`, not skills, so they have no slash command. Inside `$workflow`, describing the task picks one, and these phrases name one directly:

- "babysit this pr" or "check on pr 123" runs Babysit. It drives the PR to merge-ready and stops there. It doesn't merge unless the user asks to merge, land, or ship.
- "land the stack" runs Shipping.
- "take over this branch" runs Session pickup.
- "pause safely" runs Pause safely.
- "full autopilot on this queue" runs Autopilot-full. "stack them, don't ship" runs Autopilot-stack.
- "run the eval playbook" runs Eval.

Name the workflow when you want this plugin's babysit procedure. The Playbooks section of [`workflow`](../workflow/SKILL.md) lists every playbook and when it applies. For PR delivery, read [Opening a PR](../workflow/playbooks/opening-a-pr.md), [Babysit](../workflow/playbooks/babysit.md), or [Shipping](../workflow/playbooks/shipping.md).

tstack uses Codex's plan mode when requested. For work that spans phases or stacked PRs, asking the workflow for a plan runs the [Multi-phase plan playbook](../workflow/playbooks/multi-phase-plan.md), which writes the plan and doesn't implement it. For a design question, the Prototype playbook or Architect settles it in code first.

Principles are one-rule skills that `$workflow` reads and cites in its replies. The user rarely invokes one. They steer with the names instead, as in "apply prove it works. show me the real output." The Principles section of [`workflow`](../workflow/SKILL.md) indexes them; an explicit `$principle-<name>` selects one directly.

## Fix a run that went wrong

| Symptom | Fix |
|---|---|
| The workflow stopped guiding a new task | Mention `@tstack` with the new goal or invoke `workflow` explicitly. Plugin selection is not a persistent custom mode. |
| A question got treated as the next step of the last task | Say "new task", or say the turn doesn't need the mode. |
| Runs cost more than expected | Reduce the number of delegates and review attempts where coverage permits it. Keep model choices explicit. |
| Parallel agents overwrote each other | Assign every writer a separate worktree. A subagent does not provide checkout isolation. |
| An overnight run moved but finished nothing | A goal needs a check that can pass or fail, not a duration. A heartbeat schedules a later check. See [Codex agent tools](../workflow/references/codex-agent-tools.md). |
| The reply claims success from a green build | Ask for the real command, flow, stored value, or profile. That's the prove-it-works principle. |

For a run that drifts, [`references/prompting.md`](references/prompting.md) has one-line steers and [`references/recipes.md`](references/recipes.md) has example prompts.

## Make tstack my own

- [`$automate-me`](../automate-me/SKILL.md) drafts a personal mode skill from the user's own history, to use alongside `$workflow`.
- [`$reflect`](../reflect/SKILL.md) after a session turns its lessons into skill edits the user approves.
- `$workflow write a skill for <workflow>` runs the authoring playbook. The eval playbook tests a skill change blind.
- Fix a misbehaving skill in its own PR, not inside the feature work where it went wrong.

## Reply

Lead with the answer. Give at most one example prompt in a code block, adapted from [`references/recipes.md`](references/recipes.md) when one fits, then the link to that file. Keep it short unless the user asked for the whole map.
