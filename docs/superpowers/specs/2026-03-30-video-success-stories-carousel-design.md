# Video Success Stories Carousel — Design Spec
**Date:** 2026-03-30
**Status:** Approved

---

## Overview

Add a "Video Success Stories" carousel section to `index.html`, placed immediately before the existing `<!-- REVIEWS -->` section. The section showcases 5 handheld vertical testimonial videos with owner/dog names, a play-on-click interaction, and a left/right arrow carousel.

---

## Placement

Insert a new `<section id="video-stories">` directly above the `<!-- REVIEWS -->` comment at line ~1644 in `index.html`.

---

## Section Header

- **Background:** `var(--navy)` (`#00224b`) — dark navy, matching reference image
- **Eyebrow tag:** `VIDEO SUCCESS STORIES` (uses existing `.eyebrow-tag` class — gold, uppercase, letter-spaced)
- **Section title:** `Watch Our Graduates in Action` (uses existing `.section-title` class — white on dark bg)
- **Two pill badges** floated right: `REAL PROOF` and `ZERO EDITS`
  - Style: white border (`1px solid rgba(255,255,255,0.5)`), white text, `border-radius: 999px`, small padding
  - Displayed inline-flex, gap between them
- Header row: flex, space-between, align-items center

---

## Carousel Behavior

- **Desktop (≥768px):** 4 cards visible simultaneously
- **Mobile (<768px):** 1 card visible
- **Navigation:** Left/right circular arrow buttons on both sides of the carousel
  - Style: gold background (`var(--gold)`), dark icon, `border-radius: 50%`, ~44px diameter
  - Positioned absolutely on the left and right edges of the carousel viewport
- **Animation:** CSS `transform: translateX` transition (`0.4s ease`) on the cards track
- **Looping:** Wrap-around (carousel loops back from last to first and vice versa)
- **No autoplay, no dot indicators**

---

## Video Cards

### Dimensions & Layout
- **Aspect ratio:** 9:16 (portrait — handheld vertical video)
- **Border radius:** 16px
- **Overflow:** hidden
- Card fills its column slot with `width: 100%`

### Video Element
- `<video>` with `src`, `playsinline`, `preload="metadata"`, no `autoplay`, no `controls`
- `object-fit: cover`, fills card 100%

### Play Button
- Centered absolutely over the video
- Gold circle background (`var(--gold)`), ~60px diameter
- White play triangle SVG icon inside
- On click: toggles play/pause on the `<video>` element
- When playing: play button hides (opacity 0); clicking video again pauses and shows button
- The play button re-appears when video ends (`ended` event)

### Bottom Overlay
- Gradient overlay: `linear-gradient(to top, rgba(0,0,0,0.75) 0%, transparent 50%)`
- Positioned absolutely at the bottom of the card
- **Line 1:** Owner's first name — white, bold, `font-family: 'Barlow Condensed'`, ~18px
- **Line 2:** Dog icon (small paw/dog SVG, gold) + dog's name — gold (`var(--gold)`), ~15px

---

## Video Data

| # | Owner | Dog | URL |
|---|-------|-----|-----|
| 1 | Becca | Dixie | `https://assets.cdn.filesafe.space/h0IYVtb9xf96mkta3cwu/media/69caa7871bccb15e81c6d0d5.mp4` |
| 2 | Dawn | Dog | `https://assets.cdn.filesafe.space/h0IYVtb9xf96mkta3cwu/media/69cab67da8530249db3f643f.mp4` |
| 3 | Fran | Freya | `https://assets.cdn.filesafe.space/h0IYVtb9xf96mkta3cwu/media/69cab5c510542655f561cfc5.mp4` |
| 4 | Madison | Liberty | `https://assets.cdn.filesafe.space/h0IYVtb9xf96mkta3cwu/media/69cab5c5feee3d845db038a9.mp4` |
| 5 | Owner 2 | Dog 2 | `https://assets.cdn.filesafe.space/h0IYVtb9xf96mkta3cwu/media/69cab5c5d1fc9594d4eaf377.mp4` |

---

## Implementation Notes

- **Pure vanilla JS + CSS** — no external libraries, consistent with the rest of the page
- All styles added inline in the existing `<style>` block in `index.html`
- Section and JS added inline in `index.html` (no separate files)
- When a video plays, pause any other playing video in the carousel (only one video plays at a time)
- Section uses `data-aos="fade-up"` on cards for consistency with rest of page animations

---

## Responsive Breakpoints

```css
/* Desktop: 4 cards */
@media (min-width: 768px) {
  .vss-track { --cards-visible: 4; }
}

/* Mobile: 1 card */
@media (max-width: 767px) {
  .vss-track { --cards-visible: 1; }
}
```

Each card width = `calc(100% / var(--cards-visible))`.
