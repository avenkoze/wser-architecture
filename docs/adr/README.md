# Architecture Decision Records

Architecture Decision Records capture decisions that shape Wser's product or
engineering model.

## Status values

- **Proposed:** under active review
- **Accepted:** current direction
- **Superseded:** replaced by a newer ADR

## Index

- [ADR 0001: Use two mutually exclusive privacy profiles](0001-dual-privacy-profiles.md)
- [ADR 0002: Design browser interfaces in a web studio first](0002-web-first-interface-prototyping.md)
- [ADR 0003: Require repeatable evidence for product claims](0003-evidence-based-product-claims.md)
- [ADR 0004: Define the engine egress and remote-control boundary](0004-engine-egress-and-remote-control-boundary.md)
- [ADR 0005: Minimize idle runtime and background Push connections](0005-idle-runtime-and-push-connection-policy.md)
- [ADR 0006: Make privacy profiles an executable engine contract](0006-executable-privacy-profile-contract.md)
- [ADR 0007: Keep browser-critical surfaces native and privilege separated](0007-native-browser-surface-boundaries.md)
- [ADR 0008: Build workspaces on the native tab lifecycle](0008-native-workspace-tab-lifecycle.md)
- [ADR 0009: Bound native resource and mail panels](0009-native-resource-and-mail-panel-boundaries.md)
- [ADR 0010: Separate unlinkability from compatibility](0010-unlinkable-private-profile.md)
- [ADR 0011: Keep search-provider selection native and user controlled](0011-native-search-provider-boundary.md)
- [ADR 0012: Ship Wser Shield as a visible removable extension](0012-visible-removable-shield-extension.md)
- [ADR 0015: Bind Shield runtime monitoring to scan ownership](0015-shield-runtime-monitor-ownership.md)
- [ADR 0016: Scope native Shield evidence to documents and request outcomes](0016-native-shield-evidence-lifecycle.md)
- [ADR 0017: Bound Shield policy response sampling](0017-bound-policy-response-sampling.md)
- [ADR 0018: Preserve unavailable cookie evidence](0018-unavailable-cookie-evidence.md)
- [ADR 0019: Keep page runtime observations unverified and unscored](0019-unverified-runtime-observations.md)

- [ADR 0020: Share visible resource sampling and policy observations](0020-visible-resource-sampling.md)
- [ADR 0021: Pin rule verification trust in the extension](0021-pinned-rule-trust.md)
- [ADR 0022: Isolate private Shield history and warning decisions](0022-private-shield-history-and-warning-ownership.md)

- [ADR 0023: Preserve resource ownership and history operation order](0023-resource-sample-ownership-and-history-ordering.md)

- [ADR 0024: Preserve unavailable page-content evidence](0024-unavailable-page-content-evidence.md)
