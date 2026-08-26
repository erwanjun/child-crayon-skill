# Visual QA Checklist

The image is deliverable only when all critical checks pass.

## Critical — reject on failure

### People and relationship

- [ ] Intended real-person count is exactly correct.
- [ ] No intended person is missing.
- [ ] No person is duplicated.
- [ ] No two people are merged into one.
- [ ] No extra background person was introduced.
- [ ] Core left/right order is preserved unless the user explicitly allowed change.
- [ ] Core interaction is preserved: hug / hand-hold / lean / carry / shoulder touch / cuddle / other key relation.

### Fixed face grammar

- [ ] Faces are broad, round, soft, and slightly irregular.
- [ ] No pointed adult chin or realistic jawline.
- [ ] Eyes are tiny dots or tiny curved closed-eye marks.
- [ ] No eye whites, detailed irises, eyelids, eyelashes, or realistic brows.
- [ ] Nose is only a tiny hook/L/kink.
- [ ] No nostrils or realistic nose anatomy.
- [ ] Mouth is only a short line/arc or tiny simple circle.
- [ ] No realistic lips or teeth.
- [ ] Pale-pink round crayon cheeks are present when faces are visible.

### Proportion and line

- [ ] Heads are noticeably oversized.
- [ ] Bodies and limbs are short and simple.
- [ ] Result does not read as standard adult portrait proportions.
- [ ] Outer black contour is heavy and dominant.
- [ ] Black line is uneven, wobbly, locally broken, and imperfect.
- [ ] Repeated non-identical contour passes are visible.
- [ ] Result does not read as clean vector/ink line art.

### Fill and skin

- [ ] Colored fill is rough and incomplete.
- [ ] White paper gaps are obvious inside colored areas.
- [ ] No smooth gradient or volumetric shading.
- [ ] No glossy highlight/reflection treatment.
- [ ] Skin remains mostly white paper rather than broad peach/flesh fill.

### Background and output hygiene

- [ ] Background is mostly clean bright white paper.
- [ ] Any commemorative environment cue is sparse and subordinate.
- [ ] No complex photorealistic scenery.
- [ ] No caption, logo, signature, watermark, or frame.
- [ ] Final is one coherent scene, not a collage/contact sheet.

## Style — should pass strongly

- [ ] First impression is “a child drew this,” not “professional illustrator imitating a child.”
- [ ] First impression is not “photo with crayon filter.”
- [ ] Identity is readable mostly from hair, clothing, accessories, scale, position, and relationship.
- [ ] Minor asymmetry and clumsiness feel intentional and warm.
- [ ] Palette is soft and restrained.
- [ ] Black structure remains visually stronger than color.

## Decision

- Any Critical failure -> regenerate with a targeted correction.
- Critical all pass but Style is weak -> one focused style-strengthening retry is preferred.
- If a retry improves one item but breaks a previously correct critical item, restore the invariant explicitly on the next attempt.
