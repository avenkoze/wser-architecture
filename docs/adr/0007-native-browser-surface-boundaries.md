# ADR 0007: Keep browser-critical surfaces native and privilege separated

- **Status:** Accepted
- **Date:** 2026-08-09

## Context

Wser designs browser interfaces in a web studio, but a visual prototype must
not become a second navigation or security engine. New-tab input can represent
either a search or a destination, and privacy explanations depend on privileged
connection, content-blocking, permission, and request-classification state.
Handling either responsibility in ordinary page content would duplicate
maintained browser behavior and widen the trusted interface.

The product also needs to explain protection without exporting browsing
activity or presenting a third-party request as blocked when it actually ran.

## Decision

- The web studio remains the source of the reviewed visual and interaction
  contract. Browser-critical behavior is implemented in maintained native
  browser surfaces.
- Wser's new-tab interface runs inside the browser's native new-tab system. Its
  content process sends one narrow navigation action to the privileged browser
  process rather than resolving or loading destinations itself.
- The privileged process uses the browser's URI-fixup and default-search
  services. It accepts only HTTP and HTTPS results, rejects privileged, local,
  and script schemes, and performs navigation through the normal trusted link
  path.
- Wser Shield collects and classifies current-page signals in the browser
  process. The panel receives a plain local report for the selected browser and
  does not inject inspection code into websites.
- Shield distinguishes third parties that ran from requests blocked by browser
  tracking protection, an extension, or another policy. Classification uses
  the browser's local maintained lists and does not introduce a browsing-
  history upload.
- Shield state is bounded per top-level browsing context and resets when the
  context moves to another host. Collection can be detached immediately by
  preference.
- Visual polish, wallpaper behavior, and workspace presentation may iterate
  independently, but they may not bypass these native boundaries.

## Verification

Release candidates must demonstrate that:

1. a native new tab renders the Wser search surface and its keyboard dismissal
   behavior;
2. normal search text follows the configured default engine, ordinary and
   scheme-less web addresses navigate normally, and non-web schemes are
   rejected;
3. URI resolution and navigation are covered at both focused unit and browser
   integration levels;
4. Shield request observers attach and detach with the managed preferences;
5. Shield reports distinguish local classifications and blocking sources and
   render without website content privileges;
6. both surfaces continue to work with data submission and remote experiments
   disabled; and
7. site compatibility and performance are measured before either feature is
   promoted to a release default.

## Consequences

- The new-tab page cannot directly open privileged or local schemes from its
  custom input.
- Search configuration, history marking, and trusted navigation continue to
  follow maintained browser services instead of a Wser-specific parser.
- Shield is an explanation layer over existing defenses, not a replacement
  blocker and not proof that every tracker has been identified.
- Per-site recovery controls, localization, accessibility review, and broader
  compatibility coverage remain required before release.
- Future workspace, resource, and mail panels should use similarly narrow
  native bridges when they require browser privileges.

## Initial evidence

- Focused automated checks cover Shield preference gating, report scoring, and
  native panel rendering.
- Focused new-tab checks cover component behavior, parent-process URI
  resolution, direct web navigation, keyword search resolution, blocked
  schemes, native rendering, and active-state dismissal.
- The implementation keeps network classification local and bounds retained
  page records and classification caches.
