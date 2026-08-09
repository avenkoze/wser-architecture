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
- Each tab is associated with a workspace through the browser's session-state
  custom tab value mechanism. Newly opened tabs inherit the active workspace.
- Switching to an empty workspace creates an ordinary native new tab. The
  browser continues to own its navigation, close, discard, and restore
  lifecycle.
- Tabs outside the active workspace are hidden with a Wser-specific source.
  Wser only reveals tabs hidden by that source, preserving other browser or
  extension hiding decisions.
- Pinned tabs remain visible across workspaces.
- Synchronization is event driven and workspace definitions are cached. No
  background timer or continuous tab polling is introduced.
- The native workspace selector, rename/delete interactions, and final visual
  treatment are separate interface work built on this contract.

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
   session state.

Before release, verification must also cover a full application-process restart,
keyboard and screen-reader behavior, and workspace-switch latency and memory
overhead at realistic tab counts.

## Consequences

- Wser does not maintain a duplicate tab lifecycle or page-content copy of
  privileged tab state.
- Native tab behavior, session integration, and process ownership remain
  available to future workspace UI iterations.
- Pinned tabs have intentionally global workspace scope in the first version.
- Workspace synchronization between devices is deferred until its privacy,
  conflict, encryption, and account boundaries are designed.
- The foundation is implemented and tested, but it is not a claim that every
  session-restore or accessibility scenario is complete.
