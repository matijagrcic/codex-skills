---
name: steer-work
description: Coordinate sustained implementation, research, and project work through a persistent manager chat, bounded runner chats, durable steers, and scheduled progress checks. Use when work benefits from durable context, coordinated workers, or ongoing supervision.
---

# Steer Work

Keep the objective, shared reasoning, and decisions in one manager chat. Delegate bounded work that benefits from parallel execution, investigation, or independent verification. Keep tightly coupled decisions together. Use ordinary runner chats and scheduled follow-up; do not activate Goal mode for this workflow.

## Establish scope and authority

Inspect the project and existing work before dispatching. Turn the user's outcome into a concise brief with constraints, explicit requirements, assumptions, and observable completion criteria. Reuse established criteria; do not silently substitute easier ones.

Use the user's existing authorization for separate runner chats, messages, worktrees, and scheduling. Loading this skill alone does not authorize those actions. If necessary authority is missing, prepare the brief and concrete proposed setup, then ask only for what is missing. A request to draft or evaluate a workflow must not activate it.

Before operating chats or schedules, read [Codex runtime coordination](references/codex-runtime.md). Follow the active tools' contracts when their interfaces differ.

## Preserve decisions and steers

Use an existing project record when suitable, or keep a small manager folder in the workspace. Maintain:

- A current brief with the objective, constraints, acceptance criteria, and decisions.
- An append-only steer history, marking superseded instructions without erasing them.
- Compact state with runner IDs, ownership, worktrees, latest observed status and time, evidence, next actions, and the automation ID.

The manager owns these records. Runners return findings and artifacts without concurrently rewriting manager state. Pass relevant context explicitly; separate chats may not inherit it.

Record new user direction before the next dispatch or acceptance decision. Reconcile it against the whole brief and earlier decisions, then steer affected runners. Preserve all still-applicable requirements. Distinguish a change of method from a change of objective; resolve material uncertainty about purpose with the user.

## Delegate within a clear boundary

Unless the user chooses otherwise, keep at most two runners active in addition to the manager. This is a working default, not a claim about an optimal number. Reuse suitable idle runners and avoid overlapping assignments.

Give each runner its outcome, context, applicable steers, ownership, constraints, completion criteria, and required artifacts. Runners are leaf workers by default: no further agents, chats, Goals, or schedules. Use exclusive file ownership or isolated worktrees for concurrent edits; serialize integration. Preserve the configured model unless the user requests a change.

Give managed chats a clear action and specific target, keep vocabulary consistent, and match any progress claim to evidence. Keep chat IDs as durable identities. When installed, `name-tasks` supplies detailed naming guidance and handles user-requested title cleanups independently. A title-cleanup request does not start this supervision workflow.

Use `communicate-clearly` when installed, including its agent-coordination reference. Pass its location or relevant guidance to each runner. If unavailable, keep handoffs self-contained: identify the action and owner, preserve scope and authority, and separate observations, assumptions, plans, reported outcomes, and verified results. Reports should include evidence, verification limits, and remaining work or blockers. Use explicit labels only when they prevent misunderstanding; do not add routine acknowledgment ceremonies.

## Supervise and verify

Create or reuse one heartbeat in this manager chat when scheduling is authorized. Start at the requested interval, or 15 minutes when the user leaves cadence to judgment. Verify the saved target, interval, status, and ID.

Each wake reconciles steers, observes registered runners, checks evidence needed for decisions, and takes the next useful authorized action. Stay quiet while nothing actionable changes. Report meaningful progress, completion, failure needing attention, or a required decision.

Treat runner claims as reports until relevant artifacts, checks, or measurements support them. Verify the promised criteria without reflexively repeating entire investigations. Change the approach when evidence shows a stall; do not retry identical work indefinitely or multiply agents to hide lack of progress.

Continue useful independent work around a blocker. If all progress needs user input or authorization, report the precise blocker and pause the heartbeat. For an observable external dependency, keep quiet monitoring at an appropriate cadence within resource limits.

## Finish and stop

Finish only when the brief's acceptance criteria and required integration are verified. Pause the heartbeat, confirm its saved inactive state, and return the result with evidence and material gaps. Do not invent follow-on work.

On a user stop or pause, stop dispatching, pause the heartbeat, stop runners through available controls, and save a checkpoint. Report any runner that cannot be stopped. Respect user resource limits; obtain a decision before exceeding them.
