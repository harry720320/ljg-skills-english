---
name: ljg-present
description: "Presentation forger (Outline-Faithful). Renders orgmode/markdown outlines 1:1 as visual slides — color-block large text, ultra-bold staggered layout, original text untouched, only beautified. Three theme colors black/red/yellow (default black or inferred from filetags), can override with -r/-b/-y; --cyber for black-background green-text cyber-hacker style. Use when user says '讲这个', 'present', '做成演讲', '呈现一下', '铸成演示', '做个 slides', '标语流', '宣言体', 'slogan', 'manifesto', '按 outline 美化'. Output single HTML file to ~/Downloads/."
user_invocable: true
version: "3.0.0"
---

# ljg-present: Presentation Forger

Cast outlines into color blocks — a visual renderer that returns the stage to the speaker.

## What This Is Not

- **Not a manifesto extractor** — doesn't extract "that line", doesn't write "complete declarative sentences", doesn't reorder
- **Not Takahashi flow** — doesn't cut words to single characters
- **Not deck-style** — not the structured layout of corporate PPT

## What This Is

**Outline → Visual Renderer**:

- Input = orgmode file (`*` `**` levels + lists + tables + emphasis)
- Output = visually beautified slogan-style HTML, **1:1 preserving outline structure**
- No extraction, no rewriting, no condensation — only decides **how to render this line/section as a page**

Visual language (aesthetic reference: Felipe Franco / BIG STUDIOS manifesto aesthetics):
- **One theme color for the entire piece** — red/black/yellow pick one
- **Left-aligned stage aesthetic** — text left-aligned, oversized type naturally fills the screen
- **Ultra-large ultra-bold type** — single character 70vmin, long sentences 11vmin
- **Multi-line staggering** — auto-indent 0/1/2 by outline nesting depth
- **Keywords auto-colored** — `*emphasis*` `~code~` auto-highlighted
- **Section transitions beat rhythm** — level-1 heading `*` → emphasis cover page, rest → theme pages

## Core Philosophy

**Outline is truth. Skill is the renderer.**

Not touching content is an iron rule:
- **Don't change heading text**
- **Don't change paragraph text**
- **Don't change list item text**
- **Don't change table structure**
- **Don't reorder**

The only allowed "touch" is: **physical pagination** (splitting one long section into multiple pages), maintaining visual consistency.

## Orgmode → Page Mapping Rules

### Heading Levels

| Org Element | Page |
|---|---|
| `* Level-1 heading` |独占 **emphasis** cover page (accent background) |
| `** Level-2 heading` |独占 **theme** page (large title独占 one page) |
| `*** Level-3 heading`+ |独占 theme page (font size one step down) |

### Content Elements

| Org Element | Page Behavior |
|---|---|
| Paragraph | Theme page, split by period/line break/character count |
| `- List item` | Theme page, one per line, indent by nesting depth (0/1/2) |
| `1. Numbered list` | Same as above, keep number prefix |
| Nested list | Child items indent +1 (max indent=2) |
| `\| Table \|` | Single or multi-page, preserve table structure (bold header row) |
| `*emphasis*` | Auto `hl: true` |
| `~code~` or `=verbatim=` | Auto `hl: true` |
| Quoted `> ...` | Theme page, indent 1 display |
| Separator `-----` |独立 emphasis rest page (no content, pure color block) |
| `#+begin_example` block |独立 pre page (monospace rendered ASCII art) |

### File-level Metadata

| Org Element | Use |
|---|---|
| `#+title:` | → JSON `title` (browser tab) |
| `#+author:` or `#+date:` | → JSON `subtitle` (page footer bottom right) |
| `#+filetags:` | For theme inference (see below) |
| `#+identifier:` | Ignored |

### Theme Inference

**Priority**: explicit parameter > filetags inference > default black

Explicit override (parameters):
- `-r` / `--theme=red` → red
- `-b` / `--theme=black` → black
- `-y` / `--theme=yellow` → yellow
- `--cyber` → cyber-hacker (black background green text + CRT scan lines + HUD + terminal cursor)

Filetags auto-inference:

| filetags contains | theme | Tone |
|---|---|---|
| `:share:` `:talk:` `:manifesto:` `:keynote:` | `red` | Declaration, call to action |
| `:essay:` `:think:` `:learn:` `:note:` | `black` | Contemplation, argument |
| `:critique:` `:warn:` `:rant:` | `yellow` | Irony, alert |
| None of the above | `black` | Default contemplative |

### Pagination Rules (when content is long)

**Iron rule: maintain visual consistency after splitting. Pages from the same logical block use the same font size tier / background / indent rules.**

| Situation | Split method |
|---|---|
| Paragraph ≤ 30 chars | Single page |
| Paragraph 30-80 chars, with multiple periods | One sentence per page (medium font tier) |
| Paragraph > 80 chars | Split ~30 chars per page, add `⋯` continuation mark |
| List ≤ 4 items | Single page all displayed (staggered indent) |
| List 5-8 items | Split 2 pages, 3-4 items each (keep counts close) |
| List > 8 items | Split multiple pages, 4 items each |
| Nested list | Parent item 1 page + each child independent group (title 1 page + children 1 page) |
| Table ≤ 6 rows | Single page |
| Table > 6 rows | Split multiple pages, each keeps header row |

### Auto Emphasis (rhythm)

- All `* Level-1 headings` → emphasis cover page
- File first page (title or first non-empty text) → emphasis opening page (merged if already a level-1 heading)
- File last page (last paragraph or last item) → emphasis closing page
- `-----` separator → emphasis rest page
- Everything else is theme pages

### Auto Highlight

- org `*emphasis*` → `hl: true`
- org `~code~` `=verbatim=` → `hl: true`
- hl within emphasis pages auto-ignored (CSS `color: inherit`)

## Visual Specs

### Color Palette (only 4 colors)

```
--c-black:  #1A1A1A
--c-red:    #E63956
--c-yellow: #FFD400
--c-white:  #FFFFFF
--c-gold:   #FFE082
```

### Theme Mapping (≤ 3 colors per piece)

| theme | Default page | Emphasis page | hl color (theme pages only) |
|---|---|---|---|
| **black** Contemplation | Black bg white text | Red bg white text | Red #E63956 |
| **red** Declaration | Red bg white text | Black bg white text | Soft gold #FFE082 |
| **yellow** Irony | Yellow bg black text | Black bg white text | Red #E63956 |
| **cyber** Terminal | Black bg matrix green | Green bg black text | White #FFFFFF (with green glow + CRT scan lines + top HUD) |

### Font Stack

```
"Helvetica Neue", "Arial Black", "Inter", "PingFang SC", "Heiti SC", -apple-system, sans-serif
font-weight: 900
letter-spacing: -0.05em
```

Cyber theme additional fonts (for HUD/footer/pre):

```
"JetBrains Mono", "Fira Code", "IBM Plex Mono", "Source Code Pro", "Menlo", monospace
```

### Font Size Adaptive

Auto-tiered by the character count of "the longest line" on this page (CJK characters weighted at 1.8):

| Tier | Character count | Font size |
|---|---|---|
| single | ≤ 2 | 70vmin |
| short | 3-6 | 48vmin |
| medium | 7-14 | 28vmin |
| long | 15-26 | 16vmin |
| xlong | 27+ | 10vmin |

Multi-line pages auto-drop one tier.

### Typography

- Content area padding 6vmin 7vmin (close to edge, let large text feel screen-filling)
- **lines block horizontally centered + inline left-aligned** — `align-items: center` centers the lines block on screen horizontally (eliminates 16:9 right-side whitespace), but each line of text still starts left-aligned, indent 0/1/2 creates staggering within the block
- letter-spacing `-0.05em` — the character-squeezing feel that ultra-bold deserves
- line-height `1.05`, inter-line gap `0.15em` — multi-line wrapping still has breathing room
- Text vertical direction: centered
- Footer: bottom-left page number + bottom-right subtitle, 13px monospace, opacity 0.5

## JSON Schema

```jsonc
{
  "theme": "black|red|yellow|cyber",
  "title": "Presentation title (browser tab)",
  "subtitle": "Subtitle/brand (footer bottom right, optional)",
  "slides": [
    // Default theme page
    {
      "lines": [
        {
          "indent": 0,                    // 0/1/2 indent tier (by outline nesting depth)
          "align": "left|center|right",   // optional, default left
          "chunks": [
            {"t": "Sentence prefix"},
            {"t": "highlighted word", "hl": true},  // only effective on theme pages
            {"t": "Sentence suffix"}
          ]
        }
      ]
    },
    // Emphasis page (accent background, whole page is highlight, no inline hl allowed)
    { "emphasis": true, "lines": [...] },
    // Pre page (ASCII art / preformatted block)
    { "preTitle": "diagram_name", "pre": "...preformatted text..." }
  ]
}
```

**Field omission conventions**:
- Not writing `emphasis` = default theme page
- `chunks[].hl: true` within emphasis pages is ignored
- Writing `pre` field → this page is ASCII art page (monospace rendered)

## Call Flow

1. **Get content** (file → Read / paste → use directly / URL → WebFetch)
2. **Parse outline**:
   - org: recognize `*` `**` heading levels, `-` `1.` lists, `|...|` tables, `*emphasis*` / `~code~`, `#+begin_example` blocks
   - markdown (compatible): `#` `##` headings, `-` `*` lists, `|` tables, `**emphasis**`, ` ``` ` code blocks
   - plain text (fallback): split by blank lines, one paragraph per page
3. **Infer theme**: explicit param > `#+filetags:` > default black
4. **Apply mapping rules** to generate slides array:
   - `*` heading → emphasis cover
   - `**`+ heading → theme独占 page
   - Paragraph → theme page (per pagination rules)
   - List → theme page (staggered indent + pagination rules)
   - Table → theme page (preserve structure + pagination rules)
   - Emphasis → auto hl
   - Example block →独立 pre page
5. **Read** `assets/slogan_template.html` (cyber theme needs additional CRT scan line/HUD/cursor CSS injected on top of template)
6. **Replace placeholders**:
   - `{{TITLE}}` → file `#+title:` or explicit parameter
   - `{{SUBTITLE}}` → `#+author:` `#+date:` concatenated, or empty
   - `{{THEME}}` → inferred or explicit parameter (black|red|yellow|cyber)
   - `{{SLIDES_JSON}}` → JSON.stringify(slides)
7. **Write file** to `~/Downloads/{name}.html` (`{name}` from `#+title:` or filename, remove punctuation, ≤ 20 chars)
8. **Report path** + navigation keys `→ ← Space F Home End`

## Taste Standards

- **Outline is truth** — don't change words, don't extract, don't rewrite, don't reorder
- **Level-1 heading = emphasis cover** — natural section break, automatic rhythm
- **Level-2 heading =独占 theme page** — give headings their due weight
- **List staggering** — indent 0/1/2 reflects outline nesting depth
- **`*emphasis*` auto hl** — respect the author's markup intent
- **Consistent pagination** — same logical block gets consistent visual treatment (font tier / indent / background)
- **Keep footer** — page number + subtitle, don't delete, that's the brand's cool air
- **Left-aligned, not centered** — soul of the VACAT aesthetic

## Forbidden Zone

- **Don't extract manifesto** — don't "find the nail", the author already wrote the outline
- **Don't write new sentences** — don't reassemble "complete declarative sentences"
- **Don't reorder** — present in outline order, however the author arranged it
- **Don't delete content** — all list items/paragraphs must be presented, don't pick and choose
- **Don't put images/icons** — color blocks are the graphics (except cyber theme's HUD/scan lines, which are part of the theme)
- **Don't use transition animations** — hard cuts
- **Don't use inline hl on emphasis pages** — emphasis pages are already highlights, adding more hl creates chaos
- **Don't mix multiple themes** — one气质 per piece, no switching
- **Don't make subtitle font too large** — footer 13px, the气场 can't compete with the main title
- **Don't add emphasis arbitrarily** — only level-1 headings, first/last page, `-----` are emphasis, nothing else

## Default Language

Default output in user's language. Unless the original is in a language the user wants preserved.

## Universal Interaction

- `→` `Space` `Enter` `j` `PageDown`: next page (includes Bluetooth page turner)
- `←` `k` `PageUp`: previous page (includes Bluetooth page turner)
- `Home`/`End`: jump to first/last
- `f`/`F`: toggle fullscreen
- Touch swipe left/right: page turn
- Click right half: next page; click left half: previous page
