# Configuration and operational identity

Read when designing configuration ownership, operational identity, capability boundaries or feature toggles. Apply [shared/local adoption](../engineering/adoption.md); existing names and toolchains do not migrate automatically.

## Identity and ownership

Use [Meridian’s state and placement model](https://github.com/d1ys3nk0/meridian/blob/main/README.md#state-placement-and-metadata) to assign configuration and resources to the scope that owns them. Map the shared identities to project-owned configuration inputs where needed.

Use [Meridian’s shared dependencies and Space isolation](https://github.com/d1ys3nk0/meridian/blob/main/README.md#shared-dependencies-and-space-isolation) to define logical data boundaries and dependency ownership.

Assign configuration to the owner and scope responsible for its intended behavior, not merely to the widest scope where values happen to match. Document sources, precedence, merge and replacement semantics, and the effective non-secret values or selectors a consumer uses. Preserve whole-value replacement versus deep merge explicitly; no universal merge is implied. Keep concrete topology choices out of generic shared maps and nested conditional branches. Tracked configuration owns non-secret policy and defaults; restricted operator or secret-provider inputs own credentials. Vendor-defined key names retain their vendor contract. Keep secrets distinct from ordinary configuration and respect their access boundaries. Exercise configuration selection and merge logic with synthetic cases under [verification](../engineering/verification.md).

## Low coupling and high cohesion

Keep logic and configuration together around the capability they control. This requirement applies to all maintained code and configuration, including applications, scripts, Ansible roles and playbooks, and Terraform modules and root configurations. Give each independently configurable capability one explicit control. Enabling or disabling one capability must not silently change another. Prefer a direct setting when it is sufficient.

Keep reusable components focused on their own inputs and shared interfaces. Express intentional combinations in the caller or deployment configuration that owns the combination. Document and validate dependencies that require capabilities to operate together.

Apply these rules to new code and configuration. When modifying existing code, look for opportunities to reduce coupling in the affected area. Refactor where it improves the design, update affected callers explicitly to preserve behavior, and leave broader migrations as separate work. When two capabilities are independently configurable, verify both mixed states, with each enabled while the other is disabled.

## Redundant configuration indirection

Give each setting one authoritative declaration and keep each default at the layer that handles omission. Prefer direct references and keep mappings that serve a real ownership, precedence, or compatibility boundary. An alias that only forwards a value within the same contract needs no separate name.

When reviewing or changing configuration, trace affected values from their declaration to their consumers. Automatically remove redundant aliases and repeated fallbacks within scope when the behavior is clear. Verify that callers, override precedence, merge or replacement behavior, and omission semantics still work. Flag uncertain cases for review.

## Local environment addressing

Local VM and container environments must keep their internal service and controller endpoints independent of the host’s current Wi-Fi, Ethernet, VPN or mobile-network address. Use a declared host-only network, runtime service discovery or another stable address reachable from the intended consumers. Host loopback is suitable only when those consumers share its network namespace. Keep the address in one owned configuration contract and derive registry, storage, TLS and runtime-profile inputs from it; do not discover a physical-interface address as the default or require operators to copy it into multiple settings. Restrict published local services to their intended network.

A change of external network must not require rebuilding application images, rotating credentials, recreating data volumes or renaming runtime identities. Validate reachability from the guests or containers, including with the external connection changed or unavailable; distinguish required internet access for external services and downloads from communication within the local environment. When recovering an existing environment with unstable endpoints, preview a supported rebind, preserve image digests and state, and regenerate endpoint-bound configuration and evidence rather than reusing stale proofs. Concrete network ranges and provider behavior remain project-owned.

## Feature toggles

For a new project-owned feature environment toggle, first choose the baseline from common feature usage. The flag defaults to false: use `*_DISABLED` when the baseline is on and `*_ENABLED` when it is off. Omitted or empty values mean false. Optional shared capabilities are off by default and enabled explicitly by consumers that need them. Vendor-defined APIs, addressing parameters, runtime state markers and command switches are outside this convention. Renaming existing flags and preserving explicit behavior require a separate authorized migration.
