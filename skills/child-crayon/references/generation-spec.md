# Image Generation Spec

Use this reference to compile the request passed to `$imagegen`.

## Preferred intent

Use the imagegen `style-transfer` editing intent when a primary reference photo is being redrawn while preserving subjects and relationship structure.

Roles:

- **Primary image:** edit/stylization target and composition source.
- **Supporting images:** identity/detail references only.
- **Style anchors (if present):** style references only; never copy their people or composition.

## Prompt scaffold

```text
Use case: style-transfer
Asset type: childlike commemorative crayon portrait
Primary request: Redraw the intended real people from the primary reference as one fixed CHILD_CRAYON_V1 illustration. Preserve every intended person exactly once, their relationship, left/right order, key pose, hairstyle silhouette, clothing color family, and representative accessories. Do not preserve realistic facial anatomy.

Input images:
- Image 1: primary edit/stylization target and composition reference
- Image 2..N: supporting identity references only (when present)
- Style anchors: visual style references only (when present)

Scene/backdrop: Mostly blank bright white paper. Retain only sparse symbolic environment cues if they are commemoratively meaningful.

Subject: <insert compact unique-person map; no duplicated identities>

Style/medium: CHILD_CRAYON_V1. A sincere drawing made with a blunt, heavily pressed black child’s crayon plus a few low-saturation colored crayons on clean white paper. Oversized irregular round heads, tiny bodies, dot eyes, tiny hook/L noses, short-line mouths, pale-pink round cheek patches, thick repeated wobbly black contours, loose colored fill with visible white gaps, mostly uncolored white-paper skin.

Composition/framing: <preserve primary-photo order and interaction; simplify anatomy rather than changing relationships>

Color palette: Preserve clothing color families but reduce saturation; black remains the dominant structural color.

Constraints:
- exactly <N> unique intended people, each once;
- preserve <key relationship / interaction>;
- preserve <key hairstyle / accessory cues>;
- all faces use the same minimal grammar;
- all bodies remain deliberately childlike and short;
- black outer contours are rough, heavy, broken, and repeatedly traced;
- colored fill is loose and incomplete with obvious paper showing through;
- no text, logo, signature, watermark, or frame.

Avoid: photorealism, realistic adult faces, pointed chins, defined jaws, eye whites, eyelashes, realistic eyebrows, nostrils, realistic lips, standard body proportions, polished anime chibi, commercial cartoon polish, vector line art, smooth uniform stroke, colored-pencil texture, watercolor, 3D/clay/felt/doll look, realistic skin fill, gradients, shading, highlights, complex realistic background, extra people, duplicate people, merged people, extra limbs, collage.
```

## Prompt construction rules

- Keep the people-count sentence near both the beginning and the constraint block.
- Repeat identity-preservation constraints on every regeneration.
- Do not replace the detailed style spec with a vague phrase such as “cute crayon style.”
- Do not add creative props, scenery, slogans, or clothing not supported by the references.
- Do not ask for realistic facial fidelity.
- When the model makes the result too polished, strengthen the medium language rather than adding more visual detail.

## Output count

Generate one candidate per call. If QA fails, make a targeted retry. Never ask for a grid of four style options by default.
