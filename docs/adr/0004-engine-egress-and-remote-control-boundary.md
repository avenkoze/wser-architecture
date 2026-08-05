# ADR 0004: Bound engine data egress and remote control

- **Status:** Accepted
- **Date:** 2026-08-05

## Context

Disabling visible telemetry settings does not by itself make a browser fork
independent. A maintained browser platform contains separate usage reporting,
region discovery, remote configuration, privileged component updates, crash
reporting, push messaging, and application update channels. Some are optional
product services; others deliver security and compatibility data.

Removing every remote service would reduce security. Leaving every upstream
channel unchanged would give an external party unnecessary control over a Wser
installation. The boundary must therefore be explicit and testable.

## Decision

Wser will apply the following engine boundary:

- independent usage reporting is disabled by default and verified on a clean
  running profile;
- browser-initiated IP-based region discovery is disabled while permissioned
  website geolocation remains available;
- upstream privileged system-add-on delivery is disabled until Wser owns a
  signed channel with rollback and transparency controls;
- remote new-tab code rendering is explicitly disabled;
- experiment delivery and health-reporting components are excluded from the
  browser build graph;
- the release configuration excludes telemetry reporting, crash upload, data
  reporting, and application updating until Wser-owned services and signing
  material exist;
- extension signing, process isolation, sandboxing, safe browsing, certificate
  protections, and remote-content signature verification remain enabled.

Remote Settings is not disabled globally. Security blocklists, certificate
state, fingerprinting compatibility, and similar maintained data remain
available through signed collections. Media components retain their signed
manifest and integrity verification path.

Push messaging remains available because it is required by notification and
communication workflows. Its behavior will be governed visibly by the Private
and Socialise profile contract instead of a hidden global exception.

## Verification

Release candidates must pass three independent checks:

1. A clean-profile runtime probe verifies the expected preferences and confirms
   that safe browsing, process isolation, and extension signing remain active.
2. A build-configuration probe verifies that forbidden release components are
   absent and mandatory security features are enabled.
3. A deny-proxy startup test inventories connection attempts and fails when an
   unreviewed endpoint appears.

The endpoint allowlist is reviewed whenever the maintained browser base or a
bundled extension is updated.

The Private idle-startup gate uses exact reviewed hostnames rather than broad
domain wildcards. A forbidden endpoint or any hostname outside that list makes
the gate fail closed. Security and blocking dependencies are identified by
their function and source manifest, not accepted merely because they belong to
a familiar provider.

## Consequences

- The temporary release configuration cannot provide automatic application
  security updates. It is not a public-release configuration until Wser owns a
  signed update channel.
- Upstream security data remains a deliberate dependency rather than being
  mislabeled as telemetry.
- New remote services require an architecture decision, a named owner, a data
  contract, and regression coverage.
- Hidden instrumentation that observes browsing only to populate upstream
  product metrics is excluded from the package when it provides no security or
  user-facing function. User-requested Sync remains separable from account-
  association measurement and unrelated product calls to action.
- Claims about zero network activity or the absence of hidden behavior remain
  prohibited without repeatable binary and network evidence.

## Current evidence

- Two fresh Private profiles passed the exact-host idle-startup policy with no
  forbidden or unlisted endpoints after bundled filter fallbacks were reviewed
  against their packaged asset manifest.
- A synthetic unknown CONNECT target was rejected by the same gate, confirming
  that an empty result was not caused by a permissive test implementation.
- A hidden search-redirect measurement extension with all-URL request access
  was removed from the package; a fresh runtime add-on inventory confirmed its
  absence.
- Account Sync remains available, while account/client association metric
  generation and unrelated upstream product panels are disabled by default.
