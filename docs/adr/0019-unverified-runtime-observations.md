# ADR 0019: Keep page runtime observations unverified and unscored

Status: Accepted

Date: 2026-09-08

## Decision

Runtime observations are stored in bounded extension scan memory and accepted only through the port owned by that scan. Page session storage is no longer an evidence source. Late messages cannot update a replacement scan.

Page-context hooks and messages remain forgeable or suppressible. Runtime messages therefore do not add risk points or create high/critical findings. The panel and detector description identify them as unverified observations. Their absence is not presented as positive privacy evidence.

## Verification and consequences

Automated checks cover page-storage isolation, bounded records, port ownership and unchanged score/issue counts under forged runtime messages. An isolated development-browser test rejected a forged page-storage record while retaining runtime observations and teardown. Existing scan/history/watchdog and container checks passed; broad compatibility remains outside this verification.

This establishes storage ownership and honest scoring, not authenticated API execution. Scores can decrease because the unverified runtime contribution has been removed. Historical reports are not automatically rescored; a new scan uses the current contract.
