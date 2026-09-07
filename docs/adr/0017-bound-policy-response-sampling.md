# ADR 0017: Bound Shield policy response sampling

Status: Accepted

Date: 2026-09-07

## Decision

Shield samples at most 160,000 response-body bytes per policy candidate through a stream reader, rather than buffering the full response before truncation. Reaching the budget cancels the request and marks the report sample as truncated. The deadline includes body reading; HTTP redirects are rejected and credentials remain omitted.

## Verification and limits

Automated tests verified bounded chunk consumption, cancellation, byte accounting and small UTF-8 responses. Local HTTP tests verified redirect rejection and interruption of an unfinished body. The existing development-browser scan subset passed.

This is an application sampling budget, not an exact wire-transfer or total-memory ceiling: browser buffering can receive additional bytes before cancellation. Redirecting policy pages may no longer be analyzed. No release package or broad compatibility claim follows from these checks.
