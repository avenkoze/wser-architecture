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

## Resource management

- Expose understandable RAM and CPU measurements through an on-demand native
  service without origins, URLs, or a default polling timer. The service
  foundation and focused browser coverage are complete.
- The native Performance panel is integrated over validated, reversible
  tab-sleeping and memory controls. Unsupported hard CPU or RAM limits are not
  presented.
- Measure visible-panel sampling overhead across release platforms before
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
