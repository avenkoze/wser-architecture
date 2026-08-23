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
- Private enables full platform fingerprint resistance, content letterboxing,
  web-locale standardization, and the stricter anti-tracking, link-cleaning,
  referrer, bounce-tracking, and background-network policy. Its WebRTC policy
  accepts relay candidates only.
- Socialise may relax normal-window compatibility surfaces and enable the Push
  transport. It keeps full fingerprint resistance in private windows while
  using the compatibility-oriented fingerprinting profile in normal windows.
  It permits public server-reflexive WebRTC candidates but still hides raw local
  host candidates.
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
6. external fingerprinting tests record the exposed surfaces and repeat across
   three clean profiles; one pass/fail label is not sufficient evidence.
7. a real candidate-gathering test records only candidate classes and confirms
   that Private exposes relay candidates only and neither profile exposes raw
   local host addresses.

## Consequences

- The settings interface can bind to one engine value instead of maintaining
  independent booleans that can enter contradictory states.
- Profile behavior is versioned and observable, making migrations and support
  diagnostics explicit.
- Socialise is an intentional compatibility policy, not a global protection-off
  mode.
- Adding or weakening a managed preference requires updating the engine test,
  runtime transition probe, documentation, and architecture review together.

## Initial evidence

- The engine test completed all Private, Socialise, and invalid-value fallback
  assertions without mismatches.
- A fresh browser profile reported the versioned Private state and no hardening
  or Strict-category mismatches.
- A live Socialise-to-Private transition preserved the shared security
  invariants with zero preference mismatches.
- Equivalent 20-second deny-proxy runs observed the Push service only in
  Socialise: two connection attempts in Socialise and none in Private.
- The targeted browser Push assertions completed successfully for disabled,
  enabled, offline, subscription, retrieval, and unsubscribe paths. The local
  harness still has a post-test application-shutdown timeout to isolate before
  this check can be promoted to a clean release-gate command.

## Version 2 fingerprinting evidence

- The initial compatibility-oriented profile blocked tracking ads and invisible
  trackers, and randomized canvas and WebGL output. It still exposed the real
  timezone, screen dimensions, GPU renderer, and hardware thread count.
- Version 2 standardized those surfaces across three clean Private profiles:
  UTC, a common letterboxed viewport, a generic WebGL identity, English web
  locale, and a tiered thread count.
- All three external tests continued to block tracking ads and invisible
  trackers. The fingerprint classification improved from unique to
  nearly-unique, but did not establish anonymity or a comparative ranking.
- The external result population changes over time. Public claims therefore
  describe observed surfaces and repeat conditions rather than promising the
  strongest score.

## Compatibility smoke evidence

- Both Private and Socialise loaded eight read-only smoke targets covering
  major identity pages, a document application, media, WebRTC, a payment
  development page, and a challenge demo.
- Core WebCrypto, storage, worker, WebAssembly, WebGL, media-device, peer-
  connection, H.264, and VP9 capability surfaces remained available.
- Private exposed the standardized timezone, viewport, WebGL identity, and
  tiered hardware count. Socialise returned to the system-specific values in
  the same running browser, confirming that the compatibility switch affects
  observable web behavior.
- No credentials, payment, challenge response, camera access, or media playback
  was submitted. These results are loading and API smoke evidence, not completed
  transaction evidence.

## Version 3 WebRTC and selector evidence

- The native Privacy settings selector changed the authoritative engine value
  in both directions and restored the hardened profile without mismatches.
- With an external STUN service configured, Private produced no candidate when
  no relay was configured. Socialise produced one public server-reflexive
  candidate. Neither profile produced a raw local, private, loopback, or host
  candidate.
- Both profiles loaded the same eight read-only identity, media, payment,
  challenge, and WebRTC smoke targets. This verifies basic loading and API
  availability, not full authentication, payment, challenge, or call workflows.
- The measured Private surfaces used the maintained platform's standardized
  thread count, locale, GMT-equivalent timezone, letterboxed viewport, and
  generic WebGL identity. A development-build version string is not evidence of
  a release-population anonymity set and is not replaced with a fake user agent.
