# Style Handoff — ART 3041

1. Reference: dsgn-dept.com (Design Department) — big type, minimal, editorial. Replaces the earlier Linear/Spotify/Cienne moodboard entirely.
2. Page background is stone (#F1EFE7); all body text is near-black ink (#1C1B17); the one accent color is deep moss green (#4B5842) — used only for the second line of the headline, link underlines, hover states, and the numbered badges, never as a large fill.
3. Headings use Space Grotesk, weight 700. The hero name is the dominant visual element: oversized (clamp 58px–176px), line-height 0.86, tight letter-spacing (-0.03em), one word per line, first line in ink, second line in the accent color.
4. Body text uses Inter, weight 400, ~15px, line-height 1.6, kept short (one to two sentences) under the headline.
5. Nav is plain text, no boxed buttons: a small wordmark on the left; on the right, an underlined "Contact" link plus a small square photo thumbnail — no Home/Work/About links.
6. The photo thumbnail in the nav is click-to-replace: clicking it opens a file picker so the image can be swapped at any time; the chosen photo is remembered locally in the browser.
7. Below the headline, a single 1px hairline rule separates a small meta row (selected-work count on the left, email on the right) from the hero above.
8. The hero is typographic only — no hero photo, no collage, no moving/animated background. Big type carries the page.
9. Work list renders as an asymmetric CSS grid (6 columns on desktop): cards vary in width (2–4 columns) and sit at different vertical offsets so nothing lines up in straight rows. Collapses to a single stacked column on mobile.
10. Work items are outlined cards: 1px solid accent border, transparent fill, square corners (no border-radius), a small numbered circle badge in the accent color.
11. On hover, Work cards invert (fill becomes the accent color, text becomes the background color), lift slightly (translateY -3px), and rotate -1°.
12. These rules apply site-wide and persist across every future build or edit unless explicitly overridden.
