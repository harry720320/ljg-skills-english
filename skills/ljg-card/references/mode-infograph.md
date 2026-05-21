# Mold: Infograph (-i)

## Core Tenets

**Style serves the idea.**

There is no "default layout." The visual form of every infograph grows from the shape of that particular idea. The template only provides the canvas material (typefaces, colors, noise texture, signature). Composition, typography, layout — all of it is designed from scratch by you based on the content.

## Step 1: Read the Template

Read `assets/infograph_template.html`

The template is minimal and only provides:
- Font loading (DM Serif Display + DM Sans + KingHwa_OldSong)
- CSS variables (`--bg`, `--green`, `--pink`, `--yellow`, `--ink`, `--ink-light`, `--white`, `--serif`, `--sans`, `--mono`)
- SVG noise texture (automatically overlaid)
- `.colophon` signature bar
- `{{CUSTOM_CSS}}` and `{{CONTENT_HTML}}` slots

**No header, no canvas, no utility classes.** All CSS goes into `{{CUSTOM_CSS}}`, all HTML goes into `{{CONTENT_HTML}}`.

## Step 2: Understand the Idea

### 2.1 Extract Metadata

- **Title**: ≤ 15 characters
- **Subtitle**: One core sentence ≤ 30 characters
- **Source**: Original source of the content (author, website, etc.), used in the footer on the right (optional)
- **REF Code**: `REF—{Domain} / {Topic}` (its placement on the canvas is up to you)

### 2.2 Three Dimensions

Make three judgments about the content:

**Density** (determines the breathing rhythm of the canvas):

| Density | Core Content Volume | Visual Character |
|---------|-------------------|-----------------|
| **Sparse** | ≤ 50 characters can explain it | One giant element dominates the canvas. Negative space ≥ 60%. Impact comes from restraint. |
| **Medium** | 50-200 characters | Structured layout. 2-3 main sections. Negative space 30-50%. |
| **Dense** | 200+ characters | Multi-section dense arrangement. Annotations, grids, layering. Negative space ≤ 30%. Lab notebook feel. |

**Structure** (determines the geometry of the canvas):

| Structure | Signal | Visual Geometry |
|-----------|--------|-----------------|
| Single Point | One core concept | One anchor occupies the center of gravity, everything else recedes |
| Contrast | A vs B, old vs new | Split, opposition, two poles |
| Hierarchy | Lower layers support upper layers | Pyramid, staircase, nesting |
| Flow | Sequential order | Vertical waterfall, timeline, pipeline |
| Radiation | Core + derivatives | Center radiation, hub-spoke |
| Parallel | Multiple parallel concepts | Asymmetric grid (no equal division) |

**Mood** (determines the temperature of the canvas):

| Mood | Typography Style |
|------|-----------------|
| Contemplative | Generous negative space, serif dominant, low contrast |
| Sharp | Strong contrast, large type, pink accent points |
| Warm | Green dominant, rounded layout, hand-drawn feel |
| Technical | Mono annotations, grid textures, data-dense |

### 2.3 Output Judgment

```
Density: [sparse/medium/dense]
Structure: [single-point/contrast/hierarchy/flow/radiation/parallel]
Mood: [contemplative/sharp/warm/technical]
Palette: [contemplative/sharp/warm/technical/research/creative/business/default]
Anchor: [What is the largest element on the canvas? Where is it placed?]
```

### 2.4 Palette Selection

Select the most fitting palette based on the content's theme. The palette determines three core variables, which override template defaults in `{{CUSTOM_CSS}}`.

| Palette | `--bg` | `--green` (structural) | `--pink` (accent) | Trigger Signals |
|---------|--------|----------------------|-------------------|-----------------|
| Contemplative | `#F5F2ED` | `#C4B5A0` | `#8B5E3C` | Philosophy, cognition, essence, meaning, existence |
| Sharp | `#EDEDF0` | `#6E6E80` | `#D93025` | Critique, deconstruction, controversy, opposition, debate |
| Warm | `#F7F4EF` | `#C8B898` | `#C17F4E` | Humanities, emotion, life, stories, growth |
| Technical | `#F0F3F7` | `#8EAAB8` | `#1A936F` | Architecture, systems, algorithms, code, engineering |
| Research | `#F2F6F4` | `#7DAE96` | `#D68C45` | Papers, experiments, data, research, discovery |
| Creative | `#F6F3F2` | `#C0A89C` | `#B8432F` | Art, design, creation, aesthetics, inspiration |
| Business | `#F4F3F0` | `#A8A498` | `#2D6A4F` | Business, finance, market, investment, strategy |
| Default | `#F2F2F2` | `#B8D8BE` | `#E91E63` | When nothing else fits |

**Density correction** (fine-tune from the base color):
- **Sparse**: Accent color saturation can be increased by 10-15%. The canvas is empty; the accent needs a stronger presence.
- **Medium**: Use baseline values.
- **Dense**: Reduce structural color saturation by 10-15% to avoid visual fatigue in dense layouts.

**Selection principles**:
- Scan the content's high-frequency keywords and themes, match to the closest palette
- Mood and palette can differ — "Contemplative mood + Technical palette" is perfectly valid
- Use Default rather than a mismatch — the wrong palette is worse than no palette
- Once a palette is chosen, use it consistently across the entire image

## Step 3: Design the Canvas

### 3.1 Material System

**Typefaces and Ink Colors** (shared across all palettes):

| Variable | Value | Usage |
|----------|-------|-------|
| `--serif` | DM Serif Display → KingHwa_OldSong | Titles, large text, golden quotes |
| `--sans` | DM Sans → KingHwa_OldSong | Body text, labels |
| `--mono` | SF Mono | Data annotations, REF codes |
| `--ink` | `#2D2926` | Main text color |
| `--ink-light` | `#5C5350` | Secondary text |

**Dynamic Palette** (determined by Step 2.4):

| Variable | Role | 90/8/2 |
|----------|------|--------|
| `--bg` | Canvas background color | 90% neutral surface |
| `--green` | Structural color — blocks, borders, sections | 8% structure |
| `--pink` | Accent — 1-2 precise hits across the image | 2% emphasis |

**Override method** — write at the very beginning of `{{CUSTOM_CSS}}`:

```css
:root {
  --bg: #F0F3F7;     /* Value selected in Step 2.4 */
  --green: #8EAAB8;
  --pink: #1A936F;
}
```

### 3.2 Design Freedom

All of the following decisions are yours based on the content. **There are no defaults.**

**Anchor Position** — The title/core element can be placed:
- Top-left (traditional)
- Center (stele-carved feel)
- Right side, vertical arrangement (East Asian aesthetics)
- Bottom (revealing suspense)
- As a background ghost character (terrain)

**Canvas Division** — Can be:
- No division (sparse density)
- Horizontal split (two worlds, top and bottom)
- Vertical split (left-right contrast)
- Irregular split (clip-path slanted cuts)
- Grid (dense density lab notebook feel)

**Font Sizes** — Optimize for mobile reading (a 1080px canvas scales down by approximately 2.8x on mobile):
- Ratio of largest to smallest element ≥ 10:1
- Can use up to 400px characters (it's no longer "text," it's "terrain")
- Minimum readable annotation no smaller than 24px (~8.7px on mobile)
- Body text no smaller than 40px (~14.4px on mobile)
- Decorative text (REF codes, etc., not requiring close reading) minimum 22px

**Color** — The 90/8/2 rule (color values from the Step 2.4 palette selection):
- 90% neutral colors (`--bg` + `--white` + `--ink` text)
- 8% structural color (`--green` for one section)
- 2% accent (`--pink` for one precise hit)

### 3.3 Density Guidelines

#### Sparse (≤ 50 characters)

**One single element dominates** the canvas. Could be:
- A single Chinese character or word at 300-420px
- One golden line spanning the full width
- One formula, surrounded by silence

Remaining information (etymology, explanation) sits quietly at 24-28px in a corner or at the bottom. It does not compete for attention.

**Reference composition**:
```
┌─────────────────────────┐
│ ref-code        22px    │
│                         │
│                         │
│        坐              │
│      400px serif        │
│                         │
│  subtitle   36px        │
│                         │
│  ─── quote ───          │
│  44px serif             │
│                         │
│ [colophon]              │
└─────────────────────────┘
```

#### Medium (50-200 characters)

2-3 sections, with primary and secondary hierarchy. Anchor element at 120-180px, body text at 40-44px, subtitles at 34-40px.

Key: **Do not arrange sections evenly.** One large section takes 60%, the rest cluster together. Or use a full-width stripe to break the rhythm.

**Reference composition** (for inspiration only, not a fixed template):
```
┌─────────────────────────┐
│ Title 140px              │
│ subtitle 36px           │
├───────────┬─────────────│
│           │             │
│  Core     │  Etymology/  │
│  Explanation │  Data     │
│  40px     │  32px       │
│  2fr      │  1fr        │
│           │             │
├───────────┴─────────────│
│ ██████ Dark full-width stripe ██████│
│ Core formula / One sentence 44px   │
├─────────────────────────│
│                         │
│ Golden quote 48px serif │
│                         │
│ [colophon]              │
└─────────────────────────┘
```

#### Dense (200+ characters)

The canvas is dense but orderly. Multiple small sections. Annotation layers, grid lines visible. Lab notebook feel.

Key: **Dense does not mean cramped.** Dense means lots of information, but each piece is in its proper place. Use lines, numbers, and color blocks to distinguish hierarchy. Body text at 36-40px, annotations at 28-32px, titles at 80-108px.

**Reference composition**:
```
┌──────────┬──────────────┐
│ Title    │ ref-code 22px│
│ 84px     │ ×Data   28px │
│ sub 34px │              │
├──────────┴──────────────│
│ ┌────┐ ┌────┐ ┌──────┐ │
│ │ 01 │ │ 02 │ │      │ │
│ │Concept│ │Concept│ │  03  │ │
│ │36px│ │36px│ │Big   │ │
│ └────┘ └────┘ │Concept│ │
│               │ 40px  │ │
│               └──────┘ │
├─────────────────────────│
│ Annotation area · 28px mono      │
│ Citations · Data sources · 28px  │
│ [colophon]              │
└─────────────────────────┘
```

### 3.4 Anti-Death Checklist

| If you find yourself doing this... | Stop |
|-----------------------------------|------|
| Writing `.header { padding: 56px }` | You're thinking in old template patterns. Start from content, not from a header. |
| Every section has a white background | At least one should use `--green` or `--ink` |
| Three columns of equal width | Forbidden. Use `2fr 1fr`, `1fr 340px`, or one large with two small. |
| Title centered | Unless density=sparse and structure=single-point. Otherwise, left-align or use a non-traditional position. |
| Every image has a "formula stripe" | This is not required. Some ideas don't have formulas. |
| Using accent color in more than 3 places | Go back to 2. The accent is a bullet. |
| No element exceeds 100px | Find the one worth magnifying. |
| All text is between 30-44px | You haven't created tension. You need a ≥ 10:1 ratio. |
| Body text smaller than 36px | It will be unreadable on mobile. Minimum body text 36px, minimum annotation 24px. |
| Equal spacing between all sections | Intentionally alternate tight and loose spacing. |
| Using `max-width` to shorten text that could fit on one line | The canvas is 1080px. If a sentence fits on one line, put it on one line. Only use `max-width` for body paragraphs to control line width (≤ 56ch). **Do not constrain** titles and golden quotes — let them breathe naturally until they stop. |

## Step 4: Write CSS + HTML

All CSS goes into `{{CUSTOM_CSS}}`. All HTML goes into `{{CONTENT_HTML}}`.

**Write CSS from scratch** — do not copy class names or structures from any previous version. Class names for each image should reflect that image's content (`.etymology`, `.core-split`, `.timeline`), not generic names (`.section`, `.panel`, `.label`).

Replacement variables:

| Variable | Content |
|----------|---------|
| `{{CUSTOM_CSS}}` | All CSS for this image |
| `{{CONTENT_HTML}}` | All HTML for this image |
| `{{SOURCE_LINE}}` | Content source (optional): `<span class="info-source">Source text</span>`, empty string if no source |

Write to: `/tmp/ljg_cast_infograph_{name}.html`

## Step 5: Self-Check

**The only check that never changes**:

- [ ] Did the visual form of this image grow from the shape of its content?
- [ ] If you replaced it with completely different content, would this layout still make sense? If yes — you built a template, not a design.
- [ ] Is the ratio of largest to smallest element ≥ 10:1?
- [ ] Is accent color used ≤ 2 places?
- [ ] Does the palette match the content's theme? If the theme changed, would these colors still feel right?
- [ ] Is there one element that grabs the viewer at first glance?
- [ ] Is the negative space intentional, or leftover?
- [ ] If you told someone "this was made by AI," would they immediately believe it? If yes — redo it.
- [ ] Mobile reading check: Body text ≥ 36px? Annotations ≥ 24px? Line height ≥ 1.6? After scaling 2.8x on mobile, is the text still comfortably readable?

## Step 6: Screenshot

```bash
node assets/capture.js /tmp/ljg_cast_infograph_{name}.html ~/Downloads/{name}.png 1080 800 fullpage
```
