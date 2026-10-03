# Git Interview Questions

> **Level:** Fresher / Junior Developer
> **Focus:** Git fundamentals + practical commands
> **Goal:** Understand version control and confidently use Git in projects.

---

# 1. What is Git?

Git is a **distributed version control system**.

It tracks changes in source code and allows developers to:

* Save versions
* Compare changes
* Create branches
* Collaborate
* Revert changes
* Merge work

---

# 2. Why do we use Git?

Without version control:

```text
project-final
project-final-new
project-final-new-2
project-final-latest
```

Git provides structured version history.

```text
Code
 ↓
Git
 ↓
Commits
 ↓
Version History
```

---

# 3. What is a repository?

A repository is a project managed by Git.

It contains:

```text
Source code
Git history
Branches
Commits
Configuration
```

A repository can exist locally and remotely.

---

# 4. What is a working directory?

The working directory contains the files you are currently editing.

Example:

```text
project/
├── src/
├── package.json
└── README.md
```

Changes made here are not automatically committed.

---

# 5. What is the staging area?

The staging area contains changes selected for the next commit.

Example:

```bash
git add .
```

Flow:

```text
Working Directory
       ↓
   git add
       ↓
Staging Area
```

---

# 6. What is a commit?

A commit is a recorded snapshot of staged changes.

Example:

```bash
git commit -m "Add authentication API"
```

A good commit message explains what changed.

---

# 7. What is the basic Git workflow?

```text
Edit Files
   ↓
git status
   ↓
git add
   ↓
git commit
   ↓
git push
```

When working with a remote repository:

```text
Remote changes
   ↓
git pull
   ↓
Local changes
   ↓
git push
```

---

# 8. What does `git init` do?

It creates a new Git repository in the current directory.

```bash
git init
```

This creates the `.git` directory.

---

# 9. What does `git status` do?

It shows the current state of your working tree.

```bash
git status
```

It can show:

```text
Modified files
Untracked files
Staged files
Current branch
```

This is one of the most useful Git commands.

---

# 10. What does `git add` do?

It moves changes to the staging area.

Specific file:

```bash
git add README.md
```

All changes:

```bash
git add .
```

---

# 11. What does `git commit` do?

It records staged changes in Git history.

```bash
git commit -m "Add REST API notes"
```

A commit should represent a meaningful unit of work.

---

# 12. What does `git log` do?

It displays commit history.

```bash
git log
```

Short version:

```bash
git log --oneline
```

Example:

```text
a1b2c3d Add REST API notes
e4f5g6h Add HTTP notes
```

---

# 13. What is a branch?

A branch is an independent line of development.

Example:

```text
main
  |
  ├── feature/auth
  ├── feature/orders
  └── feature/profile
```

Branches allow developers to work on features separately.

---

# 14. How do you create a branch?

```bash
git branch feature/auth
```

Create and switch:

```bash
git switch -c feature/auth
```

Older equivalent:

```bash
git checkout -b feature/auth
```

---

# 15. How do you switch branches?

Modern command:

```bash
git switch main
```

or:

```bash
git switch feature/auth
```

---

# 16. What is merging?

Merging combines changes from one branch into another.

Example:

```bash
git switch main
git merge feature/auth
```

Conceptually:

```text
feature/auth
      ↓
    merge
      ↓
    main
```

---

# 17. What is a merge conflict?

A merge conflict occurs when Git cannot automatically combine competing changes.

Example:

```text
Developer A
→ changes same lines

Developer B
→ changes same lines
```

Git stops and asks you to resolve the conflict.

Typical flow:

```text
Merge
 ↓
Conflict
 ↓
Open files
 ↓
Resolve manually
 ↓
git add
 ↓
git commit
```

---

# 18. What is `git clone`?

`git clone` copies a remote repository to your local machine.

```bash
git clone https://github.com/example/project.git
```

Then:

```bash
cd project
```

---

# 19. What is a remote?

A remote is a reference to another Git repository, commonly hosted on a service such as GitHub.

Check remotes:

```bash
git remote -v
```

Typical remote name:

```text
origin
```

---

# 20. What is `git push`?

`git push` sends local commits to a remote repository.

Example:

```bash
git push origin main
```

First push for a branch:

```bash
git push -u origin main
```

---

# 21. What is `git pull`?

`git pull` fetches changes from a remote repository and integrates them into the current branch.

Conceptually:

```text
git pull
=
git fetch
+
integration
```

The integration may be performed using merge or rebase depending on configuration/options.

---

# 22. What is `git fetch`?

`git fetch` downloads changes and remote-tracking information without integrating those changes into your current branch.

Example:

```bash
git fetch origin
```

Then you can inspect the remote changes before deciding how to integrate them.

---

# 23. `git pull` vs `git fetch`

```text
git fetch
→ Download remote changes
→ Do not automatically integrate them

git pull
→ Fetch
→ Integrate changes into current branch
```

---

# 24. What is `.gitignore`?

`.gitignore` specifies files and directories Git should normally not track.

Example:

```gitignore
node_modules/
.env
dist/
build/
*.log
```

Important:

```text
.env
→ secrets/configuration

node_modules/
→ installed dependencies
```

These generally should not be committed.

---

# 25. What is `git diff`?

`git diff` shows changes that have not been staged.

```bash
git diff
```

For staged changes:

```bash
git diff --staged
```

Useful before committing.

---

# 26. How do you undo changes?

Discard changes in a file:

```bash
git restore filename
```

Unstage a file:

```bash
git restore --staged filename
```

Be careful with commands that discard work.

---

# 27. What is `git revert`?

`git revert` creates a new commit that reverses the effect of an earlier commit.

```bash
git revert <commit-hash>
```

This is generally safer for changes that have already been shared with others.

---

# 28. What is `git reset`?

`git reset` moves the current branch reference and can change the staging area and working tree depending on the option.

Common forms:

```bash
git reset --soft HEAD~1
git reset --mixed HEAD~1
git reset --hard HEAD~1
```

Be careful with:

```bash
git reset --hard
```

because it can discard local changes.

---

# 29. What is rebase?

Rebase moves or reapplies commits onto another base commit.

Example:

```bash
git fetch origin
git rebase origin/main
```

Conceptually:

```text
Before:

A---B---C   main
     \
      D---E feature


After rebase:

A---B---C---D'---E'   feature
```

Rebase can create a cleaner linear history, but avoid rewriting shared history without coordination.

---

# 30. What does "non-fast-forward" mean?

You may see:

```text
! [rejected] main -> main (fetch first)
```

This usually means the remote branch contains commits that your local branch does not contain.

Git prevents your push because it could overwrite remote history.

Typical solution:

```bash
git pull --rebase origin main
git push origin main
```

Resolve conflicts if necessary.

---

# Git Revision Checklist

* [ ] Git
* [ ] Repository
* [ ] Working directory
* [ ] Staging area
* [ ] Commit
* [ ] `git init`
* [ ] `git status`
* [ ] `git add`
* [ ] `git commit`
* [ ] `git log`
* [ ] Branch
* [ ] Merge
* [ ] Merge conflict
* [ ] Clone
* [ ] Remote
* [ ] Push
* [ ] Pull
* [ ] Fetch
* [ ] `.gitignore`
* [ ] Diff
* [ ] Restore
* [ ] Revert
* [ ] Reset
* [ ] Rebase

---

# Practical Git Workflow

```text
Create / Clone Repository
        ↓
Create Branch
        ↓
Write Code
        ↓
git status
        ↓
git diff
        ↓
git add .
        ↓
git commit -m "Meaningful message"
        ↓
git pull --rebase
        ↓
git push
```

### One-Line Interview Answer

> **Git is a distributed version control system used to track code changes, manage branches, maintain history, and collaborate with other developers.**
