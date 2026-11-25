# Format and tools

[Dillon Mulroy's design Gist](https://gist.github.com/dmmulroy/bd3878d1bcaad7b2800b1d0dff083991) is the format reference. Its design follows request flow, data ownership, interfaces, failures, and rollout. Its research notes record the repository evidence and platform checks supporting the choices.

## Full design structure

1. **System at a glance** — a short purpose, a Mermaid flowchart, and a component ownership table. Label trust boundaries and existing external systems where relevant.
2. **Data model** — an ER diagram, stable IDs, states and invariants. Add a small type definition or an example payload where it clarifies data shape.
3. **Interfaces** — one call from a consumer's perspective. Add an endpoint or command table when there is more than one entry point. Include expected failures and what the caller can do next.
4. **Execution paths** — sequence diagrams for service hops and a call tree for the important code path. Separate completion from asynchronous dispatch. Place transaction, retry, and human decisions where they happen.
5. **Verification and rollout** — the shortest set of proof cases and ordered milestones that can validate the design. For each test-driven development case, give the public interface, input, expected observable result, and evidence for that expectation. Use the actual caller surface for interface behavior. Give each unresolved decision a specific question.

Keep the sections that make the topic clearer. Use separate research notes only when the design needs an evidence trail substantial enough to distract from the main path.

## Shared language and test-driven development

Use [Matt Pocock’s glossary pattern](https://github.com/mattpocock/skills/blob/main/skills/engineering/domain-modeling/GLOSSARY-FORMAT.md) to settle what each concept means before naming a type. Use [pstack architecture](https://github.com/cursor/plugins/blob/main/pstack/skills/architect/SKILL.md) to show who owns state and what a caller can do. Carry the agreed terms into one observable test at a time, using expected values from a source example or an agreed rule. [Matt Pocock’s TDD skill](https://github.com/mattpocock/skills/blob/main/skills/engineering/tdd/SKILL.md) · [pstack verification](https://github.com/cursor/plugins/blob/main/pstack/skills/principle-test-behavior-not-implementation/SKILL.md)

## What Dillon uses

In his October 21, 2026 Cloudflare Connect workshop *This is my workflow: Building with AI*, Dillon demonstrates a feedback loop around four tools.

| Tool | Role in the workshop | How to apply the pattern |
|---|---|---|
| [Ghostty](https://ghostty.org/) | Terminal | Use the user's existing terminal or app surface. |
| [Herdr](https://herdr.dev/) | Agent-aware terminal multiplexer | Separate independent research from the main design when delegation is authorized. Bring back evidence and decisions. |
| [Pi](https://pi.dev/) | Coding-agent harness | Use the current harness. Keep design context concise and written down. |
| [Plannotator](https://plannotator.ai/code-review/) | Local review of agent diffs with feedback sent to the session | Review a proposal or diff before sharing it. Use an existing local annotation surface if requested and available. |

The workshop describes [HumanLayer's show-me](https://www.humanlayer.com/blog/show-me-skill) for call stacks, types, diffs, and affected files. Dillon also uses a handoff to restart with the decisions, constraints, and remaining work when the session gets long. His published [tech-spec skill](https://github.com/dmmulroy/skills/tree/main/tech-spec) expands the same idea into typed interfaces, explicit seams, and verification through real entry points. His demo mentions Effect, Alchemy, and Vite+ as project tooling. Use those when they fit the project.

This skill runs in Codex with Markdown and Mermaid. The tools described above are references for adapting the workflow. Use the project's chosen stack and tools.
