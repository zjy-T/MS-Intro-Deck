# Presentation Deck — Handover Context

Use this file to onboard any AI assistant (GitHub Copilot, Claude, etc.) to this project.

## What is this?

A 22-slide interactive HTML presentation deck for a Microsoft intro talk on June 26, 2026. The talk is titled **"From Predicting a Single Number to Agentic Coding"** and covers Tony's 6-year journey building with AI across three eras.

Everything lives in a single file: `index.html` (HTML + CSS + JS).

## Slide structure

| Slides | Era | Theme | Status |
|--------|-----|-------|--------|
| 1 | — | Hero title | Done |
| 2 | — | "Who Am I?" timeline | Done |
| 3 | — | Three-era overview cards | Done |
| 4–9 | Era 1: "The Numbers Game" | ML for catalyst prediction (undergrad research) | Done |
| 10–15 | Era 2: "The Language Leap" | NLP/LLMs, fine-tuning, RAG | Placeholder — build next |
| 16–22 | Era 3: "The Agentic Frontier" | Agentic coding, MCP, current work | Placeholder |

## Technical architecture

- **Fixed 1280×720 canvas**: The `#deck` div is always 1280×720 and CSS `transform: scale()` fits it to the viewport. All positioning inside is absolute to this coordinate space.
- **No vertical scroll**: Every `.slide` has `overflow: hidden`. Content must fit within 720px.
- **UI overlays** (`#nav`, `#progress`, `#section-indicator`, `#toc`, `#keys-hint`): All `position: absolute` inside `#deck`, not `position: fixed`.
- **Chart.js v4.4.4**: Used for line/bar charts. Must use `responsive: false` with explicit canvas `width`/`height` attributes to avoid sizing conflicts with the scaled canvas.
- **2x canvas resolution**: For sharp rendering (e.g., heatmap), draw at 2x dimensions and set CSS `width`/`height` to half. Use `dpr=2` multiplier in all drawing code.
- **Slide activation callbacks**: `onSlideEnter(slideIndex, callbackFn)` triggers animations when navigating to a slide. Index is 0-based.
- **Animations**: Snake-line chart animation (S8), waterfall heatmap animation (S9). Built with `setTimeout` chains and Chart.js `update('none')`.

## Design system

- **Font**: DM Sans (Google Fonts)
- **Colors**: Warm neutrals — `--bg: #F5F0EB`, `--text: #1A1A1A`, `--accent: #8B7355` (brown), `--surface: #FAFAF8`, `--border: #DDD9D2`
- **Style**: Clean, minimal, no emojis. Rounded corners (10px cards), subtle borders, staggered fade-in animations.
- **Slide classes**: `.slide.top` for top-aligned content, `.slide.center` for centered. Use `.anim.d1`–`.d5` for staggered entry animations.

## Data files

- `Era 1/training-data.json` — 289-row dataset used for heatmap on slide 9

## Key patterns to follow

1. Build one slide at a time with iterative feedback
2. Animations should be slow enough for live presentation pacing (~300ms between items)
3. Keep visual markers consistent — no color variation unless explicitly requested
4. Content must fit 720px height — no scrolling
5. Preview changes before reporting done
6. Images go in per-era folders (e.g., "Era 2/")

## What to build next

**Era 2 (slides 10–15)** — "The Language Leap". This era covers Tony's work with NLP, large language models, fine-tuning, and RAG systems. The existing placeholder slides in `index.html` (slides 10–15) have scaffold content that needs to be rebuilt with the same quality and interactivity as Era 1.

Look at slides 4–9 in the code for the patterns and quality bar to match.
