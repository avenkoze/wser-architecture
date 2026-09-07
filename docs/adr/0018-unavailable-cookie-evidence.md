# ADR 0018: Preserve unavailable cookie evidence

Status: Accepted

Date: 2026-09-07

## Decision

A failed cookie lookup is an unavailable measurement, not a measured zero. Unknown counts remain null and the popup identifies the score as based on incomplete evidence. A missing tab-store identifier must not fall back to another store.

The current cookie inventory is scoped to the top-level URL in its tab store and unpartitioned storage. Third-party partition inventory remains outside that scope; reporting must not imply a complete site-wide cookie count.

## Verification and limits

Automated tests distinguish failure from an empty successful lookup. An isolated development-browser test verified distinct cookies in two real containers and a controlled API failure. Existing scan, history and watchdog checks passed. Private-window, first-party isolation and third-party partition integration remain open; this decision does not claim those cases are covered.
