# Extract Workflow

Extract a piece of information into a Q-A chain.

## Voice Notification

```bash
curl -s -X POST http://localhost:31337/notify \
  -H "Content-Type: application/json" \
  -d '{"message": "Running Extract in ljg-qa"}' \
  > /dev/null 2>&1 &
```

Output text: `Running **Extract** in **ljg-qa**...`

## Step 1: Get Content

Route by input type:

| Input | Tool | Notes |
|-------|------|-------|
| URL (regular webpage) | WebFetch | Login-required pages use markdown-proxy |
| arxiv link | WebFetch (HTML version) | Get abstract + method + experiment sections |
| PDF / local file | Read | Large PDFs use pages parameter forsegmented reading |
| Direct text | Skip | Go directly to Step 2 |
| Paper/book name | WebSearch | Get URL then go through WebFetch |

Ensure you have: core argument / reasoning chain / key examples / boundary discussion.

## Step 2: Find the Idea Skeleton

After reading, be silent for 30 seconds, answer this one question:

> What is this piece's core argument? How does it support that argument? Which steps are the key turns?

Write down:

- *Core argument*: one sentence
- *3-5 key turns*: one sentence each

This is the spine of the Q chain. If the spine can't stand, the Qs below are all floating/unmoored — go back and re-read.

## Step 3: Design the Q Chain

Each key turn grows into one or a group of Qs. Qs must satisfy:

1. Can't be dismissed with a one-line definition — cuts to the heart
2. Answers can be grounded in the source material
3. Has inheritance relationship with the previous Q (Q2 naturally emerges after Q1 is answered)

Q types: four categories (action / contrast / cause / boundary) and patterns see `../References/QuestionDesign.md`. A good Q chain mixes at least three types.

*Ordering rule*: by argument dependency, not by chapter order. The original text writes background before method for narrative reasons, but Q chain should follow "first ask the root question, then ask the solution, then ask the cost."

*Count*: 5-10 Qs. Fewer is insufficient coverage, more fatigues the reader.

## Step 4: Write As

Each A strictly four parts, none can be omitted, order must not be disrupted:

```
*Conclusion*: (one sentence — can stand alone, quotable)

*Formalization*: (compress the thought into one line of visible relationships using words + simple symbols — see "Formalization Writing" below)

*How they arrived at it*:
- Step 1 (short sentence, only one reasoning step)
- Step 2
- Step 3

*Boundary*: (under what conditions does this conclusion not hold / what hasn't the argument covered)
```

Hard requirements:

- *Conclusion*: can stand alone — reader forwards this sentence to a friend, friend gets it
- *Formalization*: use words + simple symbols (→ = ≠ + × etc.) to compress the thought into one line of visible relationships — it's "geometry of thought", not "mathematical formula". Let the reader see the correspondences at a glance. See `../References/QuestionDesign.md` "Formalization Writing" for details
- *Reasoning steps*: each step only advances one inference, the previous step opens the door for the next
- *Boundary*: write "conditions where it doesn't hold", not "future work" — the former is honesty, the latter is PR jargon

### Formalization Writing (key points)

Four common patterns:

- *Equation*: `generalist = coordinator; specialist = doer`
- *Contrast*: `Old: LLM = full-stack; New: LLM = coordinator`
- *Flow*: `data → token → answer = loss + waste`
- *Progression*: `call → interface → bilingual hotline`

Use only ASCII + text. Forbid LaTeX, forbid complex math symbols. Fit on one line.

## Step 5: Check Q Chain Direction

Read through the Q order:

- *Inheritance*: after Q1 is answered, does Q2 naturally emerge?
- *Dependency*: if you delete Q3, does Q4 still hold?

If Qs are parallel (deleting one doesn't affect others), reorder or merge. Q chain is a path, not a list.

You can sketch a diagram (not in org, just your own scaffolding):

```
Q1 ─┬─→ Q2
    └─→ Q3
Q2 ──→ Q4
Q4 ──→ Q5 (closing rhetorical question)
```

## Step 6: Pass Red Lines

scan item by item:

- [ ] Each Q cannot be dismissed with a one-line definition
- [ ] Each A has all four parts (conclusion / formalization / steps / boundary)
- [ ] Formalization line reveals relationship at a glance — not a math formula, not piling up jargon
- [ ] Q chain has direction (not a parallel list)
- [ ] No "What is X" type Qs
- [ ] Q sentences ≤ 20 characters (scannable in one glance)
- [ ] No academic tone ("it is noteworthy that" "in summary" "against the backdrop of")
- [ ] A doesn't pile up jargon as safety blanket — all terminology translated into concrete actions or objects
- [ ] 5-10 Qs

Any one fails, go back and fix.

## Step 7: Write File

Get timestamp:

```bash
date +%Y%m%dT%H%M%S         # → identifier
date "+%Y-%m-%d %a %H:%M"   # → date field
```

Denote schema filename: `{YYYYMMDDTHHMMSS}--qa-{topic}__qa.org`

- `qa-` prefix: marks Q-A type (isomorphic with ljg-paper's `paper-`)
- Topic: 5-10 character extraction of core argument, remove punctuation. Prefer method name/concept name/soul-sentence keyword
- `__qa` suffix: keyword tag for denote search

Output path: `~/Documents/notes/`

Report path to user after writing.

## File Structure

```org
#+title:      {One refined sentence of the core argument — 10-25 characters}
#+subtitle:   {Original title}
#+date:       [{YYYY-MM-DD Day HH:MM}]
#+filetags:   :qa:
#+identifier: {YYYYMMDDTHHMMSS}
#+source:     {URL or source}

* Introduction

(A paragraph, 3-5 sentences: what this piece is about, why it's worth extracting as questions. Lands the reader, not a survey)

* Q1: {One sharp question, ≤ 20 chars}

  *Conclusion*: ...

  *Formalization*: ... (e.g. `A = B + C` / `Old: X → New: Y`)

  *How they arrived at it*:
  - ...
  - ...
  - ...

  *Boundary*: ...

* Q2: ...

  ...

* Closing

(One sentence that anchors the entire Q-A chain: what the author truly contributed. Not a summary, a naming)
```

Notes:

- Bold uses `*bold*` (org-mode), not `**bold**` (markdown)
- Lists use `- item`, not `* item` (`*` in org is a heading)
- Separators use blank lines or hierarchy, not `---`
- Code uses `~code~` or `=code=`, not backticks

## Acceptance

- *Q cuts to heart*: each Q cannot be dismissed with a one-line definition
- *A has formalized closure*: each A has all four parts — conclusion sentence can be quoted standalone, formalization reveals relationship at a glance
- *Q chain has direction*: deleting one Q causes subsequent collapse
- *Doesn't restate the original*: it's skeleton reconstruction, not paragraph rewriting
- *Natural language*: read each sentence silently, listen if it sounds like how a real person speaks — verb-driven, no jargon piling, no academic tone
