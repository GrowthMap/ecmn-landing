# Review "Read More" Modal — Design Spec

**Date:** 2026-04-09
**Status:** Approved

## Overview

Review cards in the `#reviews` section clamp long text to 6 lines. Longer reviews are cut off with no way to read the rest. This feature adds a "Read more" link to clipped cards that opens a simple modal with the full review.

## Behaviour

### "Read more" link
- Injected by JavaScript after page load — no changes to existing HTML
- Appears only on cards where the review text is actually clipped (detected via `scrollHeight > clientHeight` on `.review-text`)
- Styled as a small underlined text link in the site accent color, below the clipped text
- Does not appear on cards whose text fits within 6 lines

### Modal
- Triggered by clicking "Read more"
- Contains:
  - ★★★★★ stars (same gold as cards)
  - Full review text (unstyled paragraph, same font/color as cards)
  - Reviewer avatar, name, and Google Review badge at the bottom
- Centered on screen with a semi-transparent dark backdrop
- White card panel, max-width 600px, matches existing card styling (same border-radius, border, shadow, padding)
- Scrollable internally if the text is very long
- Closed by: clicking the × button (top-right), clicking the backdrop, or pressing Escape
- Focus trap: focus moves to the modal on open; returns to the triggering link on close

## Implementation Notes

- All logic lives in a single `<script>` block added before `</body>` in `index.html`
- All styles live in a `<style>` block in the `<head>` (or appended inline)
- No external dependencies
- The modal markup is created dynamically by JS and appended to `<body>`; it is reused across all cards (content swapped on open)

## Out of Scope

- Pagination or "next/prev" navigation between reviews inside the modal
- Animation beyond a simple CSS fade-in
- Any change to the 6-line clamp CSS already in place
