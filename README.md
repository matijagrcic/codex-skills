# Codex skills

Reusable Codex skills by Matija Grcic.

| Skill | Purpose |
| --- | --- |
| [manage-project](skills/manage-project/SKILL.md) | Coordinate a persistent manager chat, bounded runner chats, written steers, and scheduled progress checks. |

**Install**

Ask Codex to install the skill:

```text
Use $skill-installer to install manage-project from
https://github.com/matijagrcic/codex-skills/tree/main/skills/manage-project
```

The skill will be available on the next turn after installation.

**Use**

Start in the project you want managed. Give the manager an outcome and a way to verify it:

```text
Use $manage-project for this project.

Outcome: [desired result]
Constraints: [requirements and exclusions]
Done when: [observable acceptance criteria]

I authorize you to create and message separate runner chats for this
project, create isolated worktrees when useful, and create a scheduled
heartbeat in this manager chat every 15 minutes.

Keep at most two runners active in addition to the manager. Record my
steers and reconcile them with the full brief before dispatching work.
Verify results, keep unchanged monitoring quiet, and pause the
heartbeat when finished or when all progress needs my input.
```

The manager keeps a small durable record, delegates independent work, reviews evidence, and integrates results. The defaults are one manager, at most two active runners, and a 15-minute heartbeat; adjust them in your request.

This workflow uses ordinary chats and a saved automation rather than activating Goal mode. It requires a Codex environment with chat coordination and same-chat scheduling tools. Local scheduled work requires the host and desktop app to remain running. If a capability is unavailable, the skill reports the limitation instead of claiming background work is active.

The per-session subagent concurrency setting does not establish a global cap on independent runner chats. The manager enforces the requested runner limit. See the [optional subagent configuration](skills/manage-project/references/codex-runtime.md#optional-subagent-concurrency-setting) for Matija's clarification of the two-subagent setting.

If installed, `communicate-clearly` supplies additional handoff and reporting guidance. Essential communication principles are included in `manage-project`, so the companion is optional.

See [sources and design](docs/sources.md) for the evidence behind the workflow. No claim is made that this approach universally outperforms Goals.

**License**

[MIT](LICENSE). Attribution for adapted delegation guidance is preserved in [third-party notices](THIRD_PARTY_NOTICES.md).
