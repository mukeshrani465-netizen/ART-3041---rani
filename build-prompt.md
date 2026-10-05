# build-prompt.md — TM 8.9 Poster Generator

Reference files to attach with this prompt: `skills.md`, `reference-tm-8.9-1972.jpg`, `ui-sketch-v1.png`, `/fonts/InterTight-Variable.ttf`, `/fonts/Archivo-Variable.ttf`.

---

## Part A — Plain-language request (rewrite this in your own words)

I want a web app that makes posters in the style of the 1972 Typografische Monatsblätter 8.9 cover. The rules for the style are in skills.md, so follow them exactly.

The screen should look like my sketch. On the left there's a tall panel where I type the text: the big number, the title word, the headline, which word gets spaced out, the subhead, the box labels and the footer. Under that, a second panel for the structure and style: how many boxes, how fast they grow, the colors and the font. At the bottom left is a big Generate button. Across the top is a bar with the app name, a Shuffle button, and buttons to export SVG, PDF and PNG. The rest of the screen is the poster preview.

When I click Generate or Shuffle, I want a different poster each time, but it should always still look like it belongs to the same series. I want the SVG to open in Illustrator with the text still editable.

---

## Part B — Structured build prompt (for Claude)

**Role:** You are building a single-file web app (`index.html`, HTML + CSS + vanilla JS, no frameworks, no build step) that generates posters strictly following the attached `skills.md`. Treat `skills.md` as law; if a UI option would break a hard rule, don't offer it.

**Layout (match `ui-sketch-v1.png`, desktop ≥ 1200 px):**
1. **Top bar** (spans the right ~70% of the width, rounded, top of the screen): app title "TM 8.9 Poster Generator" on the left; on the right: `Shuffle`, seed field + lock toggle, `Export SVG`, `Export PDF`, `Export PNG`.
2. **Left panel, upper (tall, rounded) — Content:**
   - Issue tag (text), Hero number (text), Title word (text)
   - Headline (textarea, one line per row, 3–6 rows) + Sperrsatz keyword (dropdown filled from the headline's words)
   - Attribution (text), Subhead (text)
   - Box labels: repeating rows of `label` + `sub-label`, count synced to box count
   - Footer: 3 text fields (left / middle / right group)
3. **Left panel, lower (rectangle) — Structure & Style:**
   - Box count (2–5), growth ratio slider (1.30–1.80, default 1.57)
   - Label drift (down / up), dash count (5–9, odd only)
   - Ink/paper preset (curated list, one ink each; default `#1A1A1A` on `#F1EFE8`)
   - Font (Inter Tight / Archivo), format (1:1.29 default, A-series)
4. **Left panel, bottom (small button) — `Generate`:** primary action; re-renders with current settings and a new seed.
5. **Main area (everything else):** live SVG poster preview, centered, scaled to fit the height with a soft shadow. Updates live as fields change.

**Generation logic:**
- Seeded random (e.g. mulberry32). The same seed + settings must always produce the same poster.
- `Generate` = new seed, keep user text. `Shuffle` = new seed **and** randomize the unlocked structure/style settings within the ranges in `skills.md` §11.
- Randomness only varies what `skills.md` §11 allows. Never break §10.

**Rendering (must follow `skills.md`):**
- Build the poster as one SVG (viewBox 900 × 1161 for 1:1.29).
- Headline: first and last lines centered (+0.04em); middle lines force-justified to the measure by per-glyph x positions; the Sperrsatz keyword takes ~70% of the extra space. Measure text with canvas `measureText` after fonts load (`document.fonts.load`).
- Box diagram: top-aligned, geometric growth, margin to margin, grey strokes darkening per box, labels flush right and drifting down, shrink-to-fit.
- Footer: bold initials in ink, the rest light in the mid tint, scaled to fill ~93% of the measure.

**Export:**
- **SVG:** real `<text>` elements (not outlines), fonts referenced by family name plus an embedded `@font-face` (base64) so it previews correctly; must open in Illustrator with editable text.
- **PDF:** via jsPDF + svg2pdf.js from cdnjs/jsdelivr, at the poster's aspect ratio.
- **PNG:** 2× and 4×.
- File names: `tm-poster-<seed>.<ext>`.

**Quality bar:** default settings must reproduce the original TM 8.9 poster closely (compare with the reference image). Deliver one complete `index.html`, not snippets, with fonts loaded from `./fonts/`.
