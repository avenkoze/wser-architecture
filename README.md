# Wser Architecture

Wser Architecture is the public engineering journal for Wser Browser. It
records product principles, architecture decisions, verification standards,
and meaningful development milestones.

This repository intentionally contains no browser source code, packaged
builds, credentials, private research data, or local development paths.

## Product direction

Wser is a Firefox-based browser project focused on a distinct workspace-first
interface, understandable privacy controls, and measurable resource usage.
The project extends a maintained browser platform instead of building a new
engine or weakening platform security.

## Delivery model

```mermaid
flowchart LR
    A["Web design studio"] --> B["Reviewed interaction contract"]
    B --> C["Browser integration"]
    C --> D["Compatibility and security verification"]
    D --> E["Release candidate"]
```

Interface work is designed and reviewed in a local web studio before it is
integrated into browser chrome. Security-sensitive behavior is documented as
an explicit contract and verified separately from visual design.

## Current architecture areas

| Area | Direction |
| --- | --- |
| Browser platform | Maintained Firefox base |
| Interface | Vertical workspace shell with restrained dark glass surfaces |
| Privacy | Private and Socialise protection profiles |
| Tracking protection | Signed filter extension plus browser-level isolation |
| Transparency | Local Wser Shield explanations; no browsing-history upload |
| Resources | Observable tab sleeping and memory controls |

## Repository map

- [`docs/adr/`](docs/adr/) — accepted architecture decisions
- [`ROADMAP.md`](ROADMAP.md) — public engineering stages
- [`CHANGELOG.md`](CHANGELOG.md) — notable architecture progress
- [`CONTRIBUTING.md`](CONTRIBUTING.md) — publication and commit rules

## Evidence standard

Privacy, compatibility, and performance statements are treated as engineering
claims. Comparative claims require repeatable measurements under recorded,
equivalent conditions. Unmeasured goals are labeled as goals, not results.

