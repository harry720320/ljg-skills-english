---
name: ljg-push
description: Sync all updated skills in ~/.claude/skills/ljg-* to the github repo (ljg-skills), first push the master branch (org-mode output format), then switch to the md branch (markdown output format) for basic markdown conversion and push. Use when user says '/ljg-push', 'push skills', '推送 skills', '同步 skills', 'sync ljg', or whenever ljg-* skills get updated and need shipping. NOT FOR pushing non-ljg skills or arbitrary git repos.
user_invocable: true
---

# ljg-push: Push ljg-* Skills

Sync modified skills from local `~/.claude/skills/ljg-*` to the github repo in one shot, covering both master and md branches.

## Repo Paths (hardcoded)

```
SKILLS_REPO="$HOME/code/ljg-skills"       # local working repo
SKILLS_LOCAL="$HOME/.claude/skills"        # local skill source
REPO_URL="git@github.com:lijigang/ljg-skills.git"
```

If `$SKILLS_REPO` doesn't exist, the script auto-clones. If it exists but isn't the ljg-skills git repo, the script errors out (won't destroy existing directories).

## Differences Between the Two Branches

| Branch | Output Format | File Extension | Bold | File Header |
|--------|--------------|----------------|------|-------------|
| `master` (default) | org-mode | `.org` | `*bold*` | `#+title:` etc. |
| `md` | markdown | `.md` | `**bold**` | YAML frontmatter |

Skills in `~/.claude/skills/` are in *master style* (source version). md branch differences are handled by script auto-conversion + manual touch-ups when needed.

## Workflow

Follow the steps in `Workflows/Push.md` → call `Tools/Push.sh`.

## README Consistency (hard gate)

Before every push, the script forces one check: *cross-check README against local skills*.

- List all skill names from `~/.claude/skills/ljg-*`
- grep `ljg-xxx` entries in `$SKILLS_REPO/README.md`
- Find skills present locally but missing from README — *almost certainly means README is out of date*
- Hit → push aborted, report the discrepancy

Every push is an opportunity to review README. Ask yourself:

1. *Added a new skill?* README skill list / install command needs a new line
2. *Deleted a skill?* README corresponding line needs removal
3. *A skill's description changed significantly?* README summary may need updating

If README has been reviewed and truly doesn't need updates, bypass the gate:

```bash
/ljg-push --skip-readme-check
```

## Auto-Conversion Scope

Strings auto-replaced during md branch sync:

- File extension references: `__qa.org` → `__qa.md`, `__paper.org` → `__paper.md`, etc. (denote naming convention)
- Template references: `template.org` → `template.md`
- Keywords: `org-mode` → `markdown`, `Org-mode` → `Markdown`

Content *not auto-converted* (script hands off, requires manual maintenance):

- `*bold*` → `**bold**`: in markdown files `*bold*` means italic, auto-replacement would corrupt document formatting
- org headers `#+title:` `#+date:` → YAML frontmatter: too complex, left for manual handling
- File body renaming: e.g. `references/template.org` file → `references/template.md`

After encountering these differences, the script lists files *still with differences* after md push, providing a review checklist.

## Voice Notification

```bash
curl -s -X POST http://localhost:31337/notify \
  -H "Content-Type: application/json" \
  -d '{"message": "Running Push in ljg-push"}' \
  > /dev/null 2>&1 &
```

Output text: `Running **Push** in **ljg-push**...`

## Examples

*Example 1: One-click push*

```
User: /ljg-push
→ Detect skills in ~/.claude/skills/ljg-* that differ from repo
→ master: rsync + bump version + commit + push
→ md: rsync + mdize + bump version + commit + push
→ Report: which skills pushed, new version numbers, remaining manual differences
```

*Example 2: Preview what would be pushed without actually pushing*

```
User: /ljg-push --dry-run
→ List skills that would be synced
→ List markdown conversions that would be applied
→ No rsync / commit / push
```

## Gotchas

- *README drift is the easiest to miss* — add a new skill and push directly, README still on the old list. The script now has a hard gate for this; when blocked, don't blindly add `--skip-readme-check`, check README first
- *Script assumes git credentials are configured* (ssh key or PAT) — ljg-push doesn't handle authentication, fails directly on auth errors
- *master must be pushed first* — md branch markdown conversion is based on master's org version. Reversing the order breaks things
- *Untracked clutter (like `assets/measure.js`) gets rsynced to repo* — if you don't want to push it, delete it locally first, or add to `.gitignore`
- *Auto markdown conversion only touches strings* — `*bold*` and org headers are untouched. Complex md branch differences (like ljg-paper's `template.org` → `template.md`) require Jigang's manual maintenance
- *Script auto-bumps patch version in plugin.json + marketplace.json* — if you want to bump minor / major, manually edit first then run the script, the script only appends patch
- *If md branch remote is newer than local (Jigang pushed from another machine)*, the script will attempt `pull --rebase`, and if it fails, try one `reset --hard origin/md` to reapply — this discards local unpushed md branch commits. The script warns before doing this
- *Relocation record*: repo history was once at `~/.claude.backup-20260502/ljg-skills-repo/` (path with "backup" is historical artifact), moved to `~/code/ljg-skills/` on 2026-05-02
