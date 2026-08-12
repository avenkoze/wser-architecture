# ADR 0009: Bound native resource and mail panels

- **Status:** Accepted
- **Date:** 2026-08-11

## Context

Wser plans sidebar panels for resource visibility and multiple mail accounts.
Both surfaces need privileged information, but the sidebar must not become a
general privileged script environment. Resource sampling can create its own
overhead, while a mail panel introduces credentials, remote content, account
partitioning, and provider-specific network access.

## Decision

The sidebar is a renderer. Parent-process services own privileged browser and
account state and expose narrow, serializable contracts.

The resource service:

- samples native process information only after an explicit request and does
  not start a default polling timer;
- returns bounded process type, process ID, memory, and sampled CPU-rate data,
  excluding origins, URLs, windows, threads, and privileged objects;
- maps settings only to validated, reversible tab-sleep and warning policies;
- delegates manual tab sleeping and memory reclaim to maintained browser
  signals; and
- does not claim operating-system hard CPU or RAM limits, kill processes, or
  expose an unrestricted preference bridge.

The future mail service:

- is opt-in per provider and account, starts no provider connection before
  setup, and requests the least provider scopes needed for the selected
  feature;
- keeps OAuth tokens in an operating-system-backed or maintained browser
  credential store, never in preferences, DOM state, page storage, logs, or
  the visual prototype;
- partitions account state and cached metadata, excludes private windows by
  default, and deletes tokens and account cache on revocation;
- returns sanitized structured message summaries rather than provider HTML;
- blocks remote message images and other active content by default and opens a
  full message through an isolated native browser path; and
- uses reviewed provider endpoints only. It never injects into webmail pages,
  reads page credentials, or broadens itself into a general browsing-data
  bridge.

Provider selection, OAuth application registration, redirect ownership, token
revocation, and retention periods require a separate reviewed implementation
decision before account connection can ship.

## Verification

Resource integration must prove that reports are plain serializable data,
first and subsequent CPU samples behave correctly, unsupported controls are
rejected, policy ranges are enforced, and manual actions delegate to maintained
browser mechanisms. Visible-section sampling must stop when the section closes,
the native tab rail collapses, the sidebar is hidden, or the element detaches;
broader or faster sampling requires a measured overhead budget.

Mail integration must use mocked providers until explicit provider authority
exists. Release verification then requires scope and redirect review, secret-
storage inspection, account-isolation and logout tests, hostile-message
sanitization tests, private-window exclusion, deny-proxy endpoint inventory,
and a manual provider revocation test.

Neither panel may be described as complete merely because its web-studio
surface exists.

## Consequences

- Resource UI can evolve without moving process privileges into the sidebar.
- Wser exposes reversible resource controls honestly instead of presenting
  unsupported hard limits.
- Mail visual work may continue, but real accounts remain blocked on provider
  choices, OAuth authority, and the verification contract above.
- New panel capabilities require explicit fields and actions; there is no
  generic privileged message channel.

## Initial evidence

- The native resource service is event driven and coalesces concurrent
  on-demand samples.
- Focused browser coverage verifies serializable snapshots, CPU-rate deltas,
  policy validation, rejection of a hard-CPU-limit field, native tab sleeping,
  and memory reclaim delegation.
- The compact resource section renders immediately below the native vertical
  tabstrip in the existing rail; no second sidebar panel or navigation hierarchy
  is registered. It samples only while expanded and visible, and delegates its
  reversible settings and actions to the resource service. Focused normal and
  accessibility-check runs cover placement, lifecycle, and control delegation.
