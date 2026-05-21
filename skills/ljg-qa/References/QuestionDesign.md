# Question Design

How to make Q cut to the heart, and A not scatter.

## Four Q Types (Action-Contrast-Cause-Boundary)

Each type对应 one支点 of the author's argument. A good Q chain mixes at least three types.

| Type | Pattern | Example |
|------|---------|---------|
| *Action* | "How did they do it?" | "How did they transform X into Y?" |
| *Contrast* | "Why A not B?" | "Why iterative instead of parallel?" |
| *Cause* | "Why does this solution hold?" | "Why can chain reasoning emerge?" |
| *Boundary* | "When does it fail?" | "Does this approach still hold when data is sparse?" |

Significance of mixing:

- Pure action questions = tutorial
- Pure contrast = debate transcript
- Pure cause = paper
- Pure boundary = reflection

Only through mixing can you reproduce the original's real tension of "method + cost + limitation".

## Q Forbidden Patterns

- ❌ "What is X?" — dismissible with one definition, no load-bearing
- ❌ "How many steps does X have?" — doesn't count as a question, it's asking for a table of contents
- ❌ "Is X important?" — answer预设, no tension
- ❌ "How should we view X?" — academic tone, no concrete action
- ❌ "What are the characteristics of X?" — textbook chapter title, answer will be a list

## Q Design Patterns

### Action-type Q

Bad: "What is the method of this paper?"
Good: "The author says method X works — how exactly does it work? Which step is the killer?"

Key: force the answer to reconstruct the mechanism, not name it.

### Contrast-type Q

Bad: "How is method X different from method Y?"
Good: "Method Y already solves problem Z — why isn't it enough? What specific case does X handle that Y can't?"

Key: the contrast must be grounded in a concrete dilemma, not floating in abstraction.

### Cause-type Q

Bad: "Why does method X work?"
Good: "The whole thing rides on assumption A — what if A doesn't hold? What's the backup?"

Key:追问 the deepest假设, not the surface rationale.

### Boundary-type Q

Bad: "What are the limitations of method X?"
Good: "Under what conditions does method X produce worse results than random? Has anyone tested this?"

Key: the boundary must be testable, not a generic "future work" disclaimer.

## A Four-Part Structure

Each A must strictly follow four parts, none可省, order不可乱:

```
*Conclusion*: (one sentence — can be摘抄 standalone, forwarded to a friend who gets it)

*Formalization*: (compress the thought into one line of visible relationships using words + simple symbols)

*How they arrived at it*:
- Step 1 (short sentence, only one reasoning step)
- Step 2
- Step 3

*Boundary*: (under what conditions does this conclusion not hold / what hasn't the argument covered yet)
```

## Formalization Writing

Four common patterns:

- *Equation*: `generalist = coordinator; specialist = doer`
- *Contrast*: `Old: LLM = full-stack; New: LLM = coordinator`
- *Flow*: `data → token → answer = loss + waste`
- *Progression*: `call → interface → bilingual hotline`

Use only ASCII + text. Forbid LaTeX, forbid complex math symbols. Fit on one line.

The formalization line is "geometry of thought" — it makes relationships visible at a glance. It is not "mathematical form" — don't use integrals, summations, or Greek letters.

## Quality Self-Check

After writing each A, silently ask:

1. Can the conclusion sentence stand alone? (send it to a friend, they get it)
2. Does the formalization line make the relationship visible in one glance?
3. Do the reasoning steps chain — each step opens the door for the next?
4. Is the boundary specific and testable — not "needs more research"?
