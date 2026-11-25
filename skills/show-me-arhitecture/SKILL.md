---
name: show-me-arhitecture
description: Explain or propose software architecture as a reviewable Markdown design with Mermaid, typed caller examples, call stacks, and storage ownership. Use when asked to show an architecture, design a system or feature, or trace a change through code and data.
---

# Show me architecture

Make the design easy for an engineer to inspect and change. Start with what the system does, who calls it, and the architectural decision at hand. Use the compact style of the local show-me skill and the document structure of Dillon Mulroy's design Gist. For a full design or a question about his workflow, read [format and tools](references/format-and-tools.md).

## Ground the design

- Read relevant source material and the current code where available. Use the project's names, types, interfaces, and toolchain. Mark proposed paths and contracts as proposed. Surface any question that changes a boundary, invariant, approval, or rollout decision.
- Use the project glossary when available. Give verified full names followed by their abbreviations at first use. Repeat the definition or provide an adjacent key for tables and diagrams that can be read alone. Describe the role of an unexpanded system label and flag it for confirmation. Preserve source quotations and code identifiers.
- Use a concrete scenario to resolve a disputed term or boundary. Record agreed meanings in the glossary and label undecided type names or interfaces as proposals. Capture consequential architectural trade-offs in the project’s architectural decision records when agreed.
- Answer questions the available evidence can resolve. When an unresolved decision prevents a coherent design, ask the smallest question that resolves it. Show useful partial design when the rest can proceed.

## Show the system

- For a narrow question, use the smallest useful diagram, call tree, or surrounding diff. For a system proposal, start with an overview Mermaid flowchart and a table showing each component's responsibility, data ownership, and key.
- Show the interface from the caller's perspective. Sketch glossary-aligned types, input, output, allowed states, expected failures, and the owner of each mutable state before proposing implementation. Trace one real request or record from input parsing through the owning service, durable write or side effect, and response. Use a Mermaid sequence for runtime hops and a call tree for code paths.
- When persistence changes, include an ER diagram or table with keys, authoritative rows, revision history, and the transaction boundary. For reviews or approvals, show what blocks advancement, who can decide, and which exact version downstream work consumes.
- Show the consequential failure paths. Name retry ownership, the replay key, and the visible result of a partial failure where those apply. Use a short state diagram when state transitions drive behavior.
- Map the design to existing files and proposed changes. Compare alternatives when they change a material decision. For new or changed behavior, propose the first test-driven development (TDD) case: name the public interface, concrete input, expected observable result, and its independent source. Plan one failing test and the smallest passing change per slice. Match the verification surface to the behavior and close with open decisions.

Keep explanations beside the diagram, schema, or snippet they support. Use Markdown with fenced Mermaid as the default. Put long designs in a linked local Markdown file when that is easier to review. For a user-facing layout or interaction, use the applicable UI preview workflow.

Finish with a design the user can review. Describe the proposed changes without editing product code unless the user separately asks for implementation.
