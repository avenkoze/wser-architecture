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

Version 6 extends that contract to the four first-party comparison surfaces
used by Cover Your Tracks: canvas, WebGL, offline audio, and reported hardware
concurrency. The new audio and hardware surfaces use separate domain separators
over the engine's session key and full document origin, so sibling hosts do not
collapse to the same value. Offline audio receives a deterministic,
signal-preserving perturbation of at most 0.01% only after an
`OfflineAudioContext` render; live audible output is untouched. Hardware
concurrency is selected from common even desktop buckets between 2 and 16 and
is deliberately decoupled from the physical core count; Socialise retains
Firefox's true value. Full Private also disables remotely distributed FPP
web-compat exceptions, while Socialise retains them.

Version 7 makes the fingerprint posture a versioned, fail-closed surface
contract. Every maintained engine fingerprint target must be classified as
origin/session randomized, standardized, superseded by a named replacement,
permission-gated, state-partitioned, or deliberately compatible. Full Private
continues to select all maintained targets by default; a source validator fails
if a newly introduced target is absent from the Wser inventory. The running
profile publishes the corresponding fingerprint-contract version so live
audits cannot silently evaluate a different policy revision.

This design was informed by Helium's public session-token/per-origin-token
architecture, then implemented independently in Gecko. Helium is GPL-3.0 and
Wser's Gecko changes remain MPL-2.0; source code was not copied between them.

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

The version 7 release gate requires:

1. complete preference-contract tests for both profiles and invalid fallback;
2. stable repeated canvas extraction within each tested top-level site;
3. different keyed canvas output across distinct top-level sites;
4. stable repeated offline-audio output within a tested top-level site and
   different keyed audio output across tested origins, including sibling hosts;
5. hardware-concurrency values restricted to plausible even buckets and keyed
   variation across a multi-origin test set;
6. distinct Full Private and Socialise outputs under equivalent conditions;
7. no Full Private ICE candidate without a configured relay, and no raw local
   host candidate in either profile;
8. separate timer-resolution evidence for privacy and compatibility behavior;
9. repeated clean-profile external tests before any public population or
   comparative privacy claim.
10. complete source-target classification and agreement between the running
    profile's fingerprint-contract version and the audit contract.

The first clean-profile v6 external run made Cover Your Tracks classify canvas,
WebGL, audio, and hardware concurrency as randomized and report a randomized
fingerprint. This is verification evidence for that build and session, not a
guarantee that every external dataset or future test revision will use the same
classification.

## Consequences

- Full Private prioritizes unlinkability and may reduce site compatibility or
  graphics performance.
- Socialise is still protected; it is not an unprotected or legacy mode.
- External fingerprint classifications may remain “unique” or “nearly unique”
  for a low-population development version even when cross-site keyed behavior
  is working correctly.
- The two modes must be evaluated separately. Combining their best results into
  one browser score would be misleading.

## References

- [Helium Chromium source](https://github.com/imputnet/helium-chromium)
- [Helium noise-token architecture](https://github.com/imputnet/helium-chromium/blob/main/patches/helium/core/noise/core.patch)
- [Helium hardware-concurrency patch](https://github.com/imputnet/helium-chromium/blob/main/patches/helium/core/noise/hardware-concurrency.patch)
- [Helium audio patch](https://github.com/imputnet/helium-chromium/blob/main/patches/helium/core/noise/audio.patch)
