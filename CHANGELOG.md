# Architecture Changelog

This changelog records public architecture milestones rather than application
release notes.

## 2026-08-09

- Moved Wser new-tab navigation behind a narrow native browser bridge that
  resolves searches and web destinations with maintained browser services and
  rejects non-web schemes.
- Added a native, local-only Shield reporting boundary that distinguishes
  third parties that ran from requests blocked by browser protection,
  extensions, or policy.
- Required browser-critical surfaces to preserve privilege separation while
  their visual treatment continues to iterate through the web-first workflow.

## 2026-08-05

- Added a two-profile compatibility smoke matrix covering identity, document,
  media, WebRTC, payment-development, and challenge-demo surfaces, with clear
  limits on what constitutes a completed workflow.
- Upgraded the Private profile contract to full fingerprint resistance,
  letterboxing, and web-locale standardization while retaining a normal-window
  compatibility path in Socialise.
- Added a repeatable external fingerprint report probe and recorded three clean
  profile runs without turning a volatile population score into a ranking
  claim.
- Added a fail-closed, exact-host Private startup egress gate and verified its
  negative path with a synthetic unknown endpoint.
- Removed a hidden all-URL search-redirect measurement extension from the
  packaged browser while preserving search behavior and maintained source.
- Kept optional account Sync separate from account/client association metrics
  and upstream Monitor, Relay, and VPN calls to action.
- Made Private and Socialise an executable, versioned engine contract with a
  safe Private fallback and live atomic transitions.
- Required both profiles to preserve the shared safe browsing, HTTPS, cookie
  isolation, process isolation, and extension-signing baseline.
- Removed the optional ONNX Runtime from Wser builds while local machine-
  learning features remain disabled.
- Separated Remote Settings Push Broadcast from signed periodic polling.
- Defined Private as starting with the Push transport disconnected while
  retaining the web Push API for an explicit Socialise opt-in.
- Established an explicit engine boundary for data egress, remote
  configuration, and privileged component delivery.
- Required clean-profile runtime, release-build, and deny-proxy endpoint checks
  before a release candidate can claim the hardened configuration.
- Preserved signed security data, sandboxing, process isolation, safe browsing,
  certificate protections, and extension signing while removing optional
  reporting and experiment components.
- Kept automatic application updates out of the temporary release
  configuration until Wser owns a signed update and rollback chain.

## 2026-08-03

- Established the public Wser architecture journal and publication rules.
- Accepted Private and Socialise as mutually exclusive protection profiles with
  a shared security baseline.
- Adopted a web-first interface workflow with an explicit native integration
  and verification gate.
- Required repeatable, equivalent-condition evidence before publishing privacy
  or performance comparisons.
- Added the strongest Cover Your Tracks result as a Private release gate while
  keeping comparative ranking claims dependent on equivalent-condition tests.
