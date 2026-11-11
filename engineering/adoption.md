# Applying shared and local standards

Read when selecting conventions, applying a standard, creating a repository or considering alignment of an existing project. These guidelines supply shared defaults for independent projects.

## Precedence and applicability

1. Explicit instructions for the task define its scope and approved exceptions; preserve task scope and operating authority.
2. Applicable local requirements supplement shared defaults and override conflicting parts. More specific local rules take precedence within their area; retain nonconflicting requirements.
3. Where local rules leave a choice open, follow established architecture, subsystem boundaries, style, naming and comparable implementation patterns, including for new code added to an existing project. Inspect the relevant subsystem rather than copying an unrelated example. Written standards are not required for examples to establish a convention.
4. Shared standards fill remaining gaps, especially for new repositories or new areas without an established pattern. An unwritten convention is not a gap simply because no local standard spells it out.

Reference standards do not authorize automatic migration of existing code, configuration, file layout or architecture, even when the material is substantially edited. Apply alignment only when explicitly requested, within the requested area. Material departures from shared references may be noted with the benefit and transition cost of alignment; avoid repeated reminders for the same unchanged decision.

## Local requirements and conflicts

Automatically correct unambiguous violations of prescriptive local requirements within the task and causally connected consumers, verify them and report material changes afterward. Report independent violations without expanding the task. Descriptive documentation is evidence, not automatically a prescription. Following an existing pattern does not require reproducing a defect; correct its concrete cause within scope while preserving agreed behavior and design.

When local examples conflict, preserve subsystem boundaries and use maintained requirements and comparable neighboring implementations to resolve applicability. Resolve material conflicts between local requirements, agreed outcomes or technical decisions before dependent changes; follow the applicable project's question policy. Preserve other writers' work, explicit exclusions and external-operation permissions.

## Infrastructure ontology copies

Applicable workspaces carry a self-contained, unchanged copy of the [Infrastructure Ontology](../infrastructure/ontology.md), reached through their local documentation index and task-triggered agent guidance for infrastructure identity, environments, placement or deployment work. Keep concrete values, syntax, topology and exceptions in workspace-owned documents linked alongside the copy. Adoption and later copy updates require an explicitly scoped change; do not migrate other workspaces automatically.

## Independent project guidance

Keep project entrypoints self-contained: concise task routes, local requirements, and a fallback to comparable existing patterns. Use project-relative links for local guidance so the repository can be used independently. Load shared and project guidance by task.

## Skill naming

Use `cmn-<capability>` when the skill and all required support files can be copied byte-for-byte into another project and used after normal setup. Include scripts, references, invocation metadata, and configuration templates in the test. Installing prerequisites and supplying project configuration or credentials from unchanged templates count as setup. If reuse requires editing any of the copied files, use `<workspace-slug>-<capability>`. Use the bare capability slug for user-managed global skills. Provider-managed built-ins and plugin namespaces follow their provider's naming.

A common skill discovers project-specific procedures through the applicable `AGENTS.md` and follows only the routes relevant to the task. Keep local policy and configuration in project-owned guidance. Where no local guidance applies, use the generic method. If an operation depends on missing configuration, policy or authorization, report that prerequisite before proceeding.

Use kebab-case and align the installed directory, `SKILL.md` frontmatter name, invocation metadata and maintained references. Preserve the installed prefix when refreshing a workspace skill.
