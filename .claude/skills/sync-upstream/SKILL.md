---
name: sync-upstream
description: Sync upstream qwibitai/nanoclaw changes into local repo and push to wangqi/nanoclaw fork. Use when the upstream repo has new updates to pull in. Triggers on "sync upstream", "pull upstream", "merge upstream", "sync from qwibitai", "update fork".
---

# Sync Upstream Updates

Merge the latest changes from the upstream repo (`qwibitai/nanoclaw`, remote: `origin`) into the local repo, then push to the fork (`wangqi/nanoclaw`, remote: `fork`).

## Steps

### 1. Fetch both remotes

```bash
git fetch origin
git fetch fork
```

### 2. Show what's new

Check for new upstream commits and summarize them to the user before proceeding:

```bash
git log --oneline HEAD..origin/main
```

If there are no new commits, tell the user the fork is already up to date and stop.

### 3. Merge upstream into local

```bash
git merge origin/main --no-edit
```

If there are merge conflicts, show the conflicting files and resolve them:
- Prefer upstream changes for core files (`src/`, `skills-engine/`, `container/`)
- Prefer local changes for personal config files (`groups/`, `groups/main/CLAUDE.md`)
- After resolving, stage and complete the merge: `git add . && git merge --continue --no-edit`

### 4. Merge fork into local

```bash
git merge fork/main --no-edit
```

Resolve any conflicts the same way as step 3.

### 5. Push to fork

```bash
git push fork main
```

### 6. Confirm

Show the user the final git log with:

```bash
git log --oneline -10
```

And confirm the push succeeded with the new HEAD commit hash.
