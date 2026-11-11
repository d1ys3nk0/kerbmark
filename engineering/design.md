# Design and reuse

Read when choosing architecture, changing contracts, refactoring structure or evaluating complexity. Applies to software, infrastructure and tooling under [shared/local adoption](adoption.md); preserve local requirements, established conventions and explicitly agreed project decisions.

## Simplicity and reuse

Choose the simplest design that fulfills the task and required guarantees. Consider existing capabilities, removing code and omitting unnecessary mechanisms before adding abstractions. Justify material complexity with a concrete present need for security, reliability, performance or scale. Consider project stage, actual or credibly expected load, users, data sensitivity, failure impact, development and operating cost, and available economic indicators. MVP work gives greater weight to delivery speed and simplicity while retaining mandatory protection and explicit requirements. Do not invent metrics or build for hypothetical scale; inspect available facts and ask the user when missing information materially changes the choice.

When a shared protocol or capability contract is sufficient, prefer one unified reusable implementation over vendor-, organization-, site-, or environment-specific variants. Keep endpoints and vendor, organization, site and environment identifiers in configuration rather than coupling reusable behavior to them. Introduce abstractions only for demonstrated requirements; do not build speculative extension frameworks.

Apply the [low coupling and high cohesion requirement](../infrastructure/configuration.md#low-coupling-and-high-cohesion) when defining capability boundaries or refactoring existing code.

## Reliability and maintainability

- Make invalid states hard to represent: prefer explicit types, schemas, constraints, and validation at boundaries.
- Separate pure logic from side effects: keep business rules testable without networks, filesystems, databases, framework globals, or clocks.
- Prefer boring, observable systems: clear logs, explicit errors, health checks where relevant, and simple operational behavior over clever abstractions.
- Design failure paths intentionally: define what should fail fast, retry, degrade, roll back, or alert.
- Keep dependencies justified: add libraries only when they remove meaningful complexity, and avoid framework lock-in inside core logic.
- Optimize for local reproducibility: commands, checks, fixtures, and setup should be deterministic and documented enough to rerun.
- Prefer deletion over accumulation: actively remove dead code, unused config, obsolete docs, deprecated behavior, outdated names, and compatibility layers when contracts allow it.

Prefer composition over inheritance and constructor dependency injection. Keep reusable code separate from application-specific code and business logic independent from framework internals. Prefer typed structures over untyped hashes/JSON objects; in Python, use dataclasses or Pydantic models where appropriate. Avoid defensive programming that hides architectural issues.

## Module boundaries and dependencies

Prefer deep, cohesive modules with small, stable interfaces that expose only what callers need and hide the complexity needed to fulfill their contracts. Scattered related decisions, thin wrappers and pass-through layers can indicate a shallow boundary. Split responsibilities where they hide meaningful independent complexity, not merely to shorten code.

Direct source dependencies inward toward stable policy. Protect policy from frameworks, transport, persistence and vendors with interfaces where needed, implement outer adapters and wire concrete dependencies at the composition boundary. Translate external data into validated application-owned values at the edge. Use the fewest useful layers and seams; avoid speculative abstractions.

## Event-driven collaboration

Use events to decouple collaboration across domain-module and service boundaries. A publisher announces a fact through an explicit event contract without knowing which modules or services subscribe or how they react. Subscribers own their reactions; publishers must not import subscriber implementations, enumerate recipients, or invoke their handlers directly. Wiring subscriptions belongs to the composition boundary. Event contracts are explicit dependencies; this removes knowledge of peer implementations rather than eliminating every dependency.

In a modular monolith, modules communicate cross-module changes and reactions through an in-process publish/subscribe mechanism. Keep the bus interface independent of module implementations and choose synchronous or asynchronous dispatch deliberately; an in-memory bus does not inherently imply asynchronous execution or durable delivery.

For microservices, prefer publishing and subscribing to events wherever the interaction permits it. Reserve direct service calls for cases that genuinely require and justify them, such as a request that needs an immediate authoritative response. Record why an event-based interaction is unsuitable and the availability, latency and failure coupling introduced by the direct call; convenience alone is insufficient justification.

Specify the event payload, ownership, delivery and ordering expectations, failure handling and consumer idempotency according to the required guarantees. Do not assume an in-memory notification survives a process failure or commits atomically with persisted state. Where loss is unacceptable, select a durable publication mechanism appropriate to the boundary; do not introduce a distributed broker merely to connect modules within one process.

## Contracts and compatibility

- Keep public APIs, CLIs, config keys, file formats, migrations and relied-upon behavior stable and documented; change deliberately. Get explicit approval from the responsible project decision-maker before breaking public behavior.
- Define interfaces by their accepted inputs, outputs, invariants, error modes and ordering constraints, plus relevant compatibility and performance guarantees. Keep one authoritative definition of each contract and generate or validate dependent representations where practical.
- Default to hard cuts for renamed or removed internal contracts and for iterative new changes: update all references in the same change instead of adding backward compatibility, aliases, shims, or fallback-to-old-contract logic.
- Avoid backward compatibility unless explicitly requested or required by a real external contract. If a hard cut may be unsafe, pause and ask whether to proceed with a hard cut plus migration guidance or add temporary compatibility.
- When user-facing behavior is deprecated, include clear migration guidance.

## Data safety

- Treat migrations, backfills, schema edits and destructive operations as production changes: plan rollback and verify explicitly. Back up or dry-run before destructive data operations.
- Make migrations reversible when practical.
- Never hide data loss behind fallback behavior.

## Technical judgment and agreed decisions

Distinguish required product behavior, agreed technical decisions, and implementation choices left open. Product behavior includes supported user journeys, public APIs, and supported integrations. Treat internal interfaces according to their documented contract. Resolve material ambiguity with the responsible decision-maker.

Before implementing a user-proposed method, distinguish the intended outcome from the proposed means and independently assess whether the approach solves the cause at the appropriate ownership and reuse boundary. Proactively recommend a materially better approach when it avoids duplication, unnecessary complexity or a local workaround for a shared cause; do not wait for the user to notice the issue or ask for alternatives. Explain the concrete benefit and relevant trade-offs before committing to the implementation. A proposed method does not remove the agent's responsibility for technical judgment; preserve explicit constraints and agreed decisions under the rules below.

Preserve concrete technical decisions agreed in a plan, system design, ADR or the conversation until the user explicitly approves revision. Existing code and agent proposals alone do not prove user agreement; approval of one choice does not approve the others. Reassess agreed designs as evidence develops: proactively surface defects, risks and clearly better alternatives even when the current design works and has no serious defect. Explain the current choice, alternative, benefit, transition cost and risk, and request approval before changing it. Continue independent work while awaiting the answer; pause dependent work when the agreed approach prevents a correct result.

For open technical choices, apply [shared/local adoption](adoption.md). Autonomously fix in-scope defects and unambiguous local-rule violations, including structural causes, while preserving established subsystem conventions. Shared reference preferences alone do not authorize redesign or standardization of existing material. Update affected consumers, checks and technical documentation coherently, verify the result and report additional improvements afterward. Examine causally relevant layers, distinguish evidence from hypotheses, and retain suitable designs. Preserve task boundaries, concurrent edits, agreed behavior, and applicable project approval requirements.

For meaningful behavior, workflow, contract or architecture changes, prefer spec-first work; distinguish business intent from technical design. Architecture and technology choices follow the same distinction above: preserve agreed decisions, resolve product ambiguity with the responsible decision-maker, and make open technical choices autonomously within scope. If a requested action conflicts with standing guidance and existing authorization does not settle it, clarify whether it is a one-off exception or standing update.
