# ADR 0023: Preserve resource ownership and history operation order

Status: Accepted

Date: 2026-09-08

Resource subscription cleanup and pending delivery use registration identity. Optional resource monitors discard samples taken under an older preference generation. CPU differences require matching process identity and nondecreasing counters; incomplete totals remain unavailable. Focused regressions, the frontend build, targeted lint and resource UI tests passed. This is measurement correctness, not evidence of a performance gain or shared sampling for every optional monitor.

Shield history mutations execute in request order. A pending write cannot undo a later clear or persistence disable. Failed writes do not replace committed in-memory entries, and rejection does not stop later operations. After the persistence flag is successfully disabled, a failed purge reports failure but does not enable further disk writes; retry can remove retained entries. This does not promise filesystem deletion after a rejected storage operation. Controlled delayed-write/failure tests and isolated private/normal scan, warning, history-restoration and watchdog browser flows passed.
