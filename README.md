# Kerbmark Guidelines

Practical guidance for designing, changing, and operating software. For engineers and coding agents working across independent repositories.

Start with the project's own requirements and established conventions. Use [shared and local adoption](engineering/adoption.md) to decide when these guidelines apply. Open the rows relevant to the task and follow further links as needed.

## Use the frameworks together

Start here when setting up a product. Adopt each framework where its scope applies and record the product's choices with the repository that owns them.

| Framework | Owns | Use it when |
| --- | --- | --- |
| [Kerbmark](engineering/adoption.md) | Shared engineering defaults for design, verification, CI, and delivery | Choosing conventions and checks for a component or product. |
| [Umbrella](https://github.com/d1ys3nk0/umbrella#choose-a-workspace-type) | Workspace layout, repository boundaries, and documentation placement | Assembling independent repositories into one product workspace. |
| [Meridian](infrastructure/meridian.md) | Environment and deployment identity, topology, and resource ownership | Deciding where a product runs and which scope owns its state and dependencies. |
| [Armada](https://github.com/d1ys3nk0/armada#layer-entrypoints-and-target-selection) | Ansible inventory, layers, variables, roles, and operational entrypoints | Using Ansible to provision and operate infrastructure. |

Use the [reviewed framework baseline](engineering/adoption.md#reviewed-framework-baseline) to select compatible documentation revisions and maintain adoption records. Follow the [worked product workflow](engineering/product-workflow.md) from a service change through CI, target selection, and an infrastructure preview.

## Design, implementation, and verification

| When you need to | Read |
| --- | --- |
| Choose a default for a new project or apply a shared convention | [Shared and local adoption](engineering/adoption.md) |
| Resolve a design choice or reconsider an agreed decision | [Technical judgment](engineering/design.md#technical-judgment-and-agreed-decisions) |
| Simplify a design or decide when to reuse code | [Simplicity and reuse](engineering/design.md#simplicity-and-reuse) |
| Design for failure or maintainability | [Reliability and maintainability](engineering/design.md#reliability-and-maintainability) |
| Choose module boundaries or coordinate services through events | [Module boundaries](engineering/design.md#module-boundaries-and-dependencies) and [event-driven collaboration](engineering/design.md#event-driven-collaboration) |
| Define or change an API, CLI, configuration key, or other contract | [Contracts and compatibility](engineering/design.md#contracts-and-compatibility) |
| Consume a contract from another repository | [Contract snapshots](engineering/contract-snapshots.md) |
| Design responsive UI composition, alignment, or spacing | [UI layout](engineering/ui-layout.md) |
| Trace a defect to its cause | [Root-cause analysis](engineering/root-cause-analysis.md) |
| Plan a backfill, schema change, or potentially destructive operation | [Data safety](engineering/design.md#data-safety) |
| Change code, comments, logging, or error handling | [Implementation](engineering/implementation.md) |
| Choose checks or tests for a behavior change | [Behavior and regression coverage](engineering/verification.md#behavior-and-regression-coverage) and [verification categories](engineering/verification.md#verification-categories) |
| Select regular, smoke, or full tests | [Test selection modes](engineering/verification.md#test-selection-modes) |
| Evaluate a system or review completion evidence | [Evaluation integrity](engineering/verification.md#evaluation-integrity) and [review and completion](engineering/verification.md#review-selection-and-completion) |

## Tooling and formatting

| When you need to | Read |
| --- | --- |
| Select developer tools or organize a Python package | [Engineering tooling](tooling/developer-tools.md) |
| Organize Taskfiles or name setup, preview, and verification commands | [Taskfile namespaces and layout](tooling/taskfiles.md) |
| Create or rename a reusable agent skill | [Skill naming](engineering/adoption.md#skill-naming) |
| Write or edit Markdown | [Markdown source layout](formatting/markdown.md) |
| Write YAML or a template that emits YAML | [YAML source layout](formatting/yaml.md) |

## Git and documentation

| When you need to | Read |
| --- | --- |
| Edit or stage changes in a shared checkout | [Concurrent repository edits](git/concurrent-edits.md) |
| Write a commit message or coordinate a shared dependency release | [Commits and dependency delivery](git/commits.md) |
| Update documentation, record a decision, or move a plan | [Documentation accuracy and provenance](documentation/accuracy.md) |
| Choose a workspace layout, place workspace documentation, or set up Workspace Steward | [Umbrella Framework](https://github.com/d1ys3nk0/umbrella) |

## Infrastructure and delivery

| When you need to | Read |
| --- | --- |
| Define environment identity, deployment placement, availability, or state boundaries | [Meridian quick reference](infrastructure/meridian.md) |
| Assign configuration ownership, remove aliases, or define feature toggles | [Configuration and operational identity](infrastructure/configuration.md) |
| Address a local VM, container, or controller endpoint | [Local environment addressing](infrastructure/configuration.md#local-environment-addressing) |
| Declare or upgrade managed environment dependencies | [Declarative dependencies](infrastructure/dependencies.md) |
| Change a container image or verify image dependencies | [Container dependencies](infrastructure/containers.md) |
| Define CI jobs, their Task commands, or reusable pipeline components | [CI/CD and shared tooling](infrastructure/cicd.md) |
| Design infrastructure convergence, assessment, or migrations outside Ansible | [Infrastructure operations](infrastructure/migrations.md) |
| Set up an Ansible repository or work with playbooks, roles, inventories, Vault, or migrations | [Armada Framework](https://github.com/d1ys3nk0/armada) |
