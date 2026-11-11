# Infrastructure operations

Read when designing tool-independent infrastructure convergence, assessment or migrations. For Ansible playbooks and migrations, follow [Armada](https://github.com/d1ys3nk0/armada#migrations). Apply [shared/local adoption](../engineering/adoption.md) and the applicable operation and delivery authority.

Use the [Meridian Framework](https://github.com/d1ys3nk0/meridian/blob/main/README.md) when defining environments, placement, Cell roles or failure domains; concrete targets and supported controller roles remain project-owned.

Separate recurring convergence of desired configuration, explicit dependency updates, read-only assessment and historical migrations. Assessment must not repair, acquire mutation locks or advance applied-state markers. Check mode is a read-only preview only when every invoked operation actually avoids mutation. Validate the effective target and policy before accessing credentials or performing remote effects.

Keep historical detection, conversion and cleanup outside recurring convergence logic. Retain each migration and its exclusive helpers until application and verification are evidenced for every affected host, including inactive and independently operated hosts. Missing evidence remains pending; shared helpers remain until no migration references them.

## Idempotent migrations

Every migration must be idempotent independently of its completion record and safe to retry after interruption. Use idempotent operations where sufficient; otherwise inspect actual historical state and validate prerequisites before performing side effects, including rollback snapshots, replacement installation, external requests and service or scheduling changes. Keep historical applicability checks with the migration, outside declarative convergence. Revalidate before mutation when concurrent changes can invalidate the inspection.

Distinguish three outcomes: a recognized historical state requires the verified transition; absent historical state or a verified completed transition succeeds without infrastructure changes; unknown, unreadable, conflicting, busy or damaged state fails with actionable diagnostics. Absence of one historical artifact must not conceal an interrupted transition. Inspect retained snapshots and remaining artifacts, then resume safely or refuse while preserving recovery evidence. Do not equate failed inspection with lack of applicability.

A successful live no-op may be recorded as completed by the normal migration controller, using its ordinary coordination lock and bookkeeping. Read-only previews must not create those records or mutation locks and must not run mutating probes. Test fresh-state no-ops, known historical transitions, repetition without reliance on completion records, interrupted execution, refusal paths and preview behavior. Check actual side effects as well as reported change counts; application and independent acceptance remain separate obligations.
