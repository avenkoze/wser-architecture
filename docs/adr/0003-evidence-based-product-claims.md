# ADR 0003: Require repeatable evidence for product claims

- **Status:** Accepted
- **Date:** 2026-08-03

## Context

Browser privacy and performance scores are sensitive to operating-system,
network, language, display, profile, extension, and test-version differences.
A single favorable run can be misleading, while optimization specifically for
one test can reduce real-world compatibility or create a more distinctive
browser fingerprint.

## Decision

Wser will separate product goals from published results. Comparative privacy,
compatibility, and performance statements require a repeatable test record.

The minimum comparison protocol is:

1. Record browser version, operating system, network, language, timezone,
   display configuration, profile state, and enabled extensions.
2. Test competitors under equivalent conditions and within the same test
   window.
3. Run each clean-profile scenario at least three times.
4. Preserve the detailed surface-level results, not only a summary badge.
5. Run the compatibility matrix after changing a protection surface.
6. Publish a comparative statement only when the collected evidence supports
   the exact wording.

## Prohibited shortcuts

- No fabricated benchmark values or unmeasured rankings.
- No test-specific identity spoofing that is inconsistent in ordinary use.
- No disabling certificate checks, safe browsing, sandboxing, process
  isolation, or extension signing to improve a score.
- No claim of complete or universal tracking prevention.

## Consequences

- Product UI shows “not measured” until verified results exist.
- A privacy test is an acceptance input, not the complete privacy model.
- Site compatibility failures are recorded alongside protection improvements.
- Claims may be narrower than the product ambition, but remain defensible.

