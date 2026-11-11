# Documentation accuracy and provenance

Read when updating supported usage, recording decisions, or moving documentation. For workspace placement and plan paths, see [Umbrella](https://github.com/d1ys3nk0/umbrella#documentation-lifecycle).

## Accuracy and lifecycle

Documentation must stay up to date and match actual system behavior. Update affected documentation alongside implementation and configuration changes, including changed usage, interfaces and operating procedures. Do not describe proposed behavior as already implemented.

Split mixed documents into current guidance, future work and historical evidence, retaining useful cross-links and provenance. Extract still-applicable guidance before archiving a document; neither age nor completion alone makes all its contents historical.

## Durable decisions

Record approved durable decisions when settled in the existing authoritative owner. Include context, scope, decision, rationale, status, origin and any expiry or supersession; preserve historical reversals with a superseding record. Distinguish proposals, agreed decisions, verified implementation and deployment: agreement alone establishes neither implementation nor verification or delivery. Keep records concise and retain relevant evidence and provenance.

## Plan provenance

When migrating an existing plan, preserve an existing valid timestamp prefix. Otherwise derive the timestamp from its earliest Git addition, following historical paths across renames, as a reproducible approximation of creation time; record its former path and source commit. If history supplies no usable creation time, use migration time and state that fallback explicitly. Avoid overwriting filename collisions by choosing a distinct descriptive slug.
