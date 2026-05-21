# Mold: Multi-card (-m)

## Step 1: Read Template

Read `assets/poster_template.html`

## Step 1.5: Hue Perception

Shares the same hue system with the long card mold. Select `{{BG_COLOR}}` and `{{ACCENT_COLOR}}` based on content temperament:

| Content Temperament | `{{BG_COLOR}}` | `{{ACCENT_COLOR}}` | Trigger Signals |
|----------|---------------|-------------------|----------|
| Philosophical | `#FAF8F4` | `#7C6853` | cognition, thought, essence, meaning, philosophy |
| Technical/Engineering | `#F5F7FA` | `#3D5A80` | architecture, model, algorithm, system, code |
| Literary/Narrative | `#FBF9F1` | `#6B4E3D` | story, character, writing, prose, poetry |
| Science/Research | `#F4F8F6` | `#2D6A4F` | experiment, data, discovery, paper, research |
| Default | `#FAFAF8` | `#4A4A4A` | when unable to classify |

## Step 2: Content Preprocessing

- Identify heading lines (starting with `#`/`##`/`###`, or short standalone lines)
- Identify blockquotes (starting with `>`)
- Identify bold (`**text**`)
- **Identify golden lines**: standalone short sentences (usually < 25 chars), carrying core insights, rendered with `.highlight`
- Split into paragraph list by blank lines

## Step 3: Calculate Visual Weight

Template renders at 1080x1440 full resolution, body text 36px, line-height 1.7.

- Regular paragraphs: character count × 1.4
- Heading lines (h1 first card 84px): character count × 6.0
- Golden lines (`.highlight` 40px + left border + top/bottom whitespace): character count × 3.0
- `.item` groups (label + body): character count × 1.8
- Blockquotes: character count × 1.7
- Dividers: fixed 60 weight
- Code blocks: character count × 2.2
- Running title (continuation page header): fixed 70 weight

## Step 4: Greedy Splitting

- Threshold: approximately **380** character equivalent visual weight per card
- Accumulate paragraph by paragraph, split before the current paragraph when threshold exceeded
- **Split rules**:
  - Never split mid-sentence
  - Prefer splitting at paragraph/item/section boundaries
  - Headings must not stand alone (must be accompanied by at least one content element on the same card)
  - Extra-long single paragraphs force-split at sentence terminators
  - One section (h2 + 3 items) typically fits exactly one card

**Special cases**:
- Single card: don't display page number
- Multiple cards: display `1 / N` format page number

## Step 5: Format as HTML

**Basic elements:**
- Regular paragraphs → `<p>text</p>`
- Section headings (##/### level) → `<h2>heading</h2>`
- Blockquotes → `<blockquote><p>quote</p></blockquote>`
- Bold → `<strong>text</strong>`
- Lists → `<ul><li>...</li></ul>`

**Golden lines (standalone core insight short sentences, visually prominent):**
```html
<p class="highlight">golden line text</p>
```
Judgment criteria: standalone paragraph, < 25 chars, carries key insight. Use `.highlight` not `<p><strong>`.

**Item groups (并列 items with heading + body):**
```html
<div class="item">
  <p class="label">item heading</p>
  <p>item body</p>
</div>
```

**Subtitle label:**
```html
<p class="subtitle">label text</p>
```

**Divider (between sections):**
```html
<div class="divider"></div>
```

## Step 6: Render Template

For each card, replace template variables:

| Variable | Rule |
|------|------|
| `{{BG_COLOR}}` | Background color determined in step 1.5 |
| `{{ACCENT_COLOR}}` | Accent color determined in step 1.5 |
| `{{HEADER_BLOCK}}` | Continuation cards: `<div class="header"><span class="running-title">article title</span></div>`; first card or single card: empty string |
| `{{TITLE_BLOCK}}` | First card with title: `<div class="title-area"><h1>title</h1></div>`; continuation cards or no title: empty string |
| `{{BODY_HTML}}` | HTML generated in step 5 |
| `{{SOURCE_LINE}}` | Content source (optional): `<span class="info-source">source text</span>`, empty string when no source |
| `{{PAGE_INFO}}` | Multiple cards: `1 / 3`, single card: empty string |

**End marker**: only append `<p style="text-align:right;font-size:16px;color:#ACACB0;margin-top:40px;">∎</p>` at the end of `{{BODY_HTML}}` on the final card. Not on non-final pages.

Write to: `/tmp/ljg_cast_poster_{name}_{N}.html`

## Step 7: Screenshot

```bash
node assets/capture.js /tmp/ljg_cast_poster_{name}_{N}.html ~/Downloads/{name}_{N}.png 1080 1440
```

Multiple cards can be screenshotted in parallel.

On delivery, report card count + summary of each (first 30 characters).
