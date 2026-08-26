# Failure Recovery

Use narrow correction prompts. Keep successful invariants unchanged.

## Wrong person count / duplicate person

Correction:

```text
Keep the drawing style, clothing, and composition unchanged. The output must contain exactly <N> unique intended people. Remove the duplicate/extra person and do not merge any two people. Each intended person appears exactly once.
```

## Face became too realistic

Correction:

```text
Keep every person, hairstyle, clothing item, accessory, pose, and position unchanged. Simplify every visible face aggressively: two tiny black dot eyes (or tiny curved closed-eye marks), one tiny hook/L nose, one short-line mouth, two pale-pink round crayon cheeks. Remove realistic jaw, eyelids, eye whites, nostrils, lips, teeth, cheekbone modeling, and portrait shading.
```

## Anime / commercial cartoon drift

Correction:

```text
Keep subjects and relationships unchanged. Remove polished anime/commercial-cartoon styling. Make proportions clumsier and more child-drawn: wider irregular round heads, shorter bodies, narrower rounded shoulders, mitten-like hands, flatter simple shoes, imperfect asymmetry. No glossy eyes, clean cel shading, or polished mascot contours.
```

## Lines too clean or digital

Correction:

```text
Keep composition and color placement unchanged. Replace smooth digital outlines with blunt heavy black child-crayon marks: uneven thickness, wobble, rough edges, local breaks, overshoot, and 2–3 imperfect repeated contour passes. Outer silhouettes must be the heaviest marks.
```

## Fill too solid / polished

Correction:

```text
Keep people and black outlines unchanged. Make colored areas look loosely filled with a blunt crayon: inconsistent stroke direction, visible white-paper gaps, uneven coverage, slight overshoot, no gradient, no highlight, no smooth solid block.
```

## Skin filled realistically

Correction:

```text
Keep all geometry unchanged. Remove broad flesh-tone skin fill. Faces, ears, necks, and hands should remain mostly white paper, with only pale-pink circular cheek blush and at most a few faint warm crayon traces.
```

## Background too detailed

Correction:

```text
Keep every person and interaction unchanged. Remove realistic architecture, vehicles, furniture, passersby, railings, roads, lighting, and perspective. Return to bright white paper with large negative space. Keep only the smallest symbolic environment cue if it is essential to the memory.
```

## Relationship lost

Correction:

```text
Keep style and identities unchanged. Restore the primary relationship from the reference: <describe interaction>. Simplify anatomy if needed, but the semantic interaction must be immediately readable.
```

## One person lost recognizable cues

Correction:

```text
Keep the fixed simple face grammar. Improve only Person <ID> using non-facial identity cues from the references: <hairstyle silhouette>, <clothing color/shape>, <accessory>, <relative height>, <position>. Do not add realistic facial detail.
```
