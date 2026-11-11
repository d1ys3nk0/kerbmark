# Verification

Read when implementing or changing behavior, fixing defects, selecting checks or evaluating systems. Includes engineering review selection and completion. Preserve applicable project exceptions.

For new or explicitly migrated Task interfaces, follow [Taskfile namespaces and layout](../tooling/taskfiles.md) for `verify`, `verify:lint:*` and `verify:test:*`. This naming contract does not change verification categories, selection modes or existing project interfaces.

## Behavior and regression coverage

Unit, integration and end-to-end tests must prove only promised externally observable behavior, not freeze internal implementation. A unit test may isolate a pure calculation or use case that implements a user promise. Maximize sufficient unit coverage; use integration tests for service or mechanism risks units cannot prove, and end-to-end tests for cross-service or user-path risks lower levels cannot prove. Avoid duplicate assertions across levels. Contract tests separately verify compatibility between components, including internal interfaces; a frontend-to-backend API is not public merely because it uses HTTP.

Do not freeze current configurable values or private implementation details. Test configuration precedence, validation and forwarding with synthetic values when those are behaviors under test. Lint enforces adopted source, layout, naming and formatting conventions without running the application; the language or runtime used by the checking tool does not change its category. Type checking and compilation are distinct checks. Do not test instruction text. A custom linter may have behavioral tests of its own supported CLI or callable interface using synthetic accepted/rejected fixtures, rather than asserting current project values.

Prefer deterministic tests. Prefer test-first development for substantial new behavior and bug fixes: derive outcomes independently from accepted requirements, obtain a behavioral failing result when feasible, implement, then refactor while green. An unrelated setup failure is not behavioral red evidence. Preserve available red/green evidence and report chronology honestly; missing historical red evidence alone is not a blocker when present protection is adequate. Documentation-only and reversible low-impact changes need proportionate inspection, not artificial tests.

Assess whether tests exercise the real entrypoint and relevant wiring, assert independently derived outcomes, and use realistic doubles that preserve the behavior under examination. A mocked adapter does not prove that adapter's behavior. When a material test's effectiveness remains uncertain, obtain proportionate evidence such as a counterexample or controlled fault only when the risk warrants it; confirm a fault fails for the intended reason and preserve the candidate and its data.

Work in small coherent increments and run relevant feedback as the change progresses. Reuse successful evidence only while the relevant source, dependencies, configuration, fixtures and commands remain unchanged; rerun invalidated checks. Surface issues early through lint, types and tests before merge. Run applicable affected-behavior tests, linters, types, contracts and verify stages. If sufficient coverage cannot be selected reliably, run full affected-repository checks; when cross-component impact is uncertain, use existing full-system checks. Correct task-related failures and rerun invalidated checks. Missing required checks and unresolved failures are blockers, not evidence of readiness.

## Verification categories

| Category | Purpose |
| --- | --- |
| Unit | Isolated logic implementing promised user behavior, including pure calculations and use cases. |
| Integration | Remaining service behavior and real mechanism risks that unit tests cannot sufficiently prove. |
| Contract | Internal producer/consumer compatibility, including service-to-service and browser/backend interfaces. |
| E2E | Crucial complete user scenarios and real wiring risks not sufficiently verified at lower levels. |
| Lint | Adopted structural, naming, formatting and source conventions, checked statically. |
| Typecheck / compile | Separate verification of types and compilation. |

The first four categories are test types. Classify by the claim a check proves, not its filename or testing framework. A private method being callable does not make it a promised user contract. Lint is permitted for adopted conventions, not for freezing arbitrary source strings or today's settings. Existing suites named static and mixed suites retain their execution interfaces until deliberately migrated; the categories authorize no automatic removal or pipeline changes.

## Test selection modes

Modes select tests independently of test type. Extra marks expensive cases reserved for explicit manual execution. Regular excludes tests marked extra; smoke selects happy-path tests, including any that are also marked extra; full includes all scoped tests. Eligible regular and full runs execute smoke first and fail fast if it fails. CI and hooks use regular; smoke and full are manual modes. Existing project-specific smoke/deep modes remain in place until a separately authorized migration; shared guidance does not itself change pipelines or commands.

## Evaluation integrity

- Never game, overfit, or tailor a system to specific evaluation datasets, fixtures, hidden-test guesses, benchmark examples, expected outputs, or evaluator implementation details.
- Treat evaluation cases only as evidence of a general requirement or failure mode. Fix the underlying behavior so the solution generalizes to real use cases and materially different unseen inputs.
- Do not add special cases, hardcoded answers, dataset-specific heuristics, prompt branches, lookup tables, or detection logic whose primary purpose is to pass known or inferred evaluation cases.
- Do not weaken, bypass, intercept, mock, or misrepresent the behavior being evaluated, and do not modify evaluation inputs, expected outputs, scoring logic, or test infrastructure merely to obtain a passing result.
- Preserve legitimate evaluation independence: do not inspect hidden evaluation data or exploit leakage when it becomes accessible accidentally. Report suspected leakage, contamination, ambiguous scoring, or an evaluation that rewards incorrect real-world behavior.
- Prefer contract-level and adversarial verification beyond the provided evaluation cases. A passing evaluation is insufficient when the implementation does not satisfy the intended behavior in realistic use.
- If a requested change would improve an evaluation score at the expense of general correctness, robustness, safety, or real-world usefulness, refuse that approach and explain the conflict.

## Review selection and completion

Select deterministic checks through the coverage requirements above. Preserve environment, data, concurrency and external-operation permissions.

Complete the requested scope with a minimal, correct result, required checks passed, no unrelated changes, and explicit risks, assumptions and follow-up constraints. Substantiate completion with observable results. Report changes, checks, and limitations.
