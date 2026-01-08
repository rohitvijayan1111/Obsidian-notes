# Configuring git
### ✔ Set your name

`git config --global user.name "Your Name"`

### ✔ Set your email

`git config --global user.email "youremail@example.com"`

### ✔ Check your config

`git config --list`



# Terms

- git init -> used to create a .git folder which starts to track changes in files , contains commits, branches etc
- git status-> used to tell the files that have changed, the untracked files. shows which branch i am in , shows staged and unstaged changes



# git commands

git add folder/        # add folder

# 🎯 **IMPORTANT VARIATIONS YOU MUST KNOW**

## ✔ Commit all staged files:

`git commit -m "message"`

## ✔ Commit AND stage tracked files automatically:

`git commit -am "message"`

⚠ Works only for files previously tracked (not new ones).


q)if i commit everything that is in my stagging area, will the stagging area be empty? if so how will git status compare the working directory and the stagg area, it would show complete difference right

Yes. After you commit, the staging area becomes empty _relative to HEAD_.  
And no — `git status` will NOT show a “complete difference.”


- `git status` always reports **relative to the current branch**
- If you see:

`HEAD detached at a3f2e9c`

➡ You are **not on a branch**, HEAD points directly to a commit.


## Understanding of Git Status
Absolutely — **`git status` looks simple, but it’s actually reporting multiple internal states**.  
I’ll explain it **in depth**, by breaking it into:

1. What `git status` is comparing internally
    
2. All possible outcomes you can see
    
3. Why you see _that_ message
    
4. How branch/HEAD affects it
    
5. Mental model to always predict `git status`
    

---

## 🧠 Big Picture: What does `git status` really do?

![Image](https://miro.medium.com/1%2AdiRLm1S5hkVoh5qeArND0Q.png)

![Image](https://i.sstatic.net/VBe0u.png)

Every `git status` is answering **three questions**:

```
1️⃣ How does Working Directory differ from Staging Area?
2️⃣ How does Staging Area differ from HEAD (last commit)?
3️⃣ What branch is HEAD pointing to?
```

So internally Git is comparing **three snapshots**:

```
Working Directory  ⇄  Index (Staging)  ⇄  HEAD Commit
```

Keep this in mind — everything below comes from this.

---

## 1️⃣ Branch & HEAD information (top section)

You’ll almost always see something like:

```
On branch main
```

or

```
On branch feature-login
```

### What this means internally

- `HEAD` → points to `refs/heads/main` (or feature branch)
    
- `git status` always reports **relative to the current branch**
    
- Other branches are irrelevant unless you switch
    

If you see:

```
HEAD detached at a3f2e9c
```

➡ You are **not on a branch**, HEAD points directly to a commit.

---

## 2️⃣ Clean working tree (best case)

### Output:

```
On branch main
nothing to commit, working tree clean
```

### Internal state:

- Working Directory == Staging Area
    
- Staging Area == HEAD commit
    
- No differences anywhere
    

### Meaning:

✔ You haven’t changed anything  
✔ Or everything is already committed

---

## 3️⃣ Untracked files (very common)

### Output:

```
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        test.js
```

### Internal state:

- File exists in Working Directory
    
- File does NOT exist in Index
    
- File does NOT exist in HEAD
    

### Meaning:

- Git knows the file exists
    
- But Git is NOT tracking it yet
    

### Fix:

```bash
git add test.js
```

---

## 4️⃣ Modified but NOT staged

### Output:

```
Changes not staged for commit:
  modified: index.js
```

### Internal state:

- File exists in HEAD
    
- File exists in Index
    
- Working Directory version ≠ Index version
    

### Meaning:

You changed a tracked file, but didn’t stage it.

### To see what changed:

```bash
git diff
```

### To stage it:

```bash
git add index.js
```

---

## 5️⃣ Staged changes (ready to commit)

### Output:

```
Changes to be committed:
  modified: index.js
```

### Internal state:

- Index version ≠ HEAD version
    
- Working Directory == Index
    

### Meaning:

- This change WILL go into the next commit
    

### To see staged changes:

```bash
git diff --staged
```

---

## 6️⃣ Both staged AND unstaged changes (important)

### Output:

```
Changes to be committed:
  modified: index.js

Changes not staged for commit:
  modified: index.js
```

### Internal state:

- You modified the file
    
- Staged part of it
    
- Then modified it again
    

### Meaning:

Same file exists in **three different versions**:

- HEAD
    
- Index
    
- Working Directory
    

### Common in real work.

---

## 7️⃣ Deleted files

### Output:

```
Changes not staged for commit:
  deleted: config.json
```

or

```
Changes to be committed:
  deleted: config.json
```

### Meaning:

- File was tracked earlier
    
- Now removed from disk
    
- Stage it with:
    

```bash
git add -u
```

or

```bash
git rm config.json
```

---

## 8️⃣ Renamed or moved files

### Output:

```
renamed: old.js -> new.js
```

### Internal logic:

- Git detects delete + add
    
- If content is similar, it shows rename
    

---

## 9️⃣ Ignored files (you WON’T see them)

Files in `.gitignore`:

- DO NOT appear in `git status`
    
- Unless you force:
    

```bash
git status --ignored
```

---

## 🔟 Ahead / Behind remote branch

### Output:

```
Your branch is ahead of 'origin/main' by 2 commits.
```

or

```
Your branch is behind 'origin/main' by 1 commit.
```

### Meaning:

- Git compares local branch pointer
    
- With remote-tracking branch pointer
    
- Shows divergence
    

---

## 1️⃣1️⃣ Merge / Rebase / Conflict states

### During merge:

```
You have unmerged paths.
```

### During rebase:

```
You are currently rebasing branch 'feature-login'
```

### Conflict markers exist → status tells you what’s conflicted.

---

# 🔥 Mental Model (MOST IMPORTANT)

Whenever you run `git status`, ask yourself:

```
1. Did I create new files? → untracked
2. Did I modify tracked files? → modified
3. Did I run git add? → staged
4. Did I commit? → clean
5. Did I modify after staging? → staged + unstaged
6. Am I on the right branch? → HEAD info
```

---

# 🧠 Quick Mapping Table

|Status message|Meaning|
|---|---|
|untracked|file only in working directory|
|modified (not staged)|WD ≠ Index|
|staged|Index ≠ HEAD|
|clean|WD = Index = HEAD|
|ahead/behind|local vs remote pointer|
|detached HEAD|HEAD not pointing to branch|

---

# 🧪 Pro Commands to Inspect Status Internals

```bash
git diff            # WD vs Index
git diff --staged   # Index vs HEAD
git ls-files        # tracked files
git show HEAD       # last commit snapshot
git rev-parse HEAD  # where HEAD points
```

---

# 🎯 Final one-liner (interview level)

**`git status` reports how the working directory and staging area differ from the current branch’s HEAD commit, along with branch and repository state information.**

---

If you want next, I strongly recommend:

- 🔥 `git add -p` (partial staging)
    
- 🔥 `git reset` (soft/mixed/hard)
    
- 🔥 `git reflog` (time machine for mistakes)
    

# Git logs

- git log
- git log --oneline
- git log --online --graph --decorate
- git log -3 # shows the latest 3 commits
- git log file.txt # for specific files
- git log --author="rohit"
- git log --grep="login"


# ⚠️ **Very Important: What Happens If Someone Else Pushes Before You Amend?**

### ❌ Problem:

If another user **already pushed** their commits to the remote repository  
AND  
you try to amend your own commit **after pulling their changes**,

→ Amending **rewrites history**, which is dangerous.

---

# 🚨 AMEND RULE (the golden rule)

### ✔ SAFE TO AMEND **if the commit is NOT pushed**

You can amend freely.

### ❌ UNSAFE TO AMEND **if the commit IS already pushed**

Because:

- Amend changes the commit ID (SHA)
    
- Now your local history ≠ remote history
    
- Git cannot merge this automatically
    
- You will face `non-fast-forward` errors



# removing a file that is already getting tracked by git
# 🧠 Important Note

If a file was **already tracked by Git**, adding it to `.gitignore` won’t stop Git from tracking it.

You must untrack it manually:

`git rm --cached filename`


# GIT Branches

# 🚀 Basic Branch Commands

## ✔ See all branches

`git branch`

## ✔ Create a branch

`git branch feature-login`

## ✔ Switch to a branch

`git checkout feature-login`

## ✔ Create + switch (most used)

`git checkout -b feature-login`

## ✔ Delete a branch (after merge)

`git branch -d feature-login`


