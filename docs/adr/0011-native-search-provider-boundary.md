# ADR 0011: Keep search-provider selection native and user controlled

- **Status:** Accepted
- **Date:** 2026-08-24

## Context

New-tab search needs to support normal and private-window defaults, user engine
choice, optional result-region filtering, and secure address navigation. A fork
can appear to change the bundled default by editing search configuration, but
the authoritative configuration is remotely distributed and signed. Weakening
signature verification or replacing that channel would expand a product choice
into a security-boundary change.

Building an independent query router in new-tab content would also duplicate
the maintained engine's URL, alias, private-default, and URI-fixup behavior. It
would expose provider endpoints and privileged navigation decisions to a less
trusted layer.

## Decision

Gecko's native search service remains authoritative for installed engines and
the user's normal/private defaults. The new-tab surface requests the active
engine name from the parent process, displays it, and opens the native Search
settings when the user wants to change providers.

Search and address input is resolved by the maintained URI-fixup service. Only
HTTP and HTTPS destinations may leave the new-tab action. Wser does not replace
signed search configuration, silently force an engine, create a query proxy, or
record query text.

An optional result-region preference may add fixed parameters only after the
parent process validates both the region code and an explicit provider-host
allowlist. Unknown engines, invalid regions, and direct navigation remain
unchanged. Result region is never represented as an IP, VPN, timezone, locale,
or anonymity control.

Search suggestions remain off by default and may be enabled by the user.

## Consequences

- Provider choice inherits maintained Gecko behavior and private-window
  semantics.
- Search configuration signature checks and other Remote Settings consumers are
  not weakened for branding or product defaults.
- A future provider recommendation must be explicit and user controlled; it
  cannot be implemented as a hidden lock.
- Provider-result quality and manual compatibility remain evidence tasks rather
  than architectural claims.
- Supporting a new region-aware provider requires an allowlist mapping and
  focused parent-process tests.

## Verification

The accepted implementation is covered by focused new-tab component tests,
Activity Stream unit coverage, parent-process URI/provider tests, localization
lint, and an incremental browser build. Public claims remain limited to those
versioned checks.
