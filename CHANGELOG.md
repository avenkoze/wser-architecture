# Architecture Changelog

This changelog records public architecture milestones rather than application
release notes.

## 2026-08-23

- Made Private and Socialise directly selectable in the native Privacy settings
  surface and advanced the executable engine contract to version 3.
- Defined Private as a crowd-oriented fingerprint posture rather than a unique
  or per-request randomized identity. Kept release-population anonymity claims
  behind stable-build, repeated external measurement.
- Hid raw local WebRTC host candidates in both profiles. Private now accepts
  relay candidates only; Socialise permits public server-reflexive candidates
  when compatibility requires direct peer connectivity.
- Verified the profile transition contract, native selector, real ICE candidate
  classes, and eight read-only compatibility targets per profile without
  recording literal network addresses.
- Consolidated resource monitor and tab-sleep measurements into the shared
  parent-process snapshot cache with per-consumer sampling cadence.

## 2026-08-12

- Added a default-on, user-disableable native address-bar resource indicator
  for compact memory and effective CPU-frequency visibility.
- Centralized two-second live sampling in the bounded resource service so
  multiple windows share one loop and disabling the last visible subscriber
  stops it. Unsupported frequency counters fall back to sampled CPU activity.
- Verified toolbar placement, Preferences control, subscription teardown, and
  accessible naming with focused normal and accessibility-check browser runs.
- Added a compact resource section directly below the native vertical tabstrip,
  using the existing bounded resource-service contract. It is not registered as
  a second sidebar panel.
- Limited live sampling to the expanded section while the native tab rail is
  expanded and visible; closing or collapsing the rail stops its timer.
- Exposed process memory, sampled CPU activity, validated tab-sleep policy,
  manual background sleeping, and maintained memory recovery without implying
  an operating-system hard quota.
- Verified focused native rendering and control delegation with normal and
  browser accessibility-check runs. Cross-device overhead measurement and
  manual assistive-technology review remain release gates.

## 2026-08-11

- Added an on-demand parent-process resource service contract that exposes
  serializable RAM and sampled CPU data without origins, URLs, privileged
  objects, or a default polling loop.
- Limited resource controls to validated reversible browser policies and
  explicitly rejected unsupported hard CPU-limit claims.
- Defined credential, provider, content-sanitization, account-partitioning,
  private-window, and endpoint boundaries for the future mail panel.
- Added Windows forced-colors coverage and passed the focused workspace suite
  with browser accessibility checks enabled.
- Extended the 50-tab regression run with deterministic DOM and layout work;
  recorded 6.98 ms normal and 8.96 ms accessibility-check p95 local baselines.
- Separated the signed blocking extension from test-enabled builds after
  Gecko's deny-network guard identified a live third-party filter-list request;
  release builds continue to bundle the unmodified signed extension and must
  inventory its runtime endpoints.

## 2026-08-09

- Added the native workspace foundation without duplicating the browser's tab
  or session lifecycle in page content.
- Bound local workspace membership to native tab session state, preserved
  pinned tabs across workspaces, and made inactive-tab hiding source aware.
- Verified native vertical tabs, workspace switching, new-tab inheritance, and
  empty-workspace creation through focused browser integration coverage.
- Added verified local rename and delete behavior, including migration of tabs
  from a deleted active workspace to a validated fallback.
- Verified that local workspace membership is serialized and restored through
  both the native tab-state lifecycle and a same-profile application-process
  restart with a changed process ID.
- Mirrored workspace metadata into native global session state, delayed
  workspace attachment until initial session restore completed, and verified
  full recovery after an intentional parent-process crash.
- Verified global workspace selection and visibility across two native browser
  windows, including later-window attachment and close-time detachment.
- Kept windows with hidden workspace tabs alive when the last visible tab is
  closed, using Gecko's native replacement-tab lifecycle.
- Added a 50-tab switch regression baseline that verifies stable native tab
  count and workspace visibility without presenting one machine as a general
  performance claim.
- Added the native sidebar workspace selector above vertical tabs with
  accessible single-selection state and Arrow/Home/End keyboard switching;
  final visual treatment and screen-reader validation remain separate gates.
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
