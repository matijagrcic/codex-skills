---
name: name-tasks
description: Name or rename Codex tasks, threads, and chats so their titles are accurate, consistent, and easy to scan. Use for a current or selected chat, a project's chat titles, or title proposals. Supports naming only; it does not start or supervise the underlying work.
---

# Name Tasks

Make each title identify the actual work and distinguish it from neighboring chats. In Codex, tasks, threads, and chats refer to the same conversations. This skill works independently of `steer-work`.

## Establish the target and requested action

Use the current request to distinguish suggesting titles from applying renames. For a proposal or review, return proposed titles and stop before changing anything. An explicit rename request authorizes routine reversible changes within its scope; do not ask again. Loading the skill or quoting a naming tip alone does not authorize renames.

- **Current chat:** use this conversation's context. The active `set_thread_title` contract may allow omitting the ID to target the caller.
- **Selected chats:** resolve the intended chats through `list_threads` and inspect unclear matches with `read_thread`. A project is not required.
- **Project cleanup:** resolve the project through `list_projects` and current context, then filter discovered chats by actual project identity. Include pinned entries. Do not infer membership from title words. Resolve ambiguity before mutations.

Follow active tool contracts. Check listing coverage, using additional supported listings or pages when available and archived chats when in scope. A recent-chat list may be incomplete; report coverage limits instead of claiming every task was checked. If the tools cannot target the requested chat or perform renames, provide proposals and explain the limitation.

## Write titles as a readable set

Read enough context to identify the main work, including recent user direction when a chat has evolved beyond its original request. Use summaries to select what to inspect; do not infer the task solely from a vague old title.

- Start with a concrete action; the shared actor, the agent, usually need not be named.
- Put the distinguishing target early. Remove repeated lead-ins such as "Working on" or "Task for"; avoid repeating the project name or runner label before every title.
- Use the same grammatical pattern for comparable work and the same term for the same component. Preserve technical identifiers that distinguish the task.
- Vary wording, qualifiers, or tense only for meaningful differences. Keep titles compact without an arbitrary word count.
- Choose verbs that convey the actual purpose, such as investigate, implement, review, or verify. Do not describe an unresolved investigation as a successful fix.

For active work, a useful default is a continuous verb followed by a specific target. Examples illustrate supported states rather than mandatory vocabulary:

| Known work or state | Example title |
| --- | --- |
| Active investigation | Investigating checkout timeouts |
| Active implementation | Adding checkout retries |
| Active verification | Verifying checkout retries |
| Verified completed fix | Fixed checkout retry loop |
| Confirmed external wait | Waiting for checkout CI |
| Planned work or uncertain progress | Investigate checkout timeouts |

Idle, archived, or agent-turn-complete states do not prove task completion. Read evidence before using result verbs such as "Fixed" or "Verified." An assignment-style title can describe intent when progress is unknown. Leave genuinely unclear cases unchanged and explain the gap.

Review proposed titles together for consistent vocabulary and unintended ambiguity. Add a component, environment, or issue identifier when it distinguishes actual work. Preserve explicitly requested names and conventions unless the rename request covers replacing them. Keep suitable titles; do not rename merely to vary the wording.

## Apply and verify

Keep a lightweight mapping of the target, old title, and proposed title, retaining the exact chat ID when available. Current-chat targeting does not require discovering an otherwise unavailable ID. When identifying an existing chat to the user, use its returned current title verbatim and clearly distinguish proposals.

Apply authorized changes with `set_thread_title`, passing the discovered ID and supported source value, or the supported current-chat targeting option. If the result is uncertain, reread the saved title before retrying. Use available read tools to verify the result; do not edit internal app databases.

Report what changed and any skipped or unavailable targets. For a batch, include a count and keep the mapping available for recovery. No manager folder, runners, or schedule is needed. Renaming changes a label, not a task's identity or completion state; do not create, move, archive, restart, or message chats as part of title cleanup.

## Source

The readability guidance draws on Shreya Shankar's [Five Principles for Generating Readable AI Text in Bulk](https://fsdatalab.github.io/blog/agent-text-at-scale/) (29 October 2026). Scope resolution, completion evidence, and rename verification are this skill's Codex-specific applications of those principles.
