---
name: greenroom
description: Write production-ready AI image prompts (Nano Banana Pro / Google Flow and similar models) from a learned playbook, and learn new patterns from your own proven prompt+image pairs. Use whenever the user asks for an image prompt "in my style", "like my others", or "greenroom style"; asks to analyze, learn from, or update greenroom with their prompt corpus; or wants images for a website or UI: hero images, device mockups (green-screen laptop, phone, monitor), section backgrounds, 3D feature icons, card thumbnails, OG/social images, or any "web component" / "for my site" image. Also trigger on "greenroom" or "/greenroom web".
---

# Greenroom: learned image-prompt generation

Greenroom has three modes built around one idea: analyze what made a prompt work
once, write it down as a playbook, and generate every new prompt from that playbook.

Files inside this skill:

- `references/learned-patterns.md`: the distilled prompt playbook (structures,
  typography, camera, lighting, negatives, quality tags). Ships with a seed playbook;
  Learn mode rewrites it from the user's own work.
- `references/web-assets.md`: the playbook for website and UI images (chroma-green
  device mockups, isolated backgrounds, overlay space, aspect ratios by placement).
- `corpus/corpus.json`: the user's prompt+image corpus (created by the user; see
  `corpus/corpus.example.json`). Image paths in it are relative to `corpus/`.

If the user keeps their corpus somewhere else, they will say so; use that path.

## Mode 1: Learn (analyze the corpus)

Trigger: the user asks to analyze, learn, re-learn, or update greenroom with new examples.

1. Read the corpus manifest. Each entry pairs an image path with the exact prompt
   that produced it, plus optional notes and tags. If no manifest exists, show the
   user the format below and offer to create one from images and prompts they paste.
2. For each entry not yet analyzed (compare against the "Analyzed entries" list at
   the bottom of `references/learned-patterns.md`), read the image (vision) alongside
   its prompt. Ask of each pair: what did the prompt say, and what did the image
   actually deliver? Which phrases pulled visible weight (lighting terms, composition
   directives, style anchors, quality tags)? Which parts of the image succeeded that
   the prompt clearly caused? Where did the model drift from the prompt?
3. Update `references/learned-patterns.md`: merge new observations into the existing
   sections rather than appending a log. It is a distilled playbook, not a diary.
   On the first learn pass over a user's own corpus, replace the seed's examples with
   theirs and say so in the header. Keep it under ~300 lines by consolidating.
4. Append the analyzed entry ids to the "Analyzed entries" list so future runs skip them.

Why persist: analysis happens once per example, and generation reads the distilled
playbook instead of re-deriving patterns every time.

## Mode 2: Generate (create a new prompt)

Trigger: the user asks for a new image prompt: a subject, a scene, "like my others
but X", a specific aspect ratio, mood, or campaign need.

1. Read `references/learned-patterns.md`.
2. Compose a new prompt that recombines the learned patterns (structure, phrasing
   conventions, lighting and composition vocabulary, quality tags), adapted to the
   requested subject and configuration (aspect ratio, mood, target model).
3. The playbook groups work into visual families (for example typography-led posters,
   surreal composites, editorial effect portraits, studio lookbooks). Match the family
   the request implies; blend families only if asked.
4. **Output the prompt text only**: a single ready-to-paste block, no rationale, no
   headers, no commentary. If a key setting is genuinely ambiguous (aspect ratio
   matters for the use and wasn't given), ask one short question first, then output
   only the prompt.

If the playbook header still says it is the seed playbook, generation works, but
mention once that running Learn on the user's own prompts will tune it to their look.

## Mode 3: Web (prompts for website and UI assets)

Trigger: the user wants an image for a website or web component (hero, mockup,
background, section visual, icon set, thumbnail, OG image), mentions a site or page,
or says "greenroom web".

1. Read `references/web-assets.md` first, then `references/learned-patterns.md` for
   phrasing and quality vocabulary. The web playbook wins where they disagree: no
   identity lock, no baked-in text, chroma-green screens, isolated backgrounds.
2. **If the user named a specific asset** ("a hero mockup with a laptop and phone for
   a dark site"), fill any gaps with the playbook's web defaults and go straight to
   the prompt.
3. **If the request is open** ("greenroom web", "I need images for my site"), ask one
   round of up to 4 questions, only the ones the request didn't answer (use the
   AskUserQuestion tool where available):
   - Asset: hero device mockup / multi-device set / held phone / section background /
     feature icons / abstract hero / social image (see the asset menu)
   - Site background: dark (pure black) / light (pure white) / a brand colour (hex)
   - Placement: full-width hero / split half / section or card / mobile
   - Reference: is there an earlier render to match (attach it), or is this the first
     in a new series?
4. Compose the prompt from the playbook's structure. Take the aspect ratio from
   placement, the background from the site, and name the empty side for text
   overlay. When a reference render will be attached, add the
   "Use (REFERENCE IMAGE) for … only. Match it exactly." line.
5. If the user asks for several assets for one site, output one prompt per asset,
   each in its own block with a one-line label above it (the only exception to
   prompt-only output). The first is the series anchor; the rest assume it is
   attached as the reference.
6. Otherwise output the prompt only, as in Mode 2.

If a web prompt gives a result the user is happy with, offer to add it to the corpus
so Learn mode can study it.

## Corpus manifest format

`corpus/corpus.json` is a JSON array. Only `image` and `prompt` are required:

```json
[
  {
    "id": "poster-01",
    "image": "posters/poster-01.jpeg",
    "prompt": "the exact prompt text pasted from your image tool",
    "notes": "optional: what you liked about this result",
    "tags": ["optional", "editorial", "monochrome"]
  }
]
```

When adding new batches, the user appends entries; Learn mode picks up only the
un-analyzed ones.
