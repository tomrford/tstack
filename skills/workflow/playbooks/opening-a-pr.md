### Opening a PR

Invoked at the end of every other playbook.

**Worktree.** Assign each writer its own worktree through the Codex worktree tools. Pass its returned path in the brief; subagents share this workspace and do not receive isolation automatically. Preserve unrelated edits. Do not hard-reset or clean a checkout to switch tasks.

**Commits.** Follow the user's commit and delivery instructions. Use scoped commit messages. Do not amend unless asked. Keep changes as small ordered units whose evidence is reviewable.

**PRs.** Run the bundled `$deslop` skill over the diff before commit and `$no-comments` before review. Write every PR title, description, and commit body with `$technical-writing` (every layer except Diátaxis, and apply the STE vocabulary rules: one word per action, keep articles, a plain verb over `-ing` where one works), then apply `$unslop`.

**Titles.** Use a short scoped title that names the change, such as `Workflow: verify review completion at the current head`.

**Descriptions.** The PR body is a one-minute briefing, not a lab notebook, for a reviewer who has the diff. It says why the change exists, what it leaves out, what it could break, and how you proved it works. Write short, simple sentences with few identifiers, no walls of text. The body becomes the squash commit body, so keep that commit under about 40 lines. Use `##` headings, not bold lead-ins, in this order, and drop a section with nothing to say:

- `## Why`: the problem and approach, 1–3 short sentences. No SHAs, rebase genealogy, or "based on main" preamble.
- `## What changed`: 1–3 short bullets. Name a real symbol or path only when it carries the change. Name both sides of a rename or retarget.
- `## Scope`: always. 1–3 short items on what it covers and what it deliberately leaves out (a follow-up, a known gap). No symbols, paths, or file-by-file essay.
- `## Tradeoffs`: only rejected alternatives a reviewer would otherwise ask about. Skip when there was no real choice.
- `## Blast Radius`: 1–2 sentences on who or what it touches and why that is safe or risky. If main is red, state the cost of leaving it red.
- `## Verification`: 1–3 bullets, each a real run path and its outcome. Perf: one primary number with its unit, `before → after`, and a link to the arena or swarm directory for the rest. No sample-size methodology, swarm recitals, or metric tables.

After the sections, attach videos or screenshots when they prove a claim. Full SHAs, swarm or arena lane recitals, lever-correction essays, file-by-file checklists, and "CLEAN" verdicts go in a linked artifact, not the body.

**GitHub.** Follow [GitHub operations](../references/github-workflow.md) for connector discovery, PR creation, status, review, and merge operations. Local Git still owns branches and commits.

**Size and stacks.** Prefer narrow PRs. A stack is a base-branch chain. The root PR targets trunk. Each child rebases onto its parent's exact tip and targets the parent branch through the GitHub plugin. Branch from trunk only for independent work. Rebase on trunk before substantial stack work.

**Readiness.** Open PRs ready unless the user or repository requires drafts. Set the creation tool's draft field explicitly. Read back the PR's base, head SHA, and draft state before reporting status. Attach the PR URL to the current chat.

**Babysit.** Opening a PR does not start a babysit. Post the URL and keep building. Finish the phase or stack first. Run a separate babysit pass only when the user asks for one after the whole stack exists. A babysit for each new PR stalls the build and spends checks on commits later waves restart. Push back when feedback drifts from intent.

A subagent that opens a PR runs `interrogate`, `$deslop`, and `$no-comments`, and posts the URL. It returns to the parent without babysitting, unless it is an Autopilot-full or Autopilot-stack owner. That owner's brief assigns the babysit loop and is the ask `playbooks/babysit.md` waits for. The owner starts the loop after its code-ready report, reports merge-ready or STACK-READY per its playbook, and is exempt from the rules here and in `playbooks/babysit.md` that hold babysitting until a whole stack is built.
