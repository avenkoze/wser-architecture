# ADR 0022: Isolate private Shield history and warning decisions

Status: Accepted

Date: 2026-09-08

Private scan and reputation events are excluded from shared flagged history and OS notifications. Private warnings offer continue-once but cannot persist trusted hosts. Warning decisions require the owning extension, current top-level warning document, matching tab and an unexpired token. Tokens are consumed before asynchronous actions to prevent duplicate decisions.

Isolated browser checks passed private high-risk scanning, private-store cookie measurement, unchanged shared history and private/normal warning flows. Unit checks cover notification suppression, sender rejection, expiry and duplicate decisions. Previously stored history is not retroactively removed. Third-party partition and first-party-isolation cookie completeness, OS notification UI validation and release packaging remain outside these checks.
