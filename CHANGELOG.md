# Architecture Changelog

This changelog records public architecture milestones rather than application
release notes.

## 2026-08-05

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
