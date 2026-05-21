# Push Workflow

One-click sync ljg-* skills to github repo (master + md dual branches).

## Voice Notification

```bash
curl -s -X POST http://localhost:31337/notify \
  -H "Content-Type: application/json" \
  -d '{"message": "Running Push in ljg-push"}' \
  > /dev/null 2>&1 &
```

Output text: `Running **Push** in **ljg-push**...`

## Step 0: Pre-push README check (hard gate)

Before every push, ask yourself one question:

> Does the README still match the actual skill set?

Three specific things:

1. *Added a new skill?* → README skill list / install command needs a new line
2. *Deleted a skill?* → README corresponding line needs removal
3. *A skill's description changed significantly?* → README summary may need updating

The script auto-greps all `ljg-xxx` names in README and compares against `~/.claude/skills/ljg-*`. If any skill exists locally but not in README, *push is directly aborted*.

Bypass (only when you've confirmed README is reviewed and doesn't need updating):

```bash
/ljg-push --skip-readme-check
```

## Step 1: Commit (master branch)

Diff `~/.claude/skills/ljg-*` against `$SKILLS_REPO`:

```bash
cd $SKILLS_REPO
rsync -av --delete ~/.claude/skills/ljg-*/ skills/
```

Add changes:

```bash
git add skills/ljg-*/
git commit -m "sync ljg skills $(date +%Y-%m-%d)"
```

If nothing to commit, skip push and notify user: "No skill changes detected."

## Step 2: Push (master branch)

```bash
git push origin master
```

If push fails (non-fast-forward), attempt `pull --rebase` once. If that also fails, abort and report the conflict.

## Step 3: Switch to md branch

```bash
git checkout md
git merge master --no-edit
```

If merge conflicts, resolve them conservatively (md branch wins for markdown-specific formatting, master wins for content).

## Step 4: Auto-markdown-ify

Run `Tools/Push.sh` which applies:

- File extension references: `__qa.org` → `__qa.md`, `__paper.org` → `__paper.md`, etc.
- Template references: `template.org` → `template.md`
- Keywords: `org-mode` → `markdown`, `Org-mode` → `Markdown`

## Step 5: Push (md branch)

```bash
git push origin md
```

## Step 6: Switch back to master

```bash
git checkout master
```

## Step 7: Report

List: which skills were synced, new version numbers, remaining manual differences (if any).
