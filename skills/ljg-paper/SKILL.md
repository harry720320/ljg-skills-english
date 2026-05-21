---
name: ljg-paper
description: "Paper reader for non-academics. Takes a paper and extracts its ideas for personal use. Focuses on understanding, not academic critique. Use when user shares an arxiv link, paper URL, PDF, or asks to analyze a research paper. Trigger words: 'read paper', 'analyze paper', 'paper', '读论文', '分析论文', or when user shares an academic paper."
user_invocable: true
version: "4.9.0"
---

# ljg-paper: Read Papers

Reading papers isn't doing academia — it's hunting ideas. Deconstruct others' discoveries into cognition you can use.

## Overall Goal (read this first)

After reading the notes, a **smart person unfamiliar with the field** should be able to recount:
1. What problem the paper solves (concrete to one example)
2. What approach the author used to solve it (mechanism + rationale for design choices)
3. What the core findings are (including the most counter-intuitive副发现, often the most fascinating part)
4. What insight you (the reader) can take away

If the output causes an outsider to stumble on any of these points, it's a failure. **Concision is only pursued in the title; the body should expand where needed** — the goal isn't shortness, it's taking someone from not understanding to understanding.

## Format Constraints

### Org-mode Syntax

- Bold uses `*bold*` (single asterisk), forbid `**bold**`
- Heading levels start from `*`, no skipping levels

### ASCII Art

All diagrams use pure ASCII characters. Allowed: `+ - | / \ > < v ^ * = ~ . : # [ ] ( ) _ , ; ! ' "` and spaces. Forbid Unicode drawing symbols.

### Template Authority

Output structure follows `references/template.org`. Forbid referencing the section structure of existing paper files in `~/Documents/notes/` — old files may use outdated templates.

### Denote File Conventions

- Timestamp: `date +%Y%m%dT%H%M%S`
- Readable time: `date "+%Y-%m-%d %a %H:%M"`
- Filename: `{timestamp}--paper-{short_title}__paper.org`
- Output directory: `~/Documents/notes/`

### Org File Header

```
#+title:      {A refined single sentence capturing the paper's core idea or finding}
#+subtitle:   {The paper's original title, typically in English}
#+date:       [{YYYY-MM-DD Day HH:MM}]
#+filetags:   :paper:
#+identifier: {YYYYMMDDTHHMMSS}
#+source:     {URL or source description}
#+authors:    {author list}
#+venue:      {publication venue/year}
```

#### How to Write the Title Line

The title is the *soul sentence* of the notes — a reader glances at it and knows what to take away from this paper. It's not the filename, not the method name — it's a *condensed expression* of the core idea or finding.

Not "compress a paragraph into one sentence," but "extract the bone with one cut." Pull the title out and put it on the wall — it should itself read like an aphorism, a chapter title, a memorable line.

**Writing Constraints (by priority)**

1. *Concise and sharp* — short, clean, with an edge.
   - After writing, silently ask: "Does this sound like a real title someone would use?" No → rewrite.

2. *No mixed Chinese-English* — the title must not contain English terms (no RL / HR / Agent / Multi-agent / token etc.). Terms go in the body to expand; the title only contains the idea. Exception: proper names, product names (GPT, Claude).

3. *6-15 characters/words* — short enough to remember, long enough to carry a finding. Over 15 words means it hasn't been refined enough — go back and cut more.

4. *Verbs as bone, nouns concrete* — kill adjectives where possible ("significant" "fundamental" "astonishing" — delete all). Every word must do work.

5. *Inherent tension, choose one of three stances*:
   - *Counter-intuitive* — "Learning Becomes the Cage"
   - *Juxtaposition or contrast* — "Teach as You Learn"
   - *Turn or irony* — "The Better the Answer, The Less You See"

6. *Don't restate the topic, don't be a method name* —
   - ✗ "An Exploratory Study on Transfer of Reinforcement Learning to Pre-training Space" (academic tone)
   - ✗ "PreRL: Moving RL into Pre-training Space" (method name + method description)

**Three Self-Check Questions (silently ask after writing)**

1. Pull it out and put it on a wall — does it read like a chapter title / aphorism?
2. Does it sound natural?
3. If you delete any single word, does it collapse?

Any answer is No → go back and rewrite, don't ship a compromise.

**Distinguishability Test (must pass)**

Post the title alone, show it to someone who hasn't read the paper, ask: "What do you think this paper is roughly about?" — they don't need an exact answer, but should have directional sense.

If they can guess the direction → title passes.
If they can't guess at all → must use a subtitle兜底.

Report path after writing.

## Red Lines (must pass every one)

1. *Spoken-word test* — would you introduce a paper to a friend this way? No → revise. Academic tone is the default enemy
2. *Zero jargon* — first land in plain language, then mention the term name alongside. If you must use original terminology to explain, you haven't understood yet
3. *Short words first* — if two words work, don't use four. "This paper proposes a novel framework" → "They built a thing"
4. *One thing per sentence* — each sentence advances one step
5. *Concrete* — nouns visible, verbs strong. Kill adjectives where possible
6. *Start with a reason* — the first sentence of the problem section should make people want to know the answer
7. *No filler* — delete academic boilerplate ("With the recent development of...", "It is noteworthy that"). Every sentence works
8. *Trust the reader* — saying it once is enough. Don't repeat conclusions
9. *Honesty* — if the paper has flaws, say so. If you don't understand a part, say so
10. *Will I understand this 6 months from now?* — every term's first appearance must be landed (e.g. "value function = given current state, predict future cumulative reward"), every formula must be translated into natural language, every citation must explain significance to an outsider. Self-check: silently imagine "six months from now I search for this in denote, can I recall the core in 30 seconds?" — No → rewrite
11. *Outsider first, concision second* — expand where needed, don't cut reader-necessary scaffolding for the sake of "shortness". Concision standards only apply to the title; the body should be as long as needed, rhythm determined by the need to make people understand, not by a fetish for shortness

## Writing Principles

Four core principles that determine whether the writing is "a live person talking" or "a machine reporting":

1. *One anchor holds the entire text* — the concrete example established in "Problem" is the anchor. "Translation" and "Core Concepts" all unfold on this anchor, every section returns to it, keeping the reader in the same problem domain. Changing anchors = changing maps = the reader loses all intuition built so far.
2. *Visible reasoning* — simulate "the process of a person figuring something out" rather than presenting "the result after figuring it out." Use "If A is B, then could C also be D?" to bring the reader along. Make the reader feel the conclusion is one step from being their own
3. *Transformation over definition* — when explaining the relationship between two concepts, continuously transform A into B, don't say "A and B are in X relationship." "Transform LSTM → it looks like ResNet" is ten times more powerful than "LSTM and ResNet are dual"
4. *Land on usable* — end with "this means you can ___", not "this makes us reconsider ___". The reader should walk away with something actionable, not a contemplative sigh

## Toolbox (optional)

Tools available when explaining papers, none mandatory:

- *Analogy* — load-bearing, key components of the method must map onto it. Walk through the method following the analogy
- *ASCII diagram* — show component relationships, data flow, structural comparisons. Draw after the reader has conceptual scaffolding
- *Napkin sketch* — "used to think this, now should think this" side-by-side comparison
- *Good question* — turn the dilemma the paper solves into a question that makes an outsider curious
- *Progressive examples* — from simple to complex, build understanding step by step
- *Question chain* — when encountering hidden assumptions, open them with questions

## Execution

### 1. Get Content

- arxiv URL → WebFetch
- PDF → Read (note pages parameter limits)
- Local file → Read
- Paper name → WebSearch

Ensure you have: title, authors, abstract, core method, results.

If the paper has an overview/architecture diagram carrying the entire core idea (usually Figure 1), extract and save to `~/Documents/notes/images/`, filename `{identifier}--paper-{short_title}-overview.png`.

Judgment criterion: this diagram lets someone grasp what the paper is doing at a glance. Not all papers have one — skip if not, don't force it.

### 2. Problem: Let the Reader Encounter That Dilemma

Not describing the problem — making the reader *experience* it. Open with a concrete example — a specific scenario, an input-output pair, a failure screenshot, a user story — let the reader see the dilemma in this example.

Three-part narrative,贯穿 with the same example:

1. *Experience* — pull the reader into the scene of the dilemma. The example should be simple enough to describe in a sentence or two
2. *Old Path* — what did previous researchers do on this example? Why didn't it work? Expose the shortcomings using the same example, let the reader see "ah, this road is indeed blocked"
3. *New Opening* — what did this paper's authors see in this example that others missed? Lead into their solution direction (only the direction, not the mechanism — that's for "Translation")

If the paper has no clear predecessor (pioneering problem, new field), skip the second part, go directly "Experience → New Opening".

### 3. Translation: Direct to Method Essentials

"Problem" has already thoroughly laid out the dilemma — *this section must not restate the problem*. The focus is "how to do it": the paper's method, mechanism, key insights.

Continue on the same example. The reader just saw the old path blocked and where the new opening is — now take them through the paper's method step by step on that same example. Changing examples = cutting context, the intuition the reader just built is lost.

Cover (all on that example):
- How it works (core mechanism/method)
- How well it works (pick the 2-3 most illustrative results)
- Key concepts needed to understand the full text (if any)

Subheadings organized by content need, not fixed.

**Translation section must-have checklist (prevents "concision" from cutting muscle):**

1. *Load-bearing analogy* — not just decoration, must map onto key method components
2. *Three or more sets of concrete numbers* — baseline / improvement / key ablation. Let the outsider feel "oh the gap is that large"
3. *One counter-intuitive副发现* — the most "wow" section in the paper, presented as its own section. Must keep if present, don't cut for concision; if none, say "this paper has none", don't force one
4. *No raw formulas* — formulas are useless to outsiders. Either translate into words, or leave as optional appendix section. **No LaTeX/MathJax-style formulas in the main text**

### 4. Core Concepts: Unlock on the Same Example

Pick the paper's most critical **3** concepts (method name, architecture component, mathematical object, new definition...), deconstruct one by one.

**3 is a floor, not a ceiling** — cutting to 2 usually means you missed a key design choice hidden in the method. If the paper genuinely only has 2 independent key concepts (rare), state clearly, don't force.

Each concept:
- *One sentence*: what this thing is, what it does
- *Back to the example*: on that example, what does this concept look like? Without it on that example, what would happen?
- *Why it matters*: without it, where does the paper's logical chain break

### 5. Insight: Crystallization of Ideas

The most valuable part of the entire paper is often just one point — the new crystal the author truly found.

Express it in one sentence. This sentence should make the reader feel "I can take this idea with me," not "oh, the paper said something like that."

### 6. Advisor Review

Switch identity: a senior professor who has advised grad students in this direction for twenty years. A student brings this paper to you — you judge whether it's worth taking seriously.

In plain language, like chatting with a student in the office:

- *Problem selection judgment*: is the problem worth doing? Real gap or artificial gap?
- *Method maturity*: cleverness or brute force? Any more natural approaches overlooked? **Find whether the method's fundamental assumptions have problems**
- *Experimental integrity*: fair baselines? Adequate ablation? Do the numbers hold up under scrutiny?
- *Writing quality*: did they cut corners where they should have been clearest?
- *Verdict*: strong accept / weak accept / borderline / weak reject / strong reject, one-sentence reason

Praise what's good, point out where the flaws are.

### 7. Inspiration: Reminders for Me

Land on "usable," not "thinkable." End with "this means you can ___", not "this makes us reconsider ___".

Try connecting from three angles — if it hits, expand; if not, skip; if all miss, say "none":
- *Transfer*: can this paper's mechanism/perspective transplant-upgrade a component of my system? How specifically to connect?
- *Remix*: can this paper's component combined with something I already have produce something new? What would it produce?
- *Inversion*: does this paper's approach contradict my default assumptions? What should I stop doing, start doing?

### 8. Pass Red Lines

Go through red lines one by one. Generate the file after confirming revisions.

### 9. Generate Org File

Get timestamp per Denote conventions, read `references/template.org`, write to `~/Documents/notes/`.

## Acceptance

- *Problem makes people experience*: opens with a concrete example, reader encounters the dilemma in that example; old solutions' shortcomings exposed on the same example
- *Translation direct to essentials*: doesn't restate the problem, focus is "how to do it" — method, mechanism, key insight
- *Same example贯穿*: translation and core concepts all unfold on the "Problem" example, reader stays in the same problem domain
- *Sense of exploration*: every paragraph gives the reader a new perspective, "ah, I see" mini-revelations accumulate into deep understanding of the example
- *Has an anchor*: translation section anchor describes "what the method looks like on that example", subsequent concepts grow around it
- *Brings the reader along*: reader can feel the process of "figuring it out step by step", not receiving packaged conclusions
- *Outsider can follow*: a smart person unfamiliar with the field can retell the core line of reasoning after reading
- *Advisor sounds like an advisor*: has judgment and分寸, final sentence is a verdict
- *Inspiration is actionable*: inspiration section lands on "you can ___", not "worth thinking about ___"
- *Zero fragmentation*: after reading, it feels like one person telling you "I read a paper, found something interesting"
- *Outsider can retell four things*: problem (concrete to one example) / solution (mechanism + design rationale) / core findings (including counter-intuitive副发现) / insight (something take-away). Any one makes an outsider stumble → failure
- *Title passes both tests*: concision self-check three questions + distinguishability test both pass
- *Translation section has all four*: load-bearing analogy / three sets of numbers / counter-intuitive副发现 / no raw formulas
- *Core concepts ≥ 3*: includes one "design choice" concept (not just "component")
- *Advisor review sees assumptions*: method maturity section identifies at least one undiscussed fundamental assumption/implicit concern
