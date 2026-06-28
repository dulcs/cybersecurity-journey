---
tags:
  - devops
  - git
  - workflow
  - cheat-sheet
date: 2026-06-28
status: Completed
---

# 🐙 Git Essentials & Workflow Cheat Sheet

## 🗺️ The 4-Stage Architectural Workflow
Understanding Git means understanding how files move across the four logical areas before hitting the cloud.

1. **Working Directory:** Your local sandbox (untracked or modified files).
2. **Staging Area (Index):** The preparation zone (files marked to be included in the next snapshot).
3. **Local Repository (`.git`):** Your encrypted local history database containing all your historical commits.
4. **Remote Repository (GitHub):** The centralized cloud host accessible by your team or portfolio.

---

## 🕒 The Daily Core Routine (The Big Three)

Execute these three commands sequentially to save and push your daily progress:


### 1. Stage Changes
Prepares all modified and new files for the next snapshot.
```bash
git add .
````

### 2. Commit Progress

Saves a permanent structural snapshot of the staged changes in your local database.

```bash
git commit -m "Feat: implement sql injection lab 06 documentation"
```

### 3. Push to Cloud

Uploads your local snapshots directly to your remote repository on GitHub.

```bash
git push origin main
```

## 🔍 System Inspection & History Tracing

### Check Current Repository Health

Displays untracked files, modified objects, and currently staged items. Run this constantly before committing.

```bash
git status
```

### View Streamlined Commit History

Displays a clean, single-line linear timeline of your past saves and unique commit hashes.

```bash
git log --oneline
```

### Verify Remote Connections

Displays the exact URL endpoints where your repository is fetching from and pushing to.

```bash
git remote -v
```

## 🚨 Troubleshooting & Safety Nets (Fixing Common Mistakes)

> 💡 **Pro-Tip:** In Git, almost everything is reversible if you haven't forced a destructive push to the remote server.

### Scenario A: "I messed up my last commit message!"

If you just ran `git commit` but made a typo or want to rewrite the message before pushing:

```bash
git commit --amend -m "Fix: correct spelling and update payload syntax"
```

### Scenario B: "I ran `git add .` by accident, how do I unstage a file?"

If you included a file or directory you didn't mean to commit yet, you can pull it back to your working directory without losing your code:

```bash
git restore --staged <file_name>
```

### Scenario C: "My local code is a mess and I want to completely discard recent changes!"

If you experimented with some code, broke it, and want to revert your files back to the exact state of your last successful commit:

```bash
git restore .
```

### Scenario D: "I updated files on GitHub via the web UI and now my local machine is out of sync!"

Fetches the latest data changes from GitHub and automatically merges them safely into your local workspace:

```bash
git pull origin main
```