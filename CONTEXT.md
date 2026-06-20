# MS Intro Deck — Build Context

A 45-minute internal presentation for product managers and engineers at Microsoft, covering Tony Zhang's AI journey across three eras. Built as a single-file interactive HTML slide deck.

## Presenter

**Tony Zhang** — Product Manager, Edge Mobile @ Microsoft.
Previously PM at Meituan (Healthcare). MSc Tsinghua (Computational Chemistry), BSc UBC (Chemical Engineering).

## Presentation Structure (25 slides planned)

| # | Slide | Section | Type | Status |
|---|-------|---------|------|--------|
| 1 | Title — "From Predicting a Single Number to Agentic Coding" | Introduction | Hero (photo bg) | ✅ Done |
| 2 | Who Am I? — Personal timeline with photos/certs | Introduction | Light | ✅ Done |
| 3 | Six Years of Building With AI (3-era cards) | Introduction | Light | ✅ Done |
| 4–10 | Era 1 — "The Numbers Game" (7 slides) | Era 1 | Mixed | ❌ Not started |
| 11–13 | Era 2 — "Teaching Machines to See" (3 slides) | Era 2 | Mixed | ❌ Not started |
| 14–20 | Era 3 — "The Agentic Era" (7 slides) | Era 3 | Mixed | ❌ Not started |
| 21–24 | Looking Forward (4 slides) | Looking Forward | Mixed | ❌ Not started |
| 25 | Thank You | Looking Forward | Dark (copper) | ❌ Not started |

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
- `.v-timeline` / `.tl-item` — vertical timeline with gradient line (blue→era2→copper), staggered fade-in per item (300ms apart, 700ms transition)
- `.tl-images` — flex row of images within timeline items, 200px height, natural aspect ratio

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
| `bg-hiker.jpg` | #1 | Hikers on mountain ridge at sunset (replaced bg-hero.jpg) |
| `fig_scheme2.jpg` | #5 | CO₂ reduction reaction scheme |
| `fig_feature_curve_clean.jpg` | #8 | Feature count vs model accuracy |
| `fig_feature_importance.jpg` | #8 | Feature importance ranking |
| `fig_heatmap_clean.jpg` | #9 | Model prediction heatmap |
| `meituan skin analysis/picture taking.jpg` | #13 | Selfie capture UI |
| `meituan skin analysis/results.jpg` | #13 | AI analysis results |
| `screenshots/edge demo.png` | #16 | Edge Mobile demo screenshot |
| `screenshots/khora store front.png` | #18 | Khora storefront |
| `khora-ecommerce-flow-screenshot.png` | #19 | Full-stack architecture diagram |
| `slide 2/2014-1.jpg` | #2 | Syncrude R&D team dinner photo |
| `slide 2/2014-2.jpg` | #2 | Syncrude office/desk photo |
| `slide 2/2020-1.png` | #2 | Coursera cert — Python for Everybody |
| `slide 2/2020-2.png` | #2 | Coursera cert — Applied Data Science with Python |
| `slide 2/2020-3.png` | #2 | Udacity cert — Deep Learning |
| `slide 2/2020-4.png` | #2 | Udacity cert — Intro to Machine Learning with Pytorch |
| `slide 2/2020-5.png` | #2 | Udacity cert — Computer Vision Nanodegree |
| `slide 3/era 1.png` | #3 | CO₂ reduction heatmap (Era 1 preview) |
| `slide 3/era 2.png` | #3 | Meituan skin analysis app screenshots (Era 2 preview) |
| `slide 3/era 3.png` | #3 | Edge Mobile demo with toolbox (Era 3 preview) |

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
| 2026-06-19 | Title slide → hero layout with photo bg | Reference site uses full-bleed cover image; layered mountain ridges evoke "evolution" metaphor; bottom-left text, 68px serif title |
| 2026-06-19 | Title changed to "From Predicting a Single Number to Agentic Coding" | User's chosen title; subtitle "The Evolution of AI, From My Perspective" |
| 2026-06-19 | Presentation date set to June 26, 2026 | User-specified date |

| 2026-06-20 | Hero bg changed from bg-hero.jpg to bg-hiker.jpg | Gradient changed to left-to-right reveal; text moved to top-left |
| 2026-06-20 | Slide 2 rebuilt as "Who Am I?" vertical timeline | Storytelling focus — 7 milestones from 2002–now with photos and certs inline |
| 2026-06-20 | Timeline animations: slow staggered reveal | Each item fades in 300ms apart (total ~2.8s) for presentation pacing |
| 2026-06-20 | Deck expanded from 23 to 25 slides | Accounting for title and ending slides per user spec |
| 2026-06-20 | Page title updated to match slide title | "From Predicting a Single Number to Agentic Coding — Tony Zhang" |
| 2026-06-20 | Slide 3: three-era cards with preview images | Each era gets a card with title, years, description, and a representative image |
| 2026-06-20 | Era labels show "Era 1/2/3" not just numbers | More readable at a glance during presentation |
| 2026-06-20 | Era card images use consistent framing | `.era-img-wrap` with border + background padding for visual consistency across different image styles |
| 2026-06-20 | Era cards animate in individually (0.7s, 300ms apart) | Matches slide 2 timeline pacing; scoped to `.timeline-card` to avoid affecting other slides |

## Slide 2 — "Who Am I?" Details

### Timeline entries (in order)
1. **2002** — Immigrated to Canada (from Beijing, age 8)
2. **2014** — First Internship at Syncrude R&D (2 photos: team dinner, office)
3. **2018** — BASc. Chemical & Biological Engineering, UBC → moved to China for Tsinghua
4. **2019–2020** — Covid Pivot: stuck in Canada, transitioned to computational, self-taught coding/ML (5 certs: 2 Coursera, 3 Udacity)
5. **2021** — MSc. Computational Chemistry, Tsinghua University
6. **2021–2025** — PM at Meituan, Healthcare Division
7. **2026–Now** — PM at Microsoft, Edge Mobile

### Design choices
- Timeline dots: consistent copper outline, white fill
- Timeline line: solid `var(--border)` color
- Images: natural aspect ratio, 200px height, no cropping
- PDF certs converted to PNG (sips) for `<img>` compatibility
- Udacity SVGs replaced with PNG screenshots (SVGs had right-side padding issue)

## Slide 3 — "Six Years of Building With AI" Details

### Layout
- Three-column grid of era cards (`.timeline-row` → `.timeline-card`)
- Each card: "Era N" label (serif, era-colored), year range, title, description, framed preview image
- Cards have colored top borders (blue / era2 / copper) matching their era
- Subtitle is forced single-line (`white-space: nowrap`)

### Animation
- Cards stagger in individually: 0.4s → 0.7s → 1.0s delay, 0.7s duration
- Scoped via `.timeline-card.anim.d4/d5/d6` selectors (doesn't affect global d5)

### Era cards content
1. **Era 1** — "The Numbers Game" (2018–2021) — heatmap image
2. **Era 2** — "Teaching Machines to See" (2021–2023) — skin analysis app image
3. **Era 3** — "The Agentic Era" (2025–Now) — Edge Mobile demo image

## Working process
- Slides are built one at a time, each reviewed iteratively with user feedback
- Next session should start with slide 4
- User prefers storytelling/interactive style over bullet-point summaries
- User wants consistent timeline markers (no color variation between dots)
- User wants animations to be slow enough for presentation pacing

## Next Steps
- **Slide 4** is next — Era 1 section opener
- Slides 4–25 are placeholder content from the initial build; each will be rebuilt one at a time
- Era 2 has only 3 slides (11-13) — may need expansion to hit 25 total
- User may add image folders per slide (e.g. "slide 2/", "slide 3/") with assets named by year and order
