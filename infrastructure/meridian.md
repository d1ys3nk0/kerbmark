# Meridian quick reference

Source revision `51929bf887f681265892c9d9b6c4b1e6718c501b`. See the [canonical Meridian README](https://github.com/d1ys3nk0/meridian/blob/main/README.md) for the full framework.

## Identity dimensions

Use the relative order **Unit, World, Realm, Space, Area, Cell** when presenting these dimensions. An operation needs only the dimensions it consumes. Document the fixed enclosing scope whenever an identifier omits a dimension.

| Dimension | Meaning |
| --- | --- |
| **Unit** | A component such as an application backend, frontend, or infrastructure unit. |
| **World** | The product or system. |
| **Realm** | An operational purpose within a World, such as production or collaborative development. |
| **Space** | A logical application and state namespace within a World and Realm. |
| **Area** | An infrastructure area within a World and Realm that contains one or more Cells. |
| **Cell** | An installation or logical deployment target within an Area. Its final slug is opaque. |

A **Service** is a runtime service of a Unit, such as an API server or worker. One Unit can run several Services, and each Service can run several processes or replicas.

An **availability zone (AZ)** is a physical failure domain. A Cell may occupy one AZ or span several AZs or datacenters. Record provider zone names and shared physical risks separately from logical placement.

## Qualified identities

| Identity | Qualified tuple |
| --- | --- |
| Application environment | World + Realm + Space |
| Deployment target | World + Realm + Area + Cell |
| Logical deployment | World + Realm + Space + Area + Cell |

A deployment associates one environment with one target in the same World and Realm. A Space may deploy to several Cells, and a Cell may host several Spaces. Each environment has at most one logical deployment per Cell. Its Units, Services, nodes, replicas, and successive releases belong to that deployment.

### State ownership and Cell roles

Application state belongs to its World, Realm, and Space. Scope placement resources to their qualified target. A dependency that can safely isolate Spaces can serve the whole World and Realm as one logical instance.

The Cell slug is unique within its World, Realm, and Area and may repeat in another scope. Cell slugs can resemble provider or zone names. Resolve roles and physical placement from the target configuration. Master and replica responsibility, membership, and the descriptive role `cluster` are installation properties. Changing these properties preserves Cell identity. Each controller defines its supported roles and operations.
