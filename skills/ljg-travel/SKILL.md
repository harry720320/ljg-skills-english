---
name: ljg-travel
description: "Deep travel research workflow for museums and ancient architecture. Input a city name, auto-generates structured knowledge document (org-mode) + portable reference cards (PNG). Covers historical background, museum highlights, archaeological significance, and architectural heritage. Use when user says '旅行研究', '博物馆功课', '古建功课', 'travel research', '出发前功课', or provides a city name with intent to do deep cultural travel preparation."
user_invocable: true
version: "1.0.0"
---

# ljg-travel-flow: Travel Research

One command to complete: full-dimensional cultural research -- content extraction -- org document + portable cards.

Methodology draws from archaeological Desk-Based Assessment (DBA): exhaust all documentary evidence before arrival.

## Mode

**Forced NATIVE mode.** This workflow is a multi-skill pipeline (Research -- ContentAnalysis -- ljg-card), not the Algorithm 7-step process.

## Parameters

| Parameter | Description | Example |
|-----------|-------------|---------|
| City name | Required, target city | Xi'an, Luoyang, Datong |
| `-f` | Focus topic (optional) | `-f Tang Dynasty` `-f Grottoes` `-f Bronze` |
| `-q` | Quick mode, skip content extraction, only do research + document | |

## Execution

### 1. Parse Parameters

Extract city name and optional parameters from the user's message. If a focus topic is specified, all subsequent searches revolve around that topic.

### 2. Full-Dimensional Research (Research extensive -- single call, 12 Agents in parallel)

Invoke Skill tool to execute `Research`, using extensive mode.

**Core design: no separation between "knowledge mapping" and "platform discovery" -- they are different search angles of the same research operation.** 12 Agents set out simultaneously, half doing academic/encyclopedic research, half doing platform content search.

**Research outline (prompt passed to Research):**

```
Conduct deep cultural travel research on 「{city}」. This is not a travel guide -- it's an archaeological-style desk-based assessment before departure.

Research covers the following dimensions, each requiring bilingual Chinese-English search:

**Dimension A -- Historical Strata**
What important historical periods did this city experience? What material remains did each period leave in this city? How did dynastic changes affect the city's layout?

**Dimension B -- Museum Highlights**
What important museums are in this city? What are the crown jewels and core collections of each museum? Which exhibits have major archaeological significance? Must provide specific artifact names and exhibition hall locations.

**Dimension C -- Ancient Architecture**
What important ancient buildings and sites still exist? Construction period, architectural form, structural features. Which are national key cultural heritage protection units? What details should be observed when viewing the architecture (dougong brackets, color paintings, stone inscriptions, etc.)?

**Dimension D -- Archaeological Discoveries**
What major archaeological discoveries have been made in and around this city? Which museums now house the unearthed artifacts? What important stories emerged during the excavations?

**Dimension E -- Cultural Context**
Important historical figures, literary works, and cultural traditions associated with this city. Helps understand the city's cultural character.

**Dimension F -- Deep Content Discovery**
Search for in-depth explanatory content about the city's museums and ancient architecture on Bilibili (bilibili.com), Zhihu (zhihu.com), WeChat public accounts (mp.weixin.qq.com), Douyin (douyin.com), and Xiaohongshu (xiaohongshu.com).
Filtering criteria:
- Include: content with knowledge value (background, craftsmanship, archaeological process, architectural details)
- Exclude: pure check-in photo ops, recommendations without analysis, sponsored content
- Bilibili videos: prioritize explanatory content over 10 minutes
- WeChat articles: prioritize those with references or clear authorship
Return content title, URL, and one-sentence summary.

{If focus topic specified: pay special attention to content related to 「{focus topic}」, with other dimensions as background context.}
```

Wait for Research to complete, obtain full-dimensional research results.

### 3. Content Extraction (ContentAnalysis -- Optional)

If the user specified `-q` quick mode, skip this step.

From the results returned in step 2, extract all valid URLs (article links, video links).

**Launch an Agent subagent for each URL in parallel:**

Each subagent invokes the Skill tool to execute `ContentAnalysis`, passing the URL, using the fast depth level, extracting key knowledge points.

**Degradation rules:**
- If ContentAnalysis fails for a URL (inaccessible, no subtitles, etc.), skip that URL without blocking
- If all URLs fail, the workflow is not interrupted -- the research results from step 2 are sufficient to generate the document
- ContentAnalysis is an enhancement layer, not a required layer

Collect all successfully extracted content summaries.

### 4. Compose org-mode Document

Combine step 2 (research results) and step 3 (content extraction, if any) into a structured org-mode document.

**Document structure:**

```org
#+title: {City} Travel Research
#+date: {current date}
#+filetags: :travel:museum:architecture:

* City Overview
  {City}'s civilizational coordinates -- why it's worth visiting, what to see there. One paragraph outlining the city's place in Chinese civilization history.

* Historical Strata
** {Period 1} ({time range})
   Key events, remaining traces, corresponding physical objects to see.
** {Period 2}
   ...

* Museum Guide
** {Museum 1 Name}
   Address, opening hours, reservation method (if needed).
*** Crown Jewels
    - {Artifact name}: {why it matters} | What to notice: {specific observation points}
*** Key Exhibition Halls
    - {Hall name}: {key highlights}
*** Easy to Miss
    - {overlooked but worthwhile content}
** {Museum 2 Name}
   ...

* Ancient Architecture
** {Building 1 Name} ({Dynasty}, {Protection Level})
   Form overview.
*** What to Look For
    - {Specific observation point 1}: {why it's worth noting}
    - {Specific observation point 2}
** {Building 2 Name}
   ...

* Archaeological Discoveries
** {Site/Discovery 1}
   Discovery process, significance, current location of unearthed artifacts. If there are interesting excavation stories, share them.

* Suggested Routes
** Route 1: {Theme Name} ({Estimated Time})
   For whom: {description}
   1. {location} -- focus on {what} ({suggested dwell time})
   2. ...
** Route 2: {Theme Name}
   ...

* Deep Content Recommendations
  Content worth watching before departure, discovered across platforms.
** Videos
   - [[{URL}][{Title}]] -- {one-sentence summary}
** Articles
   - [[{URL}][{Title}]] -- {one-sentence summary}
** Books (if any recommendations)
   - {Book title} -- {why it's worth reading}
```

**File naming**: Use the denote naming schema, saved to `~/Documents/notes/` directory:
`{YYYYMMDDTHHMMSS}==z--{city}-travel-research.org`

**Writing requirements**:
- Every recommendation must include "why to see" and "what details to notice" -- no empty generalities
- The tone is notes written for yourself, not a tour guide script
- Write exact information when available; don't fabricate when it's not

### 5. Cast Portable Cards (ljg-card)

Extract core content from the org document in step 4, cast two cards, **executed in parallel**:

**Card A -- City Civilization Overview (infograph):**

Invoke Skill tool to execute `ljg-card -i`, with input: city historical strata + core museum list + must-see ancient architecture list essence summary. One image to understand the city's civilizational skeleton.

**Card B -- Route Quick Reference (long image):**

Invoke Skill tool to execute `ljg-card -l`, with input: route suggestions + key highlights of each location. Convenient for checking on your phone.

### 6. Summary Report

```
════ Travel Research Complete ═══════════════════════
  City: {city name}
  Knowledge document: {org file path}
  Civilization overview card: {PNG file path}
  Route quick reference card: {PNG file path}
  Research coverage: {N} museums | {M} ancient buildings | {K} archaeological sites
  Deep content: {X} videos | {Y} articles
```

## Key Constraints

- Step 2 is the core -- 12 Agents in parallel covering academic research and platform content, completed in one pass
- Step 3 (content extraction) is an enhancement layer, failure doesn't block the workflow
- The two cards in step 5 are parallelized
- The org document is the primary output, cards are derivative -- document quality takes priority
- Don't produce generic travel guides -- every recommendation must have "why to see" and "what details to notice"
- Research uses bilingual Chinese-English keywords to expand coverage
- Leave blanks rather than fabricate when there's no exact information

## Known Pitfalls

(First creation, no records yet. Accumulate through use.)
