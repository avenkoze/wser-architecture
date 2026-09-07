# ADR 0015: Bind Shield runtime monitoring to scan ownership

Status: Accepted

Date: 2026-09-07

## Context

On-demand runtime instrumentation must respect the selected scan document and must not leave API wrappers installed after a scan ends.

## Decision

The bootstrap requests authorization from the extension background before modifying page APIs or storage. Authorization checks the active scan, extension sender, top-level frame and committed document URL. A subsequent navigation cancels the scan. Completion or disconnect removes listeners and restores API properties still owned by the monitor.

Runtime signals remain page-controlled heuristic evidence. Asynchronous authorization can miss early calls, and pages can spoof or suppress these signals. Reports must state this limitation.

## Verification and consequences

Automated lifecycle and isolation checks pass. An isolated development-browser test verified target-tab instrumentation, unchanged unrelated-tab APIs, post-scan restoration and cancellation across navigation. Separate scan, header, history and watchdog checks pass; native phishing and malware protection remains enabled when the extension is disabled.

The headless regression subset excludes operating-system notifications and the reputation warning UI. It does not establish full browser compatibility. The bootstrap still contacts the background from other matching documents before authorization is denied. No performance improvement or authenticated runtime evidence is claimed.
