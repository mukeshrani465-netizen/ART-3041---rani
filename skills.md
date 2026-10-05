# skills.md (v1.3) — Designing in the manner of *Typografische Monatsblätter* 8.9 (1972)

## Purpose
This file teaches an AI how to design posters in the style of the 1972 TM 8.9 cover ("SCHRIFT: Ein System von visuellen Zeichen…"). It is the rulebook for a **poster generator web app**: every poster the app makes must obey these rules, and the randomness only varies things *inside* them. Reference image: `reference-tm-8.9-1972.jpg`.

**The idea, in one line:** a typographic lecture set as a poster. The poster *is* a diagram about language. Form acts out meaning (the word "visuellen" is made more visible by spacing it out; the boxes grow as the writing systems grow).

**Tone:** rational, calm, academic, didactic, quietly witty. No decoration, no images, no emotion carried by color. Everything is said with scale, weight, spacing and position.

---

## 1. Format & margins
- Portrait. Default ratio **W : H ≈ 1 : 1.29** (original ~23 × 30 cm, almost exactly US Letter).
- Other formats: A-series (1 : 1.414), US Letter 8.5 × 11 in, Tabloid 11 × 17 in, Poster 18 × 24 in, Poster 24 × 36 in, Movie one-sheet 27 × 40 in. All zones are percentages of H, so the system stretches to any of them; PDF export uses the real print size.
- Side margins: **9% of W** each side. Top margin: **5% of H**. Bottom margin: **3% of H**.
- **Content width** (the measure) = W − 2 × margin. Almost everything spans or centers on this measure.

## 2. Color
| Token | Value | Use |
|---|---|---|
| `paper` | `#F1EFE8` (warm off-white) | background |
| `ink` | `#1A1A1A` | all main type, box 3 |
| `ink-mid` | ink at ~60% | box 2 stroke, footer lowercase |
| `ink-light` | ink at ~35% | box 1 stroke, colon after title, micro text |

- **One ink only.** Hierarchy comes from tints of that one ink, never from a second hue.
- Generator may swap ink/paper pairs (e.g. dark red on cream, black on pale grey), but always **one ink + its tints**.

## 3. Typeface
- **One neo-grotesk family** (Akzidenz-Grotesk / Helvetica type), two weights only: **Light (300)** and **Bold (700)**. Regular (400) is allowed only for micro text.
- Recommended open-source stand-ins (Google Fonts): **Inter Tight** (primary; note it is slightly narrower than Akzidenz, so the headline looks a touch condensed), **Archivo** (has light→black in one family), **Schibsted Grotesk** or **Hanken Grotesk** (warmer, more Akzidenz).
- Never use: serifs, scripts, rounded or decorative display faces, italics. Emphasis is done with **letterspacing (Sperrsatz)**, never italics or color.

## 4. Vertical structure (top → bottom, as % of H)
| Zone | Element | Position (% H) | Alignment |
|---|---|---|---|
| 0 | Issue tag "Nr. 8.9\|1972" | 2–3% | flush right to margin |
| 1 | **Hero number** "8.9" | 5–13% | centered |
| — | air | 13–21% | — |
| 2 | **Title word** "SCHRIFT:" | 21–25% | centered |
| 3 | **Definition headline** (5 lines) | 29–55% | centered axis, middle lines justified (see §6) |
| 3a | Attribution "Tomás Maldonado · 1961" | top of headline line 1 | flush left to margin, hanging outside the text block |
| 4 | Subhead "Es gibt 3 Arten von Schriften:" | 58–60% | centered |
| 5 | Dash ruler | ~62% | spans full measure, symmetric |
| 6 | **Box diagram** (3 squares) | 65–93% | left box on left margin, right box on right margin |
| 7 | Footer masthead | 96–97% | full width, three groups |
| — | Vertical micro credit | right edge, beside box 3 | rotated 90°, tiny |

**Composition rule:** the top half is **symmetric** (centered axis). The bottom half is an **asymmetric progression** (left → right, small → large). The left margin quietly ties them together: attribution, box 1 and footer all start on it.

## 5. Typographic scale
Sizes are font-size as **% of poster height H**. Ratios matter more than exact values.

| Level | Element | Size (% H) | Weight | Case / tracking |
|---|---|---|---|---|
| 1 | Hero number | 11.5% | Bold | tight, −0.02em |
| 2 | Title word | 5.5% | **Light** | ALL CAPS, +0.03em; colon in `ink-light` |
| 3 | Definition headline | 4.8% | Bold | sentence case, leading 1.05–1.1 |
| 4 | Box 3 label | 3.8% | Bold | tight |
| 5 | Subhead | 2.2% | Bold | +0.02em |
| 5 | Box 2 label | 2.2% | Bold | — |
| 6 | Footer | 1.6% | Bold initials / Light rest | — |
| 6 | Issue tag | 1.4% | Regular | `ink-mid` |
| 7 | Box 1 label | 1.3% | Regular | `ink-mid` |
| 8 | Box sub-labels "(WORTSCHRIFT)" | 0.8% | Regular | ALL CAPS, +0.1em |
| 8 | Attribution, vertical credit | 0.6% | Regular | `ink-light` |

**Reading order (hierarchy):** 8.9 → SCHRIFT: → headline → box 3 → subhead → box 2 → box 1 → footer → micro text.

**Key contrast:** the title word is almost as large as the headline but **Light**; the headline is smaller but **Bold**. Weight, not size, separates them. Keep this.

## 6. The headline: track-justified block (signature move)
- The definition is set in 5 lines on a centered axis.
- **First line ("Ein System") and last line ("von Sprache.") are centered, not full width**, with a light base tracking of +0.04em.
- **The middle lines are forced to the full measure by letterspacing, not word spacing.** Each middle line gets whatever tracking it needs to reach the margins.
- **One keyword per poster is set in Sperrsatz** (letter-spaced, e.g. `v i s u e l l e n`, about +0.4–0.6em) and absorbs most of the extra width on its line. Other lines use gentler tracking (0–0.1em).
- Line breaks are chosen by meaning (one idea per line), not by auto-wrap.

Generator algorithm:
1. Split the headline into lines (user-set breaks, or break at phrase boundaries).
2. Center line 1 and the last line at natural width.
3. For each middle line: measure natural width → spread the gap: if a tagged keyword exists on the line, it takes ~70% of the extra space as letterspacing, the rest goes evenly to other letters.
4. Clamp tracking at 0.8em; if a line still can't reach the measure, re-break it.

## 7. The dash ruler
- A row of short horizontal dashes across the full measure, sitting between subhead and boxes.
- **Symmetric around the center axis.** Dash lengths **grow toward the center** (short at edges, longest in the middle) — a ruler that visually "measures" the diagram.
- Default: 7 dashes, lengths in ratio 1 : 2 : 3 : 6 : 3 : 2 : 1 (× 1.2% W), stroke 1.5–2 px equivalent, `ink`.

## 8. The box diagram (progression engine)
- **N outlined squares** (default 3), **no fill**, set in a row along the measure.
- **All boxes share the same top edge** and hang downward (like a bar chart turned upside down).
- Sizes grow by a constant ratio **r ≈ 1.57** (original widths ≈ 18% : 28% : 44% of the measure). Box 1 starts on the left margin; the last box ends on the right margin; gaps grow slightly with the boxes.
- **Stroke tone and weight grow with the box, but stay thin and grey:** box 1 ≈ 30% ink, box 2 ≈ 50%, box 3 ≈ 70%; widths ~1 → 1.6 px at 900 px wide. Solid-black outlines look too heavy (found in test render v1).
- **Labels sit inside each box, flush right** with a small inset (~4% of box width).
  - Label size grows with the box (see §5).
  - Label vertical position drifts downward per box: box 1 at ~10% from top, box 2 at ~33%, box 3 at ~50% (centered). The labels form a diagonal step down through the diagram.
  - Format: `number. Name` (bold) with the `(SUBLABEL)` in tiny caps on the line below, also flush right. Leave a clear gap (≈ 0.3 × label size + 1% H) so the sub-label never touches descenders.
  - A label may never exceed the box width minus insets; shrink it to fit.
- The largest box is the second-loudest element on the poster after the hero number.

## 9. Footer masthead
- One line at ~97.5% H, split into 3 groups: left group flush left, right group flush right, middle group centered in the gap. Scale the footer size so the three groups together fill ~93% of the measure (it should read as a band across the full width).
- **Initial capitals are Bold `ink`; the rest of each word is Light `ink-mid`.** The bold initials spell hidden acronyms (T M / S G M / R S I).
- The generator applies this automatically to any footer text: bold the first letter of each capitalized word.

## 10. Hard rules (never break)
1. No textures, gradients, shadows or decoration. Only type, thin rules and outlined squares. **Exception:** a picture or graphic may sit *inside* a diagram box (filled edge to edge, or fitted with a margin); its label then sits on a small paper-coloured backing, or is hidden.
2. One type family, Light + Bold.
3. One ink color plus its tints.
4. The title block is symmetric (centred on its column); the diagram is a progression (left→right in a row, top→bottom in a side column).
5. Emphasis by letterspacing and scale only — no italics, no underline, no color accent.
6. Lots of empty paper. Air above and below the title word is mandatory; never fill the space between the hero number and the title.
7. Every element aligns to the margin, the center axis, or a box edge. Nothing floats freely.
8. Text content should make sense: the poster explains or classifies something (definition + taxonomy).

## 11. What the generator may randomize (within the rules)
- Hero number/text, title word, headline text and which word gets Sperrsatz.
- **Title block position:** top (original), middle or bottom of the page.
- **Diagram position:** bottom (original), top, middle, or a **side column** (left or right). In a side column the boxes stack top→bottom, grow downward, hang from the outer or inner edge, and the dash ruler turns vertical in the gutter. The text column narrows to ~63% of the measure.
- Blocks in the same band stack with a fixed gap (4.5% H); a top block starts at 5% H, a bottom block ends at 93.5% H, a middle block centres in the space left.
- Number of boxes **0–5** (0 = subhead and ruler only; 1 = a single square flush to the right margin), growth ratio r (1.3–1.8), top- or bottom-aligned boxes.
- Label drift direction (downward default; upward allowed).
- Dash count (5, 7 or 9) and length pattern (always symmetric).
- **Ink/paper pair** from a curated list: 3 neutrals (incl. the original) and 13 strong colours (Swiss red, signal yellow, cobalt, orange, pink, mint, sky, lilac, green, oxblood, ochre, red on black, white on red). Random picks favour colour (~80%). Always one ink + its tints on one paper.
- Headline size shrinks automatically so every block fits.

- **Manual moves:** the user can drag any element (hero, title, headline, attribution, subhead, ruler, each box, footer, credits). Moves snap to the margins, centre axis, top and bottom lines; they are cleared when a new seed is generated.

## 12. Self-check before output
- Can you read the hierarchy in the order of §5 at a glance?
- Is the title Light and the headline Bold?
- Do the middle headline lines hit both margins exactly?
- Do boxes share a top edge, grow left→right, and span margin to margin?
- Is there exactly one ink?
- Does it still feel like a calm lecture, not a party flyer?
