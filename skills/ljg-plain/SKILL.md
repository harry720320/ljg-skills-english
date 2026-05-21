---
name: ljg-plain
description: "Cognitive atom: Plain (白). Rewrites any content so a smart 12-year-old groks it. Structure-free — form follows content. Use when user says '白话说', '说人话', '解释一下', 'plain', 'grok'."
user_invocable: true
version: "5.0.0"
---

# ljg-plain: Plain

Make people grok.

Doesn't prescribe how to write. Prescribes what not to write. Floor locked, ceiling open. Different topics have different optimal forms — analogy, story, Q&A, progressive examples, a long scene — form follows content.

## Format Constraints

### Org-mode Syntax

- Bold uses `*bold*` (single asterisk), forbid `**bold**`
- Heading levels start from `*`, no skipping levels

### ASCII Art

All diagrams use pure ASCII characters. Allowed: `+ - | / \ > < v ^ * = ~ . : # [ ] ( ) _ , ; ! ' "` and spaces. Forbid Unicode drawing symbols.

### Denote File Conventions

- Timestamp: `date +%Y%m%dT%H%M%S`
- Readable time: `date "+%Y-%m-%d %a %H:%M"`
- Filename: `{timestamp}--plain-{short_title}__plain.org`
- Output directory: `~/Documents/notes/`

### Org File Header

```
#+title:      plain-{short_title}
#+date:       [{YYYY-MM-DD Day HH:MM}]
#+filetags:   :plain:atom:
#+identifier: {YYYYMMDDTHHMMSS}
#+source:     {URL or source description}
```

Report path after writing.

## Red Lines (must pass every one, in priority order)

1. *Spoken-word test* — supreme law. Read it aloud, would you speak this way to a smart friend? No → revise until yes. Conjunctions aren't enemies — "but" "so" are the sound of thought turning corners, only kill mechanical conjunctions ("furthermore" "it is noteworthy that")
2. *Zero jargon* — a smart 12-year-old can retell it. When a technical term must appear, first land the meaning in plain language, then mention the term name
3. *Short words first* — if two words work, don't use four. "Conduct an analysis" → "look at". Big words don't make you look smart, they just make reading hard
4. *One thing per sentence* — each sentence advances one step. Break long sentences
5. *Concrete* — nouns you can see, verbs with muscle. "Some people feel the situation is not good" → "Zhang San said the project is going under". Kill adjectives where possible
6. *Start with a reason* — the first sentence should make you want to read the next. No preamble, no background, no "since ancient times"
7. *No filler* — delete opening ceremonies, crutch words, exaggeration signifiers. Every sentence works
8. *Trust the reader* — skip softening, justification, hand-holding. Saying it once is enough
9. *Honesty* — if you can't think clearly, say so. "About 70%" is more honest than "possibly"

## Toolbox (optional, don't need to use all)

When writing, tools you can pick from here, none are mandatory:

- *Analogy* — find structurally matching everyday experience. Good analogies are load-bearing (removing them collapses the piece), multi-layered (dig one layer deeper, still works), self-evident (no explanation needed for the analogy itself). When extending verbs to new objects, check if the Chinese verb-noun collocation feels natural
- *Good question* — find where the reader gets stuck, turn it into a question. Readers only want to continue when they're stuck
- *Crack* — where does the model/analogy fall short? That point is often the most valuable. Don't announce it, let the reader feel it themselves
- *Image* — a scene you can see with eyes closed. A forced image is worse than none
- *Story* — a specific person encounters a specific problem. The reader follows along
- *Question chain* — when encountering hidden premises, open them with a question, then answer it
- *Skeleton diagram* — when concepts involve spatial relationships, embed ASCII diagrams (`#+begin_example` blocks)

## Execution

### 1. Get Content

URL → WebFetch | Text → use directly | File path → Read | Concept → explain directly | Book/paper name → WebSearch

### 2. Write

Form is free. Pick the approach from the toolbox that best fits this topic, or don't — if there's a better way to write it, use it.

Output is a coherent article flowing from first line to last. Full text has only a file title, body has no subheadings.

Forbidden:
- Structure labels (`* Analogy` / `* Crack` etc.)
- Meta-commentary pointing to the writing process ("for example" "next we'll discuss")

### 3. Pass Red Lines

Go through the red line checklist one by one. Additional checks:

- Break formulas — no more than two negative parallelisms in the whole text; three-part structures become two or four
- Vary rhythm — alternate long and short sentences, varied paragraph endings
- Kill golden lines — anything that sounds quotable, rewrite
- Check jumps — is every logical step traceable? Sentence A says X, jumps to Y in B → add a bridge
- Check translation-ese — do verb-noun collocations feel natural? If not → change the verb or change the structure

After scanning, list revisions (which line triggered what, before → after). Don't write the list into the file.

### 4. Generate Org File

Get timestamp per Denote conventions, write file header + body, save to `~/Documents/notes/`.

## Acceptance

- *Grok*: after reading, can retell the core in your own words
- *Zero jargon*: a 12-year-old can follow
- *Memorable*: something stays in your head after reading — an image, a question, a turn, anything
- *Want to finish*: from start to end, no paragraph you want to skip
