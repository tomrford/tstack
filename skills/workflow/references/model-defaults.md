# Model defaults

Use these bundled defaults for delegates. No setup command or external model-rule file is required. The parent chat keeps the user's selected model.

| Role | `model` | `reasoning_effort` |
|---|---|---|
| Implementation, exploration, research, Swarm workers, and Reflect tooling | `gpt-6.1-sol` | `high` |
| Hardest implementation tasks, judgement, prose, How explanations, Why synthesis, Reflect judgement/divergent/synthesis, and independent judges | `gpt-6-astra` | `high` |
| Arena and Architect candidates; Interrogate reviewers | One Sol 6.1 and one Astra, using the IDs above | `high` |

Sol is the default for roles not listed. Mechanical work uses Sol high too; introduce a lighter default only after task evidence justifies it. An explicitly requested low-effort task may use `gpt-6.1-sol` with `reasoning_effort: "low"` when available. Luna is not a default role.

Use a fresh context for independent review even when it uses the same model. Arena, Architect, and Interrogate run at least two independent attempts. Report the actual models and any unavailable panel seat; do not describe a same-model panel as cross-family evidence.

Pass model and effort separately, for example `collaboration.spawn_agent({ task_name, message, fork_turns: "none", model: "gpt-6.1-sol", reasoning_effort: "high" })`. Supply a self-contained brief. Full-history forks cannot carry these overrides.

The user's task-specific selection overrides this table. Use only combinations exposed by the active tool schema. If a default is unavailable, report the gap and use the parent model without overrides; retain fresh review contexts and report the reduced model diversity. If the user explicitly requires a particular model, do not substitute it without their agreement.
