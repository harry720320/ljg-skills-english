---
name: ljg-paper-river
description: "Paper reverse-reading method: given a paper, recursively find the prior papers it critiques and improves upon (up to 5 layers), then find the latest advances after it, and tell the problem's evolutionary story forward from the source. Problem-centric, Feynman-style explanation of what problem each paper saw and its solution innovation. Use when user shares a paper and wants to understand its intellectual lineage, citation chain, problem evolution, or says '倒读', '论文溯源', '论文脉络', 'paper river', 'paper connects', 'trace back', '这篇论文的来龙去脉', '论文演化'. Also trigger when user wants to understand how a research problem evolved across multiple papers."
user_invocable: true
version: "1.0.0"
---

# ljg-paper-river: Reverse Reading

A paper is not an island. It stands on the shoulders of predecessors, and also on their scars. Dig backward to the root, then read forward — how the problem grew, what each person saw that others missed, how solutions approached truth step by step.

## Core Logic

The most common mistake in reading papers: only looking at the one in front of you, not knowing where it came from. Reverse reading flips this — first find who this paper is critiquing and improving, then find who that paper is critiquing, recursively five layers deep to the source. Then turn around and read forward from the source.

When you finish, you haven't just acquired one paper's knowledge — you've grasped an entire problem evolution line.

## Format Constraints

### Org-mode Syntax

- Bold uses `*bold*` (single asterisk), forbid `**bold**`
- Heading levels start from `*`, no skipping levels

### ASCII Art

All diagrams use pure ASCII characters. Allowed: `+ - | / \ > < v ^ * = ~ . : # [ ] ( ) _ , ; ! ' "` and spaces. Forbid Unicode drawing symbols.

### Template Authority

Output structure follows `references/template.org`.

### Denote File Conventions

- Timestamp: `date +%Y%m%dT%H%M%S`
- Readable time: `date "+%Y-%m-%d %a %H:%M"`
- Filename: `{timestamp}--paper-river-{short_title}__paper_river.org`
- Output directory: `~/Documents/notes/`

### Org File Header

```
#+title:      paper-river-{short_title}
#+date:       [{YYYY-MM-DD Day HH:MM}]
#+filetags:   :paper:river:
#+identifier: {YYYYMMDDTHHMMSS}
#+source:     {URL or source description}
#+authors:    {target paper authors}
#+venue:      {publication venue/year}
```

## Red Lines

1. *Problem as axis* — the main thread is "how the problem evolved", not "how papers are arranged". Papers are supporting characters, the problem is the protagonist
2. *Spoken-word test* — would you tell a friend about a field's development history this way? If not, revise
3. *Difference as core* — each paper's explanation centers on "how it differs from the previous one", not independent introductions
4. *Zero jargon* — land the meaning in plain language first, then mention the term name
5. *Unbroken logic chain* — from first paper to last, the causal chain must not break. The reader should feel "so that's why they did this"
6. *Honesty* — if you can't find five layers, say how many you found. If relationships between papers are uncertain, say so. Don't fabricate citations

## Writing Principles

1. *Difference-driven narrative* — don't write independent summaries for each paper and stitch them together. Begin each section with "what problem this one saw in the previous one", letting differences themselves push the narrative forward
2. *Transformation over definition* — when explaining the difference between two approaches, continuously transform approach A into approach B. "If you remove X and add Y, you get Z" — ten times more powerful than "the difference between Z and X is..."
3. *Visible reasoning* — before each solution appears, let the reader feel the pressure of "there's no choice but to do this". Simulate the discovery process, not report the discovery result
4. *One diagram beats a thousand words* — draw the lineage map before the evolutionary narrative, draw the compressed overview after. Let readers have the full picture before entering details, then return to the full picture after details

## Execution

### 1. Obtain Target Paper

- arxiv URL → WebFetch
- PDF → Read (note pages parameter limits)
- Paper name → WebSearch to find full text

Ensure you have: title, authors, abstract, introduction (especially critiques of prior work in related work / introduction).

### 2. Extract Critique Chain Clues

Carefully read the target paper's introduction and related work sections. Find:

- Where it explicitly says "prior method X has problem Y"
- Which paper(s) it claims to improve upon
- Who its comparison baselines are

From this, identify *the core paper(s) being critiqued/improved upon* (typically 1-3, choose the most direct line).

### 3. Recursive Lineage Tracing (deep research)

For the core prior papers found in step 2, repeat the same process: who is it critiquing? Who is it improving?

Recursion rules:
- Maximum 5 recursive layers (stop at layer 5 or at the field's foundational paper)
- Each layer only follows *the line most relevant to the problem*, no branching
- If a layer has no clear critique target, stop there

Use Research skill (deep research mode) to obtain key information for each layer's paper. At minimum get: title, authors, year, core problem, core solution, critique points against predecessors.

### 4. Frontier Extension

Reverse direction: after the target paper, are there new papers critiquing/improving on it?

Also search with Research skill:
- Subsequent work citing the target paper
- Latest advances on the same problem

Find the 1-3 most relevant follow-up papers, obtain the same information.

### 5. Build the Evolution Line

Organize results from steps 3 and 4 into a timeline:

```
[Oldest] Paper_0 → Paper_1 → ... → [Target Paper] → [Follow-up Papers]
```

Annotate each arrow: what problem the later one saw in the earlier one.

### 6. Forward Feynman Narrative

Starting from the oldest paper, tell the story forward. Key: not introducing each paper independently, but threading them together with problem evolution as the thread.

For each paper, tell three things (difference-focused):
1. What specific problem it saw in the predecessor's approach (illustrate with examples or scenarios)
2. The core idea of its solution (clarify with analogy)
3. What new problem this solution left behind (natural transition to the next paper)

### 7. Draw Diagrams

Two diagrams:
- *Lineage map*: placed before the evolutionary narrative, showing citation/critique relationships between papers
- *Problem-solution overview*: placed after the narrative, compressing the entire line into one screen. A glance should reveal how this line grew

### 8. Extract Insights

After reading the entire line, answer:
- What is really changing beneath this evolutionary line? (Not surface technical iteration, but deeper cognitive shifts)
- Where is it most likely headed next?

### 9. Pass Red Lines + Generate File

Go through red lines one by one. Additional checks:
- Is the causal chain coherent — string together all "what problem it saw" statements, does the logic flow
- Are differences prominent — is each paper's explanation focused on "what's different from before"

Read `references/template.org`, write to `~/Documents/notes/` per Denote conventions.

## Acceptance

- *Problem is the protagonist*: after reading, what's remembered is "how the problem evolved", not "what papers there were"
- *Unbroken causality*: from first paper to last, every turn has a "so"
- *Clear differences*: each paper's unique contribution can be stated in one sentence
- *Outsider can follow*: a smart person unfamiliar with the field can retell this evolution line after reading
- *Two diagrams stand alone*: without reading the text, just looking at the diagrams, the main idea is graspable
- *Honest labeling*: which are confirmed citation relationships, which are speculative — clearly marked
