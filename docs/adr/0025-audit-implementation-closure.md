# ADR 0025: Close the verified audit implementation scope

Status: Accepted

Date: 2026-09-08

Offline audio perturbation now derives its seed from the original complete output, document origin and session key using Mozilla NSS HMAC-SHA256. The constant-signal calibration regression no longer transfers its multipliers to different content. Repeatability, silence, finite extreme input and focused Web Audio compatibility checks passed. This closes the reproduced calibration defect; it is not a proof against every fingerprinting technique.

Resource surfaces and optional monitors share in-flight process requests and a one-second raw-data cache. Native site/extension attribution is retained; UI snapshots continue to omit raw windows. Registration/process identity and policy-generation checks remain in place. Controlled request-count and native browser checks passed. No percentage RAM or CPU improvement is claimed. Audio and shared sampling have narrow default-on rollback preferences.

Cookie evidence uses observed tab/frame/request URLs, the selected cookie store and explicit current-site partition/FPI keys derived with a pinned Public Suffix List library. Work is limited to 32 URLs, four concurrent calls, 2.5 seconds and 1,000 metadata records. Partial and unavailable evidence are explicit. Real container, private-window, partition and FPI boundary checks passed; unrelated site scopes were excluded. This is bounded observation, not an inventory of every unseen path or frame.

Native Shield checks exercised actual extension cancellation, successful sibling requests and BFCache restoration without cross-document evidence contamination. Rule expiry is enforced during a live session, and initialization can report and recover from storage failure. Unit suites, focused native builds/tests and extension validation passed.

Rule delivery uses reviewed extension versions with pinned trust anchors and rollback protection. A separate remote rule service is not enabled. The 0.8.0 development candidate is reproducible and unsigned; tooling rejects unsigned staging into a release distribution. Production signing and any independent production reputation dataset remain release dependencies. The bootstrap test-domain bundle must not be marketed as a production malware feed. This milestone closes enumerated implementation findings, not all possible browser bugs or production-release readiness.
