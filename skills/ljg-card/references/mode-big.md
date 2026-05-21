# Mold: Big Text (-b)

## Core Tenets

**A single sentence strikes the paper — inscribed on washi, suspended like an attachment.**

Spirit: A sentence must carry weight. The characters are large enough to strike the reader at a single glance. The paper is aged enough to feel like a page torn from an ancient book. The shadow is deep enough to make the paper feel like an independent attachment suspended in darkness.

Form: Cream-white washi as the base, ink-black stele-carved large characters as the body, with a seal and name at the bottom left as the signature. An outer dark frame like a tray in the night, inner cloud halos like water stains not yet dry. The characters are irregular — with chiseled rough edges and water-soaked mottling — that is time, not decoration.

**Three Pillars of Aesthetics**:
- **Heavy** — Font size large enough for 2-5 characters per line, readable at a glance; every stroke carries the weight of ink
- **Aged** — Paper has cloud halos, characters have rough edges; not a Photoshop aging filter, but actual SVG turbulence displacement
- **Suspended** — The card has a dark outer frame, deep shadow, thin inner glow; like a piece of paper suspended in mid-air

## Step 1: Read the Template

Read `assets/big_template.html`

The template provides:
- 1080x1440 fixed canvas (Xiaohongshu 3:4 HD standard)
- Outer dark background `--bg-dark` automatically creates shadow border (22px inset)
- Washi card 1036x1396 + multiple radial-gradient cloud halos + SVG noise paper grain
- `<filter id="weathered">` feTurbulence + feDisplacementMap aging filter (preconfigured with baseFrequency=0.82, scale=1.8)
- `.main-text` default serif stele-carved characters (Noto Serif SC 900 + engraved text-shadow)
- `.signature` bottom-left signature area (logo + Li Jigang)
- Template variables: `{{FONT_SIZE}}` `{{MAIN_TEXT}}` `{{SOURCE_LINE}}` `{{CUSTOM_CSS}}`

## Step 2: Understand the Content

### 2.1 Content Form

The `-b` mold is dedicated to **single-sentence/short-paragraph** output, not suitable for long text. Typical input:
- A single opinion/judgment (15-30 characters)
- A rhetorical question (10-20 characters)
- A golden quote/slogan (8-25 characters)
- At most two sentences (30-60 characters total)

If input exceeds 60 characters, remind the user: content too long, the -b mold is unsuitable. Recommend using `-l` long image or `-m` multi-card.

### 2.2 Calculate Font Size

Character count n (counting Chinese characters, English letters, punctuation, spaces — fullwidth and halfwidth each count as 1):

| Character Count | `{{FONT_SIZE}}` | Characters Per Line (approx) |
|----------------|-----------------|-----------------------------|
| ≤ 10           | 220             | 3-4                         |
| 11-16          | 190             | 4-5                         |
| 17-24          | 160             | 5-6                         |
| 25-34          | 135             | 6-7                         |
| 35-46          | 115             | 7-9                         |
| 47-60          | 98              | 8-10                        |

This is the **baseline** — can be adjusted up or down by 10-15% based on actual line break results.

### 2.3 Manual Line Breaks (Critical)

**Do not rely on the browser's automatic word wrapping.** Control the semantics of each line by inserting `<br>` in `{{MAIN_TEXT}}`.

Line break principles:
- Break on semantic units, not in the middle of a word
- Each line should have a similar character count (difference ≤ 2 characters) for visual stability
- Place punctuation at the end of a line, not starting a new line
- Starting a new line for keywords/rhetorical questions can enhance impact

Reference image line break example ("In the age when everyone has the 'Sharingan,' where does scarcity lie?"):
```
人人拥有
「寫輪眼」
的时代，
稀缺性在
哪里？
```
3-4 characters per line, with the last two lines forming the rhetorical climax.

### 2.4 Highlighting (Optional)

To emphasize a word/phrase: use `<span class="shu">keyword</span>` to color it vermilion red. **≤ 1 instance per image.** Used for concluding statements or rhetorical highlights.

## Step 3: Write the HTML

### 3.1 Main Text

```html
第一行文字<br>
第二行文字<br>
<span class="shu">高亮</span>第三行<br>
第四行
```

Mixed traditional/simplified Chinese is preserved as-is (e.g., the reference image retains traditional script for 'Sharingan').

### 3.2 Optional: Subtitle/Small Text

To add a small annotation below the main text (source/author/context), use the `.sub` class:

```html
<div class="main-text">
  主要的一句话<br>
  分成几行<br>
  <span class="sub">—— 某某某</span>
</div>
```

`.sub` automatically reduces to 42% of the main font size, softens the color, and does not apply the aging filter (maintains readability for small text).

### 3.3 Source Line (Optional)

If there is a source, fill in `{{SOURCE_LINE}}`:

```html
<div class="source-line">来源于《某某某》</div>
```

Leave as an empty string if there is no source.

### 3.4 Variable Summary

| Variable | Content |
|----------|---------|
| `{{FONT_SIZE}}` | Font size value (without px), e.g., `160` |
| `{{MAIN_TEXT}}` | Main text HTML (including `<br>` line breaks) |
| `{{SOURCE_LINE}}` | Source line HTML or empty |
| `{{CUSTOM_CSS}}` | Additional custom CSS (generally left empty; the template is sufficient) |

Write to: `/tmp/ljg_cast_big_{name}.html`

## Step 4: Self-Check

- [ ] Does the font size selection match the character count, with 2-10 characters per line?
- [ ] Are line breaks at semantic units, not in the middle of words?
- [ ] Is the main text applying `filter: url(#weathered)` for aging?
- [ ] Is the font Noto Serif SC 900 (not Inter, not PingFang default)?
- [ ] Is the color `--ink` (#2C2826) ink-black, not pure black?
- [ ] Is the washi background color `--paper` (#F4EFE6), with cloud halo texture?
- [ ] Does the outer dark background create a 22px shadow border?
- [ ] Does the bottom-left signature area exist (logo + Li Jigang)?
- [ ] Is vermilion highlighting ≤ 1 instance?
- [ ] Does the overall visual have all three qualities: Heavy, Aged, Suspended?

## Step 5: Screenshot

```bash
node assets/capture.js \
  /tmp/ljg_cast_big_{name}.html \
  ~/Downloads/{name}.png \
  1080 1440
```

**No fullpage** — the `-b` mold uses a fixed canvas of 1080x1440.

## Step 6: Delivery

Report the file path. Provide a one-sentence explanation of the line break and font size decisions.

## Prohibitions

- Do not: Input exceeding 60 characters (use -l or -m instead)
- Do not: Rely on default browser line wrapping (must use manual `<br>`)
- Do not: Font size < 90px (loses the "big text" meaning)
- Do not: Vermilion highlighting > 1 instance (loses its accent value)
- Do not: Remove the aging filter (loses the stele-carved feel)
- Do not: Change the canvas size (1080x1440 is the Xiaohongshu standard; deviation is not allowed)
