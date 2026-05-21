# Design Taste Standards (shared across all molds)

All molds must pass this standards checklist before generating HTML. This is the visual quality floor.

## 1. Baseline Parameters

| Dimension | Default | Meaning |
|-----------|---------|---------|
| DESIGN_VARIANCE | 8 | 1=perfect symmetry, 10=artistic chaos |
| VISUAL_DENSITY | 4 | 1=gallery whitespace, 10=cockpit information density |

Auto-adjusted by mold:
- `-l` Long card: DESIGN_VARIANCE=5, VISUAL_DENSITY=3 (reading comfort first). Variation achieved through **hue perception** — different content temperaments correspond to different background colors and accent colors (see mode-long.md step 2.5)
- `-i` Infograph: DESIGN_VARIANCE=7, VISUAL_DENSITY=8 (data density first). Variation achieved through **dynamic REF encoding** and **content-driven custom layouts**
- `-c` Comic: DESIGN_VARIANCE=9, VISUAL_DENSITY=2 (visual impact first). Shares hue system with long card, end marker only appears on final page

## 2. Typography Engineering

### Headings
- Large headings: `tracking-tighter` (tight letter spacing), `leading-none` (minimal line height)
- **Inter font forbidden**. Long card/comic use serif (Noto Serif SC), infograph uses mono + sans-serif mixed
- Dashboard/technical scenarios strictly forbid serif — only premium sans-serif (Geist, Satoshi, Cabinet Grotesk)

### Body Text
- Default: `text-base`, `leading-relaxed`, max line width `65ch`
- `-i` Infograph: body ≥36px, line-height ≥1.6, labels ≥24px (must remain readable after 1080px→390px mobile scaling of 2.8x)
- Paragraph text color avoid pure black, use deep gray like `#333` or `#4a4a4a`

### Numbers
- When VISUAL_DENSITY > 7 (infograph mode), all numbers use monospace (`font-family: monospace`)

## 3. Color Calibration

### Hard Rules
- Maximum **1 accent color**, saturation < 80%
- **Forbid "AI purple-blue"**: purple button glows, neon gradients are all forbidden
- Strictly unify warm/cool tone within a single image — don't oscillate between warm gray and cool gray
- **Forbid pure black** `#000000`: use Off-Black (`#1a1a1a`), Zinc-950, or charcoal

### Gradient Constraints
- Don't use gradient fill on large heading text
- Background gradients limited to subtle transitions, avoid color jumps

## 4. Layout Diversity

### When DESIGN_VARIANCE > 4
- **Forbid centered Hero**: headings must not default to centered. Use left-aligned, split-screen, asymmetric whitespace
- **Forbid "three-column cards"**: 3 equal-width parallel columns is the #1 AI-generation tell. Replace with 2-column staggered, asymmetric grid, or horizontal scroll

### When DESIGN_VARIANCE ≥ 8
- Use CSS Grid fractional units (e.g. `grid-template-columns: 2fr 1fr 1fr`)
- Allow large whitespace areas (`padding-left: 20vw`-level spatial sense)
- Allow Masonry-style staggered layout

### Cards & Containers
- Cards only used when hierarchy (elevation) has functional need
- Data metrics should "breathe" — group with `border-top`, `divide-y`, or pure whitespace, not individual boxes
- Shadows must be tinted (matching background tone), no gray default shadows

## 5. AI Generation Forbidden Checklist

Before generating any visual content, check item by item for these typical AI traces:

### Visual & CSS
- **Forbid outer glow**: no `box-shadow` default glow. Use inner borders or tinted shadows
- **Forbid oversaturated accent colors**: accent colors must blend elegantly with neutrals
- **Forbid custom cursors** (static images not relevant, but don't add them in generated HTML either)

### Typography
- **Forbid Inter font**: use Geist, Outfit, Cabinet Grotesk, or Satoshi
- **Forbid H1 screaming**: headings must not establish hierarchy through pure size scaling. Use weight and color to control

### Content & Data ("Jane Doe Effect")
- **Forbid generic names**: John Doe, Sarah Chan, Jack Su forbidden. Use creative real names
- **Forbid fake data**: no `99.99%`, `50%`, `1234567`. Use organic "dirty" data (`47.2%`, `+1 (312) 847-1928`)
- **Forbid startup cliché names**: Acme, Nexus, SmartFlow forbidden. Invent tasteful brand names
- **Forbid AI copywriting tone**: "empower" "seamless" "unlock" "next-generation" forbidden. Use concrete verbs
- **Forbid Unsplash links**: if placeholder images needed, use `https://picsum.photos/seed/{random_string}/800/600` or SVG

### Spacing & Alignment
- padding and margin must be mathematically precise, no awkward gaps
- Adjacent elements strictly aligned, visual lines connect through

## 6. Material & Surface

### Glassmorphism
If frosted glass effect needed, don't just use `backdrop-blur`. Must layer on:
- 1px inner border: `border: 1px solid rgba(255,255,255,0.1)`
- Subtle inner shadow: `box-shadow: inset 0 1px 0 rgba(255,255,255,0.1)`
Simulating physical edge refraction.

### Border Radius
- Main containers use large radius (`border-radius: 2.5rem`)
- Diffuse shadows (extremely faint, large spread): `box-shadow: 0 20px 40px -15px rgba(0,0,0,0.05)`

## 7. Factory Self-Check

After generating HTML, before screenshot, confirm item by item:

- [ ] Avoided centered Hero (when DESIGN_VARIANCE > 4)?
- [ ] Avoided three-column equal-width cards?
- [ ] Headings using non-Inter font?
- [ ] Colors unified warm/cool tone, no pure black?
- [ ] Accent colors ≤ 1 and saturation < 80%?
- [ ] Data feels real (no 99.99%-style fake data)?
- [ ] Copywriting stripped of AI tone (empower/seamless/unlock)?
- [ ] Spacing mathematically precise, no awkward whitespace?
- [ ] Shadows tinted (not gray default)?
