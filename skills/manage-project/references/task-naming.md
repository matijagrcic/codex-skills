# Task naming

Use this guidance for titles of managed chats and for a user-requested project title cleanup. In Codex, tasks, threads, and chats refer to the same conversations. The readability principles come from Shreya Shankar's [Five Principles for Generating Readable AI Text in Bulk](https://fsdatalab.github.io/blog/agent-text-at-scale/) (29 October 2026); the scope, evidence, and tool procedure below are this skill's application of those principles.

## Write titles as a readable set

- Start with a concrete action; the shared actor, the agent, usually need not be named.
- Put the distinguishing target near the start. Remove repeated lead-ins such as "Working on" or "Task for"; avoid putting the same project name or runner label before every title.
- Use a consistent grammatical pattern for comparable work and the same term for the same component. Preserve exact technical identifiers when they distinguish the task.
- Vary wording, qualifiers, or tense only for a meaningful difference in work or supported state. Keep titles compact without enforcing an arbitrary word count.
- Choose verbs that reveal the actual purpose: investigate, implement, review, or verify. Do not dress an unresolved investigation as a successful fix.

For active work, a useful default is a continuous verb followed by a specific target. These are illustrative titles, not a mandatory vocabulary:

| Known work or state | Example title |
| --- | --- |
| Active investigation | Investigating checkout timeouts |
| Active implementation | Adding checkout retries |
| Active verification | Verifying checkout retries |
| Verified completed fix | Fixed checkout retry loop |
| Confirmed external wait | Waiting for checkout CI |
| Planned work or uncertain progress | Investigate checkout timeouts |

Do not infer completion from an idle chat, an archived chat, or an agent finishing its turn. An assignment-style title can describe intent when progress is unknown. Read evidence before using a result verb such as "Fixed" or "Verified." Preserve user naming conventions unless the request covers changing them.

Review titles together so similar tasks use the same terms and distinct tasks remain distinguishable. Add a concrete component, environment, or issue identifier when needed. Update managed titles when the scope or a meaningful verified state changes; avoid cosmetic renaming on every heartbeat. Native status and the manager's records remain the sources of operational state.

## Apply a scoped rename

An explicit request to rename a project's tasks authorizes that cleanup; do not ask again for routine reversible renames. Loading this skill or quoting a tip about renaming does not by itself authorize a project-wide cleanup. A naming-only request does not authorize dispatch, scheduling, or project reorganization.

1. Resolve the intended project using `list_projects` and the current context. If the target remains ambiguous, resolve it before mutations. Inspect `list_threads`, including pinned entries, and filter by actual project identity rather than title keywords. Check listing coverage; use additional supported listings or pages when available, including archived chats when in scope. Do not claim to have renamed every task based on an incomplete recent list.
2. Read the current titles and summaries. Use `read_thread` for enough history to resolve unclear scope, stale summaries, or completion claims. Do not derive a new title from the old title alone when it is vague. Leave uncertain cases unchanged and explain the gap.
3. Build an ID-to-old-title-to-new-title mapping. Keep already suitable titles, respect explicit user titles unless their replacement is covered, and remove accidental ambiguity between proposed titles. Use the returned current title verbatim when identifying a chat to the user; clearly label proposed titles as proposals.
4. Apply changes with `set_thread_title`, passing the exact chat ID and supported source value from discovery. Follow active tool contracts; do not edit internal app databases. If a call's outcome is uncertain, reread the title before retrying.
5. Verify the saved titles through the available read tools. Report the number changed and any skipped, unavailable, or out-of-scope chats. Keep the mapping available for recovery; for ongoing management, keep it with the existing state rather than creating another ledger. Report partial coverage honestly if the tools cannot enumerate or target all requested chats.

Renaming changes a label, not the task's identity or completion state. Do not move, archive, restart, or send messages to chats as part of a title cleanup.
