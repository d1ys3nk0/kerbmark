# Container dependencies

Read when changing image dependencies or preparing container builds. Apply [declarative dependencies](dependencies.md); change the image declaration and build context first, preserving versions and lock files.

Keep agent memory, credentials and user data in their own volumes. Never put tokens in images or build arguments. Do not install image-level dependencies into directories hidden by state volumes.

Container agents prepare changes, checks and a handoff to an authorized host operator. A repository mount does not authorize host execution or application. Verification and reporting must distinguish the prepared declaration, the image build and the running container.
