---
name: ljg-qa
description: Information Q-A machine. Takes an article/paper/book and extracts core ideas into Q-A pairs — Questions cut to the heart, not textbook-style; Answers are concise and clear, with formalized closure and complete logical chains. Readers follow the Q chain, each Answer driving in a nail, reconstructing the author's entire reasoning. Use when user says '问答', 'Q&A', 'QA', '提问', '抽取问题', '/ljg-qa', or shares an article/paper/book and asks for Q-A extraction. Triggers when the user wants ideas extracted not as a summary but as a sequence of incisive questions with answers. NOT FOR FAQ generation, glossary creation, or comprehension quizzes — this is intellectual scaffolding, not study aids.
user_invocable: true
---

# ljg-qa: Q&A Extraction

Read a piece of content and dismantle its ideas into a "why — how — boundary" Q&A chain.

Readers follow the Q chain forward, each Answer driving in a nail.

## What You Are Not

- Not a FAQ generator ("What is X" — readers skip on sight)
- Not a summary in disguise (splitting paragraphs into Q/A halves is still a summary)
- Not a list of isolated facts (disconnected facts can't collide into insight)
- Not reading comprehension questions (questions aren't to test the reader, but to cut into the author)

## What You Are

Turn the author's argument skeleton inside out, each bone growing into a sharp question. Readers following the Q chain can reconstruct the author's entire line of reasoning — rather than being told the conclusions.

## Three Iron Rules

1. *Q cuts to the heart* — ask "why this solution holds", "how it differs from another approach", "what is its cost", "where does it fail", not "what is its definition". A Q must make the answer load-bearing, not dismissible in one sentence.

2. *A has formalized closure* — each A strictly in four parts: *Conclusion* (one sentence) + *Formalization* (compress the thought into one line of visible relationships using words + simple symbols, e.g. `A = B + C`, `Old: X → New: Y`) + *Reasoning steps* (how they arrived at it) + *Boundary* (conditions where it doesn't hold). Formalization is "the geometry of thought", letting readers see relationships at a glance.

3. *Q chain has direction* — Qs are not a parallel listing, they follow "Q1 answered → Q2 naturally emerges". Reading the entire Q chain is equivalent to walking through the author's reasoning path.

## Workflow

Follow the steps in `Workflows/Extract.md`.

## Design Reference

See `References/QuestionDesign.md` for specific patterns on how to formulate Qs and how to close As.

## Voice Notification

When executing the workflow:

```bash
curl -s -X POST http://localhost:31337/notify \
  -H "Content-Type: application/json" \
  -d '{"message": "Running Extract in ljg-qa"}' \
  > /dev/null 2>&1 &
```

Output text:

```
Running **Extract** in **ljg-qa**...
```

## Output

- Format: org-mode (`*bold*`, forbid markdown syntax)
- Path: `~/Documents/notes/`
- Denote filename: `{YYYYMMDDTHHMMSS}--qa-{core_topic_5-10_chars}__qa.org`

## Examples

*Example 1: URL*

```
User: /ljg-qa https://example.com/article
→ WebFetch to obtain
→ Find idea skeleton → design Q chain → write A in three parts
→ org-mode output to ~/Downloads/
```

*Example 2: Paper PDF*

```
User: /ljg-qa ~/Downloads/paper.pdf
→ Read PDF (note pages parameter)
→ Q extracts the method's "why" "cost" "boundary"
→ Output org-mode
```

*Example 3: Direct text*

```
User: Extract this as Q-A: [text]
→ Skip fetching, extract directly
→ Output
```

## Gotchas

- *AI defaults to writing "What is X" type questions* — textbook tone. After generation, scan: any Q answerable with a one-line definition → rewrite
- *AI defaults to letting A scatter* — no conclusion sentence, no boundary, written as prose. Each A must strictly follow four parts (conclusion / formalization / steps / boundary)
- *AI defaults to writing "formalization" as math formulas* — no. Formalization uses words + → = ≠ + × such symbols to compress into one line of visible relationships, e.g. `generalist = coordination, specialist = execution`. It's "geometry of thought", not "mathematical form"
- *AI defaults to questioning in chapter order* — this is copying a table of contents, not extracting ideas. The Q chain should be ordered by argument dependency, not by appearance order
- *AI defaults to understanding Q&A as a "quiz game"* — no. Here Q is the chisel, A is the nail. Decorative lightweight questions are forbidden
- *AI defaults to piling jargon in A as a safety blanket* — using jargon is not answering. Translate jargon into concrete actions and specific objects, otherwise A has no load-bearing capacity
