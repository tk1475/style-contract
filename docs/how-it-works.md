# How it works

Image models are great at subjects and terrible at consistency. Every prompt is a fresh roll of the dice, and the dice are loaded toward "glossy stock photo".

A style contract removes the dice. It is five clauses that never change, plus a few modes that can.

## The five clauses

| Clause | Pins down | If you skip it |
| --- | --- | --- |
| **Finish** | Surface texture: grain, ink, paint, lens | Everything comes back smooth and plasticky |
| **Palette** | One anchor hex, supporting colours, one accent, a ban list | "Blue" becomes navy, then teal, then purple |
| **Composition** | Shapes, scale, the copy-safe zone | Busy, centred, everything-in-frame |
| **Subject** | How many things, what is never shown | Crowds, gibberish text, fake logos |
| **Mood** | Three words, plus what it is *not* | Corporate-energetic, every time |

## Modes

The medium can change (illustration, photo, collage). The clauses cannot. Each mode is one sentence, copied into the prompt word for word.

## The tricks that do the heavy lifting

1. **Copy clauses verbatim.** Paraphrasing is how a series drifts.
2. **Say the anchor hex twice.** Once in the palette, once at the very end.
3. **"No text" goes last.** It is the instruction models forget first.
4. **Aspect ratio goes in the settings,** not in the prompt.
5. **Prompt enhancers off.** They "improve" you back to the default.
6. **Prose, not tags.** Modern models read paragraphs.

## The grading step

After every render, Claude runs a 7-point pre-flight check (finish, colour, mode, subject, composition, mood, stray text). A fail comes back with the clause that broke and the fix. Think unit tests, but for pictures.
