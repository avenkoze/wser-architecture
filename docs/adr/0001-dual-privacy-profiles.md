# ADR 0001: Use two mutually exclusive privacy profiles

- **Status:** Accepted
- **Date:** 2026-08-03

## Context

Users need a strong default privacy posture without losing access to social
sign-in, payment, conferencing, and embedded-media workflows. Independent
privacy switches can also create contradictory states in which multiple modes
are simultaneously enabled or disabled.

## Decision

Wser will expose two mutually exclusive protection profiles:

- **Private** is the default. It combines the strongest compatibility-conscious
  tracking and fingerprinting protections supported by the maintained browser
  platform.
- **Socialise** prioritizes compatibility for identity, communication, payment,
  and social-media workflows without disabling the shared security baseline.

The interface may use switch-like controls, but the underlying preference is a
single profile value. A profile change is therefore atomic.

## Shared baseline

Both profiles retain:

- signed advertisement and tracker filtering;
- site-partitioned third-party state;
- HTTPS-first navigation;
- safe-browsing protections;
- Global Privacy Control;
- extension signing, process isolation, and sandboxing.

## Consequences

- Socialise is not an unprotected mode.
- Private can use stricter social and email tracker classification.
- Site breakage is handled with visible, site-scoped recovery before any global
  reduction in protection is considered.
- The implementation must map each profile to a versioned preference contract
  so upgrades remain deterministic.

## Verification

Both profiles require separate privacy and compatibility test runs. Private is
the product default only after clean-profile tests confirm that its complete
preference contract is active.

