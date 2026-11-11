# CI/CD and shared tooling

Read when designing CI pipelines, shared components or delivery interfaces. Apply [shared/local adoption](../engineering/adoption.md) and preserve explicit operation and publication authority.

Use [Meridian’s qualified identities](meridian.md#qualified-identities) when choosing the scope of environment, deployment target, and CI tracking keys. Preserve existing input contracts until an explicitly authorized implementation change.

Task owns executable procedures shared with local development. CI invokes those procedures and owns scheduling, images, dependency preparation, secrets, variables, caches, artifacts and job dependencies. Do not invoke a hook runner in CI. Validate the effective target and policy before credentials or remote effects.

For new or explicitly migrated Task interfaces, follow [Taskfile namespaces and layout](../tooling/taskfiles.md), including verification job names that mirror the Task command they execute.

## GitLab profile

Document the interface from each job to its Task procedure, including inputs, outputs and required preparation. For a new repository-owned GitLab profile, default to a same-name Task invoked as `task "$CI_JOB_NAME"`; an existing or shared component may expose another explicit documented interface. Shared pipeline components document their call interface and do not hide consumer obligations.

Start with pipeline assembly in the repository. Extract stable reusable pipeline policy and generic images or tooling into independently versioned repositories when demonstrated reuse, clear ownership and release capacity justify it; this is an evolution, not an immediate migration. Pinned tooling prepared at job time is valid early on; a pinned prebuilt toolbox can serve mature reuse. Keep generic mechanisms separate from project policy and application consumer inputs; common tooling must not embed project inventory topology.

Keep the pipeline entrypoint focused on explicit assembly, with stage/job definitions in owning files. Generic executables validate syntax, required inputs and mechanics; pipeline policy validates supported targets and permissions before credential preparation. Consumers own their application Dockerfiles, deployment stacks, resource allocations and application variables. Reusable components distinguish cross-framework policy from framework commands, reports and caches; their interfaces include supported and rejected inputs and dependency expectations. Validate rearrangements against effective consumer configurations and test remote effects with stubs during local work. Specific partial-file reuse thresholds or project target metadata layouts are local conventions, not universal requirements.

Preserve immutable image/component pins and verify effective tools, artifacts, rules and gates when selecting images or extracting components. Tool preparation must retain integrity checks and remain separate from executable job behavior. A locally prepared image declaration, a published artifact and a successfully deployed consumer are separate claims requiring their own evidence.

For release ordering and consumer pins, follow [commit and dependency delivery](../git/commits.md).
