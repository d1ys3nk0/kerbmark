# Engineering tooling

Read when running shell commands, choosing or changing developer tooling, CI checks, or language and package structure. Apply [shared/local adoption](../engineering/adoption.md), preserving local requirements and established tooling, package layout and naming patterns even when they are not explicitly documented. Shared choices below fill only remaining gaps.

Use canonical project wrappers and automation locally. Use ast-grep for syntax-aware structural searches or rewrites; use rg for plain text and file discovery. Use mise when a specific dependency version is required.

Prefer maintained tools already available in the project or supported by its platform when they meet the operation’s requirements. For example, use rclone for S3-compatible file transfers when it supports the required permissions, integrity checks and overwrite behavior. Keep project automation focused on orchestration and use custom transfer code only for requirements the maintained tool cannot meet. Apply this preference to new or explicitly revised workflows.

For a new project without a selected toolchain, use Task for executable developer and CI procedures and Lefthook to select local hook checks. Keep repeatable commands in [Task](taskfiles.md) or repository-owned scripts; hooks invoke those procedures. Existing projects retain their established toolchain until a separately authorized migration.

For CI execution ownership and the job-to-Task interface, use [CI/CD](../infrastructure/cicd.md); keep execution logic in its canonical Task procedure rather than duplicating it in pipeline YAML.

For Python, prefer PEP 420 implicit namespace packages when tooling allows: omit unnecessary `__init__.py` and import concrete modules rather than package-level re-exports. Prefer explicit PostgreSQL naming (`pg_` or `postgres_`) over generic `db_` or `database_` names for variables and settings.
