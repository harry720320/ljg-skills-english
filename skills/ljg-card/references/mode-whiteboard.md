# Mold: Whiteboard (-w)

## Core Creed

**Making the reasoning process visible -- the traces of thought unfolding, breathing through Japanese-style negative space.**

Spirit: Concepts are strung into chains by arrows, keywords are highlighted, accompanied by simple sketched icons. It moves forward but not in a hurry -- each line is one step of reasoning, each blank space is a breath. It is not a polished conclusion, but a process of thinking unfolding.

Form follows spirit, not bound to any specific medium (not a chalkboard, not a whiteboard, not paper). The lacquer-like warm black background is simply the quietest surface that lets content emerge.

**Three Pillars of Aesthetics**:
- "Ma (Negative Space)" -- Space is not leftover; it is the protagonist. The empty areas around content and between paragraphs are part of the design.
- "Kare (Austerity)" -- Color is extremely restrained. Communicate through brightness contrast and subtle temperature shifts. Overall warm gray tone, with a touch of vermilion as the focal point.
- "Suna (Purity)" -- No decoration. No borders, no noise textures, no simulated material textures. Clean to the point where only content and air remain.

## Step 1: Read Template

Read `assets/whiteboard_template.html`

The template provides:
- Handwriting font loading (Permanent Marker + Kalam)
- CSS variables (`--bg`, `--board`, `--ink`, `--red`, `--yellow`, `--blue`, `--green`, `--orange`, `--marker-bg`)
- Chalkboard background + chalk dust texture
- Wooden picture frame (`.board-frame`)
- SVG arrow marker definitions (red `arrow-r` / white `arrow-w` / blue `arrow-b` / green `arrow-g` / yellow `arrow-y`)
- `.colophon` credit section
- `{{CUSTOM_CSS}}` and `{{CONTENT_HTML}}` slots

## Step 2: Understand Content, Choose Style

### 2.1 Extract Structure

Extract from the content:
- **Core thesis**: Summarize in one sentence
- **Reasoning chain**: How is the argument built step by step? Identify A → B → C structure
- **3-8 key concepts**: Concepts that can serve as chain nodes
- **Branching points**: Where does the reasoning diverge, converge, or turn?
- **Drawable concepts**: Which concepts can be quickly expressed with simple sketches?

### 2.2 Choose Style Path

| Style | Visual Features | Trigger Signals | Main Colors |
|-------|----------------|-----------------|-------------|
| **Logic Chain** (default) | Horizontal reasoning chain (→ connections) + vertical hierarchy + yellow keywords + embedded sketches | Has causal/reasoning/argumentation/exposition structure | `--red` arrows + `--yellow` highlights |
| **Brainstorm Wall** | Core word centered + radial branches + color block sticky notes + scattered keywords | Divergent/multi-perspective/creative/brainstorming | `--yellow` dominant |
| **Timeline** | Vertical timeline + nodes + side notes + contrasting colors | Time/stage/process/retrospective content | `--green` dominant |
| **Matrix Analysis** | 2x2 or multi-cell matrix + quadrant labels + distributed elements | Classification/comparison/evaluation/decision framework | `--blue` dominant |

**Selection Principles**:
- Default to "Logic Chain" -- best captures the chalkboard reasoning feel
- Content has multiple parallel viewpoints → Brainstorm Wall
- Content has time/stage dimension → Timeline
- Content involves classification/quadrants → Matrix Analysis

### 2.3 Color Palette -- Washi Milk White + Vermilion

Japanese minimalism. Milk-white base like handmade washi paper, ink-colored text like brush calligraphy strokes, vermilion red like a square seal focal point. Use structure and font weight to speak, not color.

| Variable | Color Value | Role |
|----------|------------|------|
| `--board` | `#F7F3EC` Washi | Milk-white base, warm handmade washi |
| `--ink` | `#2C2826` Ink | Body text, warm near-black like ink |
| `--ink-light` | `#8A8478` Gray Ink | Annotations, asides |
| `--yellow` | `#7A6B4E` Roasted Tea | Highlighted text -- roasted tea color, stable and readable on milk-white |
| `--red` | `#A09888` Stone | Arrows -- quiet stone gray, guiding without competing |
| `--shu` | `#C03C28` Vermilion | Focal point -- true vermilion red, no more than 3 per board |

Frame: `rgba(180,170,155,0.15)` extremely faint warm gray line, almost invisible against background.

**Principles**:
- On milk-white base, establish hierarchy through **font weight** and **roasted tea color**
- The contrast of ink on washi is the fundamental tension
- Circles and underlines uniformly use `--yellow` (roasted tea)
- Arrows use `--red` (stone gray), quietly guiding, not competing
- `--shu` (vermilion) only used for: conclusion box borders, core thesis circle marks, seal next to the credit. No more than 3 per board
- Vermilion is the only high-saturation color; its scarcity gives it impact

#### Content-Driven Color Temperature Shift

Default maintains wabi-sabi gray tones. Based on content themes, allow extremely subtle color temperature shifts -- no new hues, only adjust the cool/warm tendency of the base color and highlights.

**Detection**: Scan content keywords, match the dominant type. When crossing categories, use the theme with the largest scope.

| Type | Trigger Words | `--board` | `--yellow` | Halo Hue |
|------|--------------|-----------|------------|----------|
| Default (Washi) | No match | `#F7F3EC` | `#7A6B4E` | Warm Vermilion |
| Technical | AI, algorithm, model, code, architecture, system, API, data, engineering, network | `#F3F4F7` | `#5A6878` | Cool Blue |
| Humanities | Philosophy, cognition, meaning, ethics, existence, aesthetics, narrative, history, literature, psychology | `#F7F0E5` | `#8A6A3E` | Deep Warm |
| Business | Investment, business, growth, market, valuation, financing, strategy, competition, profit, ROI | `#F4F5F0` | `#5A7054` | Neutral Green |

**Implementation**: When matching a non-default type, add variable overrides + surface halo override at the top of `{{CUSTOM_CSS}}`. Default type does not override.

Technical:
```css
:root { --board: #F3F4F7; --yellow: #5A6878; }
.board > .surface { background: radial-gradient(ellipse at 25% 20%, rgba(120,140,170,0.05) 0%, transparent 50%), radial-gradient(ellipse at 75% 55%, rgba(150,165,190,0.03) 0%, transparent 45%); }
```

Humanities:
```css
:root { --board: #F7F0E5; --yellow: #8A6A3E; }
.board > .surface { background: radial-gradient(ellipse at 25% 20%, rgba(190,160,120,0.05) 0%, transparent 50%), radial-gradient(ellipse at 75% 55%, rgba(210,180,140,0.03) 0%, transparent 45%); }
```

Business:
```css
:root { --board: #F4F5F0; --yellow: #5A7054; }
.board > .surface { background: radial-gradient(ellipse at 25% 20%, rgba(130,160,130,0.05) 0%, transparent 50%), radial-gradient(ellipse at 75% 55%, rgba(160,185,155,0.03) 0%, transparent 45%); }
```

**Principles**:
- Only override `--board`, `--yellow`, and the surface halo; all other variables remain untouched
- The shift is extremely subtle -- not noticeable without side-by-side comparison, but the overall atmosphere is different
- `--ink`, `--red`, `--shu` do not change with content -- vermilion remains the sole color anchor

### 2.4 Title Design

The title is the first impression of the entire board.

**Must achieve**:
- The title is a **complete judgment/conclusion**, not a word. If the original title is just a concept name, extract the core thesis from the content as the main title, with the concept name as the subtitle
- In the main title, highlight 1-2 keywords with `--yellow`, rest in white
- Below the main title, use a chalk horizontal line as closure (SVG wavy path, opacity 0.3)

**Title Structure**:
```html
<div class="board-title">
  <div class="board-title-sub">Subtitle or guide text (smaller, ink-light)</div>
  <h1 class="board-title-main">White text<span class="y">Yellow keyword</span>white text</h1>
  <svg class="title-line" width="600" height="8">
    <path d="M0,4 Q150,0 300,4 T600,4" stroke="var(--yellow)" fill="none" stroke-width="2" opacity="0.3"/>
  </svg>
</div>
```

**Title CSS Reference**:
```css
.board-title { text-align: center; padding: 56px 48px 16px; }
.board-title-sub { font: 500 34px/1.4 var(--hand); color: var(--ink-light); margin-bottom: 4px; }
.board-title-main { font: 700 64px/1.2 var(--marker); color: var(--ink); margin-bottom: 8px; }
.board-title-main .y { color: var(--yellow); }
.title-line { display: block; margin: 0 auto; }
```

## Step 3: Design the Visual

### 3.1 Chalkboard Element Toolbox

**All visual elements implemented with CSS + SVG, no external images.**

#### Text Hierarchy

| Level | Font | Size | Color | Usage |
|-------|------|------|-------|-------|
| Main Title | `--marker` | 64-80px | `--ink` | Large title at the top of the board, keywords in yellow |
| Chain Text | `--hand` 700 | 34-40px | `--ink` | Concepts and explanations in the logic chain |
| Keywords | `--hand` 700 | 34-42px | `--yellow` | Concepts needing emphasis in the chain |
| Annotation | `--hand` 400 | 24-28px | `--ink-light` | Side notes, supplements, small text |
| Large Numbers | `--marker` | 72-120px | `--yellow` or `--red` | Data highlights |

**Chinese text handling**: Permanent Marker and Kalam have no effect on Chinese characters, falling back to PingFang SC. Chinese text maintains the chalk feel through color (yellow/red) and decoration (underline, circle marks).

#### Chalk Effects (CSS)

```css
/* Red chain arrow -- visual clue for logical progression */
.chain-arrow {
  color: var(--red);
  font: 700 34px var(--hand);
  margin: 0 6px;
  display: inline;
}

/* Yellow chalk highlight */
.chalk-yellow {
  color: var(--yellow);
  font-weight: 700;
}

/* Chalk circle mark */
.chalk-circled {
  border: 2.5px solid var(--yellow);
  border-radius: 45% 55% 50% 48%;
  padding: 2px 14px;
  display: inline-block;
}

/* Red chalk underline */
.chalk-underline {
  border-bottom: 3px solid var(--red);
  padding-bottom: 2px;
}

/* Chalk box (important conclusion) */
.chalk-box {
  border: 2.5px solid var(--ink);
  border-radius: 3px;
  padding: 14px 18px;
}

.chalk-box-red { border-color: var(--red); }
.chalk-box-yellow { border-color: var(--yellow); }
.chalk-box-shu { border-color: var(--shu); }

/* Dashed box */
.chalk-dashed {
  border: 2px dashed var(--ink-light);
  border-radius: 3px;
  padding: 14px 18px;
}

/* Numbered mark */
.chalk-num {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 36px; height: 36px;
  border-radius: 50%;
  border: 2.5px solid var(--red);
  color: var(--red);
  font: 700 22px var(--hand);
  margin-right: 8px;
}

/* Question/exclamation mark */
.chalk-question {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 44px; height: 44px;
  border: 2.5px solid var(--yellow);
  border-radius: 50%;
  color: var(--yellow);
  font: 700 28px var(--hand);
}

/* Vermilion focal point -- used sparingly, no more than 3 per board */
.shu-circle {
  border: 2.5px solid var(--shu);
  border-radius: 45% 55% 50% 48%;
  padding: 2px 14px;
  display: inline-block;
}

/* Vermilion stamp -- seal next to conclusion, wabi-sabi focal point */
.shu-stamp {
  display: inline-block;
  border: 2px solid var(--shu);
  padding: 4px 10px;
  font: 700 18px var(--hand);
  color: var(--shu);
  transform: rotate(-3deg);
  opacity: 0.7;
}
```

#### Simple Chalk Sketches (Inline SVG)

Use simple SVG paths to draw concept icons. Stroke uses `var(--ink)` or `var(--yellow)`, stroke-width: 2-3px, use stroke only, no fill (chalk line style). Each icon uses 3-5 paths.

Common: person (circle head + line body + limbs), question mark, trend chart (polyline), house (triangle + square), animal (minimal outline), lightbulb, lightning.

**Chalk texture**: Lines should not be perfectly straight; paths can have subtle micro-jitter.

### 3.2 Layout Principles

**The chalkboard is chain-based** -- the main body is a horizontal logic chain, with vertical hierarchical progression.

Core rules:
- **Chain flow**: One reasoning chain per line, concepts connected by red →, left to right
- **Vertical hierarchy**: Each level is the next step of reasoning, related between levels using indentation or spacing
- **Embedded icons**: Simple drawings and text mixed on the same line, not occupying separate areas
- **Yellow highlights**: Important concepts in yellow, standing out against white text
- **Red driven**: → arrows are uniformly red, the visual beat of logical progression
- **Rhythm**: Core reasoning chains compact (line-height 1.8x), topic transitions leave breathing room (Ma)
- **Whitespace is content**: Don't strive to fill every space. Leave large spacing before and after key transitions, giving the reader's mind a place to rest
- **Natural non-alignment**: Chains don't need strict left alignment, like natural indentation in real handwriting

#### Spacing Hierarchy (Section Separation)

**Use spacing to communicate, not lines.** There are no horizontal lines on the chalkboard -- only tight writing and loose writing.

| Level | Spacing | Usage | CSS |
|-------|---------|-------|-----|
| Zero | 0-4px | Continuation of the same chain | `.cl + .cl { margin-top: 2px; }` |
| Small | 14-20px | Different chains within the same topic | `margin-top: 16px` |
| Medium | 32-44px | Between different topics (Ma) | `margin-top: 36px` |
| Large | 52-72px | Major turn / new section (Large Ma) | `margin-top: 60px`, optionally with chalk wavy line |

**Forbidden**:
- `border-top` straight line separators -- no straight lines dividing areas on the chalkboard
- Overuse of ↓ arrows -- only use for explicit "therefore/so" progression, no more than 3 per board
- Uniform spacing -- uneven spacing looks more like handwriting

**Chalk wavy line** (only for large spacing separation, optional):
```html
<svg width="800" height="8" style="display:block;margin:0 auto;opacity:0.15;">
  <path d="M0,4 Q100,0 200,4 T400,4 T600,4 T800,4" stroke="var(--ink)" fill="none" stroke-width="1.5"/>
</svg>
```

### 3.3 Visual Composition (By Style)

#### Logic Chain (Default)
```
[Large Title -- White, centered, yellow keywords]

Red→ Concept A → Not because of X → Not Y either → But Z → Conclusion 1
                                                                  ↓
Red→ Expand conclusion 1 → [Simple drawing] → Supplementary explanation → Derive concept B
                                                                                   ↓
    Concept B → Example... → But there's a problem → [?]
                                                      ↓
Red→ Answer... → Therefore → [Final conclusion -- Red box]
```
- One reasoning chain per line. Lines connected by ↓
- Lines starting with red → are main reasoning, lines without red → are supplements
- The chain flows naturally, like writing left to right on a chalkboard
- Intersperse simple drawings appropriately to break the monotony of pure text

#### Brainstorm Wall
```
       [Color block 1]   [Color block 2]
            \     /
     [Color block 3] → [Core word] ← [Color block 4]
            /     \
       [Color block 5]   [Color block 6]

  Bottom: Key conclusion, red underline
```

#### Timeline
```
  [Title]

  ●──────●──────●──────●──────●
  Stage 1  Stage 2  Stage 3  Stage 4  Stage 5
  │       │       │       │       │
  Note    Note    Note    Note    Note
```

#### Matrix Analysis
```
  [Title]
            │ Dimension A High
    ────────┼────────
    Quadrant 1  │ Quadrant 2
            │
    ────────┼────────
    Quadrant 3  │ Quadrant 4
            │ Dimension A Low
   Dimension B Low    Dimension B High
```

## Step 4: Write CSS + HTML

All CSS goes into `{{CUSTOM_CSS}}`. All HTML goes into `{{CONTENT_HTML}}`.

**CSS written from scratch** -- class names reflect content semantics (`.premise-chain`, `.conclusion-box`), not generic names.

**Color variables**: Default wabi-sabi tones use template values directly. If content matches Technical/Humanities/Business types (see "Content-Driven Color Temperature Shift"), override `--board`, `--yellow`, and `.board > .surface` at the top of `{{CUSTOM_CSS}}`.

**Logic chain layout techniques**:
- Each chain uses `display: flex; align-items: baseline; flex-wrap: wrap; gap: 4px 6px;` for natural wrapping
- Arrows use `<span class="chain-arrow">→</span>` embedded in text flow
- Yellow keywords use `<span class="chalk-yellow">keyword</span>`
- Simple drawing SVGs use `display: inline-block; vertical-align: middle;` embedded inline
- Line spacing is uneven -- lines of the same argument compact (`margin-top: 12px`), new topics with larger spacing (`margin-top: 28px`)
- Lines starting with red → can add `padding-left` indentation for hierarchy

Variable Substitutions:

| Variable | Content |
|----------|---------|
| `{{CUSTOM_CSS}}` | All custom CSS |
| `{{CONTENT_HTML}}` | All content HTML |
| `{{SOURCE_LINE}}` | Content source (optional): `<span class="info-source">source text</span>`, empty string when no source |

Write to: `/tmp/ljg_cast_whiteboard_{name}.html`

## Step 5: Self-Check

- [ ] Is the background + warm gray text comfortable and not harsh on the eyes?
- [ ] If content matches Technical/Humanities/Business type, has the color temperature shift (--board, --yellow, halo) been applied?
- [ ] Gray tones dominant, vermilion (--shu) ≤ 3 places?
- [ ] Is the title a complete judgment sentence? Highlighted words in generated color (--yellow)?
- [ ] Is the title large and bold enough (≥ 64px)?
- [ ] Is the negative space ample -- margins ≥ 72px, breathing room between paragraphs?
- [ ] Chain text ≥ 34px? Annotations ≥ 24px?
- [ ] Section separation uses spacing hierarchy, no border-top straight lines?
- [ ] At least 2 simple drawing icons (SVG), lines using ink color?
- [ ] No skeuomorphic decoration (no noise textures, no wooden frame, no chalk texture)?
- [ ] Overall clean, quiet, warm?

## Step 6: Screenshot

```bash
node assets/capture.js /tmp/ljg_cast_whiteboard_{name}.html ~/Downloads/{name}.png 1080 800 fullpage
```
