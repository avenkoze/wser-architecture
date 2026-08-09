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
  restart restore are complete. The native selector and keyboard contract are
  integrated; screen-reader/high-contrast review and cross-device performance
  remain verification gates.
- Validate keyboard access, reduced motion, and constrained viewports.

## Privacy system

- Define the shared protection baseline and profile-specific behavior.
- Integrate Private and Socialise as one mutually exclusive preference.
- Validate site-specific recovery without globally disabling protection.

## Resource management

- Expose understandable RAM and CPU measurements.
- Add reversible limits and tab-sleeping controls.
- Measure overhead before enabling continuous monitoring by default.

## Release verification

- Run repeatable privacy, compatibility, and performance suites.
- Publish comparative claims only with equivalent recorded conditions.
- Keep security checks, extension signing, sandboxing, and safe browsing intact.
