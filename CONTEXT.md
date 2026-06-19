# MS Intro Deck — Build Context

A 45-minute internal presentation for product managers and engineers at Microsoft, covering Tony Zhang's AI journey across three eras. Built as a single-file interactive HTML slide deck.

## Presenter

**Tony Zhang** — Product Manager, Edge Mobile @ Microsoft.
Previously PM at Meituan (Healthcare). MSc Tsinghua (Computational Chemistry), BSc UBC (Chemical Engineering).

## Presentation Structure (23 slides)

| # | Slide | Section | Type |
|---|-------|---------|------|
| 1 | Title — "My AI Journey" | Introduction | Dark (blue) |
| 2 | About Me | Introduction | Light |
| 3 | Six Years of Building With AI (timeline) | Introduction | Light |
| 4 | Era 1 Section Opener — "The Numbers Game" | Era 1 | Tinted (blue) |
| 5 | The Science Problem (CO₂RR) | Era 1 | Light |
| 6 | Bottlenecking on Computation | Era 1 | Light |
| 7 | The AI-for-Science Approach (funnel) | Era 1 | Light |
| 8 | Optimizing Through Feature Reduction | Era 1 | Light |
| 9 | Results — Highly Accelerated & Accurate | Era 1 | Light |
| 10 | Era 1 Takeaway | Era 1 | Light (centered) |
| 11 | Era 2 Section Opener — "Teaching Machines to See" | Era 2 | Tinted (green) |
| 12 | Cosmetic Medicine at Meituan | Era 2 | Light |
| 13 | AI Skin Analysis (3-step flow) | Era 2 | Light |
| 14 | Era 3 Section Opener — "The Agentic Era" | Era 3 | Dark (copper) |
| 15 | 2025 Completely Changed the Game (comparison table) | Era 3 | Light |
| 16 | Showcase 1 — Edge Mobile Reimagined | Era 3 | Light |
| 17 | The Iterative Build Flow | Era 3 | Light |
| 18 | Showcase 2 — Khora E-Commerce Platform | Era 3 | Light |
| 19 | The End-to-End Stack (architecture) | Era 3 | Light |
| 20 | The Real Cost of Vibe Coding | Era 3 | Light |
| 21 | Lessons Learned | Looking Forward | Dark (blue) |
| 22 | What This Means for Product Managers | Looking Forward | Light |
| 23 | Thank You | Looking Forward | Dark (copper) |

## Design System

### Typography
- **Display / headings**: Instrument Serif (Google Fonts) — elegant, editorial
- **Body text**: DM Sans (Google Fonts) — clean, geometric sans-serif

### Color Palette (low-saturation, 低饱和)

All colors were intentionally desaturated after initial feedback that the original blue (#2C3E6B) and copper (#B0603A) were too harsh.

| Variable | Hex | Usage |
|----------|-----|-------|
| `--blue` | `#5C6B7F` | Dusty slate — Era 1 accent, stat cards, dark slide bg |
| `--blue-light` | `#7A8799` | Lighter variant for hover/secondary |
| `--blue-bg` | `#ECEEF2` | Tinted background for Era 1 slides |
| `--copper` | `#9E8575` | Warm taupe — Era 3 accent, callout borders, cost bars |
| `--copper-light` | `#B8A090` | Lighter variant |
| `--copper-bg` | `#F2ECE8` | Tinted background for Era 3 slides |
| `--era2` | `#6E928A` | Muted sage — Era 2 accent |
| `--era2-bg` | `#E9EFED` | Tinted background for Era 2 slides |
| `--bg` | `#F7F6F3` | Warm off-white page background |
| `--surface` | `#FFFFFF` | Card / callout background |
| `--surface-alt` | `#EDEAE5` | Image placeholder / alt surface |
| `--text` | `#1A1A1A` | Primary text |
| `--text-secondary` | `#555` | Body text / descriptions |
| `--text-muted` | `#8A8A8A` | Labels, captions |
| `--border` | `#DDD9D2` | Card borders |

### Dark Slides
- Blue dark: uses `var(--blue)` as background (`#5C6B7F`)
- Copper dark: uses `#7D6E64` (muted warm gray-brown)
- Nav/counter/section-indicator switch to white via `body.dark-nav` class

### Slide Variants (CSS classes)
- `.dark-slide` — dark background, white text
- `.copper-dark` — warm dark variant
- `.tinted-blue`, `.tinted-era2`, `.tinted-copper` — subtle tinted backgrounds
- `.centered` — vertically + horizontally centered content
- `.top` — content starts from top with extra padding

### Component Library
- `.stat-card` / `.stat-card.accent` / `.stat-card.copper` — metric cards with colored borders
- `.callout` / `.callout.copper-border` — left-border highlighted quotes
- `.bullet-list` — copper-dot bullet lists
- `.cmp-table` / `.cmp-row` / `.cmp-header.yes|.no` — comparison table (blue vs copper headers)
- `.funnel` / `.funnel-step` — horizontal process funnel
- `.skin-steps` / `.skin-step` — numbered step cards
- `.build-flow` / `.build-step` — copper-top-border process cards
- `.cost-bars` / `.cost-bar` — horizontal bar chart
- `.takeaway-grid` / `.takeaway-card` — 2x2 card grid with colored top borders
- `.point-box` — centered quote/takeaway box
- `.timeline-row` / `.timeline-card` — 3-column era timeline
- `.img-frame` — bordered image container
- `.img-placeholder` — dashed-border placeholder (with fallback onerror on `<img>`)
- `.era-label` / `.era1-label|.era2-label|.era3-label` — colored pill badges
- `.divider` — 48px copper accent line

## Technical Details

### Navigation
- **Keyboard**: Arrow keys (←→↑↓), Space (forward), Home/End
- **Buttons**: Prev/Next at bottom center
- **Touch**: Swipe left/right (60px threshold)
- **Hash deep links**: `#1` through `#23` — works on load and updates on navigate
- **TOC dots**: Right edge, appears on mouse hover near right side

### Transitions
- Uses `visibility: hidden/visible` (NOT opacity) to prevent slide overlap during transitions
- `.anim` children animate in with staggered `transition-delay` (`.d1` through `.d5`, 80ms apart)
- Content fades up 12px with 0.45s ease

### Progress Bar
- Fixed top, 3px height
- Gradient from `var(--blue)` to `var(--copper)` (slate → taupe)

### Image Fallbacks
All `<img>` tags have `onerror` handlers that replace with styled `.img-placeholder` divs showing emoji + description. This handles missing images gracefully.

### Dev Server
Run with `npx serve -l 3080 -s .` or use the `.claude/launch.json` config:
```json
{
  "name": "deck",
  "runtimeExecutable": "npx",
  "runtimeArgs": ["serve", "-l", "3080", "-s", "/Users/tonyzhang/Desktop/Presentation Deck"],
  "port": 3080
}
```

### Responsive
- At `≤1200px`: tighter padding, stat grids collapse to 2-col, two-col layouts stack

## Image Assets Used

| File | Slide | Content |
|------|-------|---------|
| `fig_scheme2.jpg` | #5 | CO₂ reduction reaction scheme |
| `fig_feature_curve_clean.jpg` | #8 | Feature count vs model accuracy |
| `fig_feature_importance.jpg` | #8 | Feature importance ranking |
| `fig_heatmap_clean.jpg` | #9 | Model prediction heatmap |
| `meituan skin analysis/picture taking.jpg` | #13 | Selfie capture UI |
| `meituan skin analysis/results.jpg` | #13 | AI analysis results |
| `screenshots/edge demo.png` | #16 | Edge Mobile demo screenshot |
| `screenshots/khora store front.png` | #18 | Khora storefront |
| `khora-ecommerce-flow-screenshot.png` | #19 | Full-stack architecture diagram |

## Reference Style
Inspired by [eclipse.tasteful.work](https://eclipse.tasteful.work/#1) — minimalist, sophisticated, progressive disclosure, section-based navigation. Not a copy; same tier of quality and polish.

## Design Decision Log

| Date | Decision | Reason |
|------|----------|--------|
| 2026-06-19 | Switched from opacity to visibility transitions | Opacity caused old slides to bleed through during 0.45s transition |
| 2026-06-19 | Added two accent colors (blue + copper) | Original monochrome black/white was "too boring" |
| 2026-06-19 | Reduced slide padding from 80px/120px to 48px/72px | Slides were only ~30% full; target is 50-60% content density |
| 2026-06-19 | Desaturated all colors (低饱和) | Blue #2C3E6B and copper #B0603A were too harsh on the eyes |
| 2026-06-19 | Added dark slide variants for section bookends | Title, Era 3 opener, Lessons, Thank You use dark backgrounds for rhythm |
| 2026-06-19 | Image onerror fallbacks | Graceful degradation when images aren't loaded |

## Next Steps
- Per-slide review and refinement (user wants to go one slide at a time)
- Era 2 has only 3 slides (11-13) — may need expansion
- Some image placeholders could be replaced with actual screenshots
- Backend screenshots (`khora backend*.png`, `sneaker gan.png`) exist but aren't used yet
