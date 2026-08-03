# ADR 0002: Design browser interfaces in a web studio first

- **Status:** Accepted
- **Date:** 2026-08-03

## Context

Direct browser-chrome iteration couples visual exploration to long build and
restart cycles. It also makes it difficult to compare complete screens, test
interaction states, and separate product design decisions from integration
constraints.

## Decision

Wser will design complete browser surfaces in a local web studio before moving
them into browser chrome. The studio is an interaction prototype and design
contract, not an alternative browser implementation.

The workflow is:

1. Define the screen and its real product states.
2. Build the visual and interaction model in the web studio.
3. Review layout, motion, keyboard behavior, and constrained viewports.
4. Record the accepted interaction contract.
5. Integrate the accepted design with native browser controls and preferences.
6. Verify the integrated result again in the browser build.

## Design constraints

- Dark translucent surfaces are used as material, not decoration.
- Gradients are reserved for rare background depth and never used as generic
  control borders or shortcut fills.
- Motion uses transform and opacity where possible, supports reduced motion,
  and must not add continuous high-frequency work.
- Prototype data must be clearly distinguishable from measured product data.
- Native security state and permission behavior cannot be simulated away during
  integration.

## Consequences

- Visual iteration is faster and easier to review.
- The web studio cannot be treated as proof that native integration works.
- Every screen needs an explicit integration and verification step.
- Shared design tokens can move into browser chrome only after the visual model
  is accepted.

