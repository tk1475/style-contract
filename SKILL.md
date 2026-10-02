---
name: style-contract
description: Use when generating, prompting, art-directing or reviewing AI images (GPT Image, Nano Banana, Seedream, Midjourney, Flux, Imagen) that must share one consistent look, such as brand imagery, hero art, social posts, ads, deck visuals or a series. Builds a written style contract for the project (or loads one from STYLE.md or presets/), writes prompts from it, and checks every result against it.
---

# Style Contract

AI images drift. Ask for ten images and you get ten styles, most of them the same glossy default. A style contract fixes that: a short, strict document that every image must obey, written so an image model can follow it and a human can check it.

The contract governs the look. It never limits the subject: any scene is allowed if the contract holds.

## Workflow

1. **Load the contract.** Look for `STYLE.md` in the project root. If there is none, ask whether to use a preset from `presets/` or build a new one. Never prompt without a contract.
2. **Build one if needed** (see *Building a contract*). Save it as `STYLE.md` so every later session uses the same rules.
3. **Pick exactly one mode** for the image.
4. **Write the prompt** with the recipe below.
5. **Run the pre-flight check** on every result. Regenerate or fix anything that fails; never ship a near miss.

## Building a contract

Work from what the user has: a brand guide, a website, a few images they love, or just adjectives. Ask at most three questions, then draft and let them react. A good contract has five parts. Use `templates/STYLE.template.md`.

| Part | What to pin down | Why |
| --- | --- | --- |
| **Finish** | The surface of the image: grain, print texture, paint, lens. One sentence that would be true of a zoomed-in crop of any image. | Finish is what makes a set read as one family. It is also the first thing models drop. |
| **Palette** | One anchor colour as an exact hex, two or three supporting colours, one accent with a rule for how often it appears, and banned colours. | Models drift on colour. A named hex plus a ban list holds far better than "brand blue". |
| **Composition** | The shapes and scale the frame uses, and the copy-safe zone if text will be overlaid. | Stops the busy, centred, everything-in-frame default. |
| **Subject rules** | How many subjects, what is never shown (crowds, logos, text, tech clichés), and when people are allowed. | Keeps images on message and avoids model gibberish text. |
| **Mood** | Three or four words, plus what the mood is not. | Guards against the corporate-energetic default. |

Then define **two to four modes**: the media the brand may use (for example illustration, photo, collage, 3D). Each mode is one reusable clause naming a medium, an era or tradition, and a lighting style. Modes vary the medium; the five parts above never vary.

Finish with an **off-brand tells** table: the three to six ways you expect output to drift, and the fix for each.

To pull a contract out of existing images: describe what all of them share (that becomes the contract) separately from what varies (that becomes modes). Sample colours from the images rather than guessing hexes.

## Prompt recipe

Current models follow plain descriptive prose better than comma-separated tags. Write one paragraph, in this order:

```
[SCENE: the subject and setting, described plainly and concretely].
Rendered as [MODE clause, copied from the contract].
[PALETTE sentence: anchor colour by name and exact hex, supporting colours, the accent and where it appears].
[FINISH sentence, copied from the contract, stated forcefully].
[MOOD and COMPOSITION words]. Full bleed, no border.
[Repeat the anchor hex]. No text, no logos, no watermarks.
```

Rules that hold across models:

- **Copy the contract's clauses word for word.** Paraphrasing each time is how a series drifts.
- **Name the anchor hex twice**, in the palette sentence and again at the end.
- **Put the no-text instruction last.** It is the instruction most often ignored.
- **Set the aspect ratio in the tool or API**, not inside the prompt.
- **Turn off prompt enhancers** or "magic prompt" features. They rewrite your clauses into the default look.
- **Anything that would carry writing** (a sign, a screen, a document) gets: "any writing on it appears only as abstract grey lines, with no letters or numbers."
- **If copy will be overlaid**, add: "the [upper half] is one clean, uninterrupted field of [anchor colour]."
- **Attach a reference image** when the model accepts one, and say "match this exact palette and finish; change the scene to [SCENE]."
- **Show the thing, not a metaphor.** If the image is for a product feature, put the real output in the scene (the document, the chart, the screen) instead of a symbol for it.

### Model notes

- **GPT Image**: strong instruction following; most likely to add stray text, so keep the no-text line last.
- **Nano Banana (Gemini image)**: excellent with a reference image attached. Sometimes adds a paper border or frame; keep "full bleed, no border" and crop if needed.
- **Seedream**: follows prose well; benefits most from a reference image.
- **Midjourney**: prefers shorter prompts; put the mode clause and palette first, and use a style reference image instead of long finish sentences.
- **Flux**: good with exact colour words; keep the paragraph tight.
- **All models** smooth away grain and texture by default. If the finish comes back clean, escalate the wording rather than accepting it.

## Fixing colour after generation

Even a good render lands a few degrees off the anchor hue. When the colour matters, measure the dominant anchor-coloured pixels and shift only those toward the target hue, leaving the accent, skin and neutrals alone. A small script with Pillow or ImageMagick is enough; offer to write one.

## Pre-flight check

Run on every image before it ships:

1. The finish covers the whole frame, including flat areas like sky.
2. The anchor colour dominates and matches the hex by eye.
3. It reads as exactly one mode.
4. Subject count and accent rule are respected.
5. The composition matches; the copy zone is clean if one was asked for.
6. The mood is right, and none of the "not" words apply.
7. No stray text, logos, watermarks or borders.

Report failures by number and regenerate with the matching fix from the contract's off-brand tells table.
