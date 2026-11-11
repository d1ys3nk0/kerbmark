# Meridian quick reference

Source revision `cac3ed6dce070aa159dcf1c0342ea1fad7f065eb`. See the [canonical Meridian README](https://github.com/d1ys3nk0/meridian/blob/cac3ed6dce070aa159dcf1c0342ea1fad7f065eb/README.md) for the full framework at this revision.

## Identity dimensions

Use the relative order **Service, Unit, World, Realm, Space, Area, Cell** when presenting these dimensions. An operation needs only the dimensions it consumes. Document the fixed enclosing scope whenever an identifier omits a dimension.

| Dimension | Meaning |
| --- | --- |
| **Service** | A runtime service of a Unit, such as an API server or worker. One Unit can run several Services, and each Service can run several processes or replicas. |
| **Unit** | A component such as an application backend, frontend, or infrastructure unit. |
| **World** | The product or system. |
| **Realm** | An operational purpose within a World, such as production or collaborative development. |
| **Space** | A logical application and state namespace within a World and Realm. |
| **Area** | An infrastructure placement scope within a World and Realm. |
| **Cell** | An installation or logical deployment target that can occupy one or more Areas. Its slug is opaque. |

An **availability zone (AZ)** is a physical failure domain. A Cell may occupy one AZ or span several AZs or datacenters. Record provider zone names and shared physical risks separately from logical placement.

## Qualified identities

| Identity | Qualified tuple | URI pattern |
| --- | --- | --- |
| Logical application environment | World + Realm + Space | `{world}-{realm}-{space}` |
| Server | World + Realm + Area + Node ID | `{realm}-{area}-{nodeId}.{world}` |
| Deployment Cell | World + Realm + Cell | `{world}-{realm}-{cell}` |

Record each Cell's Areas in placement configuration. The same Cell URI identifies the target across all its Areas. In the server URI, `nodeId` identifies the node within its World, Realm, and Area.

A logical deployment associates one Space with one Cell in the same World and Realm. Its qualified tuple is World + Realm + Space + Cell. A Space may deploy to several Cells, and a Cell may host several Spaces. Each environment has at most one logical deployment per Cell. Its Units, Services, nodes, replicas, and successive releases belong to that deployment.

### State ownership and Cell roles

Application state belongs to its World, Realm, and Space. Scope placement resources to their qualified target. A dependency that can safely isolate Spaces can serve the whole World and Realm as one logical instance.

The Cell slug is unique within its World and Realm and may repeat in another World or Realm. Cell slugs can resemble provider or zone names. Resolve roles and physical placement from the target configuration. Master and replica responsibility, membership, and the descriptive role `cluster` are installation properties. Changing these properties preserves Cell identity. Each controller defines its supported roles and operations.
