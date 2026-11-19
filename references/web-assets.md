# Greenroom web playbook

Prompts for images that go into websites: hero mockups, section visuals, backgrounds,
cards, social images. Read this together with `learned-patterns.md`; this file
overrides it where they disagree (web assets are product shots, not fashion posters,
so there is no identity lock and no baked-in typography).

## The anchor prompt (proven result)

This prompt produced a green-screen laptop on a concrete ledge that went live as a
production website hero. Follow-up renders in the same series (a multi-device set, a
hand-held phone, a studio monitor) were made by attaching it as the reference image.

```
Style: Photorealistic 3D product render, premium tech-brand hero shot, studio quality, isolated on pure black.

Main Subject: A modern space-grey MacBook Pro, lid open at about 100 degrees, resting on a thick slab of rough dark charcoal concrete that juts out like a ledge. The laptop sits on the slab's left end and its left third overhangs empty black space, so the anodized aluminium underside and two small rubber feet are visible from below.

Screen: CRITICAL: the display is a perfectly flat, uniform solid chroma green (#00FF00) from edge to edge. No interface, no text, no logo, no reflections, no gradient, no glare. The thin black bezel and small top notch stay clearly visible around the green, with crisp, straight edges. The green gives off no light and casts no glow on the aluminium or the concrete.

Camera: Low three-quarter view from slightly below the ledge, looking up. The front-left corner of the laptop's base is closest to the camera, and the lid's right side recedes. 50mm lens, f/8, everything sharp. The camera is pushed far back so there is a lot of black negative space above and around the subject. The whole laptop is in frame with nothing cropped; only the concrete slab runs off the right edge of the frame.

Scene: Nothing else. No table, no floor, no wall, no horizon. The laptop and slab float in an infinite black void.

Concrete: Dense dark-grey cast concrete with real pitting, small air holes and a rough broken texture. The front face sits in shadow, with a soft contact shadow where the laptop rests on it.

Lighting: Low-key studio lighting. A single soft key light from the upper left grazes the top edge of the lid and the front lip of the base, giving a thin, crisp highlight along the aluminium edges. A faint cool rim light comes from behind on the right. Everything else falls off into deep shadow. Subtle and moody, never bright.

Palette: Pure void black background (#000000), graphite and space-grey metal, charcoal concrete, and the one flat green screen. No other colours.

Quality: 8K, ultra-realistic, high-end product photography, true-to-life material rendering, accurate aluminium micro-texture, clean geometry, matte finish, subtle film grain.

Aspect Ratio: 21:9

Negative: no text, no logos, no Apple logo, no UI on the screen, no reflections on the screen, no green light spill, no keyboard visible, no extra devices, no hands, no people, no floor, no background gradient, no vignette glow, no lens flare, no bokeh, no plastic look, no warped or bent laptop geometry, no AI artifacts, no watermark.
```

## Why it worked (apply these to every web asset)

1. **Built for compositing, not for looking finished.** The image is a raw part that
   code will finish. Every choice serves the next step: key, warp, mask, overlay.
2. **A flat chroma screen with its own CRITICAL block.** Flat #00FF00, edge to edge,
   no UI, no glare, no gradient, and above all *no glow and no light spill* on the
   metal or the surface. Spill is what ruins a key. Bezel and notch "crisp, straight
   edges" so the four screen corners can be found and a screenshot warped in.
3. **Isolated on a pure #000000 void.** "No table, no floor, no wall, no horizon."
   The black drops out with a screen/lighten blend or a luminance mask, so the object
   sits on any dark section, hatch pattern or gradient the site already has.
4. **Framing tells the layout where the object meets the page.** "Camera pushed far
   back", "whole laptop in frame with nothing cropped", and exactly one element
   allowed to bleed off one named edge ("only the concrete slab runs off the right
   edge"). That bleed edge is where the image butts against the viewport.
5. **Negative space is placed, not just requested.** Say which side stays empty and
   why ("black negative space above" so a headline can sit there).
6. **Unbranded hardware.** "No Apple logo", "no logos", no text. Keeps it usable for
   any client and avoids garbled marks.
7. **House tech lighting.** Low-key, one soft key from the upper left drawing a thin
   crisp highlight on metal edges, a faint cool rim from behind right, the rest falls
   into shadow. Restrained palette: black, graphite, one material (concrete), the
   green. Use this as the default unless the site's palette says otherwise.
8. **Geometry negatives.** "No warped or bent laptop geometry", "no keyboard visible"
   (the low angle hides it; saying so stops the model from forcing it in).
9. **Series consistency by reference image.** Follow-up shots attach the first render
   and say: "Use (REFERENCE IMAGE) for lighting, concrete material, camera height and
   colour grade only. Match it exactly." Name what to copy and imply what to change.
10. **Hands never touch the screen.** For held devices: "NOTHING covers the screen:
    no finger or thumb overlaps the display", plus a full hand-anatomy negative list.

## Web rules (defaults for every web prompt)

- **No text in the image.** Headlines, labels and buttons are HTML. Only bake in
  text when the asset is a social/OG card and the user gives the exact words.
- **Aspect ratio from where it sits on the page:**
  - full-width hero 21:9 (or 16:9); split hero half 4:5 or 1:1
  - section/feature visual 4:3 or 3:2; card thumbnail 16:9 or 1:1
  - mobile hero / phone-held shot 4:5 or 9:16
  - Open Graph / social share 1.91:1 (state it as 1200x630 framing)
  - background texture or pattern 16:9, tileable if asked
- **Background matches the site.** Dark site: pure #000000 void. Light site: pure
  #FFFFFF or a named off-white with hex, "seamless infinite cyclorama, no horizon
  line". Transparent is not available, so pick the colour the page already uses
  or one that is trivial to mask.
- **Leave room for overlay:** for heroes and banners name the empty side ("left 40%
  is empty black for the headline").
- **Screens:** always chroma green with the CRITICAL block above, unless the user
  wants a finished screen with a specific UI. Then describe the UI in broad shapes
  (nav bar, large heading block, three cards), never real copy.
- **Backgrounds and textures:** low contrast, low detail in the middle so text stays
  readable, "even exposure, no vignette", no focal subject.
- **Icons and 3D objects:** one object per image, centred, same camera angle and
  light across the set so they read as a family; say "part of a matching set".
- **People (testimonials, team, about):** only with a reference photo of the real
  person. Never invent faces presented as real customers.
- **Series:** when the user is making more than one asset for the same site, the
  first approved render becomes the reference image for the rest (rule 9).

## Asset menu (what to offer when the user just says "web")

| Asset | Default framing | Notes |
|---|---|---|
| Hero device mockup | laptop/monitor on a plinth or ledge, 21:9 | the anchor prompt; change plinth material to match brand |
| Multi-device set | laptop + phone (+ tablet), 21:9 or 16:9 | every screen green; "about a hand's width apart" |
| Held phone | hand from bottom right, 4:5 | no fingers on screen; optional watch/sleeve for character |
| Monitor / desk scene | studio monitor, 16:9 | still isolated; no desk clutter unless asked |
| Product on plinth | the client's product, 4:5 or 1:1 | needs a product reference image |
| Abstract hero visual | sculptural form, glass, light, 21:9 | no subject to key; negative space for headline |
| Section background | texture/gradient/material, 16:9 | quiet centre, no focal point |
| Feature icons (3D) | single object, 1:1 | set of matching objects, same light and angle |
| Card / blog thumbnail | 16:9 | one clear subject, readable small |
| Social / OG image | 1.91:1 | may include the exact quoted title text |

## Structure

Use the labeled-fragment brief from `learned-patterns.md` in this order:
`Style → Main Subject → Screen (if any) → Camera → Scene → Material → Lighting →
Palette → Quality → Aspect Ratio → Negative`. Use a `Use (REFERENCE IMAGE) for …
only` line right after Style whenever a reference is attached.

## After the image

Mention only if the user asks how to use it. The usual pipeline, in any image tool
or a short Python/OpenCV script:

1. Key out the #00FF00 screen to get a mask, and find its four corners.
2. Remove green spill from the bezel and nearby edges (desaturate greens there).
3. Perspective-warp a page screenshot into those four corners and composite it
   under the bezel.
4. Drop the #000000 void with a screen/lighten blend or a luminance mask so the
   device sits on the site's own background.
