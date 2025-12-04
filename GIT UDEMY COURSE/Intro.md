````markdown
# Git Complete Guide

## Table of Contents
- [What is Git](#what-is-git)
- [Why Use Git](#why-use-git)
- [Who Uses Git](#who-uses-git)
- [Git vs GitHub](#git-vs-github)
- [Installation and Setup](#installation-and-setup)
- [Command Line Basics](#command-line-basics)
- [Git Fundamentals](#git-fundamentals)
- [Core Git Commands](#core-git-commands)
- [Working with Branches](#working-with-branches)
- [Advanced Concepts](#advanced-concepts)
- [Deep Dive: Git Internals](#deep-dive-git-internals)

---

## What is Git

Git is just one of the many version control systems available today. Other well-known ones include Subversion, CVS, and Mercurial.

---

## Why Use Git

Git helps us:
- Track changes across multiple files
- Compare versions of a project
- "Time travel" back to old versions
- Revert to a previous version
- Collaborate and share changes
- Combine changes

**ANALOGY**: Similar to checkpoints in a game, where if anything happens the game will be loaded from that point
- Checkpoints
- Branching

---

## Who Uses Git

- Developer/engineering teams
- Non-tech people
- Government
- Scientists
- Writers

---

## Git vs GitHub

### GIT
- Git is the version control software that runs locally on your machine
- You don't need to register for an account
- You don't need the internet to use it
- You can use Git without ever touching GitHub

### GitHub
- GitHub is a service that hosts Git repositories in the cloud and makes it easier to collaborate with other people
- You do need to sign up for an account to use GitHub
- It's an online place to share work that is done using Git

---

## Installation and Setup

### Various Ways to Interact with Git
- Command line
- GUI → GitKraken

> Git requires UNIX based interface, so we need to install git bash for Windows

### Download & Setup
- Default branch name is "master", but you could use any
- Try to install the git usage in VSC, rather than VIM (for text editor)

### Configuring Git

To configure the name that Git will associate with your work:
```bash
git config --global user.name "Tom Hulce"
````

Configure your email (when we get to GitHub, you'll want your Git email address to match your GitHub account):

```bash
git config --global user.email blah@blah.com
```

**To check the user name:**

```bash
git config user.name
```

---

## Command Line Basics

### 🧩 1. Opening File Manager from Terminal

#### Windows

```bash
start .
```

✔ Opens File Explorer in the current folder

#### macOS / Linux

```bash
open .
```

✔ Opens Finder / Files in the current folder

---

### 📄 2. Creating Files

#### touch

```bash
touch filename.txt
touch file1 file2 file3
```

✔ Creates empty files  
✔ Also updates the "last modified" timestamp

---

### 📁 3. Creating Folders

#### mkdir

```bash
mkdir folder1
mkdir folderA folderB
```

✔ Creates one or multiple directories

---

### 📂 4. Listing Files

#### ls -a

```bash
ls -a
```

✔ Shows all files including hidden files (`.git`, `.env`, etc.)

---

### 🗑️ 5. Deleting Files/Folders

#### ⚠️ Dangerous Command

```bash
rm -rf foldername
```

- **-r** → recursive (delete inside folders)
- **-f** → force (no confirmation)

✔ Used to delete folders permanently  
⚠️ No recycle bin → irreversible

---

### 🧭 6. Navigation Commands

```bash
pwd              # show current path
cd folder        # move into folder
cd ..            # go back one level
cd /             # go to root
cd ~             # go to home directory
```

---

## Git Fundamentals

### Repository

A Git "Repo" is a workspace which tracks and manages files within a folder.

### Committing

Making a commit is similar to making a save in a video game. We're taking a snapshot of a git repository in time.

When saving a file, we are saving the state of a single file. With Git, we can save the state of multiple files and folders together.

---

## Core Git Commands

### 🧩 1. `git init` — Initialize Git Repository

#### ✔ What it does:

- Creates a hidden `.git` folder inside your project
- Converts normal folder → Git-controlled folder
- Starts version control

#### 🔧 Command:

```bash
git init
```

#### 🎯 When to use:

- At the **very beginning** of a new project
- Before you start tracking any files

#### 🧠 Internal working:

- Creates `.git` folder
- Inside it: commits, branches, logs, configurations
- Entire Git magic happens here

#### 📌 Example:

```bash
mkdir myproject
cd myproject
git init
```

Output: `Initialized empty Git repository...`

---

### 🟦 2. `git status` — See What's Happening

#### ✔ What it does:

- Shows files you changed
- Shows untracked files
- Shows which branch you're on
- Shows what's staged and unstaged

#### 🔧 Command:

```bash
git status
```

#### 🎯 Use this every time:

- Before adding files
- Before committing
- To understand what Git sees

#### 📌 Example output:

```
Untracked files:
  index.html
```

---

### 🟩 3. `git add` — Move Files to Staging Area

#### ✔ What it does:

- Selects the files you want to include in next commit
- Sends them to **staging area**

#### 🔧 Commands:

```bash
git add file.txt    # add specific file
git add folder/     # add folder
git add .           # add EVERYTHING
```

#### 🎯 Why staging area exists?

- So you can choose **which changes** go into commit
- Gives fine control
- Prevents accidental commits

#### 🧠 Internal working:

- Git takes a snapshot of the file
- Stores it temporarily in staging area
- After `git add .`, it indicates to commit

---

### 🟥 4. `git commit` — Create a Checkpoint

#### ✔ What it does:

Creates a **permanent snapshot** of your project.

#### 🔧 Command:

```bash
git commit -m "message"
```

#### 🎯 Good commit messages:

- "Added login page"
- "Fixed home page UI bug"
- "Updated database config"

#### 🧠 Internal working:

- Git creates a **commit object**
- Stores:
    - Snapshot of files
    - Your name/email
    - Time
    - Commit message
    - Unique ID (SHA)
- After committing it says "Working tree clean. no changes to commit"

#### 📌 Example:

```bash
git add .
git commit -m "Initial commit"
```

#### Doubts that I got:

- **What is Untracked files?** → Files that are newly created and not already in git
- **Why do we need staging area?** → Because sometimes we may not commit all the files

---

### 5. `git log` — View Commit History

#### What it shows:

- All commits
- Commit IDs (SHA)
- Author name
- Email
- Commit date/time
- Commit message

#### Command:

```bash
git log
```

#### Sample Output:

```
commit a3dfd1234e89c91cbe58fa12e65e67cd1ab2234a
Author: Rohit
Date:   Sun Feb 16 10:52:21 2025

    Added user authentication feature
```

You'll see commits from latest → oldest. It is like the **timeline / history viewer** of your Git project.

#### Useful Variations:

|Command|Meaning|
|---|---|
|`git log`|Full commit history|
|`git log --oneline`|One-line summary of commits|
|`git log --graph`|Visual tree of branches|
|`git log -p`|Log with code diff|
|`git log file.txt`|History of a specific file|
|`git log --author=""`|Filter by author|
|`git log --since=""`|Filter by date|

---

### 6. `git commit -a -m` — Stage and Commit in One Step

```bash
git commit -a -m "message"
```

#### ✔ Meaning:

- `-a` → Automatically stages ALL **tracked** modified files
- `-m` → Commit message directly without opening editor

---

## ATOMIC Commits

### ✅ Definition

An **Atomic Commit** is a commit that focuses on _one single purpose_ or _one single logical change_.

### 📌 Meaning:

- Each commit should do **ONE thing only**, not many
- The commit should be **small, understandable, and reversible**
- If something goes wrong, you can revert that one small unit without affecting unrelated code

---

## 📝 Commit Message Style Guidelines

### 1. Present tense, not past

- ❌ "Fixed bug"
- ✔ "Fix bug"

### 2. Imperative style

Write like **an instruction or command to the codebase**.

**Examples:**

- "Add login authentication"
- "Update dashboard route"

**Think of it as:** "What should this commit _do_ to the code?"

Because tools like Git auto-generate messages like: **"This commit will…"**

So your message should complete the sentence:

- **This commit will _Add login page_** ✔
- **This commit will _Fixed login page_** ❌ (wrong tense)

---

## Shortened Commit Logs in Git

By default, `git log` shows **big, detailed commit messages**, author, date, and full SHA (40 characters). This becomes hard to read when history grows.

So Git provides a way to show a **clean, one-line, shortened version** of each commit.

### 🧩 Command:

```bash
git log --pretty=oneline --abbrev-commit
```

### ⭐ What This Command Does

#### ✔ `--pretty=oneline`

- Shows every commit in **one single line**
- Removes author, date, extra details
- Gives you a cleaner history

#### ✔ `--abbrev-commit`

- Shortens the long 40-char commit ID (SHA) to ~7 characters
- Easier to read
- Easier to copy/paste
- Still unique enough to identify commits

### 🎯 Example Output

```
a1b2c3d Fix user login bug
d4e5f6a Add JWT authentication
```

**GitKraken** - Use it to do in a GUI

---

## Amending a Commit in Git

Sometimes after making a commit, you realize:

- You forgot to add a file
- You made a typo in the commit message
- You want to update the commit message
- You forgot to stage a change

Git allows you to **fix ONLY the previous commit** using:

```bash
git commit --amend
```

### ⭐ What `git commit --amend` Does

When you run amend:

- It **replaces** the previous commit
- It does NOT create a new commit
- It becomes a **new edited version** of the old commit
- The commit **SHA changes** (important)

**⚠️ Warning:** Only amend commits that you haven't pushed yet—amending pushed commits rewrites history and can break your team's work.

---

## `.gitignore`

- Tells Git which files/folders NOT to track
- Prevents pushing unwanted files to GitHub
- Keeps repo clean and secure
- Use template generators like Toptal/gitignore.io

### 🧠 Important Note

If a file was **already tracked by Git**, adding it to `.gitignore` won't stop Git from tracking it. You must untrack it manually:

```bash
git rm --cached filename
```

---

## Working with Branches

**A Git branch is like a separate copy of your project where you can work without affecting the main code.**

Think of it like _parallel universes_ of your code.

We could do feature branching and later merge it into the main branch.

### Branch Commands

#### ✔ See all branches

```bash
git branch
```

#### ✔ Create a branch

```bash
git branch feature-login
```

#### ✔ Switch to a branch

```bash
git checkout feature-login
```

or

```bash
git switch feature-login
```

#### ✔ Create + switch (most used)

```bash
git checkout -b feature-login
```

or

```bash
git switch -c feature-login
```

#### ✔ What switching does?

- It moves HEAD to that branch
- Code in your working directory changes according to the commit that branch points to

#### ✔ Delete a branch (after merge)

```bash
git branch -d feature-login
```

---

## Advanced Concepts

### Branch Naming Convention

#### ✔ In older Git versions, the default branch name was:

`master`

#### ✔ In 2020, GitHub changed the default branch to:

`main`

#### 📌 Why the change?

To use more inclusive, neutral naming

---

### HEAD — The Current Location Pointer

#### ✔ HEAD is a **pointer**

It always points to the **branch you are currently on**.

#### 📌 Example:

If you're on `main`, then:

```
HEAD → main
```

If you switch to `feature-login`, then:

```
HEAD → feature-login
```

#### ✔ Why is HEAD important?

Because **Git bases all operations** on where HEAD is pointing. Your next commit will go into the branch where HEAD is.

---

### Git Branches — Pointers to Latest Commit

#### ✔ A Git branch is just a **pointer**

It points to the **latest commit** in that branch's timeline.

**Example commit history:**

```
A → B → C → D
```

If `main` is here:

```
main → D
```

If you create a new branch from this point:

```
main → D
feature-login → D
```

When you make a new commit on the feature branch:

```
feature-login → E
```

Branches simply move forward as new commits are added.

---

## Deep Dive: Git Internals

### 1) Fundamental Concepts (Super Important)

- **Commit** = an object (SHA) that contains a pointer to a tree (snapshot of files), metadata (author/date/message) and parent(s)
- **Tree** = snapshot of file/directory structure (and blobs)
- **Branch** = a _name_ that points to a commit. Technically it is a file `refs/heads/<name>` storing a commit SHA. Very cheap/fast
- **HEAD** = a special _pointer_ that says "which commit (and therefore which branch) you're currently on". Usually `HEAD` is a **symbolic ref** to a branch like `refs/heads/main`. It can also be a direct SHA (detached HEAD)

Think: branches are just lightweight labels pointing at commits. Commits point to snapshots (trees). Files are not copied when you create a branch.

---

### 2) Visual: How Pointers Look (ASCII)

**Initial repo:**

```
A -- B -- C (main)

HEAD -> refs/heads/main (points to C)
refs/heads/main -> C
```

**Create a new branch `feature-1`:**

```
A -- B -- C (main)
         \
          (feature-1)

HEAD -> refs/heads/main (still points to C)
refs/heads/main -> C
refs/heads/feature-1 -> C  # new pointer created, points to same commit C
```

No files were copied. `feature-1` simply points to commit `C`.

**When you make a new commit on `feature-1` (after switching):**

```
A -- B -- C (main)
         \
          D (feature-1)

HEAD -> refs/heads/feature-1 -> D
refs/heads/main -> C
```

---

### 3) What `git branch <name>` Does

- Creates a new file `refs/heads/<name>` that contains the commit SHA where `HEAD` currently points (usually the current branch's tip)
- **It does NOT move HEAD**. So after `git branch feature`, you are still on the old branch until you `git switch`/`checkout` it
- **It does NOT duplicate working tree files**. Files on disk remain as they are until you switch branches (which updates the working tree)

**Command example:**

```bash
git branch feature-1  # creates refs/heads/feature-1 with same SHA as current branch HEAD
```

---

### 4) What `git switch <branch>` (or `git checkout <branch>`) Does

When you switch branches Git performs these main steps:

1. Checks for **uncommitted changes** that would be overwritten by switching. If such changes exist, Git refuses unless you force or stash them
2. Updates the `HEAD` symbolic ref to point to `refs/heads/<branch>` (so HEAD now points at the branch)
3. Updates the **index (staging area)** and **working directory** to match the commit pointed to by the branch (the branch's tree). Files are added/removed/changed on disk so they reflect that commit

So switching changes what commit your working tree represents. It does **not** change other branch pointers.

---

### 5) Why Creating a Branch Doesn't Copy Data

Commits store entire tree snapshots (or references to blobs/trees) inside `.git/objects`. Branch names are just refs to commit SHAs.

Creating a branch is writing one small file with a SHA — super cheap.

The working tree is only updated when you switch.

---

### 6) `git status` — What Does It Show and Why?

`git status` reports file differences **relative to three things**:

1. **HEAD (the commit your current branch points to)** — shows what's committed in the current branch tip
2. **Index / Staging Area** — shows what you have staged (what will go into the next commit)
3. **Working Directory** — shows what's currently changed in the files on disk compared to the index and HEAD

**Important consequences:**

- `git status` only shows the **state of the current branch/working directory**, because `HEAD` points to exactly one commit (one branch). It does **not** compute statuses for all other branches — that would be expensive and not helpful in normal workflows
- If you have the same uncommitted changes and then switch branches (and Git allows the switch), the working directory will be updated and `git status` will report differences relative to the new HEAD commit

**Example flows:**

**A) You are on `main`:**

```
HEAD -> main (C)
working tree == tree of C
git status  # compares working tree vs index vs HEAD(C)
```

**B) You `git branch feature`** (still on main) and `git status` still shows status relative to `main` (HEAD unchanged)

**C) You `git switch feature`** (now feature points to C too) — HEAD changes to `refs/heads/feature`. `git status` still compares working tree vs HEAD (now feature). If there are no changes in commits, results may look the same

So the result appears the same across branches only when the commits they point to produce identical file trees or when you have no uncommitted changes.

---

### 7) What If Two Branches Point to the Same Commit?

If `main` and `feature` both point to the same commit SHA, then after switching between them you will see identical working tree and identical `git status` outputs (assuming you haven't made new commits).

Only the pointer (branch name) changed.

---

### 8) Detached HEAD

If you `git checkout <commit-SHA>` (not a branch name) HEAD becomes detached:

HEAD points directly to a commit SHA, not to a branch ref.

Any new commits you make in detached HEAD are not reachable by any branch unless you create a branch to capture them.

---

### 9) Inspect Pointers and Objects — Useful Commands

Run these in a repo to see what's happening:

**Show where HEAD points:**

```bash
git rev-parse --abbrev-ref HEAD  # prints branch name (or "HEAD" if detached)
git symbolic-ref HEAD             # shows refs/heads/<branch>
git rev-parse HEAD                # prints commit SHA of HEAD
```

**List refs:**

```bash
git show-ref                      # list all refs and committed SHAs
ls .git/refs/heads/               # shows branch files
cat .git/refs/heads/main          # the SHA that `main` points to
```

**See short branch pointers in graph form:**

```bash
git log --oneline --graph --decorate --all
```

**Inspect a commit tree:**

```bash
git show --pretty=fuller <commit-SHA>
git ls-tree <tree-SHA>            # show files in a tree object
git cat-file -p <object-SHA>      # inspect raw objects (commits/trees/blobs)
```

**See the reflog (local movement of HEAD):**

```bash
git reflog
```

**Find what commit a branch currently points to:**

```bash
git rev-parse --verify refs/heads/feature-1
```

---

### 10) What Happens with Uncommitted Changes When Switching Branches?

- If the changes **do not** conflict with files in the target branch, Git will carry those uncommitted changes across the switch (your working tree changes are preserved relative to the new HEAD). `git status` then shows differences relative to the new HEAD
- If the changes **would be overwritten** (file in target branch differs and switch would change it), Git refuses and asks you to `stash`, `commit`, or `discard` changes first

This behaviour is why people often `git stash` before switching branches when they want to temporarily save work.

---

### 11) Merging and Pointer Movement (Fast-Forward vs Merge Commit)

**Fast-forward:** If target branch has no new commits, merging moves the target branch pointer forward to the source tip (no merge commit).

**Example:** `main` -> C, `feature` -> D where C is ancestor of D. Merging `feature` into `main` moves `main` to D.

**Merge commit (3-way merge):** If both branches have new commits, Git creates a new commit whose parents are the two branch tips and updates the target branch to that new commit.

Pointers are updated by writing new SHA into `refs/heads/<branch>`.

---

### 12) Remote Branches and Tracking Pointers

Remote branches like `origin/main` are just refs stored to represent what the remote last advertised.

Your local `main` is independent — you update it by pulling (which may fast-forward or merge).

`git push` updates remote refs if permitted.

---

### 13) Practical Checklist / Cheatsheet (What to Use When)

**See current branch and HEAD:**

```bash
git rev-parse --abbrev-ref HEAD
```

**Create branch but stay on current:**

```bash
git branch feature-1
```

**Create and switch to new branch:**

```bash
git checkout -b feature-1
# or
git switch -c feature-1
```

**Inspect branch pointers and history:**

```bash
git show-ref
git log --oneline --graph --decorate --all
```

**See status relative to current HEAD:**

```bash
git status
```

**Stage tracked modifications and commit in one:**

```bash
git commit -a -m "message"
```

**If you want to experiment without disturbing branch pointers:**

```bash
git switch --detach
```

**Save uncommitted work before switching:**

```bash
git stash
git switch feature-1
git stash pop  # reapply
```

---

### 14) Quick Answers to Your Exact Bullet Questions

- **"HEAD -> current location"** — Yes: HEAD points to the current branch ref or directly to a commit (detached)
- **"Git branches -> pointer for each branch to point to latest commit"** — Right. `refs/heads/<branch>` stores the SHA of the latest commit on that branch
- **`git branch <name>` — does the new branch have data of the previous branch?** It points to the same commit as the branch you created it from, so the snapshot (tree) visible from that commit is the same — but no files were copied. It's just a pointer to the same history
- **`git switch <branch>`** — Updates HEAD to point to the branch and updates working tree/index to match its commit
- **`git status` shows the status of the current branch only** — Because it compares working tree/index against the commit HEAD currently points to. Other branches are just pointers and don't affect the current working tree unless you switch to them
- **`git commit -a -m "msg"`** — Stages modified & deleted tracked files and commits them; it does not auto-add new (untracked) files

---

## Summary

This guide covers everything from basic Git concepts to advanced internals. Use it as a reference while working with Git, and remember:

- Git is about managing snapshots of your project over time
- Branches are lightweight pointers to commits
- HEAD tells Git where you currently are
- Understanding how Git stores data helps you work more effectively

Happy coding! 🚀