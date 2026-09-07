# ADR 0014: Workspace resource budget and scan lifecycle ownership

Status: accepted for development

## Context

Workspace visibility and loaded-tab resource accounting must agree. Asynchronous
extension scans also require stable ownership so an older completion cannot
remove a newer scan for the same tab.

## Decision

Workspace assignment synchronizes the native owning window. Automatically
sleeping background tabs includes tabs hidden by the workspace feature while
preserving existing media, pinned-tab and native discard protections. Tabs
hidden by another extension retain their previous automatic treatment. A
focused preference restores the previous hidden-tab budget policy.

Scan cleanup and late continuations operate on the scan they own. Repeated
start requests for a tab with an active scan reuse that scan rather than
installing another monitor and reloading again.

## Verification and consequences

Targeted tests reproduced the previous failures before the changes. Native
workspace and sleep-policy regression checks, extension lifecycle checks, and
an isolated browser discard probe passed after the changes. These checks are
not a claim of measured memory savings, full media compatibility, or a signed
release. Broader privacy/reporting findings and release packaging remain
separate work. Each correction is independently reversible.
