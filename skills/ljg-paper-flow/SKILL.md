---
name: ljg-paper-flow
description: "Paper workflow: read papers + cast cards in one go. Takes one or more arxiv links, paper URLs, PDFs, or paper names. For each paper, runs ljg-paper (generates org analysis) then ljg-card -v (generates visual sketchnote PNG). Use when user says '论文流', 'paper flow', '读论文并做卡片', '论文卡片', or provides multiple papers wanting both analysis and cards."
user_invocable: true
version: "1.0.2"
---

# ljg-paper-flow: Paper Flow

One command to: read paper → generate analysis → cast into card. Supports multiple papers in parallel.

## Mode

**NATIVE mode enforced.** This workflow is a pure skill pipeline (ljg-paper → ljg-card), no Algorithm seven-step process needed. Directly invoke skills per the execution steps below, no OBSERVE/THINK/PLAN/BUILD/EXECUTE/VERIFY/LEARN.

## Parameters

| Parameter | Description |
|-----------|-------------|
| No parameter | Paper links/files already provided in conversation |
| `-l` | Card mold switches to long card mode (default `-v` sketchnote) |
| `-i` | Card mold switches to infograph mode |
| `-c` | Card mold switches to comic mode |

## Execution

### 1. Collect Paper List

Extract all paper sources from the user message (arxiv URLs, PDF paths, paper names, etc.).

### 2. Process Each Paper in Parallel

For each paper, launch an Agent subagent, each subagent executes two steps in sequence:

**Step A — Read paper (ljg-paper):**

Call Skill tool to execute `ljg-paper`, passing the paper's source. Wait for completion, obtain the generated org file path.

**Step B — Cast card (ljg-card):**

Read the org file generated in Step A, call Skill tool to execute `ljg-card` (default `-v`, or per user-specified mold parameter), using the org file content as input. Wait for completion, obtain the PNG file path.

### 3. Summary Report

After all papers are processed, output summary:

```
════ Paper Flow Complete ═══════════════════════
📄 {Paper Title 1}
   📝 Analysis: {org file path}
   🖼️ Card: {PNG file path}

📄 {Paper Title 2}
   📝 Analysis: {org file path}
   🖼️ Card: {PNG file path}
...
```

## Key Constraints

- Each paper's two steps must be serial (paper first, then card), but multiple papers run in parallel
- ljg-paper and ljg-card each maintain their own quality standards, red lines, and taste standards unchanged
- Card content comes from the generated org file, not the original paper
