# Mold: Long Card (-l / default)

## Step 1: Read Template

Read `assets/long_template.html`

## Step 2: Content Preprocessing

- Identify heading lines (starting with `#`/`##`/`###`, or short standalone lines)
- Identify blockquotes (starting with `>`)
- Identify bold (`**text**`)
- **Identify golden lines**: standalone short sentences (usually < 25 chars), carrying core insights, rendered with `.highlight`
- Split into paragraph list by blank lines
- **No splitting**: all content goes into a single card

## Step 2.5: Hue Perception

Select a background color + accent color based on content temperament, creating resonance between each card and the content:

| Content Temperament | `{{BG_COLOR}}` | `{{ACCENT_COLOR}}` | Trigger Signals |
|----------|---------------|-------------------|----------|
| Philosophical | `#FAF8F4` | `#7C6853` | cognition, thought, essence, meaning, philosophy |
| Technical/Engineering | `#F5F7FA` | `#3D5A80` | architecture, model, algorithm, system, code |
| Literary/Narrative | `#FBF9F1` | `#6B4E3D` | story, character, writing, prose, poetry |
| Science/Research | `#F4F8F6` | `#2D6A4F` | experiment, data, discovery, paper, research |
| Default | `#FAFAF8` | `#4A4A4A` | when unable to classify |

Judgment basis: scan high-frequency keywords and topics in the content, match the closest set. No need for precision — prefer default over mismatching.

## Step 3: Format as HTML

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

**Prompts (green-background highlight, for key questions/prompts):**
```html
<p class="prompt">prompt text</p>
```
Judgment criteria: "prompting" content that needs the reader to pause and read carefully. Typical scenarios:
- **Question** in Q&A (Answer uses regular paragraph)
- Key follow-up questions ("Then why isn't X the same as Y?")
- Reading guidance prompts ("Stop here and think for a moment")
- Call-to-action directive sentences

Visually rendered with **light green background + dark green left border**, distinct from `.highlight` (left border + large font):
- `.highlight` = the author's golden conclusion
- `.prompt` = a question/prompt thrown to the reader

No more than 5 `.prompt` instances per card, avoid highlight overuse.

**Drop cap (first body paragraph):**
The first regular paragraph (not `.subtitle`, `.highlight`, `.item`) adds `dropcap` class:
```html
<p class="dropcap">paragraph body...</p>
```
Only the first body paragraph uses this, creating a classic editorial opening ritual.

**Item groups (parallel items with heading + body):**
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

## Step 4: Render Template

Replace template variables:

| Variable | Rule |
|------|------|
| `{{BG_COLOR}}` | Background color determined in step 2.5 |
| `{{ACCENT_COLOR}}` | Accent color determined in step 2.5 |
| `{{TITLE_BLOCK}}` | With title: `<div class="title-area"><h1>title</h1></div>`; without title: empty string |
| `{{BODY_HTML}}` | All HTML generated in step 3 |
| `{{SOURCE_LINE}}` | Content source (optional): `<span class="info-source">source text</span>`, empty string when no source |

Write to: `/tmp/ljg_cast_long_{name}.html`

## Step 5: Screenshot

```bash
node assets/capture.js /tmp/ljg_cast_long_{name}.html ~/Downloads/{name}.png 1080 800 fullpage
```
