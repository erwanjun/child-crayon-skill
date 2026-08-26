---
name: child-crayon
description: Turn one or more reference photos into exactly one consistent childlike crayon doodle while preserving the real people count, relationships, pose hierarchy, hairstyle, clothing, and representative accessories. Use when the user invokes $child-crayon or asks for the fixed “儿童蜡笔涂鸦 / child crayon doodle” style defined by this Skill. Delegate raster rendering to the imagegen Skill, then visually validate the result against the bundled style and QA references before delivery. Do not use for generic crayon art, photorealistic portraits, commercial cartoon styles, or unrelated image edits unless the user explicitly wants this fixed style.
---

# Child Crayon

Convert photographs into one stable, intentionally naive child-crayon drawing language. The goal is not photorealistic facial resemblance. Preserve identity through hairstyle silhouette, clothing, accessories, body differences, position, pose, and interaction while keeping every face extremely simple.

## Core contract

Follow this priority order whenever constraints conflict:

1. Correct number of real people, unique identities, and relationships.
2. Fixed child-crayon visual grammar.
3. Original position, pose, body direction, and interaction.
4. Clothing and representative accessories.
5. Background/environment.

Childlike warmth and deliberate clumsiness outrank realistic portrait fidelity.

Never add, delete, duplicate, merge, or substitute people.

## Required references

Before generating, read:

- [references/style-spec.md](references/style-spec.md) — non-negotiable visual grammar.
- [references/subject-analysis.md](references/subject-analysis.md) — people counting, multi-photo identity handling, primary-photo selection, composition.
- [references/generation-spec.md](references/generation-spec.md) — how to compile the ImageGen request.
- [references/qa-checklist.md](references/qa-checklist.md) — acceptance gate after generation.
- [references/failure-recovery.md](references/failure-recovery.md) — targeted correction rules when the first result fails.

If the repository contains real examples under `assets/style-anchors/`, inspect them after reading the text spec. Treat them as the visual center of the style, while the written rules remain the hard boundary.

## Workflow

### 1. Inspect every supplied photo

Determine internally:

- the number of unique real people across all photos;
- hairstyle silhouette and hair color for each person;
- clothing shape, layers, and dominant colors;
- representative accessories such as hats, glasses, earrings, ribbons, bouquets, or bags;
- left/right order, foreground/background relation, body direction, and relative scale;
- interactions such as hand-holding, hugging, leaning, carrying, shoulder-touching, or cuddling;
- whether the environment has meaningful commemorative value.

Do not expose this analysis unless the user explicitly asks for it.

### 2. Resolve multi-photo references

If multiple photos are supplied:

- choose the photo with the clearest complete group and interaction as the **primary composition reference**;
- use other photos only as **supporting identity references** for hairstyle, clothing, accessories, or obscured details;
- render each unique person exactly once;
- never create a collage or repeat a scene merely because the same person appears in several references.

If identity mapping is ambiguous but the task is still safely executable, prefer the most conservative interpretation rather than inventing a new person.

### 3. Lock the style before rendering

Load `references/style-spec.md` in full. Do not compress away REQUIRED or NEVER rules when constructing the rendering request.

The fixed style is `CHILD_CRAYON_V1`:

- oversized round heads and short bodies;
- tiny dot eyes or very short curved closed-eye marks;
- tiny hook/L-shaped noses;
- short-line or tiny-circle mouths;
- round pale-pink crayon cheeks;
- blunt, heavy, irregular black crayon outlines with repeated imperfect strokes;
- loose low-saturation crayon fill with visible white paper gaps;
- mostly uncolored white-paper skin;
- clean white-paper background with only sparse symbolic environment cues when meaningful.

This style must not drift toward anime chibi, commercial mascot art, polished children’s-book illustration, vector line art, colored-pencil drawing, watercolor, 3D, clay, felt, or a crayon filter over a realistic portrait.

### 4. Render through `$imagegen`

Use the installed `imagegen` Skill and its default built-in image-generation path.

Treat the primary photo as the edit/stylization target and supporting photos as identity references. Use the `style-transfer` intent described by `imagegen` when applicable.

Construct the request using `references/generation-spec.md`.

Generate **exactly one candidate at a time**. Do not return a contact sheet, collage, or several alternatives unless the user explicitly asks for variants.

### 5. Validate visually

Inspect the generated image against `references/qa-checklist.md`.

Reject and regenerate when any critical condition fails, including:

- wrong number of people;
- duplicated or merged person;
- core relationship or interaction lost;
- realistic facial anatomy appears;
- adult portrait proportions appear;
- line work becomes clean, smooth, thin, or vector-like;
- fill becomes solid, glossy, shaded, or gradient-based;
- background becomes complex or photorealistic;
- text, logo, signature, watermark, or frame appears.

### 6. Correct narrowly

If the first result fails, read `references/failure-recovery.md` and regenerate with the smallest targeted correction possible. Preserve everything that already works.

Prefer one focused correction per retry, for example:

- “Keep all people and poses unchanged; simplify every face to two dot eyes, a tiny hook nose, and a short-line mouth.”
- “Keep composition unchanged; replace smooth digital outlines with thick, repeatedly traced blunt black crayon strokes.”
- “Keep subjects unchanged; remove realistic background detail and return to mostly blank white paper.”

Avoid restarting the art direction from scratch when only one dimension is wrong.

### 7. Deliver

Default conversational behavior:

- return one final image;
- do not explain the internal analysis;
- do not print the internal generation prompt;
- do not add decorative text around the image.

If Codex is operating in a repository/workspace and a persistent file is requested, save the selected result to the user-requested path or a non-destructive project path and report that path minimally, following the `imagegen` Skill’s save-path rules.

## Non-goals

This Skill is not intended to:

- maximize facial likeness through realistic anatomy;
- recreate exact photographic lighting;
- preserve complex architecture or scenery;
- make polished anime chibi art;
- make generic “crayon texture” portraits;
- infer missing people or reconstruct hidden clothing with elaborate detail.

## Invocation examples

```text
Use $child-crayon on these family photos. Keep each person exactly once and return one final image.
```

```text
用 $child-crayon 把这几张合照画成固定的儿童蜡笔涂鸦，只出一张最终图。
```

```text
Use $child-crayon. Treat photo 2 only as a hairstyle reference; keep photo 1 as the composition.
```
