# Implementation

Read before changing code, infrastructure or executable tooling. Read design standards for structural or contract changes, verification standards for behavior and checks, and format standards only for formats being edited; select them through the [catalog](../README.md).

Apply [shared/local adoption](adoption.md): inspect comparable neighboring code and preserve the subsystem's architecture, style, naming and patterns, including for new additions. Shared references fill only remaining gaps; they do not authorize retrofitting existing material. Use semantic names that convey meaning in few characters within those conventions. Fix root causes at the responsible layer with the smallest correct change; avoid scope creep and unnecessary comments or documentation. Keep commands, checks, fixtures and setup reproducible. For repositories using OpenSpec, review relevant existing specifications before changes and update them when needed to keep implementation, specifications and documentation consistent.

## Code comments

- Do not add comments that describe what code does or narrate its steps. Make the code clear through naming and structure.
- Add explanatory comments only where the reasoning is non-obvious: explain why a choice is necessary, including constraints, invariants, tradeoffs, or workarounds in obscure or surprising parts of the code. Omit comments when the rationale is already clear.
- When editing code, remove or rewrite redundant or stale explanatory comments in the touched area; avoid unrelated comment cleanup.
- Preserve required tool directives, legal notices, and the YAML section headings used for navigation under the [YAML layout guidelines](../formatting/yaml.md). These are structural or operational annotations, not code narration.

## Observability and operations

- Prefer actionable logs over noisy logs.
- Errors should include enough context to debug without exposing secrets.
- Production fallbacks should be measurable, not silent.

Make external service calls observable. Include useful response-body details on errors only after removing secrets and sensitive data. During development, fail fast and loudly instead of masking problems with silent degradation. Use graceful degradation, retries and fallbacks for production where needed; keep them observable.
