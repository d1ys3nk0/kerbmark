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

## Infrastructure identity

For infrastructure identity, environment, placement, and deployment guidance, route readers to a local Meridian quick reference. Copy the marked block from the [canonical README](https://github.com/d1ys3nk0/meridian/blob/main/README.md) and record its source commit. Keep concrete values, syntax, topology, and exceptions in project-owned guides.

## Reviewed framework baseline

This baseline records reviewed documentation compatibility, not tested runtime integration. The Kerbmark revision containing this record identifies its engineering guidance, Meridian snapshot, and worked product example. Read the other frameworks at the exact revisions below; links to their default branches may show newer guidance outside this baseline.

| Framework | Reviewed commit | Authoritative scope |
| --- | --- | --- |
| Umbrella | [`7cac443e85e2aa77f02e4434a8c856328c4f4acc`](https://github.com/d1ys3nk0/umbrella/blob/7cac443e85e2aa77f02e4434a8c856328c4f4acc/README.md) | Workspace layout, repository boundaries, and documentation placement. |
| Meridian | [`cac3ed6dce070aa159dcf1c0342ea1fad7f065eb`](https://github.com/d1ys3nk0/meridian/blob/cac3ed6dce070aa159dcf1c0342ea1fad7f065eb/README.md) | Runtime identity, placement, and state ownership. |
| Armada | [`19cdeef4a561bc6ac647a49cf68cfd4357ff086f`](https://github.com/d1ys3nk0/armada/blob/19cdeef4a561bc6ac647a49cf68cfd4357ff086f/README.md) | Ansible inventory, layers, variables, roles, and operations. |

Record the product's selected full framework commits and approved exceptions in its existing engineering documentation, following Umbrella's repository ownership rules. Link to component-owned identity mappings, command contracts, and verification evidence. Record the selected Kerbmark commit as well as the three provider commits; a moving branch name is not a reproducible adoption record. A baseline does not require adopting every framework or override established local contracts.

### Maintaining compatibility

1. Identify the changed contracts and affected consumers. Inspect upstream changes between the adopted and proposed revisions, including changes to identity scope and ownership boundaries.
2. Select explicit provider commits and refresh copied excerpts from committed source. Compare the Meridian quick-reference block verbatim with its recorded source revision.
3. Review dependent examples, local links, and cross-framework file and heading targets against the selected revisions. Check separate Cells, multi-Area Cells, partial operation scope, Space isolation, and non-mutating previews where relevant.
4. Record the reviewed revisions, remaining limitations, and approved local exceptions with their owners. Preserve standalone repository use and distinguish documentation review from runtime acceptance evidence.
5. Publish provider commits before publishing consumer baseline updates that reference them. Verify that the referenced commits are available, and update only consumers whose adoption is in scope.

Upstream changes alone do not authorize consumer migrations. For an explicitly scoped identity migration, follow [Meridian's migration guidance](https://github.com/d1ys3nk0/meridian/blob/cac3ed6dce070aa159dcf1c0342ea1fad7f065eb/README.md#migrating-area-qualified-cell-identities) and preserve existing state and completion history.

## Independent project guidance

Keep project entrypoints self-contained: concise task routes, local requirements, and a fallback to comparable existing patterns. Use project-relative links for local guidance so the repository can be used independently. Load shared and project guidance by task.

## Skill naming

Use `cmn-<capability>` when the skill and all required support files can be copied byte-for-byte into another project and used after normal setup. Include scripts, references, invocation metadata, and configuration templates in the test. Installing prerequisites and supplying project configuration or credentials from unchanged templates count as setup. If reuse requires editing any of the copied files, use `<workspace-slug>-<capability>`. Use the bare capability slug for user-managed global skills. Provider-managed built-ins and plugin namespaces follow their provider's naming.

A common skill discovers project-specific procedures through the applicable `AGENTS.md` and follows only the routes relevant to the task. Keep local policy and configuration in project-owned guidance. Where no local guidance applies, use the generic method. If an operation depends on missing configuration, policy or authorization, report that prerequisite before proceeding.

Use kebab-case and align the installed directory, `SKILL.md` frontmatter name, invocation metadata and maintained references. Preserve the installed prefix when refreshing a workspace skill.
