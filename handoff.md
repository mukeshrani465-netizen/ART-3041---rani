# handoff.md — TM 8.9 Poster Generator

_Last updated: 2026-10-01 (app v1.2, on the course site)_

## How to use this file
Paste this file + `skills.md` + the reference poster into a **new** Claude chat whenever the current chat gets slow, forgets decisions, or starts breaking things. Update the "Done / Decisions / Next" sections at the end of every work session.

## Project
ART 3041 / 3150, typography module, weeks 5–6. A single-page web app (`index.html`) that generates posters in the style of *Typografische Monatsblätter* 8.9 (1972). Style rules live in `skills.md`. AI tool: **Claude** (not Gemini) for the whole project.

## Files
- `reference-tm-8.9-1972.jpg`: the original poster
- `Poster_Visual_Analysis.pdf`: my written analysis
- `skills.md` (v1.3): style rules the app follows
- `build-prompt.md`: Part A plain-language request, Part B structured prompt
- `ui-sketch-v1.png`: interface wireframe
- `index.html`: the app (v1.2). Fonts are embedded, so this one file is all the app needs. Lives at `poster-generator/index.html` in the course site repo; card **10 · Poster Generator** on the homepage links to it, and "← All projects" links back.
- `fonts/`: InterTight + Archivo static Light/Regular/Bold (used by the app and needed in Illustrator); `fonts/variable/` originals
- `test/`: first static test renders from `skills.md`

## Done
- Poster chosen, analysis written, `skills.md` v1 → v1.1 after a test render.
- UI sketched; build prompt written.
- **App v1 built and tested:**
  - Left: Content panel (collapsible sections), Structure & Style panel, Generate button. Top bar: Shuffle text, 9 variations, Reset to TM 8.9, seed + lock, Export SVG / PDF / PNG. Main area: live preview.
  - Generate = new seed; re-rolls every *unlocked* setting (growth ratio, dash count, box alignment, label drift, palette) plus small zone shifts. Same seed = same poster.
  - Shuffle text loads one of 8 definition + taxonomy texts (German and English).
  - 9 variations shows a 3×3 grid of seeds; click one to use it.
  - Font upload slot (the decorative FontSpace fonts can go here).
  - Exports: SVG with real text (font names = PostScript names, e.g. `InterTight-Bold`, so Illustrator matches installed fonts), vector PDF via jsPDF with embedded fonts, PNG at 3×.

- **App v1.1 (after the professor's slides):** 16 ink/paper pairs (13 strong colours; Generate and 9 variations favour colour ~80%); Title block position Top/Middle/Bottom; Diagram position Top/Middle/Bottom/Left side/Right side (side = boxes stacked in a column, vertical dash ruler); box count 0–5 (0 = no boxes, 1 = single box). All new settings have Lock boxes and are included in Generate. `skills.md` → v1.2.
- **App v1.2:** US formats (Letter, Tabloid, 18×24, 24×36, 27×40) next to TM and A-series; PDF exports at real print size. "Move elements" mode: drag any element with the cursor, snaps to margins / centre / top / bottom (Shift-drag = free), arrow keys nudge (Shift ×10), Backspace resets one element, "Clear moves" resets all; moves clear on Generate / new seed / Shuffle text / Reset. Each box can hold an uploaded image (Fill box or Fit inside, Keep label on/off, Remove); label gets a paper-coloured backing over a picture. SVG export is now grouped (`hero`, `title`, `headline`, `box-1`…) so Illustrator shows named groups. `skills.md` → v1.3.

## Decisions & why
- **Two weights only (Light + Bold)**: the poster separates title from headline by weight, not size.
- **Headline middle lines justified by letterspacing; one Sperrsatz keyword** (plus the word spaces around it) absorbs ~70% of the extra width.
- **Boxes top-aligned, growth ~1.57×, strokes grey and darkening**, measured from the original. If the boxes run out of height, they shrink and the gaps widen so the row still spans margin to margin.
- **Headline size shrinks automatically** for long text so the diagram always has room.
- **Colours are solid mixes, not transparency**, so PDF/Illustrator files print cleanly.
- **Fonts:** Google Fonts neo-grotesks. The FontSpace fonts are decorative, personal-use demos (Qindret has no digits, Caramel Sundae no colon), so they're only offered through Upload.
- From the professor's slides I took only what fits this poster: colour range and movable layout. Kept out his presets, shape layers, effects, custom type areas (not needed for this style).
- Borrowed from the professor's example (Modernist Poster Maker): seeded shuffle, seed lock, 9-variant grid, reset, font upload, SVG/PNG export. Left out shapes, brushes, textures (they break `skills.md` §10). Images are allowed only inside boxes (my request, v1.2).

## Known limits
- Uploaded images are kept after a page reload only if they fit in browser storage; large photos may need re-uploading.
- PDF text is placed with the browser's measurements; jsPDF doesn't kern, so the PDF can differ from the SVG by a hair.
- Opening `index.html` by double-clicking (file://) may block font loading; use GitHub Pages or a local server.
- Uploaded .otf/.woff fonts work in SVG/PNG; the PDF falls back to Inter Tight (jsPDF needs .ttf).

## Next
1. Upload the homepage `index.html` (with card 10) and the `poster-generator/` folder to the course site repo; open the live link and test Export.
2. Export an SVG and a PDF, open both in Illustrator, confirm the text is editable (install the fonts from `/fonts` first).
3. Stress test (step 9): try to recreate a Müller-Brockmann Tonhalle poster; screenshot what breaks; give the screenshots + this file + `skills.md` to a **fresh** Claude chat to rewrite the prompt and `skills.md`.
4. Refine, then generate the final poster series.
