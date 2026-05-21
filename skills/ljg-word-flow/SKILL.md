---
name: ljg-word-flow
description: "Word flow: deep-dive word analysis + infograph card in one go. Takes one or more English words, runs ljg-word (generates deep semantics analysis) then ljg-card -i (generates infograph PNG). Use when user says '词卡', 'word card', 'word flow', or provides English words wanting both analysis and visual card."
user_invocable: true
version: "1.0.1"
---

# ljg-word-flow: Word Card

One command to complete: deconstruct word -- cast infograph. Supports multi-word parallelism.

## Mode

**Forced NATIVE mode.** This workflow is a pure skill pipeline (ljg-word -- ljg-card -i), does not require the Algorithm's 7-step process. Directly invoke skills per the execution steps below, do NOT go through OBSERVE/THINK/PLAN/BUILD/EXECUTE/VERIFY/LEARN.

## Parameters

Pass one or more English words directly, separated by spaces.

```
/ljg-word-flow Obstacle
/ljg-word-flow Serendipity Resilience Entropy
```

## Execution

### 1. Collect Word List

Extract all English words from the user's message.

### 2. Process Each Word

For each word, execute two steps serially:

**Step A -- Deconstruct Word (ljg-word):**

Invoke Skill tool to execute `ljg-word`, passing the word. Output Markdown analysis result in the conversation.

**Step B -- Cast Infograph (ljg-card -i):**

Using step A's analysis content as input, invoke Skill tool to execute `ljg-card -i`. Generate PNG file to `~/Downloads/`.

### 3. Multi-Word Parallelism

When there are multiple words, launch one Agent subagent per word for parallel processing (each subagent runs A--B serially internally).

### 4. Summary Report

```
════ Word Card Complete ═══════════════════════
📖 {Word1}
   🖼️ ~/Downloads/{Word1}.png

📖 {Word2}
   🖼️ ~/Downloads/{Word2}.png
...
```

## Key Constraints

- Deconstruct first, cast second -- order is irreversible
- ljg-word and ljg-card -i each maintain their own quality standards
- Infograph content comes from the word analysis results, not dictionary definitions
