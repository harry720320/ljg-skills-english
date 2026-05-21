---
name: ljg-invest
description: Investment analysis. Generates an in-depth investment analysis report. Not traditional investment analysis — the core judgment is whether the project is an "order-creating machine". Use when user says '投资报告', '投资分析', '分析这个项目', '写投资报告', 'investment report', 'invest analysis', or provides entrepreneur conversation records wanting investment evaluation. Also trigger when user pastes or references meeting notes, pitch decks, or founder interviews and asks for analysis.
---

# Investment Report

Generate an investment analysis report. Only one question at the core: is this thing creating new order, or just moving old order around?

## Cognitive Starting Point

Wealth is not money — it's order illuminated by desire. Investing is trading the order in your hand for a better order-generating machine.

So don't weigh, read the form:
- Don't ask "how much is this company worth," ask "does this machine turn"
- Don't ask "how big is the market," ask "what outdated lens is the market using to see it"
- Don't ask "how much can it go up," ask "what am I trading for what, and who becomes smarter after the trade"

## Input

Company name, business plan, text description, conversation records, or any material describing the project. For well-known companies, just the name is enough — use Research skill or subagents to fetch the latest financial reports and industry data.

## Report Structure

The five blocks below are a skeleton, not a fill-in-the-blank form. For any given project, whichever block has the most substance gets the most space; thin blocks get a line or two or are skipped entirely. The report serves judgment, not completeness.

### I. What This Is

A table + a custom market-segment definition.

| Dimension | Content |
|-----------|---------|
| Project Name | |
| Segment Definition | In our own language, not market labels |
| Stage | |
| Financing | Amount / Valuation / Terms (fill if known, mark if not) |
| Data Snapshot | Key operational metrics |

Segment definition must pierce through surface labels. "Search engine company" is keeping it at arm's length — "monopoly operator of human cognitive infrastructure" is getting inside — the latter tells you what it's really doing.

### II. Order-Creating Machine Assessment

This is the heart of the entire report. Don't score by item — answer one question: **does this machine turn?**

Look from three angles:

**Is the flywheel spinning?**
Does the system have a structure that gets better with use — more users → more data, more data → better product, better product → more users? Is this loop already spinning, just starting, or stalled? How long has it been spinning? Accelerating or constant? If not spinning, what's jamming it?

**After impact, stronger or weaker?**
Competition arrives, technology shifts, market collapses — does this machine shatter, withstand, or consume the impact as fuel? Has it been hit before? What was the outcome?

**Are resources pushed here or pulled here?**
Does expansion rely on negotiating one by one, buying piece by piece (push), or do others rush in because not coming means losing out (gravity)? Any signs of "aggregating without pushing"?

**Overall Assessment**:
- Order-Creating Machine — flywheel spinning, strengthens after impact, resources come on their own
- Potential — flywheel has structure but not yet verified to spin
- Order Mover — rearranging what already exists, no new order being generated

### III. Creation Formula

Every order-creating machine has a core algorithm. Express it in one sentence.

Reference:
- Amazon = profit → reinvest → lower costs → lower prices → more users → more profit
- Tesla = hardware gathers data → data trains algorithms → algorithms redefine hardware
- Google = every time humanity shifts how it finds answers, become the default infrastructure for the new way

Then answer:
- How many times has this formula been verified? To what degree?
- Are others running similar formulas? Where do they differ?

### IV. What the Market Sees vs. What We See

This section determines investment timing.

**Where is it on the S-curve?**
Accumulation phase, inflection point, acceleration phase, plateau. If before the inflection — what conditions could trigger it?

**What old lens is the market using?**
What label has the market stuck on it? What does this label obscure? What does our framework see that the market doesn't? How big is the perception gap — this is the source of excess returns.

Three signals to detect cognitive discount:
- Requires very complex explanation for others to understand?
- Persistent pricing anomalies (sum of parts ≠ whole)?
- All existing analogies fail ("like X but not X")?

**What does it control that no one can take away?**
What is the source of power — data, distribution, standards, network effects? Is this control static (brand, patents) or dynamic (grows stronger over time)?
Could this scarcity shift in the future? Can the project shift with it?

**Whose coattails is it riding?**
Three costs are collapsing — understanding cost, coordination cost, action cost. Which one is this project riding? How much of the energy released by the collapse is it capturing?

### V. Trade or Not

**Trade recommendation**: Recommend Investment / Recommend Observation / Recommend Pass

**If investing**: suggested amount range, key terms

**Core assumptions**: what assumptions does this decision rest on? Attach an exit signal to each — what data appearing means the assumption was wrong, time to run.

**Unresolved questions**: 3-5 questions critical to the decision but still unanswered, ranked by priority.

### Final Line

Answer in one sentence: what is the essence of this project? Creating new order, or moving old order?

## Output

- Format: org-mode
- Directory: `~/Documents/notes/`
- Naming: denote schema — `YYYYMMDDTHHMMSS==z--investment-analysis-PROJECT_NAME.org`
  - Example: `20260326153000==z--investment-analysis-example-ai.org`
- Use Write tool to write, report the full path when done

## Generation Rules

1. Based on real information, don't fabricate. If information is insufficient, mark it directly, don't force it
2. Dare to judge. "Could be good or bad" is meaningless — not allowed
3. Every judgment comes with evidence — data, citations, specific facts
4. Forbidden phrases: huge market, excellent team, broad prospects, blue ocean
5. Write until it's clear, ignore word count. If two thousand words suffices, two thousand. If seven thousand is needed, seven thousand
6. Write in English
