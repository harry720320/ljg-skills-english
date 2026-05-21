# Mold: Comic (-c)

## Core Tenets

**The tension between black and white is everything.**

The comic mold uses the visual language of Japanese black-and-white manga to tell stories. This is not typography with comic panel borders — it is using panel rhythm, black-and-white contrast, focus lines, and negative space to create drama. Color is almost never used; at most one gray tone (screentone gray). Power comes from the density of ink and the tension of composition.

## Step 1: Read the Template

Read `assets/comic_template.html`

The template provides:
- Font loading (Noto Serif SC + DM Sans)
- CSS variables (`--bg`, `--ink`, `--ink-mid`, `--ink-light`, `--white`, `--accent`, `--tone`)
- SVG filters: `#inkgrain` (ink texture), `#halftone` (screentone), `#roughen` (rough edges)
- `.colophon` signature bar
- `{{CUSTOM_CSS}}` and `{{CONTENT_HTML}}` slots

## Step 2: Understand the Content, Choose the Style

### 2.1 Extract Narrative Elements

Extract from the content:
- **Core conflict/tension**: What is opposing what in this content?
- **3-5 key moments**: Scenes or concepts that can become "panels"
- **Emotional arc**: From what state to what state?
- **Visual anchor**: The concept with the most visual impact

### 2.2 Determine Number of Cards

Decide whether to generate one or multiple comic cards based on content volume:

| Content Volume | Core Ideas | Number of Cards | Notes |
|---------------|-----------|----------------|-------|
| Short text (< 1000 chars) | 1-3 | 1 card | All ideas compressed into one page |
| Medium text (1000-3000 chars) | 3-5 | 2-3 cards | Each card focuses on 1-2 core ideas |
| Long text (> 3000 chars) | 5+ | 3-5 cards | Each card focuses on 1-2 core ideas |

**Principles**:
- **Completeness first**: Better to have one extra card than to miss an idea. Every core argument of a long text must be presented
- **Each card stands on its own**: Independent title, independent panel layout, independent narrative arc. Not a forced cut of long content
- **Series numbering**: For multi-card layouts, mark the top-right corner with `01/N` ~ `N/N`
- **First card sets up, last card concludes**: The first card establishes the conflict/problem, the last card gives the conclusion/solution

### 2.3 Extract Original Images

When the original text contains images (from WebFetch markdown `![](url)` or HTML `<img>` tags):
- Collect all image URLs
- Determine which images are relevant to core ideas (ignore logos, ads, decorative images)
- Relevant images will be embedded in panels in Step 4

### 2.4 Select Comic Style

| Style | Visual Features | Trigger Signals | CSS Variable Override |
|-------|----------------|-----------------|----------------------|
| **Katsuhiro Otomo — Precision Ruins** | Dense ultra-fine lines, mechanical/architectural details, rich grayscale, precise perspective | Technology/systems/architecture/complex mechanisms, high information density | `--tone: #D0D0D0` |
| **Takehiko Inoue — Ink Wash Negative Space** | Large areas of negative space, ink wash gradation, visible brushstrokes, minimal composition | Philosophy/contemplation/aesthetics/humanities, needs breathing room | `--tone: #E8E0D8` |
| **Kentaro Miura — Dark Oppression** | Large areas of solid black, extreme contrast, dense texture, strong sense of oppression | Conflict/dilemma/dark side/struggle, intense emotion | `--bg: #F0F0F0; --tone: #C0C0C0` |
| **Taiyo Matsumoto — Raw Bold Lines** | Uneven line thickness, irregular composition, energetic feel, seemingly rough yet precise | Movement/energy/creativity/breakthrough, impactful | `--tone: #E0E0E0` |
| **Jiro Taniguchi — Quiet Precision** | Architectural-level fine lines, restrained expression, silver-photograph grayscale, tranquil | Daily life/observation/detail/quiet power | `--tone: #E5E5E5` |

**Selection principles**:
- Default to "Takehiko Inoue" — the most versatile black-and-white aesthetic
- Content has technical/system complexity → Katsuhiro Otomo
- Content has intense conflict or dark side → Kentaro Miura
- Content has energy/breakthrough/movement → Taiyo Matsumoto
- Content is quiet observation/daily life → Jiro Taniguchi

**Series consistency rule (same-source multi-card)**: When generating multiple comic cards from the same text source (same article, same book, same report), make a single overall judgment for the entire text source, select one style, and use it consistently across all cards. Do not select a style per individual concept — style jumps will break the reading flow. Base the judgment on the overall character of the text source, not the mood of any particular section.

## Step 3: Design the Canvas

### 3.1 Comic Visual Element Toolkit

**All elements implemented with CSS + SVG. Black-and-white dominant, gray screentone as accent, no colors.**

#### Panel Layout

The core of comics is panel layout. Use CSS Grid to implement irregular panel layouts:

```css
/* Basic panel */
.panel {
  border: 3px solid var(--ink);
  background: var(--white);
  position: relative;
  overflow: hidden;
  padding: 28px 32px;
}

/* Bleed panel (content breaks through border) */
.panel-bleed {
  border: none;
  margin: -3px;
  z-index: 2;
}

/* Slanted panel */
.panel-slanted {
  clip-path: polygon(0 0, 100% 8%, 100% 100%, 0 92%);
}
```

#### Focus Lines

Used to emphasize key concepts and create a "strike" effect:

```css
.focus-lines {
  position: relative;
}
.focus-lines::before {
  content: '';
  position: absolute;
  inset: 0;
  background: repeating-conic-gradient(
    var(--ink) 0deg 0.5deg,
    transparent 0.5deg 5deg
  ) center/100% 100%;
  opacity: 0.06;
  pointer-events: none;
}
```

#### Speed Lines

Express motion, change, impact:

```css
.speed-lines {
  background-image: repeating-linear-gradient(
    90deg,
    transparent,
    transparent 4px,
    var(--ink) 4px,
    var(--ink) 4.5px
  );
  opacity: 0.08;
}
```

#### Speech Bubbles / Thought Bubbles

```css
.speech-bubble {
  background: var(--white);
  border: 2.5px solid var(--ink);
  border-radius: 20px;
  padding: 16px 22px;
  position: relative;
  font: 700 32px/1.4 var(--serif);
}
.speech-bubble::after {
  content: '';
  position: absolute;
  bottom: -16px;
  left: 40px;
  border: 8px solid transparent;
  border-top-color: var(--ink);
}

/* Thought bubble (round tail) */
.thought-bubble {
  border-radius: 50% 50% 50% 50% / 40% 40% 60% 60%;
}
.thought-bubble::after {
  width: 12px; height: 12px;
  border-radius: 50%;
  background: var(--ink);
  border: none;
  bottom: -20px;
}

/* Shout bubble (jagged edge) */
.shout-bubble {
  clip-path: polygon(
    0% 20%, 5% 0%, 15% 15%, 25% 0%, 35% 10%,
    50% 0%, 65% 10%, 75% 0%, 85% 15%, 95% 0%,
    100% 20%, 95% 35%, 100% 50%, 95% 65%, 100% 80%,
    95% 100%, 85% 85%, 75% 100%, 65% 90%, 50% 100%,
    35% 90%, 25% 100%, 15% 85%, 5% 100%, 0% 80%,
    5% 65%, 0% 50%, 5% 35%
  );
  background: var(--white);
  padding: 28px 36px;
  font: 900 38px/1.3 var(--serif);
}
```

#### Screentone

In comics, gray is not gray — it's screentone:

```css
.screentone {
  background-image: radial-gradient(circle, var(--ink) 1px, transparent 1px);
  background-size: 5px 5px;
  opacity: 0.15;
}

/* Gradient screentone */
.screentone-gradient {
  background-image: radial-gradient(circle, var(--ink) 1px, transparent 1px);
  background-size: 5px 5px;
  -webkit-mask-image: linear-gradient(to bottom, black, transparent);
  mask-image: linear-gradient(to bottom, black, transparent);
  opacity: 0.2;
}
```

#### Onomatopoeia / Sound Effects

Large, slanted sound effect characters — the soul of comics:

```css
.sfx {
  font: 900 80px/1 var(--serif);
  color: var(--ink);
  transform: rotate(-8deg) skewX(-5deg);
  letter-spacing: -3px;
  text-shadow: 3px 3px 0 var(--tone);
  -webkit-text-stroke: 1px var(--ink);
}
```

#### Ink Wash

The core of the Takehiko Inoue approach — using CSS gradients to simulate ink wash:

```css
.ink-wash {
  background: linear-gradient(
    135deg,
    var(--ink) 0%,
    rgba(26,26,26,0.6) 20%,
    rgba(26,26,26,0.15) 50%,
    transparent 70%
  );
}
```

### 3.2 Typography Principles

**Comic typography is not article typography.**

- **Vertical text is optional**: Japanese comics are originally read vertically. Key text can use `writing-mode: vertical-rl` to create a manga feel
- **Extreme font size contrast**: Titles 120px+, body 32px, annotations 20px, ratio ≥ 6:1
- **Bold = emphasis**: In comics, bold means "the voice got louder"
- **Negative space = silence**: Large empty areas are not unfinished — they are deliberate pauses
- **Black blocks = pressure**: Solid black areas create a sense of oppression and drama

### 3.3 Panel Composition (by Style)

#### Katsuhiro Otomo — Precision Ruins
```
+------------------+--------+
|                  | Detail |
|   Wide panorama  |  Small |
|   (tech diagram) |  panel |
|                  +--------+
|                  |  Data  |
+--------+---------+ Small  |
| Text   | Text    | panel  |
| panel  | panel   |        |
+--------+---------+--------+
```
Features: Square panels, precise lines, high information density

#### Takehiko Inoue — Ink Wash Negative Space
```
+-------------------------+
|                         |
|    Large negative space  |
|         Core concept     |
|    (ink wash background) |
|                         |
+------------+------------+
|  Narrow    |  Narrow    |
|  panel     |  panel     |
|  Idea A    |  Idea B    |
+------------+------------+
```
Features: Abundant negative space, few panels, each panel carries less information but carries it heavily

#### Kentaro Miura — Dark Oppression
```
+--+--------------------+--+
|Bk|                    |Bk|
|ed|   Core conflict    |ed|
|  |   (solid black +   |  |
|  |    white text)     |  |
+--+---------+----------+--+
|   Dense    |   Dense   |
|   panel    |   panel   |
| (screentone)| (pure B&W)|
+------------+-----------+
```
Features: Large areas of solid black, white text reversed out, oppressive feel

#### Taiyo Matsumoto — Raw Bold Lines
```
  +-------+
  | Slanted \
 /   panel   +--------+
+    Core concept      |
|   (large bold type)  |
+-----+       +--------+
      |        |
      |   Irregular |
      |   small     |
      |   panel     |
      +-------------+
```
Features: Slanted panels, uneven border thickness, full of kinetic energy

#### Jiro Taniguchi — Quiet Precision
```
+-------------------------+
|   Fine scene panel       |
|   (wide horizontal,      |
|    cinematic scope)      |
+------------+------------+
|            |            |
| Square     | Square     |
| panel      | panel      |
| Detail A   | Detail B   |
|            |            |
+------------+------------+
|   Bottom narrative panel |
+-------------------------+
```
Features: Regular panels, wide cinematic horizontal panels, quiet and even

### 3.4 Handling Original Images

When Step 2.3 collected relevant supporting images:
- **Prefer the original image**: Use `<img>` tags to directly reference original image URLs, placing them inside comic panels
- **Image as panel content**: The original image occupies a full panel, with a 3px border, integrated into the panel system
- **Black-and-white toning**: `filter: grayscale(100%) contrast(1.2);` to maintain the comic black-and-white feel. If the original image is already black-and-white or line art, the original color can be preserved
- **Image CSS**: `width: 100%; height: auto; object-fit: cover; display: block;`
- **When image is unavailable** (404 / CORS), skip the image, do not use a placeholder

## Step 4: Write CSS + HTML

All CSS goes into `{{CUSTOM_CSS}}`. All HTML goes into `{{CONTENT_HTML}}`.

**Write CSS from scratch** — class names reflect the content, not generic names.

**Core constraints**:
- Color palette is limited to black (`--ink`), white (`--white/--bg`), and gray (`--tone`), with occasional use of `--ink-mid`
- For emphasis, use pure black reversed out (white text on black background), not color
- Borders are uniformly 2.5-3px, simulating brush strokes
- At least one panel should "bleed" (content breaks through normal margins) to create a comic feel

Replacement variables:

| Variable | Content |
|----------|---------|
| `{{CUSTOM_CSS}}` | All CSS (including :root overrides) |
| `{{CONTENT_HTML}}` | All HTML |
| `{{SOURCE_LINE}}` | Content source (optional): `<span class="info-source">Source text</span>`, empty string if no source |

Write to:
- Single card: `/tmp/ljg_cast_comic_{name}.html`
- Multiple cards: `/tmp/ljg_cast_comic_{name}_{N}.html` (N = 01, 02, ...)

## Step 5: Self-Check

- [ ] Does it look like a comic page at first glance? If it looks like "ordinary typography with added borders," redo it
- [ ] Are there at least 3 panels? A comic without panels is not a comic
- [ ] Is the black-and-white contrast strong? Is there a solid black area?
- [ ] Is there at least 1 comic-specific element (focus lines/speed lines/dialogue bubbles/sound effects/screentone)?
- [ ] Is there contrast in panel sizes? (One large panel + several small ones, not all equal)
- [ ] Is color avoided? Gray is only used as screentone `--tone`
- [ ] Is body text ≥ 32px? Titles ≥ 72px?
- [ ] Is there one panel that draws the viewer in at first glance?
- [ ] Are equal division, symmetry, and uniform spacing avoided?

## Step 6: Screenshot

Single card:
```bash
node assets/capture.js /tmp/ljg_cast_comic_{name}.html ~/Downloads/{name}.png 1080 800 fullpage
```

Multiple cards: screenshot each one, with sequence numbers in filenames
```bash
node assets/capture.js /tmp/ljg_cast_comic_{name}_01.html ~/Downloads/{name}_01.png 1080 800 fullpage
node assets/capture.js /tmp/ljg_cast_comic_{name}_02.html ~/Downloads/{name}_02.png 1080 800 fullpage
# ... execute for each card
```
