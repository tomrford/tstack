# Codex agent tools

Use the tools available in this session and read their current schemas. Names below describe the desktop contract; unavailable capabilities remain explicit gaps.

## Subtasks in this chat

Use `collaboration.spawn_agent({ task_name, message, fork_turns })` for scoped subtasks. Give each brief the goal, immutable revision when relevant, permitted paths, verification, required skill reads, and report format. Use `fork_turns: "none"` for independent review or a model override. Include the necessary context explicitly. Full-history forks inherit the parent's model and reasoning.

Subagents share this workspace on the current execution host. Assign each writer an isolated worktree through `create_worktree`, or a separate output directory, and include its absolute path in the brief. A spawn does not select a branch or move execution to another machine. A read-only brief forbids writes but is not a sandbox permission setting. Verify actual tool and MCP access.

- `list_agents` reads state without starting work.
- `send_message` steers a running agent without starting a new turn.
- `followup_task` starts an idle agent's next turn; do not use it as a status probe.
- `wait_agent` waits for an update; receive and verify the resulting report before accepting it.
- `interrupt_agent` stops the current turn and retains the agent's context.

Respect the session's concurrency limit. Refill slots as workers finish. A new fix round normally gets a fresh context; retain an agent only when its live process or uncommitted state is needed. The parent owns the evidence, final synthesis, and any external publication.

## Separate chats and connected machines

Use subagents for internal steps. Use a separate user-owned chat when the user explicitly requests a new task that should have its own durable history and be independently steerable. A project-scale coordinator can propose this decomposition, but a request to orchestrate does not itself authorise creating or messaging other chats.

For an authorised new chat, call `list_projects` and select the saved repository project on its configured host. Use `create_thread` with that project and its checkout, or an explicitly requested worktree. Include the full brief, relevant skill paths, and intended revision. Follow it with `wait_threads`; inspect earlier context with `read_thread`. Use returned host and chat IDs in subsequent calls. `send_message_to_thread` requires the user's explicit authorisation to message that task.

Orchestration uses this machine and machines available through its configured Codex remote connections and remote control. Discover available hosts and projects from the active tools rather than assuming a connection exists. A separate chat on a connected host runs against that host's files, toolchains, credentials, and processes. Verify its repository, revision, writable paths, and app-driving capabilities before assigning work; a local file path is not automatically available there.

When moving an existing chat is requested and supported, use `handoff_thread` and follow its operation with `get_handoff_status`. Select only destinations exposed by the current schema and confirm completion before continuing. If this session exposes only the current host, keep work there and report unavailable remote access. Do not treat an internal subagent as a remote worker.

## Continuing now and waking later

Continue an authorised task in the current chat. Create a goal with `create_goal({ objective })` only when the user explicitly requests a goal. Add a token budget only when requested. Inspect with `get_goal` and follow the active status-transition rules for `update_goal`. Mark complete only after proving the outcome.

For requested schedules, reminders, monitoring, or later follow-ups, use `automation_update` with `kind: "heartbeat"` for this chat. Specify the cadence, evidence to check, allowed actions, and completion or cancellation condition. Use a standalone cron task only when the user asks for a new task per run. A heartbeat schedules a future turn; it does not keep subagents alive or move execution to another host.

Keep monitoring quiet while nothing meaningful changes. Notify on completion, failure, a material change, or required user action. Update or remove the monitor when its purpose ends. Local scheduled work requires the app and host to remain available. Within an active run, wait for the relevant agent or check completion; do not create a second polling loop.

## History and questions

Use current conversation context first. For requested prior work, scope by project, topic, and time, then use `list_threads` and `read_thread` with pagination. Their summaries and truncated outputs are not a complete transcript. If proof needs raw local evidence, resolve an exact supplied session path or thread ID and verify its workspace metadata before reading; do not search unrelated global session history.

Use `request_user_input_async` when available for missing preferences while continuing independent work. Otherwise use the available question tool or ask in chat. Ask only what the environment and evidence cannot establish. Use the tool's documented question schema.
