# A worked product workflow

Unicorn is a fictional product with an application backend and an Ansible infrastructure repository. This example follows a Core service change through CI and an infrastructure preview. The project owns the example command syntax and target mappings.

The examples use `uncrn`, a short, distinctive abbreviation of Unicorn. Use the same slug in commands, resource names, and documentation so it stays easy to type and search for.

## Assemble the workspace

Use an [Umbrella system-oriented workspace](https://github.com/d1ys3nk0/umbrella#choose-a-workspace-type) and register `svc-core` and `iac-ansible` as independent children. The root’s `docs/engineering/architecture.md` records the product topology and links to the integration procedure. The `svc-core` repository owns the backend, its tests, and its CI. The `iac-ansible` repository owns the inventory, playbooks, and operator guide, including the target arguments and the resources each operation can change.

## Verify the service change

Suppose Core adds a background export worker. In `svc-core`, run the repository’s `task verify:lint` and `task verify:test`. The latter includes a test that an accepted export request eventually produces a retrievable file in its own Space. CI invokes those same checks and supplies the test dependencies. If the checks pass, CI can build the release artifact under the repository’s delivery policy. See [Taskfile namespaces](../tooling/taskfiles.md) and [CI/CD](../infrastructure/cicd.md).

## Resolve the infrastructure target

In [Meridian’s identity model](../infrastructure/meridian.md#qualified-identities), Unicorn uses World `uncrn` and Realm `lab`. The `sbx` and `tst` application environments both deploy to `(uncrn, lab, hst)`. The `sbx` environment also deploys to `(uncrn, lab, vgt)`. PostgreSQL is Realm-shared and each Space uses its own logical database. An export file store dedicated to `sbx` serves that Space in both Cells. Unicorn operates and recovers that store at Space scope.

The product’s integration procedure links to the operator guide in `iac-ansible`, which documents the project’s implementation of [Armada’s target mapping](https://github.com/d1ys3nk0/armada#mapping-meridian-identities-to-ansible-targets). Before rolling out the worker, an operator can preview convergence of its host prerequisites from that repository using the example command.

```sh
task play:setup:check -- uncrn lab hst app
```

In this example the first three arguments select the Cell and `app` selects the layer. Placement configuration associates `hst` with Area `edg`. The dispatcher resolves that combination to `inventories/lab-edg/hosts.yml`, `playbooks/app/setup.yml`, and the `hst_app` inventory host group. It validates the combination and the host selection before accessing credentials. This is a Cell-level infrastructure preview. Installing the worker for `sbx` is a separate deployment operation whose selection also includes the Space and the release artifact.

## Check the boundaries

| Scenario | Expected result |
| --- | --- |
| A separate installation is added in another Area of `(uncrn, lab)`. | It gets a distinct Cell slug, such as `hst-remote`; the selector `uncrn lab hst` still identifies only the original Cell. |
| Cell `(uncrn, lab, k8s)` spans Areas `east` and `west`. | Both Areas belong to one Cell and each Space has one logical deployment in that Cell. Whole-Cell operations account for affected hosts in both Areas. |
| An operator selects only the `east` hosts of that multi-Area Cell. | Locks coordinate with overlapping whole-Cell operations, and partial success cannot mark a whole-Cell migration complete. |
| An operator resets `tst`. | The reset clears only `tst` resources. The `sbx` database and export files survive, and the shared PostgreSQL service stays up. |
| `sbx` runs in both Cells. | Both placements reach the same Space-owned export file store through the product’s documented access and recovery contract. |
| A pre-convergence migration would clean up a historical resource after cutover. | The preview writes no completion record and takes no mutation lock. If a live migration run confirms the cutover is still pending, the migration reports deferred, stays pending, and is retried on the next eligible run. |

Keep the product’s acceptance evidence with the procedure or component that owns the behavior. The [migration outcomes](../infrastructure/migrations.md#migration-outcomes) define when a controller may record completion.
