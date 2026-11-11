# Taskfile namespaces and layout

Apply this interface to new projects using Task and explicitly authorized Taskfile refactors. Existing projects retain their established commands until migration is requested; this standard does not authorize automatic alignment or override project-specific requirements.

Keep the root `Taskfile.yml` focused on includes, shared wiring and command discovery. Split executable procedures by responsibility into included Taskfiles under `.taskfiles/`. Use purpose-based namespaces, operation-first command names and colon-separated subcommands; pass explicit targets as arguments where applicable. Target grammar, execution modes and infrastructure boundaries remain project-local.

Every mutating operational Task has a non-mutating preview named by appending `:check` to the complete command: `reconcile:check` previews `reconcile`, and `reconcile:apply:check` previews `reconcile:apply`. Preview every invoked operation without mutation, including locks, applied-state markers and probes; report what would happen and refuse when safety cannot be established. Read-only status and verification commands do not need an additional preview. This naming rule does not authorize migrating unrelated existing interfaces.

Reserve `kit:*` for the repository's development toolkit and environment lifecycle. Use applicable commands such as `kit:setup`, `kit:reset`, `kit:clean`, `kit:conf`, `kit:install` and `kit:upgrade`; do not create empty commands merely to complete the set. Do not use `app:`, `local:` or `env:` for this responsibility in newly adopted interfaces. Keep infrastructure provisioning commands such as `setup` distinct from `kit:setup`.

For consumer-owned `deps:*:update` commands that install contracts from explicit local or remote Git sources, follow [contract snapshots between repositories](../engineering/contract-snapshots.md). Keep these mutations outside setup and verification aggregates.

Use the following verification hierarchy:

| Command | Responsibility |
| --- | --- |
| `verify` | Run all configured verification groups |
| `verify:lint` | Run all linters and static validation |
| `verify:lint:<check>` | Run one named check, such as `verify:lint:yaml` |
| `verify:test` | Run all test suites |
| `verify:test:<suite>` | Run one named suite, such as `verify:test:integration` |

Keep type, syntax and format checks individually identifiable. Namespaces group commands without changing their [verification categories or selection modes](../engineering/verification.md#verification-categories). Aggregates invoke their children, avoid duplicate execution and stop on failure; a leaf runs only its selected check and necessary prerequisites. Verification must not apply fixes. Expose formatting and other mutations through explicit commands such as `format`, outside the verification aggregate.

Keep executable check logic in Task procedures or repository-owned scripts invoked by those procedures. Hooks and CI invoke the same procedures; do not duplicate command lists in their callers. CI verification job names match the Task command they execute: `verify:lint`, `verify:test` or a selected leaf such as `verify:lint:yaml`. Do not add artificial `:all` suffixes or split CI jobs merely to mirror every available leaf. CI retains ownership of preparation and execution policy under the [CI/CD standard](../infrastructure/cicd.md).
