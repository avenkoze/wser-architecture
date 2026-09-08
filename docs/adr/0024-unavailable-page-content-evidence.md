# ADR 0024: Preserve unavailable page-content evidence

Status: Accepted

Date: 2026-09-08

A failed or timed-out content scan produces unavailable evidence, not a successful empty page measurement. Reports expose content availability, mark the score incomplete and display an explanation. The general positive low-risk message remains suppressed for incomplete evidence. Available network/cookie observations are retained; the heuristic score is not a full-site assurance.

The regression failed before correction and the unit suite passed afterward. An isolated browser check injected content collection failure while cookie measurement succeeded, verified incomplete evidence, restored collection and verified measured evidence. Scan, history and watchdog checks also passed. This does not prove visibility into every frame, storage partition or server-side operation.
