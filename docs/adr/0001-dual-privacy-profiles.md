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

- **Private** is the default. It targets a standardized crowd fingerprint and
  combines strict tracking protection with relay-only WebRTC candidate policy.
- **Socialise** prioritizes compatibility for identity, communication, payment,
  and social-media workflows without disabling the shared security baseline or
  exposing raw local WebRTC host addresses.

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
- Private is not a “unique identity” mode. Per-request identity inconsistency is
  not treated as anonymity.
- Private can require a configured relay for peer-to-peer communication;
  Socialise may expose a public server-reflexive candidate for compatibility.
- Private can use stricter social and email tracker classification.
- Site breakage is handled with visible, site-scoped recovery before any global
  reduction in protection is considered.
- The implementation must map each profile to a versioned preference contract
  so upgrades remain deterministic.

## Verification

Both profiles require separate privacy and compatibility test runs. Private is
the product default only after clean-profile tests confirm that its complete
preference contract is active.
