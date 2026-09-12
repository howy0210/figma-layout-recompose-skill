---
name: figma-layout-recompose
description: Recompose a completed Figma design into one or more new target-size frames while preserving approved content, brand, components, and visual hierarchy. Use for requests such as 1464x600 to 600x450, banner or social-size adaptation, desktop-to-tablet/mobile layout, responsive reflow, or creating a differently proportioned artboard from an existing design. Perform real Figma edits through the official Figma integration; do not use for simple proportional scaling, code-only responsive implementation, or redesigning the brand/content without approval.
---

# Figma Layout Recompose

Create an editable target frame that reads as the same approved design at a different size. Treat the source as evidence and art-direct the target; do not uniformly scale the source until it fits.

## Required capabilities

- Use the official Figma MCP connection for all reads and writes.
- Before the first write, load and follow the installed `figma-use` Skill.
- For a full screen, composed view, or design-system-backed layout, also load `figma-generate-design`.
- Require a source Figma frame or selection and exact target width and height. If several source frames could be authoritative, resolve that ambiguity before writing.

If `use_figma`, `get_metadata`, or visual capture is unavailable, stop after reporting the missing capability. Do not substitute raster image generation for an editable Figma result.

## Protect the source and scope

- Keep the approved source frame unchanged unless the user explicitly asks to modify it.
- Default locked items: wording, facts, links, logos, brand colors, typefaces, image identity, component identity, and states.
- Changing layout, crop, wrapping, spacing, and responsive ordering is authorized by a recomposition request. Removing content, rewriting copy, detaching instances, or editing shared main components is not.
- Put the target beside the source or in the user-named Section/Page. Name it `<source name> - <width>x<height>` unless the file already uses another convention.
- Record the source frame, target size, locked items, permitted changes, and any required safe area before mutating the canvas.

## Inspect before composing

Read the exact source node with structured metadata and a screenshot. Identify:

- semantic regions and their reading order;
- primary message, primary action, supporting copy, legal copy, and decorative content;
- components, instances, variables, styles, Auto Layout, constraints, masks, and clipping;
- text widths and wrapping, image subjects/focal points, logo clear space, and any intentional overlap;
- whether the deliverable is a fixed-format graphic or a scrollable/responsive interface.

When the source is large, inspect major regions separately. Never infer a design solely from layer names or a downscaled full-frame screenshot.

## Choose a treatment for every region

Classify each meaningful region before editing:

- **Copy**: same component, token, style, icon, logo, or content.
- **Translate**: same relationship with target-appropriate dimensions, wrapping, spacing, or alignment.
- **Recompose**: change axis, columns, order, grouping, disclosure, or position while preserving meaning and hierarchy.
- **Media adapt**: change crop, focal anchor, mask, scale mode, or approved asset variant without losing the subject.
- **Preserve**: retain intentional target-specific behavior already present.
- **Block**: a safe result would require content deletion, brand change, an unknown focal point, or another decision outside scope.

Read [recomposition-rules.md](references/recomposition-rules.md) when the aspect ratio changes materially, the design contains important media, or the correct reading order is not obvious. For multiple target sizes or more than one major region, use [decision-ledger.md](references/decision-ledger.md).

## Build the target

1. Duplicate the source top-level frame so image fills, variables, styles, and instance linkage remain available. Move the duplicate to a clear page position and rename it.
2. Set the duplicate to the exact target dimensions. Do not scale all descendants as a group.
3. If the new composition is substantially different, replace only the necessary wrapper structure while reusing cloned children and component instances. Do not detach instances merely to make layout easier.
4. Edit in this order:
   - target bounds, safe area, outer padding, and major regions;
   - layout axis, columns, semantic order, and grouping;
   - child widths, text wrapping, component variants, and media crop;
   - internal gaps, alignment, and component sizing;
   - typography adjustments that remain within the approved type system;
   - masks, decorative positioning, and final clipping.
5. Use Auto Layout for structurally related children. Use absolute positioning only for intentional overlays or decoration.
6. Preserve variables and styles. Prefer existing component variants and design-system tokens over new raw values.
7. Keep overflow visible while diagnosing layout. Enable clipping only when the target format requires it and all required content is confirmed inside the frame.

For a batch of target sizes, complete and validate the hardest or most dissimilar size first. Reuse its decision rules, not its raw coordinates, for the remaining sizes.

## Fit rules

- For fixed-format graphics, the target frame size is immutable. Recompose hierarchy and media to fit; do not silently omit required content or reduce text below the approved system minimum.
- For application UI, preserve scrolling and interaction semantics. Do not force an entire page into the target height unless that height is an explicit product requirement.
- Recalculate text wrapping before accepting row, module, or frame heights.
- If all locked content cannot fit legibly, return `Open` or `Blocked` with the exact conflict instead of hiding, clipping, or excessively shrinking it.

## Validate visually and structurally

After the skeleton and after every major region:

1. Capture the target region or frame.
2. Check hierarchy, reading order, whitespace balance, text wrapping, focal subject, and component treatment against the source.
3. Check metadata for exact target dimensions, hierarchy, instance linkage, constraints, and overflow.
4. Fix only the discrepant region; do not recreate a correct frame because one region failed.

Final acceptance requires:

- exact requested frame size;
- original source unchanged;
- locked content and brand assets accounted for;
- no uniform whole-design scaling presented as recomposition;
- no clipped or overlapping required text, lost primary action, unintended overflow, or cropped essential subject;
- appropriate target reading order and visual hierarchy;
- reusable components remain instances and tokens/styles remain bound where available;
- final screenshot evidence for the complete target plus close-ups of dense or high-risk regions.

Return `Pass`, `Open`, or `Blocked`, the created frame ID/link, a concise Copy/Translate/Recompose/Media-adapt summary, and any exceptions. Follow `figma-use` recovery rules; never retry a possibly partial write blindly.

## Upstream basis

This workflow synthesizes the Figma official [`figma-use`](https://github.com/figma/mcp-server-guide/tree/main/skills/figma-use) and [`figma-generate-design`](https://github.com/figma/mcp-server-guide/tree/main/skills/figma-generate-design) Skills with the MIT-licensed [`cross-device-recomposition-spec`](https://github.com/Fay1Yee/design-agent-skills/tree/main/skills/cross-device-recomposition-spec) and [`sync-responsive-figma-from-web`](https://github.com/Fay1Yee/design-agent-skills/tree/main/skills/sync-responsive-figma-from-web) workflows. Follow the installed official Skills as the current source of truth for Figma tool mechanics.
