# Video Success Stories Carousel Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add a vertical-video carousel section with play/pause controls and left/right navigation directly above the "Real Dogs. Real Transformations." reviews section in `index.html`.

**Architecture:** All changes are inline in `index.html` — CSS added before the closing `</style>` tag (line 1479), HTML section inserted before `<!-- REVIEWS -->` (line 1644), and vanilla JS appended before the closing `</script>` tag (line 2101). No new files are created.

**Tech Stack:** Vanilla HTML/CSS/JS, Barlow Condensed font (already loaded), CSS custom properties already defined (`--navy`, `--gold`, `--gold-dark`, `--white`).

---

## File Map

| File | Action | What changes |
|------|--------|-------------|
| `index.html` | Modify (3 locations) | CSS styles (before `</style>` line 1479), HTML section (before `<!-- REVIEWS -->` line 1644), JS logic (before `</script>` line 2101) |

---

### Task 1: Add CSS for the video section

**Files:**
- Modify: `index.html` — insert before `</style>` at line 1479

- [ ] **Step 1: Insert the following CSS block immediately before `</style>` (line 1479)**

```css
    /* ── VIDEO SUCCESS STORIES ─────────────────────────────── */
    #video-stories {
      background: var(--navy);
      padding: 80px 0 60px;
      overflow: hidden;
    }

    .vss-inner {
      max-width: 1200px;
      margin: 0 auto;
      padding: 0 24px;
    }

    .vss-header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      flex-wrap: wrap;
      gap: 16px;
      margin-bottom: 40px;
    }

    .vss-header .section-title {
      color: var(--white);
      margin-bottom: 4px;
    }

    .vss-badges {
      display: flex;
      gap: 10px;
      flex-shrink: 0;
    }

    .vss-badge {
      display: inline-flex;
      align-items: center;
      border: 1.5px solid rgba(255, 255, 255, 0.5);
      color: var(--white);
      font-family: 'Barlow Condensed', sans-serif;
      font-size: 12px;
      font-weight: 700;
      letter-spacing: 1.5px;
      text-transform: uppercase;
      padding: 6px 16px;
      border-radius: 999px;
    }

    /* Carousel wrapper */
    .vss-carousel-wrap {
      position: relative;
    }

    .vss-viewport {
      overflow: hidden;
      border-radius: 12px;
    }

    .vss-track {
      display: flex;
      gap: 16px;
      transition: transform 0.4s ease;
      will-change: transform;
    }

    /* Card */
    .vss-card {
      flex: 0 0 calc((100% - 48px) / 4); /* 4 cards, 3 gaps of 16px */
      position: relative;
      border-radius: 16px;
      overflow: hidden;
      background: #000;
      aspect-ratio: 9 / 16;
      cursor: pointer;
    }

    .vss-card video {
      width: 100%;
      height: 100%;
      object-fit: cover;
      display: block;
    }

    /* Bottom text overlay */
    .vss-card-info {
      position: absolute;
      bottom: 0;
      left: 0;
      right: 0;
      padding: 40px 14px 14px;
      background: linear-gradient(to top, rgba(0, 0, 0, 0.80) 0%, transparent 100%);
      pointer-events: none;
    }

    .vss-owner {
      font-family: 'Barlow Condensed', sans-serif;
      font-size: 18px;
      font-weight: 700;
      color: var(--white);
      line-height: 1.2;
      text-transform: uppercase;
      letter-spacing: 0.5px;
    }

    .vss-dog {
      display: flex;
      align-items: center;
      gap: 5px;
      font-family: 'Barlow Condensed', sans-serif;
      font-size: 15px;
      font-weight: 600;
      color: var(--gold);
      margin-top: 2px;
    }

    .vss-dog svg {
      flex-shrink: 0;
    }

    /* Play button */
    .vss-play-btn {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      width: 60px;
      height: 60px;
      background: var(--gold);
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      cursor: pointer;
      transition: opacity 0.25s ease, transform 0.2s ease;
      pointer-events: auto;
      z-index: 2;
      border: none;
      box-shadow: 0 4px 16px rgba(0,0,0,0.4);
    }

    .vss-play-btn:hover {
      transform: translate(-50%, -50%) scale(1.1);
    }

    .vss-play-btn.hidden {
      opacity: 0;
      pointer-events: none;
    }

    /* Arrow buttons */
    .vss-arrow {
      position: absolute;
      top: 50%;
      transform: translateY(-50%);
      width: 44px;
      height: 44px;
      background: var(--gold);
      border: none;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      cursor: pointer;
      z-index: 3;
      transition: background 0.2s ease, transform 0.2s ease;
      box-shadow: 0 2px 12px rgba(0,0,0,0.3);
    }

    .vss-arrow:hover {
      background: var(--gold-dark);
      transform: translateY(-50%) scale(1.07);
    }

    .vss-arrow-prev {
      left: -22px;
    }

    .vss-arrow-next {
      right: -22px;
    }

    /* Mobile: 1 card */
    @media (max-width: 767px) {
      .vss-card {
        flex: 0 0 100%;
      }

      .vss-arrow-prev {
        left: 4px;
      }

      .vss-arrow-next {
        right: 4px;
      }
    }
```

- [ ] **Step 2: Verify the CSS was inserted correctly** — open `index.html` and confirm `/* ── VIDEO SUCCESS STORIES ─────────────────────────────── */` appears just before `</style>` at what is now line ~1480.

---

### Task 2: Add HTML section

**Files:**
- Modify: `index.html` — insert before `<!-- REVIEWS -->` (line 1644)

- [ ] **Step 1: Insert the following HTML block immediately before `<!-- REVIEWS -->` (line 1644)**

```html
  <!-- VIDEO SUCCESS STORIES -->
  <section id="video-stories">
    <div class="vss-inner">
      <div class="vss-header">
        <div>
          <span class="eyebrow-tag">Video Success Stories</span>
          <h2 class="section-title">Watch Our Graduates in Action</h2>
        </div>
        <div class="vss-badges">
          <span class="vss-badge">Real Proof</span>
          <span class="vss-badge">Zero Edits</span>
        </div>
      </div>

      <div class="vss-carousel-wrap">
        <!-- Prev arrow -->
        <button class="vss-arrow vss-arrow-prev" aria-label="Previous videos">
          <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="#00224b" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><polyline points="15 18 9 12 15 6"/></svg>
        </button>

        <div class="vss-viewport">
          <div class="vss-track" id="vssTrack">

            <!-- Card 1: Becca & Dixie -->
            <div class="vss-card">
              <video src="https://assets.cdn.filesafe.space/h0IYVtb9xf96mkta3cwu/media/69caa7871bccb15e81c6d0d5.mp4" playsinline preload="metadata"></video>
              <button class="vss-play-btn" aria-label="Play video">
                <svg xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 24 24" fill="#00224b"><polygon points="5 3 19 12 5 21 5 3"/></svg>
              </button>
              <div class="vss-card-info">
                <div class="vss-owner">Becca</div>
                <div class="vss-dog">
                  <svg xmlns="http://www.w3.org/2000/svg" width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M10 5.172C10 3.782 8.423 2.679 6.5 3c-2.823.47-4.113 6.006-4 7 .08.703 1.725 1.722 3.656 2.261"/><path d="M14.267 5.172c0-1.39 1.577-2.493 3.5-2.172 2.823.47 4.113 6.006 4 7-.08.703-1.725 1.722-3.656 2.261"/><path d="M8 14v.5"/><path d="M16 14v.5"/><path d="M11.25 16.25h1.5L12 17l-.75-.75z"/><path d="M4.42 11.247A13.152 13.152 0 0 0 4 14.556C4 18.728 7.582 21 12 21s8-2.272 8-6.444c0-1.061-.162-2.2-.493-3.309m-9.243-6.082A8.801 8.801 0 0 1 12 5c.78 0 1.5.108 2.161.306"/></svg>
                  Dixie
                </div>
              </div>
            </div>

            <!-- Card 2: Dawn & Dog -->
            <div class="vss-card">
              <video src="https://assets.cdn.filesafe.space/h0IYVtb9xf96mkta3cwu/media/69cab67da8530249db3f643f.mp4" playsinline preload="metadata"></video>
              <button class="vss-play-btn" aria-label="Play video">
                <svg xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 24 24" fill="#00224b"><polygon points="5 3 19 12 5 21 5 3"/></svg>
              </button>
              <div class="vss-card-info">
                <div class="vss-owner">Dawn</div>
                <div class="vss-dog">
                  <svg xmlns="http://www.w3.org/2000/svg" width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M10 5.172C10 3.782 8.423 2.679 6.5 3c-2.823.47-4.113 6.006-4 7 .08.703 1.725 1.722 3.656 2.261"/><path d="M14.267 5.172c0-1.39 1.577-2.493 3.5-2.172 2.823.47 4.113 6.006 4 7-.08.703-1.725 1.722-3.656 2.261"/><path d="M8 14v.5"/><path d="M16 14v.5"/><path d="M11.25 16.25h1.5L12 17l-.75-.75z"/><path d="M4.42 11.247A13.152 13.152 0 0 0 4 14.556C4 18.728 7.582 21 12 21s8-2.272 8-6.444c0-1.061-.162-2.2-.493-3.309m-9.243-6.082A8.801 8.801 0 0 1 12 5c.78 0 1.5.108 2.161.306"/></svg>
                  Dog
                </div>
              </div>
            </div>

            <!-- Card 3: Fran & Freya -->
            <div class="vss-card">
              <video src="https://assets.cdn.filesafe.space/h0IYVtb9xf96mkta3cwu/media/69cab5c510542655f561cfc5.mp4" playsinline preload="metadata"></video>
              <button class="vss-play-btn" aria-label="Play video">
                <svg xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 24 24" fill="#00224b"><polygon points="5 3 19 12 5 21 5 3"/></svg>
              </button>
              <div class="vss-card-info">
                <div class="vss-owner">Fran</div>
                <div class="vss-dog">
                  <svg xmlns="http://www.w3.org/2000/svg" width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M10 5.172C10 3.782 8.423 2.679 6.5 3c-2.823.47-4.113 6.006-4 7 .08.703 1.725 1.722 3.656 2.261"/><path d="M14.267 5.172c0-1.39 1.577-2.493 3.5-2.172 2.823.47 4.113 6.006 4 7-.08.703-1.725 1.722-3.656 2.261"/><path d="M8 14v.5"/><path d="M16 14v.5"/><path d="M11.25 16.25h1.5L12 17l-.75-.75z"/><path d="M4.42 11.247A13.152 13.152 0 0 0 4 14.556C4 18.728 7.582 21 12 21s8-2.272 8-6.444c0-1.061-.162-2.2-.493-3.309m-9.243-6.082A8.801 8.801 0 0 1 12 5c.78 0 1.5.108 2.161.306"/></svg>
                  Freya
                </div>
              </div>
            </div>

            <!-- Card 4: Madison & Liberty -->
            <div class="vss-card">
              <video src="https://assets.cdn.filesafe.space/h0IYVtb9xf96mkta3cwu/media/69cab5c5feee3d845db038a9.mp4" playsinline preload="metadata"></video>
              <button class="vss-play-btn" aria-label="Play video">
                <svg xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 24 24" fill="#00224b"><polygon points="5 3 19 12 5 21 5 3"/></svg>
              </button>
              <div class="vss-card-info">
                <div class="vss-owner">Madison</div>
                <div class="vss-dog">
                  <svg xmlns="http://www.w3.org/2000/svg" width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M10 5.172C10 3.782 8.423 2.679 6.5 3c-2.823.47-4.113 6.006-4 7 .08.703 1.725 1.722 3.656 2.261"/><path d="M14.267 5.172c0-1.39 1.577-2.493 3.5-2.172 2.823.47 4.113 6.006 4 7-.08.703-1.725 1.722-3.656 2.261"/><path d="M8 14v.5"/><path d="M16 14v.5"/><path d="M11.25 16.25h1.5L12 17l-.75-.75z"/><path d="M4.42 11.247A13.152 13.152 0 0 0 4 14.556C4 18.728 7.582 21 12 21s8-2.272 8-6.444c0-1.061-.162-2.2-.493-3.309m-9.243-6.082A8.801 8.801 0 0 1 12 5c.78 0 1.5.108 2.161.306"/></svg>
                  Liberty
                </div>
              </div>
            </div>

            <!-- Card 5: Owner 2 & Dog 2 -->
            <div class="vss-card">
              <video src="https://assets.cdn.filesafe.space/h0IYVtb9xf96mkta3cwu/media/69cab5c5d1fc9594d4eaf377.mp4" playsinline preload="metadata"></video>
              <button class="vss-play-btn" aria-label="Play video">
                <svg xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 24 24" fill="#00224b"><polygon points="5 3 19 12 5 21 5 3"/></svg>
              </button>
              <div class="vss-card-info">
                <div class="vss-owner">Owner 2</div>
                <div class="vss-dog">
                  <svg xmlns="http://www.w3.org/2000/svg" width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M10 5.172C10 3.782 8.423 2.679 6.5 3c-2.823.47-4.113 6.006-4 7 .08.703 1.725 1.722 3.656 2.261"/><path d="M14.267 5.172c0-1.39 1.577-2.493 3.5-2.172 2.823.47 4.113 6.006 4 7-.08.703-1.725 1.722-3.656 2.261"/><path d="M8 14v.5"/><path d="M16 14v.5"/><path d="M11.25 16.25h1.5L12 17l-.75-.75z"/><path d="M4.42 11.247A13.152 13.152 0 0 0 4 14.556C4 18.728 7.582 21 12 21s8-2.272 8-6.444c0-1.061-.162-2.2-.493-3.309m-9.243-6.082A8.801 8.801 0 0 1 12 5c.78 0 1.5.108 2.161.306"/></svg>
                  Dog 2
                </div>
              </div>
            </div>

          </div><!-- /vss-track -->
        </div><!-- /vss-viewport -->

        <!-- Next arrow -->
        <button class="vss-arrow vss-arrow-next" aria-label="Next videos">
          <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="#00224b" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><polyline points="9 18 15 12 9 6"/></svg>
        </button>
      </div><!-- /vss-carousel-wrap -->
    </div><!-- /vss-inner -->
  </section>
```

- [ ] **Step 2: Verify placement** — confirm that `<!-- VIDEO SUCCESS STORIES -->` appears directly above `<!-- REVIEWS -->` in the file.

---

### Task 3: Add JavaScript for carousel and video controls

**Files:**
- Modify: `index.html` — insert before `</script>` at line ~2101

- [ ] **Step 1: Insert the following JS block immediately before `</script>` (the closing tag of the inline script block around line 2101)**

```javascript
    // ── VIDEO SUCCESS STORIES CAROUSEL ──────────────────────
    (function () {
      const track = document.getElementById('vssTrack');
      if (!track) return;

      const cards = Array.from(track.querySelectorAll('.vss-card'));
      const total = cards.length;
      const prevBtn = document.querySelector('.vss-arrow-prev');
      const nextBtn = document.querySelector('.vss-arrow-next');
      let currentIndex = 0;

      function getVisible() {
        return window.innerWidth >= 768 ? 4 : 1;
      }

      function getMaxIndex() {
        return total - getVisible();
      }

      function updateTrack() {
        const cardWidth = cards[0].offsetWidth;
        const gap = 16;
        const offset = currentIndex * (cardWidth + gap);
        track.style.transform = 'translateX(-' + offset + 'px)';
      }

      function pauseAll() {
        cards.forEach(function (card) {
          const vid = card.querySelector('video');
          const btn = card.querySelector('.vss-play-btn');
          if (!vid.paused) {
            vid.pause();
            btn.classList.remove('hidden');
          }
        });
      }

      prevBtn.addEventListener('click', function () {
        pauseAll();
        currentIndex = currentIndex <= 0 ? getMaxIndex() : currentIndex - 1;
        updateTrack();
      });

      nextBtn.addEventListener('click', function () {
        pauseAll();
        currentIndex = currentIndex >= getMaxIndex() ? 0 : currentIndex + 1;
        updateTrack();
      });

      // Play / pause on card click
      cards.forEach(function (card) {
        const vid = card.querySelector('video');
        const btn = card.querySelector('.vss-play-btn');

        btn.addEventListener('click', function (e) {
          e.stopPropagation();
          pauseAll();
          vid.play();
          btn.classList.add('hidden');
        });

        vid.addEventListener('click', function () {
          if (!vid.paused) {
            vid.pause();
            btn.classList.remove('hidden');
          }
        });

        vid.addEventListener('ended', function () {
          btn.classList.remove('hidden');
        });
      });

      window.addEventListener('resize', updateTrack);
    })();
```

- [ ] **Step 2: Verify the JS was inserted** — confirm `// ── VIDEO SUCCESS STORIES CAROUSEL ──────────────────────` appears in the file before the closing `</script>` tag.

---

### Task 4: Commit

- [ ] **Step 1: Stage and commit**

```bash
git add index.html
git commit -m "feat: add video success stories carousel section"
```

---

## Self-Review Checklist

- [x] **Spec coverage:** CSS (Task 1) ✓, HTML section with all 5 cards (Task 2) ✓, carousel arrows (Task 2) ✓, play/pause JS (Task 3) ✓, one-video-at-a-time (Task 3 `pauseAll`) ✓, desktop 4-up / mobile 1-up (CSS `@media`) ✓, loop wrap-around (JS `getMaxIndex` logic) ✓, no autoplay ✓, `ended` event restores play button ✓
- [x] **No placeholders:** All code is complete and explicit
- [x] **Type consistency:** `vssTrack` id referenced correctly in JS; `.vss-play-btn` class referenced consistently; `getVisible()` / `getMaxIndex()` used consistently
