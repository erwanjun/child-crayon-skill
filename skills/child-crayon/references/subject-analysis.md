# Subject Analysis

Use this internal pass before rendering. Do not show it unless the user asks.

## A. Build the unique-person map

For each real person, record a compact identity tuple:

```text
Person ID:
Primary photo occurrence:
Other photo occurrences:
Hair silhouette / color:
Clothing silhouette / dominant colors:
Representative accessories:
Relative body size:
Position in primary photo:
Interaction with others:
```

Do not identify people by name unless the user supplied names. Use neutral internal IDs such as P1, P2, P3.

## B. Count conservatively

The expected output count equals the number of unique intended real people, not the sum of person appearances across all reference images.

Watch for:

- the same person appearing in multiple photos;
- reflections or printed photos inside the scene;
- partial people at the edge who may or may not be intended subjects;
- background passersby who should be removed;
- a baby being carried and partly occluded;
- repeated close-up reference images of one subject.

When the user clearly supplies supporting references of the same people, do not duplicate them.

## C. Pick one composition source

Primary composition photo selection order:

1. correct intended group is complete;
2. interactions are easiest to understand;
3. body positions are least occluded;
4. clothing and accessories are reasonably visible;
5. background quality matters last.

Do not average several compositions together.

## D. Preserve relationship before exact pose detail

If exact anatomy cannot be retained under the naive style, preserve the semantic interaction:

- holding hands;
- arm around shoulder;
- leaning together;
- hugging;
- carrying a child;
- child sitting in lap;
- bouquet held in front;
- person standing slightly behind another.

A simplified childlike pose that preserves the relationship is better than realistic anatomy that breaks the style.

## E. Identity cue ranking

Use, roughly in this order:

1. hairstyle silhouette;
2. clothing color and silhouette;
3. distinctive accessory;
4. relative height/build;
5. placement in the group;
6. pose/interaction;
7. minimal face marks only as expression, never as realistic likeness.

## F. Background decision

Ask internally:

> If this environment disappears, does the commemorative meaning materially change?

If no, remove it.

If yes, keep only 1–3 symbolic cues in a lighter, simpler crayon language.
