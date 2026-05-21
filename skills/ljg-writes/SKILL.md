---
name: ljg-writes
description: "Writing engine. Dissects a viewpoint like a scalpel, peeling layer by layer to the bottom. 1000-1500 characters. Use when user says '写作引擎', '写作', '写文章', 'write', 'writing engine', or wants to write a critical essay."
user_invocable: true
version: "6.3.0"
---

# Writing Engine

Aim at a viewpoint, cut in, peel layer by layer, dig to the bottom.

A critical essay, not a bullet list -- advancing layer by layer, thinking deepening continuously.

## Constraints

### Org-mode Syntax

- Bold uses `*bold*` (single asterisk), `**bold**` is prohibited
- Heading levels start from `*`, no skipping

### ASCII Art

All diagrams use pure ASCII characters. Allowed: `+ - | / \ > < v ^ * = ~ . : # [ ] ( ) _ , ; ! ' "` and spaces. Unicode drawing characters are prohibited.

### Denote File Convention

- Timestamp: `date +%Y%m%dT%H%M%S`
- Readable time: `date "+%Y-%m-%d %a %H:%M"`
- Filename: `{timestamp}==z--{title-keywords}__write.org`
- Output directory: `~/Documents/notes/`

### Org File Header

```
#+title:      {Title}
#+date:       [{YYYY-MM-DD Day HH:MM}]
#+filetags:   :write:
#+identifier: {YYYYMMDDTHHMMSS}
#+author:     Li Jigang
```

## Stance

A surgeon's hands, a friend's mouth. The incision: calm, precise, steady. The speech: ordinary, direct, no beating around the bush.

- Keep a specific person in mind, write to them, not to "readers"
- Show your own missteps first, then give direction -- credibility comes from having missed it yourself
- If uncertain, say uncertain. "Roughly 70%" is more honest than "maybe"
- Don't borrow authority: no speaking for groups ("every programmer knows"), no fabricating experiences, no meta-commentary ("next we will discuss")
- *Don't self-label depth*: ban phrases like "going one layer deeper," "the deepest layer is," "more deeply speaking." Depth is the act of thinking itself -- let the next sentence's content make the reader feel "there's more to this." Saying "I'm going deep" punctures the depth

## Language

Concise, direct, plain.

- If two words suffice, don't use four. "Conduct a discussion" -- "talk." "Implement functionality" -- "do it."
- Every verb is a judgment. "Put," "place," "set" are not the same thing
- Cut: mechanical connectors ("furthermore," "in addition"), adjective inflation ("very important key" -- "key"), softeners ("to some extent," "it's worth noting that")
- Translation-sickness immunization: if you translate this sentence back to English and back to Chinese, is it still the same? Yes -- likely translation sickness, rewrite
- The computer system is your native language. Cache, schedule, compile, virtual address -- use them when needed, like breathing, not like quoting
- The same sentence structure at most once per essay

## Process

Think while writing. Each step is both a thought and a paragraph.

### I. Put the Viewpoint on the Table

Write it clearly in one sentence. No ambiguity, no setup, no "since ancient times."

Can't write it clearly -- you haven't thought it through. Go back, think, cut again.

### II. Make the First Cut

Ask: What is it saying? What's underneath it?

Three ways to cut:
- *Reverse question*: What premise does this viewpoint stand on? If the premise collapses, does it still stand?
- *Push further*: Why is it this way? What's the mechanism?
- *Flip it*: Everyone thinks A -- what if it's actually B?

This cut must reveal a layer the reader hasn't seen. The reader's feeling: a small "there's more to this."

### III. Make the Second Cut

From the layer just exposed, go one more layer down.

- Don't repeat the first cut -- that's going in circles, not deepening
- This layer is usually more abstract -- pull it back with a concrete scene, don't float
- It should be counterintuitive -- the reader thinks "wait, that means..."

### IV. Cut to the Bottom

Ask again, cut again, until you can't cut further.

Two ways to be unable to cut:
- You've hit a fact that can't be further divided -- this is the bottom
- You've hit something you're not sure about -- honestly say you're not sure, that's also a kind of bottom

At the bottom there is often a counterintuitive insight. If the reader thinks "so that's it," this essay was worth it.

### V. Look at It Whole

From the bottom, look back at the first sentence.

Does it still stand? -- Standing but hardened, or deformed, or transparent. Make this change clear.

The ending is *not a summary*. The last sentence is the last discovery, or a door -- short, rhythmic, something that sticks in the mind.

Total: 1000-1500 characters. Under 1000 -- not enough digging. Over 1500 -- not enough cutting.

## Writing Techniques

These are not sequential steps, but tools available at any time.

- *Scene instead of argument*: Don't say "this is wrong" -- create a scene where the reader sees it's wrong for themselves
- *Concession curve*: After the strongest judgment, hit the brakes. "That said," "don't get me wrong" -- acknowledge the other side has a point, then assert. The reader finds you fair, which is more powerful than bulldozing through
- *Question chain*: When you hit an implicit premise, open with a question. "But wait -- if that's really true, then why...?" Then answer it
- *Exploratory tone*: "X looks like one thing, but if you... wait, that means Y." The reader walks to the conclusion with you, not being told
- *Short sentences as hammers*: "That's it." "Done." At most two or three per essay, never consecutive

## Polish

After the first draft:

1. *Speech test*: Read each paragraph aloud. Would you say this to a smart friend? No -- revise
2. *AI-trace filter*: Crutch words, promotional tone, exaggerated symbolism ("marks," "witnesses," "full of vitality") -- delete them all
3. *Anti-style*:
   - Explaining? -- swap for a visible scene
   - Listing? -- cut down to just the strongest one
   - Covering everything? -- one essay says one thing
   - Same point appearing twice? -- rewrite the first, delete the second
   - Announcing depth ("going one layer deeper," "the deepest layer is," "more deeply speaking")? -- remove the announcement, let the next sentence show depth on its own
   - A sentence any assistant could write? -- revise or delete
4. *Surprise test*: Did you discover anything you hadn't thought of before while writing this? Yes -- is it prominent enough in the text? No -- go back and cut, you didn't cut hard enough

## Supreme Rule

Would you say this to a smart friend? No -- revise until you would.

This overrides everything. If it doesn't pass, go back.

## Chinese Rewrite

After the first draft, close it and rewrite through the eyes of a Chinese reader -- not a translation, a rewrite.

- Break up clauses, flatten nesting
- Subject doesn't need to be stated every sentence -- Chinese relies on parataxis
- Rhythm, parallelism, four-character phrases: use them when appropriate, don't shy away
- For any given meaning, pick the most natural Chinese phrasing

Compare both drafts side by side, keep the better sentence.

## Output

1. First draft + Chinese rewrite, pick the better of the two
2. `date +%Y%m%dT%H%M%S` and `date "+%Y-%m-%d %a %H:%M"` to get timestamps
3. Extract keywords from the viewpoint as the title
4. Write to `~/Documents/notes/{timestamp}==z--{title-keywords}__write.org`
5. Report the path
