# greenroom

**A Claude skill that writes AI image prompts that actually work, for websites and
for your own style.**

Greenroom turns prompts that already worked into a playbook, then writes new prompts
from that playbook. It started as a personal prompt-engineering tool for Nano Banana
Pro in Google Flow, and it's best at the images a website needs: hero device mockups
with chroma-green screens, isolated backgrounds, 3D feature icons, section textures
and social cards. It works with any image model that takes long, structured prompts.

The name comes from its signature move: every device screen it asks for is a flat
`#00FF00` chroma green with no glow or spill, so you can key it out and drop your
real UI in.

---

## The three modes

### 1. Web: prompts for website and UI assets

Ask for an image for a site and Greenroom writes a prompt built for **compositing**,
not for looking finished. The image is a raw part your code or design tool finishes.

- **Chroma-green screens** (`#00FF00`, edge to edge, no UI, no glare, no light spill)
  with crisp bezels, so the four corners are easy to find and warp a screenshot into.
- **Isolated on a pure void** (`#000000` for dark sites, `#FFFFFF` for light ones) so
  the object drops onto any section background.
- **Aspect ratio from placement**: 21:9 full-width hero, 4:5 split hero, 4:3 section,
  16:9 card, 1.91:1 OG image.
- **Negative space placed on purpose**: it names which side stays empty for your
  headline.
- **No baked-in text or logos.** Headlines are HTML.
- **Series consistency**: your first approved render becomes the reference image for
  the rest of the set.

If you just say `greenroom web`, it asks up to four quick questions (asset, site
background, placement, reference) and then writes the prompt. Asset menu: hero device
mockup, multi-device set, held phone, monitor scene, product on plinth, abstract hero,
section background, 3D feature icons, card thumbnail, social/OG image.

```
greenroom web: hero mockup, laptop and phone, dark site, full-width
```

### 2. Generate: new prompts in a learned style

Ask for any image prompt and Greenroom composes it from the playbook in
`references/learned-patterns.md`: proven prompt structures (labeled-fragment brief,
markdown campaign brief, creative-director role-play, JSON style object, cinematic
prose), typography rules that render reliably, camera and lens vocabulary, limited
named palettes, anti-AI negative blocks, quality tags. It matches the visual family
your request implies (typography posters, surreal composites, editorial effect
portraits, studio lookbooks) and returns **one ready-to-paste prompt, nothing else**.

```
give me a greenroom prompt: surreal poster, giant hand lifting a tiny figure off a rooftop, 4:5
```

It ships with a seed playbook so it works out of the box. Run Learn to make it yours.

### 3. Learn: train it on your own prompts

Give Greenroom the prompts that worked for you, paired with the images they made.
It reads each image next to its prompt, works out which phrases actually showed up in
the result (and where the model drifted), and merges that into the playbook. Each
example is analyzed once and recorded, so later runs only look at new ones.

1. Put your images in `corpus/` (or anywhere; tell Claude the path).
2. Create `corpus/corpus.json`. Copy `corpus/corpus.example.json` to start:

   ```json
   [
     {
       "id": "poster-01",
       "image": "posters/poster-01.jpeg",
       "prompt": "the exact prompt you used",
       "notes": "optional: what you liked about it",
       "tags": ["optional", "editorial"]
     }
   ]
   ```

3. Tell Claude: `greenroom learn`.

Your `corpus/` folder is in `.gitignore`, so your images and prompts stay private if
you fork this repo and push your changes.

---

## Install

**Claude Code**

macOS / Linux:

```bash
git clone https://github.com/BetzalelTusk/greenroom ~/.claude/skills/greenroom
```

Windows (PowerShell):

```powershell
git clone https://github.com/BetzalelTusk/greenroom "$HOME\.claude\skills\greenroom"
```

To use it in one project only, clone into that project's `.claude/skills/greenroom`
instead. Start a new session and Claude picks it up.

**Claude.ai / Claude desktop app**

Download this repo as a ZIP (Code → Download ZIP), then add it under
Settings → Capabilities → Skills.

## What's inside

```
greenroom/
├── SKILL.md                      # how Claude runs the three modes
├── references/
│   ├── learned-patterns.md       # the prompt playbook (Learn mode rewrites this)
│   └── web-assets.md             # the website/UI asset playbook + anchor prompt
└── corpus/
    └── corpus.example.json       # format for your own prompt+image pairs
```

## Make it your own

Fork it. The two playbooks are plain Markdown, so you can edit them by hand too:
change the default lighting, add an asset type to the menu, add a visual family. Pull
requests with new proven patterns (and the image that proves them) are welcome.

## License

MIT
