<p align="right">
  <strong>English</strong> · <a href="./README.zh-CN.md">简体中文</a>
</p>

<p align="center">
  <img src="./assets/readme/hero.svg" width="100%" alt="Child Crayon — turn reference photos into one consistent childlike crayon doodle with Codex.">
</p>

<p align="center">
  <a href="./LICENSE"><img src="https://img.shields.io/badge/license-MIT-111111?style=flat-square" alt="MIT License"></a>
  <img src="https://img.shields.io/badge/Agent%20Skill-child--crayon-F3A7B8?style=flat-square" alt="Agent Skill: child-crayon">
  <img src="https://img.shields.io/badge/style-CHILD__CRAYON__V1-9FB6D9?style=flat-square" alt="Style version CHILD_CRAYON_V1">
</p>

**Child Crayon** is a reusable Agent Skill for turning one or more reference photos into **one stable, deliberately naive child-crayon drawing language**.

It is not a “crayon filter” prompt. The Skill separates the job into subject analysis, style locking, ImageGen rendering, visual QA, and targeted recovery — so the result is more repeatable across singles, couples, families, and multi-photo references.

<p align="center">
  <img src="./assets/readme/style-grammar.svg" width="100%" alt="The fixed Child Crayon visual grammar: round heads, dot faces, blunt black crayon lines, loose color, and white paper.">
</p>

## What it protects

| Preserve aggressively | Simplify aggressively |
| --- | --- |
| exact number of intended people | realistic facial anatomy |
| unique identities — each person once | adult portrait proportions |
| left/right order and group relationship | photographic lighting and depth |
| hugs, hand-holding, carrying, leaning | complex scenery and clutter |
| hairstyle silhouette, clothing, accessories | polish that makes the result feel professionally illustrated |

Identity comes mainly from **hair, clothes, accessories, scale, placement, and interaction** — not from adding realistic eyes, noses, lips, or jawlines.

<p align="center">
  <img src="./assets/readme/workflow.svg" width="100%" alt="Child Crayon workflow: inspect photos, build a unique-person map, lock the style, render with ImageGen, then run visual QA and retry narrowly when needed.">
</p>

## Install

### Option 1 · Skills CLI

```bash
npx skills add erwanjun/child-crayon-skill
```

### Option 2 · Ask your Agent

```text
Install this Skill: https://github.com/erwanjun/child-crayon-skill
```

### Option 3 · Manual

Copy `skills/child-crayon/` into your Agent Skills directory.

The Skill delegates raster rendering to the installed **`imagegen`** Skill and uses its default built-in image-generation path.

## Use

```text
Use $child-crayon on these family photos. Keep every real person exactly once and return one final image.
```

```text
Use $child-crayon. Photo 1 is the composition; photos 2 and 3 only clarify hairstyle and glasses.
```

```text
用 $child-crayon 把这几张照片画成固定的儿童蜡笔涂鸦。不要拼贴、不要重复人物，只输出一张最终图。
```

More examples live in [`examples/`](./examples/README.md).

## The fixed visual language

`CHILD_CRAYON_V1` is intentionally narrow:

- oversized, slightly irregular round heads;
- tiny dot eyes or tiny curved closed-eye marks;
- tiny hook/L-shaped noses;
- short-line mouths;
- pale-pink circular crayon cheeks;
- heavy, blunt, uneven black contours traced more than once;
- loose low-saturation color with obvious white-paper gaps;
- skin left mostly as the white of the paper;
- clean white background with only sparse symbolic environment cues when they matter.

The hard boundary is in [`style-spec.md`](./skills/child-crayon/references/style-spec.md).

The Skill explicitly rejects photorealistic portrait anatomy, polished anime chibi, commercial mascot art, vector-clean outlines, colored-pencil rendering, watercolor, 3D/clay/felt looks, smooth gradients, realistic skin fill, complex backgrounds, extra people, duplicated people, collage layouts, signatures, and watermarks.

## Why a Skill instead of one giant prompt?

A long prompt can describe a look. A Skill can **operate a repeatable workflow**.

1. **Inspect** every supplied photo.
2. **Resolve identities** so the same person is never rendered twice just because they appear in multiple references.
3. **Choose one composition** rather than averaging several photos into a collage.
4. **Lock the style** using a versioned written spec and optional visual anchors.
5. **Render one candidate** through `$imagegen`.
6. **Reject critical failures** with a visual QA checklist.
7. **Retry narrowly** without destroying parts that were already correct.

That separation is the main engineering idea in this repository.

## Quality gate

A result is rejected when any critical invariant fails, including:

- wrong person count;
- missing, duplicated, or merged people;
- lost core relationship or interaction;
- realistic adult face anatomy;
- standard adult proportions;
- smooth/thin/vector-like black outlines;
- solid glossy fill, shading, gradients, or realistic skin color;
- complex photorealistic background;
- text, logo, signature, watermark, frame, or collage output.

See the complete [`qa-checklist.md`](./skills/child-crayon/references/qa-checklist.md) and targeted [`failure-recovery.md`](./skills/child-crayon/references/failure-recovery.md).

## Style anchors

Text defines the **boundary**. Great examples define the **center**.

If you have 3–6 outputs that perfectly match the intended look, place them under [`assets/style-anchors/`](./assets/style-anchors/README.md). The Skill will inspect those examples after loading the written rules.

Recommended set:

```text
anchor-single.png
anchor-couple.png
anchor-family.png
anchor-group.png
```

This repository intentionally does **not** ship private family photographs or pretend that decorative README artwork is a model output.

## Repository anatomy

```text
child-crayon-skill/
├── README.md
├── README.zh-CN.md
├── assets/
│   ├── readme/                 # GitHub-safe SVG presentation
│   └── style-anchors/          # optional canonical generated examples
├── skills/
│   └── child-crayon/
│       ├── SKILL.md            # execution contract
│       ├── agents/openai.yaml  # Agent UI metadata
│       └── references/
│           ├── style-spec.md
│           ├── subject-analysis.md
│           ├── generation-spec.md
│           ├── qa-checklist.md
│           └── failure-recovery.md
├── evals/                      # regression scaffold; no private photos
└── examples/
```

## Evals, not vibes

The [`evals/`](./evals/README.md) directory is deliberately small today, but it establishes the direction: test people-count preservation, multi-reference deduplication, relationship retention, face grammar, line quality, fill quality, and background simplification across a permission-cleared benchmark.

If the style changes intentionally, version it instead of silently mutating `CHILD_CRAYON_V1`.

## Privacy

Photos used with this Skill may contain highly personal material. **Do not commit private photos to a public repository.** Keep local evaluation inputs in an ignored `private/` directory, and only publish reference images that you have the right to redistribute.

## Contributing

Issues and PRs are useful when they bring a reproducible edge case, a better QA rule, tighter multi-photo handling, a targeted failure recovery, or documentation improvements without weakening the fixed style.

See [`CONTRIBUTING.md`](./CONTRIBUTING.md).

## Acknowledgements

The README structure is inspired by the project-native approach of [`oil-oil/beautify-github-readme`](https://github.com/oil-oil/beautify-github-readme): use visual assets to establish identity, but keep the real explanation, commands, and engineering contract searchable in Markdown.

The rendering workflow is designed to compose with OpenAI Codex's `imagegen` Skill rather than reimplement image generation.

MIT License
