# Architecture Roadmap

## Foundation

- Maintain a security-preserving Firefox base.
- Keep product-specific systems isolated from the upstream baseline.
- Record architecture decisions and verification gates.

## Interface system

- Complete the browser shell and core panels in the web design studio.
- Freeze interaction contracts before browser integration.
- Keep navigation and security-sensitive inspection behind narrow native
  browser bridges.
- Integrate native tab and workspace state without duplicating the browser's
  tab lifecycle in page content. The foundation and same-profile process
  restart and parent-process crash recovery are complete. The native selector
  and keyboard contract are integrated. Automated high-contrast and
  accessibility checks are complete; manual screen-reader review and
  cross-device performance remain verification gates.
- Validate keyboard access, reduced motion, and constrained viewports.

## Privacy system

- Define the shared protection baseline and profile-specific behavior.
- Integrate Private and Socialise as one mutually exclusive preference.
- Validate site-specific recovery without globally disabling protection.

## Site protection

- Ship Wser Shield as a signed, visible, removable distribution extension with
  a local and clearable evidence history.
- Keep phishing/malware reputation, TLS, downloads, sandboxing, and extension
  signing in the maintained native security layer.
- Authenticated-rule and bypass behavior now run against reserved test domains;
  production navigation blocking remains gated on signed distribution,
  removal-persistence, and production rule-update evidence.

## Resource management

- Expose understandable RAM and CPU measurements through an on-demand native
  service without origins, URLs, or a default polling timer. The service
  foundation and focused browser coverage are complete.
- The compact resource section is integrated below the native vertical tabs in
  the existing rail, over validated, reversible tab-sleeping and memory
  controls. No second sidebar panel is registered, and unsupported hard CPU or
  RAM limits are not presented.
- A compact native memory/effective-CPU indicator is integrated beside the
  address bar and defaults on. Its setting tears down the shared service
  subscription; multiple browser windows do not create independent samplers.
- Measure visible-section sampling overhead across release platforms before
  changing its conservative lifecycle or cadence.

## Mail panel

- Keep the panel renderer separate from provider credentials and privileged
  account state.
- Select providers and register Wser-owned OAuth applications before connecting
  real accounts.
- Verify least scopes, token storage, account partitioning, message
  sanitization, private-window exclusion, logout, revocation, and endpoint
  inventory before release.

## Release verification

- Run repeatable privacy, compatibility, and performance suites.
- Publish comparative claims only with equivalent recorded conditions.
- Keep security checks, extension signing, sandboxing, and safe browsing intact.
- Keep live third-party distribution extensions out of test-enabled builds;
  review their signed package and endpoint inventory in release builds.
