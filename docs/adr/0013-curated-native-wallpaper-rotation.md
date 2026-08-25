# ADR 0013: Use a curated native catalogue for wallpaper rotation

- **Status:** Accepted
- **Date:** 2026-08-26

## Context

Wser needs a changing new-tab background without creating an unbounded image
search surface, copying another browser's artwork, or replacing the browser's
maintained wallpaper controls. A runtime stock-image query makes visual output,
licensing, availability, and privacy dependent on arbitrary search results.

Two established browser patterns informed the design. One uses a signed,
metadata-validated component catalogue that can update independently of the
browser binary. Another bundles an image directory and makes a uniform random
selection when the new-tab surface mounts. Wser already inherits a signed
wallpaper catalogue and cache from its browser base, so a separate updater or
image transport would duplicate trusted infrastructure.

## Decision

- Automatic wallpaper rotation remains inside the native new-tab wallpaper
  system.
- The source catalogue is the browser's signed wallpaper collection and native
  attachment cache.
- Eligibility is an explicit source-controlled allow-list of reviewed record
  identifiers. New remote records, temporary campaigns, solid colours, and
  unknown assets do not enter rotation automatically.
- A new automatic option selects one eligible record uniformly when each
  new-tab instance initializes and keeps that selection stable for the life of
  that page.
- Existing fixed-wallpaper selection, wallpaper visibility, and user-upload
  controls remain authoritative and user selectable.
- No competitor wallpaper files or arbitrary search results are redistributed.
  If no eligible catalogue record is available, the normal empty background is
  used.

## Consequences

- The pool can receive updated bytes through the maintained signed catalogue
  while its membership remains reviewable in source control.
- Fresh Wser profiles can offer visual variety without adding a new tracking or
  image-provider request path.
- Independent random selection can repeat across adjacent tabs; avoiding all
  repeats would require cross-tab history and is not part of this decision.
- Adding or removing an eligible wallpaper requires an allow-list review and
  the browser catalogue must continue to contain the referenced record.

## Verification

Release candidates must demonstrate that:

1. only allow-listed image records enter the automatic pool;
2. temporary and unknown records are rejected;
3. separate new-tab instances can resolve different eligible records;
4. the selected record's native theme and background position are applied;
5. the normal fixed, disabled, and uploaded-wallpaper paths still work; and
6. missing or unavailable catalogue data does not trigger an arbitrary fallback
   request.
