# ljg-skills-english

English translation of [ljg-skills](https://github.com/lijigang/ljg-skills) — a custom skill collection for [Claude Code](https://docs.anthropic.com/en/docs/claude-code).

## Installation

One-line install using the [skills CLI](https://github.com/vercel-labs/skills) (powered by `npx`):

```bash
# Install all skills (globally)
npx skills add harry720320/ljg-skills-english -g --all

# Install a single skill
npx skills add harry720320/ljg-skills-english -g --skill ljg-card

# Install multiple specific skills
npx skills add harry720320/ljg-skills-english -g --skill ljg-card --skill ljg-learn

# List available skills in the repo
npx skills add harry720320/ljg-skills-english -l
```

**Parameters:**

| Parameter | Description |
|-----------|-------------|
| `-g` | Global install to `~/.claude/skills/` (recommended). Omit to install to current project `.claude/skills/` |
| `--skill <name>` | Install a specific skill, repeatable |
| `--all` | Install all skills in the repo |
| `-l` | List available skills only, no install |

### ljg-card dependencies

`ljg-card` requires Playwright for screenshots. After installation, run:

```bash
cd ~/.claude/skills/ljg-card && npm install && npx playwright install chromium
```

### Alternative: git clone

```bash
git clone https://github.com/harry720320/ljg-skills-english.git ~/.claude/plugins/ljg-skills-english
```

## Skills

| Skill | Description |
|-------|-------------|
| **ljg-card** | Content caster — transforms content into PNG visual cards (long `-l`, infograph `-i`, multi-card `-m`, sketchnote `-v`, comic `-c`, whiteboard `-w`, big-fonts `-b`) |
| **ljg-learn** | Concept anatomist — deconstructs any concept through 8 dimensions (history, dialectics, phenomenology, linguistics, formalization, existentialism, aesthetics, meta-philosophy), compressed into an epiphany |
| **ljg-paper** | Paper reader — extracts core ideas from papers for non-academics, focused on understanding not critique |
| **ljg-paper-river** | Paper river — reverse reading: recursively traces prior papers (up to 5 layers) + latest advances, telling the problem's evolutionary story from the source |
| **ljg-book** | Book dissector — five moves to extract the skeleton: core question / foundational assumptions / analytical framework / core conclusions / God's-eye compression of the entire book |
| **ljg-qa** | Information Q-A machine — extracts core ideas from articles/papers/books into a Q-A chain, questions cut to the heart, answers in four parts (conclusion / formalization / steps / boundaries) |
| **ljg-plain** | Plain speech engine — rewrites any content so a smart 12-year-old can grok it |
| **ljg-rank** | Rank reduction engine — given a domain, finds the irreducible independent generators behind it |
| **ljg-think** | Arrow to the root — takes an idea or phenomenon and drills vertically down to its irreducible essence |
| **ljg-word** | Word mastery — deep deconstruction of a single English word's core semantics and epiphany moment |
| **ljg-writes** | Writing engine — dissects an idea like a scalpel, peeling back layer by layer. 1000-1500 words |
| **ljg-invest** | Investment analysis — core judgment: is the project an "order-creating machine" |
| **ljg-read** | Reading companion — accompanies you through any text, English three-layer translation (faithfulness-expressiveness-elegance) + structural annotation + deep questioning + cross-domain insights |
| **ljg-relationship** | Relationship analysis — 5-layer structural diagnosis + psychoanalytic depth, guiding users through dialogue to "see" the real structure of relationship issues |
| **ljg-roundtable** | Roundtable discussion — truth-seeking structured multi-person dialectical dialogue, generating ASCII thinking-framework diagrams each round |
| **ljg-travel** | Travel research — input a city name, generates deep cultural research document (org-mode) + portable reference cards (PNG) |
| **ljg-skill-map** | Skill map — scans all installed skills, renders a visual overview |
| **ljg-present** | Presentation forger — default Takahashi flow (one keyword per page, cream background black text); `-s` slogan flow (VACAT/BIG STUDIOS style: black-red dual color blocks, ultra-bold, full declarative sentences filling the screen) |
| **ljg-push** | Push engine — one-click sync of local `~/.claude/skills/ljg-*` to github repo (master + md dual branches) |

## Workflows

Workflows chain multiple skills into a single command.

| Workflow | Skill Chain | Description |
|----------|-------------|-------------|
| **ljg-paper-flow** | ljg-paper → ljg-card -c | Read paper + make comic card in one go |
| **ljg-word-flow** | ljg-word → ljg-card -i | Word deep analysis + infograph card in one go |

## Output Format

This English fork outputs Markdown (`.md`) format, suitable for Obsidian / VSCode / Notion and other Markdown ecosystem tools.

For the original Chinese version with dual-format support (Org-mode + Markdown), see [lijigang/ljg-skills](https://github.com/lijigang/ljg-skills).
