# 🌱 Git Commands: Basic to Advanced

A comprehensive reference guide covering almost everything you need in Git.

---

## Table of Contents

1. [Command Quick Reference Table](#1-command-quick-reference-table)
2. [Installing & Configuring Git](#2-installing--configuring-git)
3. [Starting a Repository](#3-starting-a-repository)
4. [Staging & Committing](#4-staging--committing)
5. [Branching](#5-branching)
6. [Merging & Rebasing](#6-merging--rebasing)
7. [Remotes](#7-remotes)
8. [Inspecting History](#8-inspecting-history)
9. [Undoing Changes](#9-undoing-changes)
10. [Stashing](#10-stashing)
11. [Tags](#11-tags)
12. [Diffing](#12-diffing)
13. [Submodules](#13-submodules)
14. [Rewriting History](#14-rewriting-history)
15. [Hooks](#15-hooks)
16. [Worktrees](#16-worktrees)
17. [Bisect & Blame](#17-bisect--blame)
18. [.gitignore & Attributes](#18-gitignore--attributes)
19. [Advanced & Plumbing Commands](#19-advanced--plumbing-commands)
20. [Troubleshooting & Recovery](#20-troubleshooting--recovery)
21. [Appendix: Core Concepts Explained](#21-appendix-core-concepts-explained)
22. [Workflow Roadmaps & Common Scenarios](#22-workflow-roadmaps--common-scenarios)

---

## 1. Command Quick Reference Table

### 📁 Repository Commands

| Command                      | Use                                       |
| ----------------------------- | ------------------------------------------ |
| `git init`                    | Initialize a new repository                |
| `git clone <url>`             | Clone a remote repository                  |
| `git status`                  | Show working tree status                   |
| `git config`                  | Get/set configuration options              |
| `git remote -v`               | List remotes                               |
| `git log`                     | Show commit history                        |

### ➕ Staging & Committing

| Command                       | Use                                        |
| ------------------------------ | -------------------------------------------- |
| `git add <file>`               | Stage a file                                 |
| `git add .`                    | Stage all changes                            |
| `git add -p`                   | Interactively stage hunks                    |
| `git commit -m "msg"`          | Commit staged changes                        |
| `git commit -am "msg"`         | Stage tracked files & commit                 |
| `git commit --amend`           | Modify the last commit                       |
| `git rm <file>`                | Remove file from working tree & index        |
| `git mv <old> <new>`           | Move/rename a tracked file                   |
| `git restore <file>`           | Discard working-tree changes                 |
| `git restore --staged <file>`  | Unstage a file                               |

### 🌿 Branch Commands

| Command                              | Use                                    |
| -------------------------------------- | ----------------------------------------- |
| `git branch`                          | List local branches                     |
| `git branch <name>`                   | Create a new branch                     |
| `git branch -d <name>`                | Delete a branch (safe)                  |
| `git branch -D <name>`                | Force-delete a branch                   |
| `git checkout <branch>`               | Switch to a branch                      |
| `git switch <branch>`                 | Switch to a branch (modern)             |
| `git switch -c <branch>`              | Create & switch to a new branch         |
| `git checkout -b <branch>`            | Create & switch to a new branch (legacy)|
| `git branch -m <old> <new>`           | Rename a branch                         |
| `git branch -r`                       | List remote-tracking branches           |
| `git branch -a`                       | List all branches (local + remote)      |

### 🔀 Merge & Rebase Commands

| Command                          | Use                                     |
| ----------------------------------- | ------------------------------------------ |
| `git merge <branch>`               | Merge a branch into current branch        |
| `git merge --no-ff <branch>`       | Merge with a merge commit always created  |
| `git merge --abort`                | Abort a conflicted merge                  |
| `git rebase <branch>`              | Reapply commits on top of another branch  |
| `git rebase -i <ref>`              | Interactive rebase                        |
| `git rebase --continue`            | Continue after resolving conflicts        |
| `git rebase --abort`               | Abort a rebase                            |
| `git cherry-pick <commit>`         | Apply a specific commit onto current branch |

### 🌐 Remote Commands

| Command                             | Use                                     |
| -------------------------------------- | ------------------------------------------ |
| `git remote add <name> <url>`         | Add a new remote                          |
| `git remote remove <name>`            | Remove a remote                           |
| `git remote rename <old> <new>`       | Rename a remote                           |
| `git fetch`                           | Download objects/refs without merging     |
| `git pull`                            | Fetch + merge (or rebase) from remote     |
| `git pull --rebase`                   | Fetch + rebase local commits              |
| `git push`                            | Push commits to remote                    |
| `git push -u origin <branch>`         | Push & set upstream tracking              |
| `git push --force-with-lease`         | Safer force push                          |
| `git push --tags`                     | Push all tags                             |

### 🕵️ Inspection Commands

| Command                              | Use                                     |
| --------------------------------------- | ------------------------------------------ |
| `git log --oneline`                    | Compact commit history                    |
| `git log --graph --all --decorate`     | Visual branch graph                       |
| `git show <commit>`                    | Show details of a commit                  |
| `git diff`                             | Show unstaged changes                     |
| `git diff --staged`                    | Show staged changes                       |
| `git blame <file>`                     | Show who changed each line                |
| `git reflog`                           | Show history of HEAD movements            |
| `git bisect start`                     | Start binary search for a bad commit      |

### 🧹 Undo & Reset Commands

| Command                          | Use                                        |
| ------------------------------------ | --------------------------------------------- |
| `git reset --soft <commit>`         | Move HEAD, keep changes staged                |
| `git reset --mixed <commit>`        | Move HEAD, unstage changes (default)          |
| `git reset --hard <commit>`         | Move HEAD, discard all changes                |
| `git revert <commit>`               | Create new commit that undoes a commit        |
| `git clean -fd`                     | Remove untracked files & directories          |
| `git stash`                         | Save uncommitted changes for later            |
| `git stash pop`                     | Reapply and remove latest stash               |
| `git stash list`                    | List all stashes                              |

---

## 2. Installing & Configuring Git

```
# Ubuntu / Debian
sudo apt-get update
sudo apt-get install git

# CentOS / RHEL
sudo yum install git

# macOS (Homebrew)
brew install git

# Windows — Download from https://git-scm.com/download/win

# Verify installation
git --version

# ── Identity ──────────────────────────────────
git config --global user.name "Your Name"
git config --global user.email "you@example.com"

# ── Editor & default branch ───────────────────
git config --global core.editor "vim"
git config --global init.defaultBranch main

# ── Aliases ────────────────────────────────────
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
git config --global alias.lg "log --oneline --graph --all --decorate"

# ── Line endings ───────────────────────────────
git config --global core.autocrlf input   # macOS/Linux
git config --global core.autocrlf true    # Windows

# ── Credential storage ─────────────────────────
git config --global credential.helper cache
git config --global credential.helper store
git config --global credential.helper "cache --timeout=3600"

# ── Colors ──────────────────────────────────────
git config --global color.ui auto

# ── View config ────────────────────────────────
git config --list
git config --list --show-origin
git config user.name                # Single value
git config --global --edit          # Open config in editor

# ── Config scopes (in precedence order) ────────
# --local   (repo only, .git/config)
# --global  (user-wide, ~/.gitconfig)
# --system  (machine-wide)
```

---

## 3. Starting a Repository

```
# Initialize a new repo
git init
git init my-project
git init --bare                      # Bare repo (no working tree, for servers)

# Clone a repo
git clone https://github.com/user/repo.git
git clone git@github.com:user/repo.git       # SSH
git clone --depth 1 <url>                    # Shallow clone (latest commit only)
git clone --branch <branch> <url>            # Clone specific branch
git clone --recurse-submodules <url>         # Clone with submodules
git clone <url> my-folder-name               # Clone into custom folder name

# Check repo status
git status
git status -s                        # Short format
git status -sb                       # Short format + branch info

# Show repo info
git rev-parse --show-toplevel        # Path to repo root
git rev-parse --is-inside-work-tree  # Check if inside a git repo
```

---

## 4. Staging & Committing

```
# Stage changes
git add file.txt
git add file1.txt file2.txt
git add .                            # Stage everything in current dir
git add -A                           # Stage everything (incl. deletions)
git add -u                           # Stage modified/deleted tracked files only
git add -p                           # Interactively stage hunks
git add -N file.txt                  # Track an untracked file without staging content

# Commit
git commit -m "Add login feature"
git commit -m "Title" -m "Longer description body"
git commit -am "msg"                 # Stage tracked changes + commit
git commit --amend                   # Edit last commit (message and/or content)
git commit --amend --no-edit         # Add staged changes to last commit, keep message
git commit --amend -m "New message"  # Change last commit's message
git commit --allow-empty -m "msg"    # Create commit with no changes

# Signed commits
git commit -S -m "Signed commit"
git config --global commit.gpgsign true

# View staged vs unstaged changes
git diff                             # Unstaged changes
git diff --staged                    # Staged changes (also --cached)
git diff HEAD                        # All changes vs last commit

# Remove / rename files
git rm file.txt                      # Remove from disk + index
git rm --cached file.txt             # Remove from index only (keep on disk)
git rm -r folder/                    # Remove directory
git mv old.txt new.txt               # Rename/move a tracked file

# Unstage / discard changes
git restore --staged file.txt        # Unstage (keep working changes)
git restore file.txt                 # Discard working-tree changes
git restore --source=HEAD~1 file.txt # Restore file from a previous commit
git checkout -- file.txt             # Legacy equivalent of restore
```

---

## 5. Branching

```
# List branches
git branch                           # Local branches
git branch -r                        # Remote-tracking branches
git branch -a                        # All branches
git branch -v                        # With last commit info
git branch --merged                  # Branches merged into current
git branch --no-merged                # Branches not yet merged

# Create branches
git branch feature/login
git switch -c feature/login          # Create + switch (modern)
git checkout -b feature/login        # Create + switch (legacy)
git switch -c feature/login origin/main   # Branch from a specific ref

# Switch branches
git switch main
git checkout main
git switch -                         # Switch to previous branch

# Rename / delete
git branch -m old-name new-name      # Rename branch
git branch -m new-name               # Rename current branch
git branch -d feature/login          # Delete (safe, must be merged)
git branch -D feature/login          # Force delete
git push origin --delete feature/login   # Delete remote branch

# Track a remote branch
git branch -u origin/main            # Set upstream for current branch
git branch --set-upstream-to=origin/main main
git switch --track origin/feature-x  # Create local branch tracking remote

# Compare branches
git log main..feature/login          # Commits in feature not in main
git diff main..feature/login         # Diff between branches
git branch --contains <commit>       # Branches containing a commit
```

---

## 6. Merging & Rebasing

### Merging

```
# Merge a branch into current branch
git switch main
git merge feature/login

# Fast-forward vs merge commit
git merge feature/login              # Fast-forwards if possible
git merge --no-ff feature/login      # Always create a merge commit
git merge --ff-only feature/login    # Fail unless fast-forward is possible

# Squash merge (single commit, no merge history)
git merge --squash feature/login
git commit -m "Add login feature"

# Handling conflicts
git merge feature/login
# ... resolve conflicts in files ...
git add resolved-file.txt
git commit                           # Completes the merge
git merge --abort                    # Bail out and restore pre-merge state

# Merge strategies
git merge -X ours feature/login      # Prefer our side on conflicts
git merge -X theirs feature/login    # Prefer their side on conflicts
```

### Rebasing

```
# Rebase current branch onto another
git switch feature/login
git rebase main

# Continue / abort / skip during conflicts
git rebase --continue
git rebase --abort
git rebase --skip

# Interactive rebase (edit, squash, reorder, drop commits)
git rebase -i HEAD~5
git rebase -i main

# Interactive rebase actions (edit in the opened file):
# pick   = keep commit as-is
# reword = keep commit, edit message
# edit   = keep commit, pause to amend
# squash = combine with previous commit, merge messages
# fixup  = combine with previous commit, discard message
# drop   = remove commit entirely

# Rebase and preserve merge commits
git rebase -i --rebase-merges main

# Autosquash (pairs with commit --fixup / --squash)
git commit --fixup <commit>
git rebase -i --autosquash main~5

# Onto (move a range of commits to a new base)
git rebase --onto main feature-old feature-new

# Cherry-pick a specific commit
git cherry-pick <commit-hash>
git cherry-pick <commit1> <commit2>
git cherry-pick --no-commit <commit>  # Apply without committing
git cherry-pick --continue            # After resolving conflicts
git cherry-pick --abort
```

---

## 7. Remotes

```
# List / inspect remotes
git remote -v
git remote show origin

# Add / remove / rename
git remote add origin https://github.com/user/repo.git
git remote add upstream https://github.com/original/repo.git
git remote remove origin
git remote rename origin upstream
git remote set-url origin git@github.com:user/repo.git

# Fetch (download, don't merge)
git fetch
git fetch origin
git fetch --all
git fetch --prune                    # Remove stale remote-tracking refs
git fetch origin main:main           # Fetch into a local branch directly

# Pull (fetch + integrate)
git pull
git pull origin main
git pull --rebase                    # Rebase instead of merge
git pull --ff-only                   # Fail unless fast-forward
git pull --no-commit                 # Fetch + merge, but don't commit

# Push
git push
git push origin main
git push -u origin feature/login     # Push + set upstream
git push --all                       # Push all branches
git push --tags                      # Push all tags
git push origin --delete feature/login   # Delete remote branch
git push --force                     # Force push (dangerous)
git push --force-with-lease          # Safer force push (checks remote state)

# Syncing a fork
git remote add upstream https://github.com/original/repo.git
git fetch upstream
git switch main
git merge upstream/main
git push origin main
```

---

## 8. Inspecting History

```
# Basic log
git log
git log --oneline
git log -n 5                         # Last 5 commits
git log --author="Jane"
git log --since="2 weeks ago"
git log --until="2024-01-01"
git log --grep="fix"                 # Search commit messages

# Visual graph
git log --graph --oneline --all --decorate
git log --graph --pretty=format:"%h %ad | %s%d [%an]" --date=short

# File history
git log -- file.txt                  # Commits touching a file
git log -p -- file.txt                # With diffs
git log --follow -- file.txt         # Follow renames

# Show a specific commit
git show <commit>
git show HEAD
git show HEAD~2
git show <commit>:path/to/file.txt   # File content at a commit

# Search history content
git log -S "functionName"            # Commits that added/removed a string (pickaxe)
git log -G "regex.*pattern"          # Commits matching a regex diff

# Reflog (local history of HEAD/branch movements)
git reflog
git reflog show main
git reset --hard HEAD@{2}            # Restore to a reflog entry

# Shortlog (summary by author)
git shortlog -sn                     # Commit counts per author

# Diff stats
git log --stat
git log --shortstat
```

---

## 9. Undoing Changes

```
# Discard working-tree changes
git restore file.txt
git checkout -- file.txt             # Legacy
git checkout -- .                    # Discard all working-tree changes

# Unstage files
git restore --staged file.txt
git reset file.txt                   # Legacy

# Undo commits (moves HEAD/branch pointer)
git reset --soft HEAD~1              # Undo commit, keep changes staged
git reset --mixed HEAD~1             # Undo commit, keep changes unstaged (default)
git reset --hard HEAD~1              # Undo commit, discard changes entirely
git reset --hard <commit>            # Reset branch to specific commit
git reset --hard origin/main         # Reset local branch to match remote

# Revert (safe undo — creates a new commit, doesn't rewrite history)
git revert <commit>
git revert HEAD
git revert --no-commit <commit>      # Stage revert without committing
git revert <oldest>..<newest>        # Revert a range of commits

# Amend last commit
git commit --amend -m "Corrected message"
git commit --amend --no-edit         # Add staged changes, keep message

# Remove untracked files
git clean -n                         # Dry run — show what would be removed
git clean -f                         # Remove untracked files
git clean -fd                        # Also remove untracked directories
git clean -fx                        # Also remove ignored files
git clean -fdx                       # Remove everything untracked/ignored

# Recover a deleted branch
git reflog                           # Find the commit SHA
git branch recovered-branch <sha>

# Recover a deleted file
git checkout <commit-before-deletion> -- path/to/file.txt
```

---

## 10. Stashing

```
# Save changes for later
git stash
git stash push -m "WIP: login form"
git stash push -- file.txt           # Stash a specific file
git stash --include-untracked        # Also stash untracked files
git stash --all                      # Also stash ignored files

# List stashes
git stash list

# Apply stashes
git stash apply                      # Apply latest, keep it in stash list
git stash apply stash@{2}            # Apply a specific stash
git stash pop                        # Apply latest and remove it from list
git stash pop stash@{1}

# Inspect stashes
git stash show                       # Summary of latest stash
git stash show -p                    # Full diff of latest stash
git stash show -p stash@{1}

# Remove stashes
git stash drop                       # Drop latest stash
git stash drop stash@{2}
git stash clear                      # Remove all stashes

# Create a branch from a stash
git stash branch new-branch-name stash@{0}
```

---

## 11. Tags

```
# List tags
git tag
git tag -l "v1.*"                    # Filter by pattern

# Create tags
git tag v1.0.0                       # Lightweight tag
git tag -a v1.0.0 -m "Release 1.0.0" # Annotated tag (recommended)
git tag -a v1.0.0 <commit> -m "msg"  # Tag a specific past commit

# Inspect a tag
git show v1.0.0

# Push tags
git push origin v1.0.0               # Push a single tag
git push --tags                      # Push all tags
git push origin --follow-tags        # Push commits + annotated tags

# Delete tags
git tag -d v1.0.0                    # Delete locally
git push origin --delete v1.0.0      # Delete on remote

# Checkout a tag (detached HEAD)
git checkout v1.0.0
git switch --detach v1.0.0

# Create a branch from a tag
git switch -c hotfix/1.0.1 v1.0.0
```

---

## 12. Diffing

```
# Working tree vs index
git diff

# Index vs last commit
git diff --staged
git diff --cached                    # Same as --staged

# Working tree vs last commit
git diff HEAD

# Between two commits
git diff <commit1> <commit2>

# Between two branches
git diff main..feature/login
git diff main...feature/login        # Diff from common ancestor (triple-dot)

# Specific file(s)
git diff -- file.txt
git diff main feature/login -- file.txt

# Summary stats only
git diff --stat
git diff --name-only                 # Just filenames
git diff --name-status               # Filenames + change type (A/M/D)

# Word-level diff (useful for prose)
git diff --word-diff

# Ignore whitespace
git diff -w
git diff --ignore-all-space

# Diff against a stash
git diff stash@{0}
```

---

## 13. Submodules

```
# Add a submodule
git submodule add https://github.com/user/lib.git libs/lib

# Clone a repo with submodules
git clone --recurse-submodules <url>
git submodule update --init --recursive   # After a normal clone

# Update submodules
git submodule update --remote             # Pull latest from submodule's remote
git submodule update --remote --merge
git submodule foreach git pull origin main

# Status
git submodule status

# Remove a submodule
git submodule deinit -f libs/lib
git rm -f libs/lib
rm -rf .git/modules/libs/lib

# Sync submodule URL changes
git submodule sync
```

---

## 14. Rewriting History

```
# Amend the most recent commit
git commit --amend

# Interactive rebase to edit older commits
git rebase -i HEAD~5

# Split a commit
git rebase -i HEAD~3
# mark commit as "edit", then:
git reset HEAD^
git add -p                           # Stage part of the changes
git commit -m "First part"
git add .
git commit -m "Second part"
git rebase --continue

# Rewrite author info across history (use with caution)
git filter-branch --env-filter '
  export GIT_AUTHOR_NAME="New Name"
  export GIT_AUTHOR_EMAIL="new@example.com"
' --tag-name-filter cat -- --branches --tags

# Modern replacement for filter-branch (faster, safer)
# https://github.com/newren/git-filter-repo
git filter-repo --path secrets.txt --invert-paths   # Remove a file from all history
git filter-repo --replace-text expressions.txt      # Redact strings from history

# Squash entire branch history into one commit
git reset $(git commit-tree HEAD^{tree} -m "Squashed history")

# Force-push rewritten history (coordinate with your team!)
git push --force-with-lease origin feature/login
```

---

## 15. Hooks

```
# Hooks live in .git/hooks/ (executable scripts, no extension)
ls .git/hooks/

# Common hooks
.git/hooks/pre-commit          # Runs before a commit is created (lint, tests)
.git/hooks/commit-msg          # Validate/modify commit message
.git/hooks/pre-push            # Runs before push (e.g., run test suite)
.git/hooks/post-checkout       # Runs after checkout/switch
.git/hooks/post-merge          # Runs after a merge completes

# Example pre-commit hook
cat > .git/hooks/pre-commit << 'HOOK'
#!/bin/sh
npm run lint
HOOK
chmod +x .git/hooks/pre-commit

# Skip hooks for one commit/push
git commit --no-verify -m "msg"
git push --no-verify

# Shared hooks across a team — set a custom hooks directory
git config core.hooksPath .githooks
```

---

## 16. Worktrees

```
# Add a worktree (separate working directory for another branch)
git worktree add ../hotfix hotfix-branch
git worktree add -b new-branch ../new-branch-dir main

# List worktrees
git worktree list

# Remove a worktree
git worktree remove ../hotfix
rm -rf ../hotfix && git worktree prune   # Manual cleanup if needed

# Lock a worktree (prevent pruning, e.g. on removable media)
git worktree lock ../hotfix
git worktree unlock ../hotfix
```

---

## 17. Bisect & Blame

```
# Bisect — binary search for the commit that introduced a bug
git bisect start
git bisect bad                       # Current commit is bad
git bisect good v1.0.0               # Known good commit
# Git checks out a midpoint commit — test it, then:
git bisect good                      # or
git bisect bad
# ... repeat until Git identifies the offending commit ...
git bisect reset                     # Return to original HEAD

# Automated bisect with a test script
git bisect start HEAD v1.0.0
git bisect run npm test

# Blame — see who last changed each line
git blame file.txt
git blame -L 10,20 file.txt          # Only lines 10-20
git blame -w file.txt                # Ignore whitespace changes
git blame -C file.txt                # Detect moved/copied lines
```

---

## 18. .gitignore & Attributes

```
# .gitignore syntax
node_modules/
*.log
.env
.env.*
dist/
build/
.DS_Store
*.pyc
__pycache__/
!important.log                       # Negate — don't ignore this file

# Check why a file is ignored
git check-ignore -v file.txt

# Ignore a file already tracked (stop tracking, keep locally)
git rm --cached file.txt
echo "file.txt" >> .gitignore

# Global gitignore (applies to all repos)
git config --global core.excludesfile ~/.gitignore_global

# Per-repo, untracked ignore (not shared, not committed)
# .git/info/exclude

# .gitattributes examples
* text=auto
*.sh text eol=lf
*.png binary
*.jpg -diff
CHANGELOG.md merge=union
*.min.js linguist-generated=true
```

---

## 19. Advanced & Plumbing Commands

```
# Show object type/content
git cat-file -t <hash>               # Show type (blob/tree/commit/tag)
git cat-file -p <hash>               # Pretty-print content

# List refs
git show-ref
git for-each-ref

# Find dangling/unreachable commits (e.g., after a hard reset)
git fsck --unreachable
git fsck --lost-found

# Garbage collection & repo maintenance
git gc
git gc --aggressive
git prune                            # Remove unreachable objects
git repack -a -d                     # Repack objects

# Repo size / object counts
git count-objects -v

# Archive a repo/branch as a zip or tar
git archive --format=zip HEAD -o repo.zip
git archive --format=tar main | gzip > main.tar.gz

# Bundle a repo (for offline transfer)
git bundle create repo.bundle --all
git clone repo.bundle my-clone

# Find common ancestor of two branches
git merge-base main feature/login

# Show which commit a tag/ref points to
git rev-parse main
git rev-parse HEAD~3

# Sparse checkout (only check out part of a large repo)
git sparse-checkout init --cone
git sparse-checkout set folder1 folder2

# Partial clone (defer downloading blobs)
git clone --filter=blob:none <url>
git clone --filter=tree:0 <url>
```

---

## 20. Troubleshooting & Recovery

```
# "I committed to the wrong branch"
git reset --soft HEAD~1              # Undo commit, keep changes staged
git switch correct-branch
git commit -m "msg"

# "I need to recover a deleted branch"
git reflog
git branch recovered <sha-from-reflog>

# "I accidentally ran git reset --hard"
git reflog                           # Find the commit before the reset
git reset --hard HEAD@{1}

# "I have merge conflicts and want to start over"
git merge --abort
git rebase --abort

# "My branch has diverged from remote and I want to match it exactly"
git fetch origin
git reset --hard origin/main

# "I want to see what changed in my last pull"
git log ORIG_HEAD..HEAD

# "I committed a large file / secret by mistake"
git rm --cached bigfile.zip
git commit --amend --no-edit
# For history already pushed, use git filter-repo (see section 14)

# "Detached HEAD state — how do I get back?"
git switch main                      # Or whichever branch you want
# To save work done in detached HEAD:
git switch -c new-branch-name        # Before switching away

# "Permission denied (publickey)" over SSH
ssh -T git@github.com                # Test SSH connection
ssh-keygen -t ed25519 -C "you@example.com"
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519

# Check for corruption
git fsck --full

# Verbose remote debugging
GIT_CURL_VERBOSE=1 git push
GIT_TRACE=1 git push
```

---

## 21. Appendix: Core Concepts Explained

This section explains the *why* behind the commands above — the mental model that makes the rest of this cheatsheet click.

### Repository (repo)

A repository is a project folder that Git is tracking. It contains your files plus a hidden `.git/` directory holding the entire history, configuration, and metadata. A **local repository** lives on your machine; a **remote repository** (e.g. on GitHub) is a copy hosted elsewhere that you sync with via `push`/`pull`/`fetch`. A repo can be "bare" (no working files, just history — used on servers) or "non-bare" (has a working directory you edit).

### The Three (or Four) Areas

Git tracks your files across distinct areas, and almost every command moves content between them:

- **Working directory** — the actual files on disk that you edit.
- **Staging area (a.k.a. "index")** — a holding zone for changes you've marked to include in the *next* commit. `git add` moves changes here.
- **Repository (commit history)** — the permanent, saved snapshots. `git commit` moves staged changes here.
- **Remote** — a separate copy of the repository (e.g. on GitHub) that you sync with via `push`/`fetch`/`pull`.

```
working directory  --add-->  staging area  --commit-->  local repo  --push-->  remote
                                                              <--pull/fetch--
```

### Staging

Staging is the act of choosing *which* changes will go into your next commit, separately from actually making that commit. This two-step process (stage, then commit) lets you group related changes together even if you edited several unrelated things at once — e.g. `git add -p` lets you stage only specific hunks of a file, leaving the rest for a later commit.

### Committing

A commit is a permanent, named snapshot of your staged changes, plus metadata (author, timestamp, message, and a pointer to the previous commit). Commits form a chain — each one "remembers" its parent — which is what makes Git's history a traversable graph rather than just a list of file versions. A good commit is small, focused, and has a message explaining *why*, not just *what*.

### Branching

A branch is simply a movable, lightweight pointer to a specific commit. When you create a branch, Git doesn't copy any files — it just adds a new pointer. As you commit on that branch, the pointer moves forward automatically. This is why Git branches are cheap to create and switch between, unlike in some older version control systems. `main` (or `master`) is just a branch like any other, by convention treated as the primary line of development.

### HEAD

`HEAD` is a pointer to whatever commit you currently have checked out — usually indirectly, via a pointer to the current branch (which itself points to a commit). When you switch branches, `HEAD` moves to point at the new branch. A **"detached HEAD"** state means `HEAD` points directly at a commit instead of a branch (e.g. after `git checkout <tag>`) — commits made here aren't attached to any branch and can be lost unless you create a branch to hold them.

### Merging vs. Rebasing

Both integrate changes from one branch into another, but they do it differently:

- **Merging** creates a new "merge commit" that ties two histories together, preserving exactly what happened and when. History becomes non-linear (it branches and re-joins), but nothing is rewritten — safe for shared/public branches.
- **Rebasing** takes your branch's commits and replays them one-by-one on top of another branch's latest commit, producing a clean, linear history as if you'd started from there all along. This rewrites commit hashes, so it should generally be avoided on branches other people have already pulled.

Rule of thumb: rebase your own local, not-yet-shared work to keep history tidy; merge when integrating into a shared branch.

### Fast-Forward

A "fast-forward" merge happens when the branch you're merging into hasn't diverged at all — its pointer can simply be moved forward to match the other branch, with no new merge commit needed. If both branches have new commits since they diverged, a fast-forward isn't possible and Git creates a real merge commit (or you rebase first).

### Remote & Remote-Tracking Branches

A **remote** is a named reference to another copy of the repository (commonly `origin`). A **remote-tracking branch** (e.g. `origin/main`) is your local repo's read-only snapshot of what a branch looked like on the remote the last time you talked to it — it only updates when you `fetch` or `pull`. Your actual local branch (`main`) is separate and is what you commit to; pushing sends your local branch's commits to update the remote.

### Fetch vs. Pull

`git fetch` downloads new commits/branches from a remote but does **not** touch your working files or local branches — it just updates your remote-tracking branches, so you can inspect changes safely before integrating them. `git pull` is effectively `fetch` followed immediately by a `merge` (or `rebase`, with `--rebase`) into your current branch.

### Conflicts

A merge/rebase conflict happens when Git can't automatically reconcile changes because the same lines were edited differently on both sides. Git pauses and marks the conflicting sections in the file (`<<<<<<<`, `=======`, `>>>>>>>`) for you to resolve by hand, then you `add` the resolved file and `continue`/`commit` to finish.

### Stashing

The stash is a temporary, local-only shelf for uncommitted changes. It lets you save your in-progress work and revert to a clean working directory — useful when you need to switch branches or pull updates without committing half-finished work. Stashes aren't shared with remotes and aren't part of your commit history until you explicitly reapply them.

### Tags

A tag is a fixed pointer to one specific commit — unlike a branch, it never moves forward. Tags are typically used to mark release points (`v1.0.0`). **Annotated tags** store extra metadata (author, date, message) and are recommended for releases; **lightweight tags** are just a name pointing at a commit, with nothing else attached.

### Reflog

The reflog is a local, personal safety net that records every point `HEAD` has been (commits, resets, checkouts, rebases) — even ones no branch points to anymore. It's what makes "undoing an undo" possible: if you `reset --hard` and regret it, the old commit is usually still recoverable via `git reflog`. The reflog is local-only and expires over time; it isn't shared with remotes.

### Working Tree vs. Index vs. Commit (for diffing)

When comparing versions, it helps to know exactly what's being compared: `git diff` compares working directory to the staging area; `git diff --staged` compares the staging area to the last commit; `git diff HEAD` compares the working directory directly to the last commit, skipping the staging area entirely.

### Upstream

"Upstream" has two related meanings in Git: (1) the remote branch that your local branch is configured to track and compare against (set via `-u`/`--set-upstream-to`), which is what makes plain `git pull`/`git push` (no arguments) know where to sync; and (2) in a fork workflow, the original repository you forked from, as opposed to `origin` (your own fork).

### Cherry-Picking

Cherry-picking takes a single specific commit from anywhere in the repo's history and re-applies just that one change onto your current branch, without touching anything else from where it came from. Useful for pulling one bug fix into a release branch without merging an entire feature branch.

### Ancestors, `~` and `^`

`HEAD~1` (or `HEAD^`) means "the commit before HEAD"; `HEAD~3` means "three commits before HEAD" (walking first-parent history). `^` is used to select a specific parent of a merge commit (`HEAD^2` = second parent), while `~` walks a straight line of first-parents. These notations let you reference relative history without typing out full commit hashes.

---

## 22. Workflow Roadmaps & Common Scenarios

This section is the "which situation am I in, and what do I actually do" guide. One golden rule underlies almost everything below:

> **Golden Rule:** Before you start new work, always sync with the remote first (`git pull` / `git fetch`). Before you walk away from work, always push it (or at least commit it). Treat the remote as the source of truth that every machine/session should reconcile with, both coming and going.

---

### Scenario 1 — Starting a brand-new project

There are two valid orders. Pick based on whether you want GitHub or your local machine to be the "birthplace" of the repo.

**Option A — Create the remote first, then clone (recommended for most people)**

This avoids ever having to manually connect a local repo to a remote — GitHub does it for you.

```
Create repo on GitHub  ->  Clone it locally  ->  Track files  ->  Make changes  ->  Commit  ->  Push
```

```
# 1. On GitHub: click "New repository", optionally add a README/.gitignore/license
# 2. Clone it locally
git clone git@github.com:you/project.git
cd project

# 3. Add/edit files, then track & commit as normal
git add .
git commit -m "Initial commit"
git push
```

**Option B — Start locally, connect to GitHub after**

Use this when you're prototyping and aren't sure yet whether/where you'll host it.

```
Init locally  ->  Track files  ->  Make changes  ->  Commit  ->  Create empty remote repo  ->  Link remote  ->  Push
```

```
# 1. Start locally
mkdir project && cd project
git init

# 2. Track & commit your first changes
git add .
git commit -m "Initial commit"

# 3. On GitHub: create a NEW, EMPTY repository (no README/.gitignore — avoid conflicting history)
# 4. Link it and push
git remote add origin git@github.com:you/project.git
git branch -M main
git push -u origin main
```

**Which should you pick?** Option A is simpler and avoids the "unrelated histories" conflict you get in Option B if you initialize the GitHub repo with a README. Use Option B only if you already have local work before you decided to put it on GitHub.

---

### Scenario 2 — Pulling an existing project from GitHub to work on it

This is just cloning — no `init` needed, since the repo (and its history) already exists remotely.

```
Clone  ->  Track files (if adding new ones)  ->  Make changes  ->  Commit  ->  Push
```

```
git clone git@github.com:someone/project.git
cd project

# (Optional) work on a feature branch instead of committing straight to main — see Scenario 5
git switch -c feature/my-change

# Make your changes, then:
git add .
git commit -m "Describe what changed"
git push -u origin feature/my-change   # first push of a new branch needs -u
```

---

### Scenario 3 — Coming back to an existing local project (same machine, later day)

You do **not** restart or re-clone. You **pull**, to catch anything that changed remotely (from you on another machine, a teammate, or a merged PR) since you last touched it — then continue.

```
Pull  ->  [Branch, if starting new work]  ->  Track files  ->  Make changes  ->  Commit  ->  Push
```

```
cd project
git status                   # sanity check: any leftover uncommitted work?
git switch main              # make sure you're on the branch you think you're on
git pull                     # sync with remote before doing anything new

# Starting something new? branch off:
git switch -c feature/new-thing

# Do your work, then:
git add .
git commit -m "msg"
git push -u origin feature/new-thing
```

If `git status` shows uncommitted changes from last time, decide: finish and commit them, or `git stash` them if they're not ready, before pulling.

---

### Scenario 4 — Switching between machines (e.g. laptop and desktop)

**Yes — always push before you leave a machine, and always pull as soon as you sit down at a different one.** The remote is what keeps the two machines in sync; if you forget to push, your other machine has no way to see that work.

```
Machine A: ... make changes ... -> Commit -> Push
                                                |
                                                v
Machine B: Pull -> ... continue work ... -> Commit -> Push
```

```
# On Machine A, before switching:
git add .
git commit -m "WIP: partial feature"   # commit even if unfinished — see note below
git push

# On Machine B, before starting:
git pull
# continue where you left off
```

**If work isn't ready to commit yet:** don't force a commit message like "WIP" into shared history if you'd rather not — instead use `git stash`, but note stashes are **local only** and won't transfer between machines. For cross-machine handoff of incomplete work, a real (even messy) commit that you clean up later with `git rebase -i` is usually more reliable than a stash.

---

### Scenario 5 — Day-to-day feature work with branching (the most common real workflow)

This is the full version of the second diagram you sketched, spelled out:

```
Pull main  ->  Branch  ->  Track files  ->  Make changes  ->  Commit (repeat)  ->  Push branch  ->  Open PR  ->  Merge  ->  Pull main again
```

```
# 1. Make sure your main is current
git switch main
git pull

# 2. Create a branch for the piece of work
git switch -c feature/checkout-flow

# 3. Work in a loop: edit files, stage, commit — as many times as needed
git add .
git commit -m "Add checkout form"
git add .
git commit -m "Wire up validation"

# 4. Push the branch (first time needs -u to set upstream)
git push -u origin feature/checkout-flow

# 5. Open a Pull Request on GitHub, get it reviewed, merge it there (or locally — see below)

# 6. After merge, clean up locally
git switch main
git pull                          # brings down the merged changes
git branch -d feature/checkout-flow
```

**Merging locally instead of via PR:**

```
git switch main
git pull
git merge feature/checkout-flow
git push
git branch -d feature/checkout-flow
```

---

### Scenario 6 — Quick answers to your specific confusions

| Question | Answer |
| --- | --- |
| New project — remote first or local first? | Either works; **remote-first + clone** is simpler and avoids history conflicts. Use local-first only if work already exists before you decide to host it. |
| Existing project, days later — pull or start fresh? | Always **pull**. Never re-clone/re-init an existing local repo just because time passed — you'd lose local history/config. |
| Switching machines — do I push? | **Yes, always**, before leaving a machine. And always **pull** on arrival at the other machine, before making new changes. |
| Do I need a branch every time? | Not strictly, but it's the safer default for anything beyond a trivial one-line fix — it keeps `main` always deployable and makes your change reviewable/revertible in isolation. |
| I forgot to pull and now `push` is rejected | Someone (possibly you, on another machine) pushed first. Run `git pull` (or `git pull --rebase`) to integrate their changes, resolve any conflicts, then push again. |
| I have uncommitted changes but need to pull | Either commit them first, or `git stash`, then `git pull`, then `git stash pop` to bring them back on top of the updated code. |

---

## Quick Reference Cheatsheet

| Task                     | Command                                     |
| -------------------------- | ---------------------------------------------- |
| Initialize repo            | `git init`                                    |
| Clone repo                 | `git clone <url>`                             |
| Check status                | `git status`                                  |
| Stage all changes          | `git add .`                                   |
| Commit                     | `git commit -m "message"`                     |
| Create & switch branch     | `git switch -c feature/x`                     |
| Switch branch              | `git switch main`                             |
| Merge branch                | `git merge feature/x`                         |
| Rebase onto main            | `git rebase main`                             |
| Fetch remote changes        | `git fetch`                                   |
| Pull (fetch + merge)        | `git pull`                                    |
| Push branch                 | `git push -u origin feature/x`                |
| View history                 | `git log --oneline --graph --all`             |
| Undo last commit (keep changes) | `git reset --soft HEAD~1`                 |
| Discard local changes        | `git restore .`                               |
| Stash changes                | `git stash`                                   |
| Apply latest stash           | `git stash pop`                               |
| Tag a release                 | `git tag -a v1.0.0 -m "Release"`              |
| Cherry-pick a commit           | `git cherry-pick <hash>`                      |
| Show diff                      | `git diff`                                    |
| Clean untracked files           | `git clean -fd`                               |

---

*Command reference targets Git 2.30+. `git switch`/`git restore` are the modern (2.23+) replacements for the overloaded `git checkout`; both forms are shown where relevant.*
