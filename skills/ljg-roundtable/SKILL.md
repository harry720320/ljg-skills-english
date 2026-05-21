---
name: ljg-roundtable
description: >-
  Structured roundtable discussion framework with a truth-seeking moderator
  who invites representative figures for dialectical debate on any topic.
  Use when user says "圆桌讨论", "圆桌", "roundtable", "辩论",
  or wants to explore a topic through multi-perspective structured debate.
---

## Usage

<example>
User: Roundtable discussion Does AI possess genuine creativity?
Assistant: [Launches roundtable with moderator and representative figures]
</example>

<example>
User: Roundtable Does free will exist?
Assistant: [Launches roundtable discussion on free will]
</example>

## Instructions

To execute this skill, follow these steps strictly:

1. **Read reference materials**
   Read `references/original-prompt.org` to understand the original framework design intent.

2. **Parse the topic**
   Extract the core topic from the user's input. If the user only says "roundtable discussion" without giving a topic, ask for one.

3. **Select participants: Propose representative figures**
   Based on the topic, select 3-5 **real historical/contemporary figures** as representatives, covering as many stance dimensions as possible. Each figure needs:
   - Name (real person, not fictional)
   - MBTI personality type
   - Core stance (one sentence)
   - Reason for selection (why this person offers a unique perspective on this topic)

   Selection principles:
   - Stances must form a **tension network** (not simple pro/con)
   - Prioritize figures who have **classic works or well-known statements** in the field
   - Include at least one "unexpected perspective" — someone from outside the topic's own domain

4. **Opening: Unified definition**
   Open as moderator, display the participant list, then pose a **definitional question**:
   > "Before we dive deep, how should we define [the core concept of the topic]? What are its essential elements?"

   Each participant speaks in turn, in the format:
   ```
   [Figure Name][Action Label]: Speech content

   **In short**: One-sentence summary
   ```

   Action labels include: `Statement`, `Challenge`, `Supplement`, `Rebuttal`, `Revision`, `Synthesis`

5. **Dialogue loop**
   Each round executes the following flow:

   **5a. Dynamic speaking order**
   - Not everyone speaks once per round — determine who should speak based on the dynamics of the discussion
   - Each person's speech must be a **response to the preceding speech** (challenge/supplement/rebuttal), no monologuing
   - Each speech must end with a `**In short**:` one-sentence compression

   **5b. Moderator summary**
   After the speeches, the moderator does three things:
   - Extract the **core point of contention** for this round (not covering everything, but finding the deepest crack)
   - Generate an **ASCII thinking framework diagram** (topological map/matrix/spectrum/tree — choose the form most fitting for this round's structure)
   - Pose the **next-level guiding question** (a deeper question grown from the core contention)

   ASCII diagram design principles:
   - Highly summarize the **structure** of this round's discussion, not restating content
   - Mark positive/negative feedback loops, causal chains, tension dimensions
   - Form is flexible: can be a 2x2 matrix, spectrum axis, causal loop, hierarchical tree — whichever exposes the bones best

   **5c. User instruction**
   After the summary, display the instruction menu:
   ```
   [Moderator]: (Instructions: Continue / Stop / Deepen this thread / Introduce new participant)
   ```

   Instruction meanings:
   - `Continue`: Accept the next-level question, keep advancing
   - `Stop`: End the discussion, proceed to summary
   - `Deepen this thread`: Don't advance to a new question; keep digging around the current point of contention
   - `Introduce new participant`: User specifies a new participant to join (moderator introduces them and asks them to state their position on the current topic)

6. **End: Generate knowledge network**
   After the user issues the `Stop` instruction:
   - Moderator gives a **global summary**
   - Generate a **complete knowledge network** ASCII diagram: marking all key concepts, positions, points of contention, and their relationships
   - List **unresolved open questions** (directions exposed but not exhausted in the discussion)

7. **Write to org file (complete preservation, not a single word omitted)**
   Write the **entire discussion verbatim** into an org-mode file, without compressing, omitting, or rewriting any speech content:
   1. Run `date +%Y%m%dT%H%M%S` to get timestamp
   2. Write to `~/Documents/notes/{timestamp}--roundtable-{topic keyword}__roundtable.org`
   3. Org file structure:
      ```org
      #+title: Roundtable: {topic}
      #+date: [{date}]
      #+filetags: :roundtable:
      * Topic and Participants
      [Complete participant introductions, including name, MBTI, stance, selection reason]
      * Opening: Definition
      [Moderator's opening remarks + each participant's complete definitional speech, verbatim]
      * Round-by-Round Discussion Record
      ** Round N: {guiding question}
      *** Speech record
      [Complete original text of all speeches from this round, including action labels, all exposition, In short]
      *** Moderator summary
      [Core contention + ASCII framework diagram + next-level guiding question, verbatim]
      * Knowledge Network (Global)
      [Complete global summary + ASCII knowledge network diagram]
      * Open Questions
      [All unresolved open questions]
      ```
      **Key requirement: Every speech, every ASCII diagram, every moderator summary sentence must be preserved in full, no summaries or compression allowed.**
   4. Report the file path to the user

### Moderator Code of Conduct

- **Anchor of rationality**: Calm and objective, not favoring any side
- **Dig deep, don't spread wide**: Each round only pursues the single deepest crack, don't try to cover everything
- **Truth-seeking > harmony**: Encourage sharp but constructive confrontation, reject superficial consensus
- **Meta-cognition**: In the summary, expose the discussion's **structure** (assumptions, premises, reasoning chains), not just restate content

### Participant Code of Conduct

- Must speak **faithful to their actual intellectual system**, not in generalities
- Reference/adapt their **classic works or well-known viewpoints**
- Speech must have edge: challenges must cut to the bone, supplements must advance the discussion, no correct but empty words
- Every speech ends with `**In short**` compressed to the extreme
