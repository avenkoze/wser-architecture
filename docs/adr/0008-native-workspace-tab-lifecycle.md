# ADR 0008: Build workspaces on the native tab lifecycle

- **Status:** Accepted
- **Date:** 2026-08-09

## Context

Wser needs a compact workspace switcher above its vertical tabs. A workspace
changes which tabs are visible, but it must not create a second tab model with
its own close, select, pin, restore, and accessibility behavior. Those concerns
already belong to the browser's maintained tab and session systems.

The foundation also needs to stay local, avoid continuous polling, preserve
other reasons a tab may be hidden, and leave room for a later native switcher
without coupling the engine to the current visual prototype.

## Decision

- Gecko's native vertical tabstrip and real browser tabs remain authoritative.
  Workspaces filter those tabs instead of mirroring them in page content.
- Workspace definitions are bounded, sanitized, and stored in the local
  profile. Cloud synchronization is out of scope for the first version.
- Workspace definitions and the active workspace are also mirrored into
  native global session state. The workspace service attaches only after the
  initial session restore has loaded global metadata and native tab state.
- Each tab is associated with a workspace through the browser's session-state
  custom tab value mechanism. Newly opened tabs inherit the active workspace.
- Switching to an empty workspace creates an ordinary native new tab. The
  browser continues to own its navigation, close, discard, and restore
  lifecycle.
- Tabs outside the active workspace are hidden with a Wser-specific source.
  Wser only reveals tabs hidden by that source, preserving other browser or
  extension hiding decisions.
- Pinned tabs remain visible across workspaces.
- Closing the last visible tab keeps the browser window open and delegates
  replacement creation to Gecko's native new-tab lifecycle. Explicit window
  closing and toolbar-less popup behavior remain unchanged.
- Synchronization is event driven and workspace definitions are cached. No
  background timer or continuous tab polling is introduced.
- The native workspace selector lives in the browser sidebar above the native
  vertical tabstrip and calls the workspace service directly. Final visual
  treatment remains separate interface work built on this contract.

## Verification

The first implementation passed formatting, focused static analysis, a fast
browser build with no compiler warnings, and a focused browser integration
test. The test covers:

1. use of the native vertical tabstrip;
2. creation of a bounded local workspace;
3. active-workspace inheritance for new tabs;
4. creation and selection of a native tab for an empty workspace;
5. source-labelled hiding of inactive tabs; and
6. restoration of the correct native tab selection when switching back;
7. local workspace rename and color changes; and
8. deletion of an active workspace with native tabs moved to a validated
   fallback; and
9. serialization and restoration of workspace membership through native tab
   session state; and
10. creation, workspace inheritance, and selection of a native replacement
    when the last visible workspace tab closes; and
11. stable tab count and correct visibility across 40 switches with 50 added
    native tabs; and
12. restoration after a same-profile application-process restart with a
    changed process ID, including workspace definitions, active workspace,
    native tab membership, URLs, visibility, and selection; and
13. a native sidebar selector with single-selection semantics, accessible
    names, roving focus, and Arrow/Home/End keyboard switching; and
14. recovery after an intentional parent-process crash with a changed process
    ID, including workspace definitions, active workspace, native tab
    membership, URLs, visibility, and selection; and
15. global workspace selection and visibility across two native browser
    windows, including attachment of a later window and detachment on close.
16. Windows forced-colors behavior with system colors and a selected-state
    indicator that does not depend on workspace color; and
17. the full focused suite with browser accessibility checks enabled, plus a
    50-tab run in which ten documents contain deterministic DOM, layout, and
    form-control work.

The latest local Windows development runs measured 6.98 ms p95 normally and
8.96 ms p95 with accessibility checks enabled. This is a local regression
baseline, not a cross-device product-performance claim. The automated 250 ms
p95 ceiling only guards against a severe regression.

Before release, verification must still include manual screen-reader review,
workspace-switch latency and memory overhead with representative full pages
across the supported device matrix, and separate session-restore scenarios on
additional supported platforms. Automated high-contrast, accessibility, and
deterministic loaded-document checks do not replace that matrix.

## Consequences

- Wser does not maintain a duplicate tab lifecycle or page-content copy of
  privileged tab state.
- Native tab behavior, session integration, and process ownership remain
  available to future workspace UI iterations.
- Profile preferences remain the local baseline for ordinary startups, while
  native global session state keeps workspace metadata in the same recovery
  snapshot as tab membership after a crash.
- The first native selector uses event-driven preference updates and no
  continuous polling or decorative motion.
- Pinned tabs have intentionally global workspace scope in the first version.
- Closing a workspace's last visible tab yields a native new tab rather than
  unexpectedly terminating a window that still owns hidden workspace tabs.
- Workspace synchronization between devices is deferred until its privacy,
  conflict, encryption, and account boundaries are designed.
- The foundation is implemented and tested, but it is not a claim that every
  session-restore or accessibility scenario is complete.
