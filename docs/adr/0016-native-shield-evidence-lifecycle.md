# ADR 0016: Scope native Shield evidence to documents and request outcomes

Status: Accepted

Date: 2026-09-07

## Context

An origin may have both loaded and blocked requests. A report must retain both observations and must not carry evidence from a previous document on the same host.

## Decision

Native Shield records belong to the top-level inner window. Request completion updates the entry captured when the request was observed, rather than looking up a potentially newer document by origin. Pending or failed requests do not establish successful loading. Loaded/allowed and blocked observations remain independent when merging the browser content-blocking log.

The panel labels an unidentified extension blocker generically. Successful network completion does not prove script execution; the panel describes loading or permission to load.

## Verification and consequences

Focused browser and unit checks passed for document identity, history changes, reload, actual HTTP completion, simulated mixed and late request outcomes, content-blocking log merging and panel wording. The development frontend build passed. Real extension blocking, back-forward cache and broad site compatibility remain outside this verification.

An origin can appear in both outcome lists; their combined length is not a unique-origin count. Existing report field names remain compatible. The change repairs reporting correctness and does not introduce a new blocking policy or a performance claim.
