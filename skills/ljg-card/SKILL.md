---
name: ljg-card
description: "Content caster (铸). Transforms content into PNG visuals. Seven molds: -l (default) long reading card, -i infograph, -m multi-card reading cards (1080x1440), -v editorial sketchnote (problem→failure→pivot→insight→naming, magazine + archive layout), -c comic (manga-style B&W), -w whiteboard (marker-style board layout), -b big-fonts attachment card (1080x1440, weathered stele inscription style for Xiaohongshu). Output to ~/Downloads/. Use when user says '铸', 'cast', '做成图', '做成卡片', '做成信息图', '做成海报', '视觉笔记', 'sketchnote', '杂志', 'editorial', '漫画', 'comic', 'manga', '白板', 'whiteboard', '大字', '附件图', 'big fonts', '小红书卡片'. Replaces ljg-cards and ljg-infograph."
user_invocable: true
version: "2.3.0"
---

# ljg-card: Cast

Cast content into visible form. Content goes in, PNG comes out. The mold determines the shape.

## Parameters

| Parameter | Mold | Dimensions | Description |
|-----------|------|------------|-------------|
| `-l` (default) | Long card | 1080 x auto | Single reading card, content auto-extends height |
| `-i` | Infograph | 1080 x auto | Content-driven adaptive visual layout |
| `-m` | Multi-card | 1080 x 1440 | Auto-split into multiple reading cards |
| `-v` | Sketchnote | 1080 x auto | Editorial magazine feature: problem→failure→pivot→insight→naming (6 layout molds / 4 typeface contrasts / detective case-file details) |
| `-c` | Comic | 1080 x auto | Japanese B&W manga style, dynamically selects manga artist visual language |
| `-w` | Whiteboard | 1080 x auto | Whiteboard marker style, structured block diagrams + arrows + color markup |
| `-b` | Big fonts | 1080 x 1440 | Stele inscription big characters + washi paper + outer shadow, Xiaohongshu attachment style (single sentence / short passage) |

## Constraints

This skill outputs visual files (PNG), not subject to the Org-mode, Denote, and ASCII-only conventions in L0.

## Shared Foundation

### Getting Content

- URL --> WebFetch to obtain
- Pasted text --> use directly
- File path --> Read to obtain

### File Naming

Extract title or core idea from content as `{name}` (use directly in Chinese, remove punctuation, ≤ 20 characters).

### Screenshot Tool

```bash
node assets/capture.js <html> <png> <width> <height> [fullpage]
```

Run from the skill root directory. Requires playwright in `node_modules/` under skill root. If errors:

```bash
npm install playwright && npx playwright install chromium
```

### Footer

- Left side: logo + Li Jigang (hardcoded in template)
- Right side: content source (optional) — show when there's a clear source (author name, arxiv ID, website name, etc.), leave empty otherwise. Use `{{SOURCE_LINE}}` variable: when there's a source, fill `<span class="info-source">source text</span>`, otherwise empty string. Applies to `-l`, `-i`, `-v`, `-c`, `-w` molds (`-m` multi-card has no footer, not applicable).

### Delivery

1. Report the file path

## Taste Standards

**Shared across all molds.** Before executing any mold, first Read `references/taste.md`, as the visual quality baseline runs through the entire process.

Core principle: anti-AI-generated traces — no Inter font, no pure black, no three-column cards, no centered Hero, no AI copywriting tone, no fake data.

## Execution

Select the mold based on the parameter, Read `references/taste.md` + the corresponding mode file, then follow the steps:

### -l (default): Long Card

Read `references/mode-long.md`, follow its steps.

Template: `assets/long_template.html`

### -i: Infograph

Read `references/mode-infograph.md`, follow its steps.

Template: `assets/infograph_template.html`

### -m: Multi-card

Read `references/mode-poster.md`, follow its steps.

Template: `assets/poster_template.html`

### -v: Sketchnote

Read `references/mode-sketchnote.md`, follow its steps.

Template: `assets/sketchnote_template.html`

### -c: Comic

Read `references/mode-comic.md`, follow its steps.

Template: `assets/comic_template.html`

### -w: Whiteboard

Read `references/mode-whiteboard.md`, follow its steps.

Template: `assets/whiteboard_template.html`

### -b: Big Fonts

Read `references/mode-big.md`, follow its steps.

Template: `assets/big_template.html`
