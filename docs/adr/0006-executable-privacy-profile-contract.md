# ADR 0006: Make privacy profiles an executable engine contract

- **Status:** Accepted
- **Date:** 2026-08-05

## Context

Private and Socialise were defined as product profiles, but a profile selector
is not meaningful if it only changes interface state. The browser engine needs
one authoritative selection, deterministic preference sets, safe fallback
behavior, and evidence that switching profiles does not weaken the shared
security baseline.

## Decision

- A single mutually exclusive profile value selects either Private or
  Socialise. New and invalid profiles resolve to Private.
- The engine applies the selected profile after the browser profile is loaded
  and observes later changes during the same session.
- Each applied profile records a versioned state marker so diagnostics and
  release tests can distinguish a selected label from an applied contract.
- Private enables the stricter anti-tracking, fingerprinting, link-cleaning,
  referrer, bounce-tracking, and background-network policy.
- Socialise may relax normal-window compatibility surfaces and enable the Push
  transport, but it keeps stronger private-window protections.
- Total Cookie Protection, Global Privacy Control, core tracker and malicious
  content defenses, HTTPS protection, process isolation, and extension signing
  remain common invariants.

## Verification

Release candidates must demonstrate that:

1. a never-opened profile starts in the versioned Private state;
2. Private, Socialise, and invalid-value fallback match their complete expected
   preference sets in an automated engine test;
3. a running browser can switch Socialise and return to Private atomically;
4. safe browsing, HTTPS protection, cookie isolation, process isolation, and
   extension signing remain enabled in both transition snapshots;
5. comparative privacy claims remain subject to the separate repeatable-
   evidence policy.

## Consequences

- The settings interface can bind to one engine value instead of maintaining
  independent booleans that can enter contradictory states.
- Profile behavior is versioned and observable, making migrations and support
  diagnostics explicit.
- Socialise is an intentional compatibility policy, not a global protection-off
  mode.
- Adding or weakening a managed preference requires updating the engine test,
  runtime transition probe, documentation, and architecture review together.
