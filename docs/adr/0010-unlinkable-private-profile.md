# ADR 0010: Separate unlinkability from compatibility

- **Status:** Accepted
- **Date:** 2026-08-23
- **Supersedes:** The Private fingerprint strategy in ADR 0001 and ADR 0006

## Context

The original Private profile standardized fingerprint surfaces toward a shared
crowd. That strategy is useful when a sufficiently large, consistently shipped
browser population shares the same values, but a development build cannot
guarantee that population. Wser also needs a genuinely distinct compatibility
profile for sites and benchmarks that depend on precise timers or direct
peer-to-peer connectivity.

Randomizing every observable call independently is not acceptable. It creates
internally inconsistent identities, breaks sites, and can itself become a
fingerprint. The unlinkability contract must instead be coherent within a site
while preventing a reusable value from following the user between sites or
browsing sessions.

## Decision

Wser keeps one mutually exclusive engine value with two policies:

- **Full Private** uses the maintained engine's top-level-site and browsing-
  session keyed fingerprinting defenses. Repeated reads within a site remain
  coherent, different top-level sites receive different keyed output, and
  returning to Full Private rotates the temporary randomization keys. Strict
  state partitioning, letterboxing, and relay/proxy-only WebRTC remain active.
- **Socialise** retains the maintained engine's site-keyed graphical defenses
  and shared safe-security baseline, but restores compatibility-oriented timer
  precision and permits public server-reflexive WebRTC candidates. It never
  permits raw local host candidates.

The implementation uses an explicit, reviewed fingerprint-target set. Targets
that would prompt, block extraction, force a constant value over a keyed value,
or duplicate another selected target are excluded when they conflict with the
coherent-output contract.

## Invariants

- Safe Browsing, HTTPS protection, state partitioning, process isolation,
  sandboxing, and extension signing are not weakened by either profile.
- The remote address of a normal HTTPS connection is outside browser
  fingerprint defenses. Hiding it requires a trusted VPN, Tor, or equivalent
  network relay.
- A profile label does not guarantee a public test site's population-dependent
  classification or a specific anonymity-set size.
- Existing documents may retain their old timer and fingerprint context until
  reloaded; the interface must request a reload after profile changes.

## Verification

The version 4 release gate requires:

1. complete preference-contract tests for both profiles and invalid fallback;
2. stable repeated canvas extraction within each tested top-level site;
3. different keyed canvas output across distinct top-level sites;
4. distinct Full Private and Socialise outputs under equivalent conditions;
5. no Full Private ICE candidate without a configured relay, and no raw local
   host candidate in either profile;
6. separate timer-resolution evidence for privacy and compatibility behavior;
7. repeated clean-profile external tests before any public population or
   comparative privacy claim.

## Consequences

- Full Private prioritizes unlinkability and may reduce site compatibility or
  graphics performance.
- Socialise is still protected; it is not an unprotected or legacy mode.
- External fingerprint classifications may remain “unique” or “nearly unique”
  for a low-population development version even when cross-site keyed behavior
  is working correctly.
- The two modes must be evaluated separately. Combining their best results into
  one browser score would be misleading.
