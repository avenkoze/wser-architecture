# ADR 0022: Isolate private Shield history and warning decisions

Status: Accepted

Date: 2026-09-08

Private scan and reputation events are excluded from shared flagged history and OS notifications. Private warnings offer continue-once but cannot persist trusted hosts. Warning decisions require the owning extension, current top-level warning document, matching tab and an unexpired token. Tokens are consumed before asynchronous actions to prevent duplicate decisions.

Isolated browser checks passed private high-risk scanning, private-store cookie measurement, unchanged shared history and private/normal warning flows. Unit checks cover notification suppression, sender rejection, expiry and duplicate decisions. Previously stored history is not retroactively removed. Third-party partition and first-party-isolation cookie completeness, OS notification UI validation and release packaging remain outside these checks.

Warning failures remove unused one-time allowances and permit retry only in the original unexpired warning document. Rejected messages restore warning controls. Trusted-host writes and clears are serialized, and effective trust changes only after persistence succeeds. Injected storage/navigation/message failures and private/normal browser flows passed. Successfully persisted user trust is retained if a later navigation fails.
