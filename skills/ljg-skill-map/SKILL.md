---
name: ljg-skill-map
description: "Skill map viewer. Scans all installed skills and renders a visual overview -- name, version, description, category at a glance. Use when user says 'skills', '技能', '技能地图', 'skill map', '我有哪些技能', '看看技能', '列出技能', 'list skills'. Also trigger when user asks what skills are available or installed."
user_invocable: true
version: "1.0.0"
---

# ljg-skill-map: Skill Map

Scans all installed skills under `~/.claude/skills/` and generates a visual map at a glance.

## Execution

### 1. Scan

Run `scripts/scan.sh` to get JSON data for all skills (name, version, invocable, desc).

### 2. Categorize

Based on skill name and description, automatically categorize skills as follows:

| Category | Icon | Meaning | Typical Members |
|----------|------|---------|-----------------|
| Cognitive Atoms | ◆ | Atomic operations for content processing | ljg-plain, ljg-word, ljg-writes, ljg-paper |
| Output Casting | ▲ | Transform content into deliverables | ljg-card |
| Network Reach | ● | Interact with the external world | agent-reach |
| System Operations | ■ | Agent self-maintenance and management | datetime-check, memory-review, save-conversation, skill-creator, ljg-skill-map |
| Environment Setup | ★ | One-time installation and configuration | Her-init |

Categorization is based on name prefix and description keywords. New skills that cannot be categorized are placed under "Uncategorized".

### 3. Render

Present in ASCII box-drawing format as follows:

```
╔══════════════════════════════════════════════════════════╗
║              SKILL MAP  ·  {N} skills installed         ║
╠══════════════════════════════════════════════════════════╣
║                                                          ║
║  ◆  Cognitive Atoms                                      ║
║  +-----------------+----------------------------------+  ║
║  | ljg-plain v4.0  | Plain -- great Q&A + analogies   |  ║
║  | ljg-word  v1.0  | Deep English word deconstruction |  ║
║  | ljg-writes v4.0 | Writing engine                   |  ║
║  | ljg-paper v2.0  | Paper reading & analysis         |  ║
║  +-----------------+----------------------------------+  ║
║                                                          ║
║  ▲  Output Casting                                       ║
║  +-----------------+----------------------------------+  ║
║  | ljg-card  v1.5  | Cast -- content to PNG visuals   |  ║
║  +-----------------+----------------------------------+  ║
║                                                          ║
║  ...                                                     ║
╚══════════════════════════════════════════════════════════╝
```

Rules:
- One block per category, category icon + name as title
- Skill name left-aligned, version number immediately following (`-` if no version)
- Description truncated to one line, preserving core meaning
- Skills with `user_invocable: true` get a `/` suffix (indicating it can be invoked directly via `/skill-name`)
- Bottom stats line: total count, invocable count, categorized count

### 4. Output

Render the ASCII map directly in the conversation. No file is generated, nothing written to disk.
