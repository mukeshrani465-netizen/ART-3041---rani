# Style Handoff — Mukesh Rani, ART 3041

These rules describe the current homepage (index.html). Follow them for every build or edit of this site.

1. **Color.** White page background `#FFFFFF`. Headings in ink `#1C1B17`, body text in gray `#4A4A4A`, small labels in muted gray `#8A8A8A`. Cards are filled with blush pink `#F8DCE3`; numbers and drawings use deep pink `#C9788D`. No other colors.
2. **Type.** Headings in Space Grotesk Bold, letter-spacing −0.02em, line-height 1.1, sized 32–42px. Body in Inter 400–600 at 17px, line-height 1.5. Both fonts are embedded in the file as base64 so they load without Google Fonts.
3. **Intro.** One centered column, 520px wide, text aligned left, with 110px of space above the heading. Name as the heading, then one or two short sentences.
4. **Links.** Inline links stay gray and underlined (1px line, 3px below the text). On hover they darken to ink. No buttons.
5. **Project cards.** Projects sit in a centered, wrapping row. Each card is a 150px pink square with 18px rounded corners and a soft shadow, a large 56px deep-pink number in the middle, and a small uppercase gray label underneath.
6. **Tilt.** Every card is rotated between −8° and +8°, alternating left and right so neighbors never lean the same way. The angle is set per card with `--tilt`.
7. **Hover.** On hover or keyboard focus a card straightens to 0° and lifts 6px over 0.25s. Keyboard focus also shows a 2px ink outline.
8. **Drawings.** Each card carries a small hand-drawn line drawing (an animal, flower or object) in deep pink: 2px rounded strokes, white fills, 38px in the top-left corner, or wrapped around the whole card.
9. **Corner photo.** A 56px round photo is fixed in the top-right corner. Clicking it lets you pick a new photo, which is remembered in the browser.
10. **Phones.** At 600px and below, cards shrink to 130px, numbers to 46px, and the gaps tighten so two cards fit per row.
11. **Motion.** Hover is the only motion on the site. When the visitor has reduced motion turned on, cards don't animate.
12. **Project pages.** Every project page uses the same fonts and colors and ends with a “back to homepage” link. These rules apply to every future build or edit unless I override them.

Always give me a full downloadable file, never code snippets.
