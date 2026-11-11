# Declarative dependencies

Read when installing or updating dependencies in a managed environment. Declare installations and upgrades in the environment's canonical definitions before an authorized operator applies them, scoped to the requested components and prerequisites. Do not install dependencies only into the current runtime.

Use the target environment's declarative mechanism; macOS-specific tooling is not a Linux requirement. Removals and upgrades require an explicit task; a package missing from a list does not authorize deleting it. Respect host/container access and application permissions.

Distinguish a prepared declaration from an applied installation. Verify executable/import availability and actual runtime state before claiming completion.
