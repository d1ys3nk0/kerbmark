# Infrastructure operations

Read when designing tool-independent infrastructure convergence, assessment or migrations. For Ansible playbooks and migrations, follow [Armada](https://github.com/d1ys3nk0/armada#migrations). Apply [shared/local adoption](../engineering/adoption.md) and the applicable operation and delivery authority.

Use the [Meridian quick reference](meridian.md) when defining environments, placement, Cell roles or failure domains; concrete targets and supported controller roles remain project-owned.

Separate recurring convergence of desired configuration, explicit dependency updates, read-only assessment and historical migrations. Assessment must not repair, acquire mutation locks or advance applied-state markers. Check mode is a read-only preview only when every invoked operation actually avoids mutation. Validate the effective target and policy before accessing credentials or performing remote effects.

Keep historical detection, conversion and cleanup outside recurring convergence logic. Retain each migration and its exclusive helpers until application and independent verification are evidenced for the full affected scope, including inactive and independently operated hosts or targets. Missing evidence remains pending; shared helpers remain until no migration references them.

## Idempotent migrations

Every migration must be idempotent independently of its completion record and safe to retry after interruption. Use idempotent operations where sufficient; otherwise inspect actual historical state and validate prerequisites before performing side effects, including rollback snapshots, replacement installation, external requests and service or scheduling changes. Keep historical applicability checks with the migration, outside declarative convergence. Revalidate before mutation when concurrent changes can invalidate the inspection.

### Migration outcomes

| Outcome | Condition | Completion |
| --- | --- | --- |
| Applied | The transition ran and its result was verified. | May record completion. |
| Verified no-op | Inspection confirmed a known fresh state or an already completed transition. | May record completion. |
| Deferred | Inspection confirmed that a known prerequisite, such as convergence, is still pending. Report the prerequisite and retry on the next eligible run. | Leave pending. |
| Failed | Inspection or execution failed, or the state is unknown, unreadable, conflicting, busy, or damaged. Report actionable diagnostics and preserve recovery evidence. | Leave pending. |

Record completion only after verifying the outcome across the full scope covered by that record. A record for a target spanning several hosts must account for every affected host in that target. Keep execution completion and independent acceptance evidence distinct.

Absence of one historical artifact must not conceal an interrupted transition. Inspect retained snapshots and remaining artifacts, then resume safely or refuse while preserving recovery evidence. Failed inspection leaves the migration pending as failed.

Read-only previews must not create completion records, acquire mutation locks, or run mutating probes. Test fresh-state no-ops, known historical transitions, repetition without relying on completion records, interrupted execution, deferral, refusal paths, and preview behavior. Check actual side effects as well as reported change counts.
