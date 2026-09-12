# Recomposition rules

Read this reference when a new aspect ratio forces structural change, when media has a meaningful subject, or when the target reading order is uncertain.

## Determine the deliverable type

### Fixed-format graphic

Examples: campaign banner, social card, display ad, event graphic, thumbnail.

- The target width and height are fixed.
- Preserve the primary message, brand, required legal copy, logo clear space, and essential subject.
- Rebalance negative space and reposition decoration freely within the approved visual language.
- Crop media by focal subject, not by the source frame's coordinates.
- If all required content cannot remain legible, report the conflict instead of silently deleting or shrinking it.

### Application interface

Examples: desktop, tablet, mobile, dashboard panel, modal.

- The width usually determines reflow; height may represent a viewport rather than a content limit.
- Preserve semantic order, controls, states, navigation destinations, and scroll reachability.
- Replace multi-column or side-by-side regions with the clearest reading sequence when width becomes unsafe.
- Change interaction only to an equivalent target-appropriate pattern; do not remove an action because hover or space is unavailable.

## Preserve hierarchy, not coordinates

Use this priority unless the source or user establishes another:

1. brand identity and required safety/legal elements;
2. primary message or task;
3. primary action;
4. essential explanatory content or product subject;
5. supporting information;
6. decorative elements.

This order governs collision resolution; it does not authorize deleting lower-priority content.

## Common aspect-ratio transformations

Treat these as hypotheses and verify them against the actual design.

### Very wide to square or compact landscape

- Change left/right split regions into a stack or controlled overlap.
- Narrow text blocks and allow intentional wrapping before reducing type size.
- Move the primary action nearer the primary message.
- Re-crop wide photography around the subject; use an approved alternate asset if available.
- Reduce decorative spread and preserve logo clear space.

For `1464x600 -> 600x450`, expect genuine recomposition: the source ratio is much wider, so a scaled or center-cropped copy is unlikely to preserve both message and subject.

### Tall to wide

- Convert a long stack into grouped columns only when semantic order remains clear.
- Avoid distributing unrelated content merely to fill width.
- Reframe vertical media or use an approved wide asset; do not stretch it.

### Same ratio, different scale

- First test constraints and Auto Layout.
- Proportional scaling may be acceptable only when text, minimum targets, stroke weight, logo clear space, and asset resolution remain valid and the user asked for a scaled derivative.
- Otherwise use target-specific spacing and type tokens.

## Media adaptation

- Identify the essential subject and any directional gaze or implied motion.
- Preserve readable text embedded in imagery and required product details.
- Prefer crop/position changes over geometric stretching.
- Preserve image fill and mask editability.
- Use a different asset only when it is already approved or the user authorizes the substitution.
- Validate the crop at the final target dimensions, not only while zoomed into the canvas.

## Typography and spacing

- Preserve the font family and approved styles.
- Change text-box width and wrapping before changing type scale.
- Keep emphasis relationships between headline, supporting copy, CTA, and legal text.
- Use existing type and spacing variables; do not invent a parallel token system.
- Avoid solving fit through compressed line height, unreadably small text, or equalized gaps that erase hierarchy.

## Failure signals requiring recomposition

- the primary message or action is no longer visible or prominent;
- columns make text or controls too narrow;
- essential media subject falls outside the crop;
- logo or legal clear space is violated;
- text overlaps, clips, or wraps into an unintended hierarchy;
- decoration competes with content after resize;
- the result needs large empty bands merely because the source was scaled to fit.
