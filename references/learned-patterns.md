# Greenroom learned patterns

**Seed playbook.** Distilled from a private corpus of 12 prompt+image pairs (Nano
Banana Pro via Google Flow) plus 9 more results viewed without their prompts. The
techniques below are general; the examples are described, not copied. Run Learn mode
on your own corpus to replace this with patterns from your work.

## Reference identity (the single most important pattern for people)

When an image is built around a recurring character, the identity comes from an
**attached reference image**, never from prose description. Prompts write the
subject as a placeholder — `[REFERENCE IMAGE CHARACTER]`, `(REFERENCE IMAGE)`,
"Use my uploaded photo as the identity reference" — and keep the description to
wardrobe and props that should stay constant (for example: black rectangular
sunglasses, black leather gloves, a high-collar coat). A stylized stand-in such as a
glossy white faceless mannequin works well as a recurring brand character.

Pair the placeholder with an aggressive **identity-lock block**: "IMPORTANT FACE
LOCK: Maintain EXACT SAME FACE… Preserve identical facial structure, jawline,
hairstyle…", "Face preservation priority: maximum. Identity consistency: maximum."
This held the same identity across very different scenes. When generating a prompt
with a recurring character: assume a reference image will be attached, write the
subject as a placeholder, and include a compact identity-lock block.

## Prompt structures that worked (pick per job)

1. **Labeled-fragment brief**: `Main Subject: … Pose: … Camera: … Typography: …
   Lighting: … Aspect Ratio: …` with terse fragments. Fast to write, reliably
   followed. Default choice.
2. **Markdown campaign brief**: bold section headers plus a closing **Negative**
   block. Best for layout-heavy Swiss or editorial posters.
3. **Agentic role-play**: "Act as a Creative Director… PHASE 1 / PHASE 2 / …" with
   decision menus the model resolves itself. Use when the model should invent
   brand-level choices (a collab partner, colorway, logo treatment).
4. **JSON style object**: nested `style` / `elements` / `output` spec. Best for
   effect transforms with many tunable parameters (glitch slices, dissolves).
5. **Single-paragraph cinematic prose** with ALL-CAPS emphasis islands. Works for
   surreal composites; keep the caps for hard constraints only.

Whatever the format, the same skeleton appears: style/genre declaration up top →
subject + identity lock → camera/lens/angle → scene → typography (exact text) →
lighting → palette → quality tags + aspect ratio → negatives.

## Typography

- Exact display text is always **quoted verbatim**, short (2–5 words), and given a
  placement instruction: "wrapped around the inside walls of the bag", "integrated
  behind the subject", "vertical", line-broken in the prompt ("I AM A\nCREATOR").
- Small supporting copy gets an exact position: "Small text in bottom left:",
  "upper left". Nano Banana Pro renders this accurately when short and quoted.
- Treat type as a layout element the subject sits inside or in front of (letters
  partially hidden by the figure): say "partially behind and around the model".
- "Text accuracy: high" and "no text" are both respected.

## Composition & camera

The strongest results come from **novel viewpoints**, stated plainly and early:
top-down aerial with tilt-shift; POV from inside a shopping bag looking up; forced
perspective with a giant hand pinching a tiny subject; extreme 20mm negative space;
head-and-shoulders side profile; three-quarter turn with raised chin. Specific
hardware language is standard and effective: "85mm lens, f/1.8", "24mm wide-angle,
ground-level, f/2.8", "100mm Macro, f/8", a named full-frame camera body. Call out
negative space explicitly ("camera pushed far back, creating significant negative
space").

## Lighting & color

- Lighting calls that worked: "professional studio lighting with clear shadows",
  chiaroscuro / single hard key, "soft light source from the top left", "overcast
  natural daylight" for concrete and street scenes, "dramatic spotlight from upper
  right".
- Palettes are **limited and named**, often with hex: `#e3e3e3`, `#F2F2F2`,
  `#000000` ("Pure Void Black"). A strong default: black / white / cream plus one
  accent (red, or gold/mustard). A monochrome portrait with a single coloured accent
  panel is a reliable signature move.

## Constraint & negative language

- Hard constraints get ALL-CAPS flags: "IMPORTANT", "CRITICAL", "NOTHING should go
  beyond the white stripes". Spatial containment rules stated this way are respected.
- Anti-AI negative blocks close most prompts: no plastic skin, beauty filters,
  cartoon anatomy, over-sharpening, glowing edges, excessive HDR, fake typography,
  watermarks, AI artifacts. Also works as `--no blur, compression artifacts, noise…`.
- **Known drift**: numeric counts are weakly enforced ("4 people" produced 3). If an
  exact count matters, state it redundantly (words + digits) or accept drift.

## Quality tags & finish

Standard closer set: "8K", "ultra-realistic", "masterpiece", "editorial / magazine
cover quality", "cinematic color grading", "subtle film grain", "matte finish",
"museum-quality paper texture". Always declare the aspect ratio explicitly: 9:16,
4:5, 3:4, 21:9.

## Templates & parameterization

Prompts can be written as **reusable templates**: `[BRAND NAME]`, `[Character Name]`,
`{argument name="clothing color" default="red"}`, "If the accent color is not
specified, automatically select one premium shade". When generating, keep this habit
if the user asks for a template; otherwise resolve all placeholders.

## Visual families

1. **Typography-led brand posters**: campaign posters where short quoted slogans and
   the subject share the layout; collab posters; product-on-table flat lays.
2. **Surreal composites**: clone crowds, a giant hand, a horse in a living room,
   bird or ash swarms, a figure dissolving into particles.
3. **Editorial effect portraits**: motion-blur half-face, vertical slice glitch,
   paper-fragment collage, double-exposure heads.
4. **Lookbook / studio minimal**: ivory rooms, outfit triptychs, character
   turnarounds, polaroid close-ups.

Match the family the request implies; blend only when asked.

## Analyzed entries
<!-- Learn mode appends corpus entry ids here, one per line. The seed playbook's
     private entries are not listed. -->
