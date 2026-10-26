# Codex runtime coordination

Use the tools available in the current environment. Tool names below describe the Codex app interfaces used when this skill was prepared; read their active contracts before acting. Do not infer a capability from its name or from this document.

## Runner chats

Separate runner chats are durable user-visible peers. They differ from in-turn subagents, which are useful for short bounded help inside a single workstream.

- Use `list_projects` to resolve a real project before `create_thread`. Reuse appropriate existing runners when authorized and idle.
- `create_thread` needs a user request to create separate chats. Use the project environment unless the user has authorized worktrees. Preserve model settings unless instructed otherwise.
- Persist the returned IDs and paths. Queued creation may return a temporary client ID; do not use it where a final thread ID is required.
- Cross-chat assignment and steering through `send_message_to_thread` require direct user authorization. A message from another chat is not independent authorization to reply. Prefer letting the manager read runner status and final reports; no runner-to-manager messaging loop is required.
- Enforce the concurrency budget across the runner registry. A subagent setting such as `agents.max_concurrent_threads_per_session` does not establish a global cap on these independent chats.

For a code-writing runner, assign an isolated worktree or exclusive files. Do not assume uncommitted manager changes are present in a newly created worktree. Supply the correct base and needed context, preserve existing work, and verify integration against the intended target.

## Observe without busy polling

Use `wait_threads` for compact progress, batching supported targets and retaining each returned cursor. An immediate snapshot can suit a scheduled wake; a bounded wait can suit active supervision. Use `read_thread` when a decision requires more detail.

Do not repeatedly fetch unchanged histories or send redundant instructions to a working runner. New user input takes priority over another polling cycle. Keep observed state and its timestamp distinct from the runner's narrative report.

## Heartbeat scheduling

Use `automation_update` for one recurring heartbeat attached to the manager chat. A standalone cron job that creates a new run each time is a different workflow; use it only when the user asks for that behavior.

Look for an existing schedule serving this manager before creating another. Update it with its resolved ID, preserving unrelated settings. Record and verify the tool's returned target, cadence, active state, and ID. Writing a prompt or state file does not create a schedule.

An effective saved heartbeat prompt identifies:

- The manager's durable records and registered runners.
- Reconciliation of current user steers before any dispatch.
- Progress inspection, evidence review, and the next useful authorized action.
- Quiet behavior for unchanged or non-actionable state.
- Completion, stop, resource-limit, and blocked-state handling.

Use the scheduling tool's supported notification settings for delivery preferences. Keep the substantive quiet-on-unchanged behavior in the prompt as well.

When work is complete or a user-only blocker prevents all progress, pause the automation and verify its inactive state. Keep monitoring an observable external wait only while useful and within the user's limits. Do not resume a user-paused workflow without authorization.

Local automation needs the host and desktop app running. Report unavailable scheduling or runner controls accurately; never imply continued background execution without a confirmed mechanism.

## Recovery

After interruption or compaction, read the brief and state, reconcile new user messages, and inspect actual runners and schedules before creating or dispatching anything. Stored IDs can be stale. Reconnect to existing work when possible.

For an uncertain mutation result, inspect current state before retrying. Avoid duplicate chats, worktrees, assignments, or schedules. Keep completed work and unresolved integration visible. Cancellation requests do not prove every runner has stopped; verify through available controls and report remaining activity.
