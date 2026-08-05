# ADR 0005: Minimize idle runtime and background Push connections

- **Status:** Accepted
- **Date:** 2026-08-05

## Context

Features that are disabled in the interface can still add binary weight or open
background connections. Wser's default Private profile must therefore be
defined by observable build and network behavior, not only by visible settings.

The maintained browser base can package an on-device inference runtime even
when Wser's machine-learning features are disabled. It can also open a Push
connection during an otherwise blank startup. Remote Settings uses that Push
channel for immediate change notifications, while a separate timer can retrieve
signed security and compatibility data periodically.

## Decision

- Wser builds do not bootstrap or package the optional ONNX Runtime while local
  machine-learning features are disabled.
- Private Attribution submission and its origin trial remain disabled. Source
  and IPC removal is deferred until its footprint and fork-maintenance cost are
  measured.
- Remote Settings does not subscribe to Push Broadcast in Wser. Signed periodic
  polling remains enabled for security and compatibility collections.
- The default Private profile starts with the Push transport disconnected.
  The web Push API surface remains present and Socialise can enable the
  transport for user-approved notification and communication workflows.

## Verification

Release candidates must demonstrate that:

1. the generated release configuration contains no ONNX Runtime path;
2. the packaged browser contains no ONNX Runtime binary;
3. a fresh running profile exposes the required Private defaults without
   weakening safe browsing, isolation, signing, or HTTPS protection;
4. a clean blank startup does not contact the browser Push or region-discovery
   services;
5. signed Remote Settings polling and bundled filter updates remain available.

## Consequences

- The default Private profile does not receive website Push notifications until
  the user selects a profile or setting that enables the transport.
- Socialise must apply the Push transport change atomically and explain its
  background-network effect.
- Security and compatibility data can arrive on the periodic schedule instead
  of immediately through Push Broadcast.
- Reintroducing an inference runtime requires a named product feature, a size
  and resource budget, and a separate architecture review.
