# ADR 0012: Ship Wser Shield as a visible removable extension

- **Status:** Accepted
- **Date:** 2026-08-24

## Context

Wser needs one first-party surface where users can inspect site-risk evidence,
understand observed tracker destinations, review sites flagged during use, and
control site-specific exceptions. Hiding this surface in privileged browser
code would make its permissions, state, and removal behavior less legible. A
second separately branded auditing extension would duplicate the same product
role.

At the same time, a removable extension cannot be the sole owner of browser
security. Phishing and malware reputation, certificate errors, HTTPS upgrades,
download protection, sandboxing, and extension signing are maintained engine
responsibilities and must survive extension removal.

## Decision

Wser Shield is the single first-party protection extension. Release builds
install its signed XPI through Firefox's distribution-extension mechanism on a
fresh profile. It remains visible in the toolbar and add-on manager, and the
user may disable or remove it. A recorded user removal is not silently reversed
on later starts or application upgrades.

The earlier site-auditor codename is retired rather than shipped as a second
extension. Its verified detector work may be migrated into Wser Shield.

Shield owns explainable site reports, observed third-party destination
categories, a clearable local flagged-site history, user-visible warnings, and
future authenticated Wser rule packages. Heuristic observations do not hard
block navigation by default. Any Wser rule that can block navigation must be
versioned, authenticated, rollback protected, and covered by browser-level
bypass and removal tests.

Firefox Safe Browsing, TLS/certificate interstitials, HTTPS-First, download
protection, sandboxing, and extension signing remain authoritative native
layers. Ad and tracker filtering remains a separate extension responsibility.

Full Private keeps Shield history in memory for the current session by default.
No cookie values, storage values, form values, or URL query values are stored.
A future remote reputation design may not send full visited URLs without a new
privacy review and explicit user data contract.

## Consequences

- Users can see what Shield is doing, inspect its evidence, and remove it.
- Removing Shield does not remove the browser's maintained security core.
- Site reports distinguish native verdicts, authenticated Wser rules, and local
  heuristics instead of presenting one opaque score.
- The product does not claim arbitrary malware inspection or certainty from
  browser-side heuristics.
- Release packaging must verify signature, fresh-profile install, disable and
  removal controls, removal persistence, local-data clearing, warning bypass,
  and coexistence with native Safe Browsing.

## Verification

The current source gate covers manifest identity, visible toolbar registration,
declared zero data collection, local detector fixtures, bounded session history,
and WebExtension lint. Automatic navigation blocking and persistent Socialise
history remain unavailable until real-browser integration tests cover their
security and privacy contracts.
