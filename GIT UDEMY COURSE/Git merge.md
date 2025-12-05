Below is a **clean, organized, professionally formatted Markdown version** of your notes on **Git Merge**, including diagrams for clarity.

---

# **Git Merge — Clean & Clear Explanation**

## **How Merging Works in Git**

Merging is the process of combining changes from one branch into another.

### ✔ Step 1: Move to the branch that should receive the changes

```bash
git switch <target-branch>
```

Example: merging a feature into `main`:

```bash
git switch main
```

### ✔ Step 2: Merge the other branch _into_ the current branch

```bash
git merge <other-branch-name>
```

Example:

```bash
git merge feature-login
```

---

# **Types of Merges in Git**

There are **two** main types of merges:

---

# 1️⃣ **Fast-Forward Merge**

### ✔ When does it happen?

A fast-forward merge occurs when:

- The target branch has **not moved** after you created your feature branch
    
- There are **no divergent commits**
    

In other words, the target branch is **directly behind** the feature branch.

### ✔ Example:

```
main:     A ─ B
feature:  A ─ B ─ C ─ D
```

Merging feature into main:

```
main becomes: A ─ B ─ C ─ D
```

### ✔ What happens internally?

- Git simply **moves the branch pointer forward**
    
- No new commit is created
    

### ✔ How logs look:

```text
A
B
C
D
```

No merge commit appears because nothing needed merging — just a pointer update.

---

# 2️⃣ **3-Way Merge (Non–Fast-Forward Merge)**

### ✔ When does it happen?

A non-fast-forward merge occurs when:

- **Both branches have new commits**
    
- Their histories **diverged**
    

Example:

```
main:     A ─ B ─ C
               \
feature:         D ─ E
```

Both `main` and `feature` have unique commits.

### ✔ What Git does:

Git creates **a merge commit** that has **two parent commits**:

```
main:     A ─ B ─ C ──── M
               \       /
feature:         D ─ E
```

Here:

- `M` is the **merge commit**
    
- Parents of `M` are:
    
    - The tip of `main` → `C`
        
    - The tip of `feature` → `E`
        

### ✔ Merge commit message (auto-created):

```
Merge branch 'feature'
```

---

# **How the Logs Look for Non–Fast-Forward Merge**

Using:

```bash
git log --oneline --graph --decorate
```

You’ll see something like:

```
*   ab12cd Merged feature into main   ← merge commit
|\  
| * de45f2 E: feature update
| * 93ac01 D: feature start
* | 7f21b4 C: main update
|/  
* 4c9a88 B
* 1a2b3c A
```

This clearly shows:

- Two branches diverging
    
- A merge commit joining them
    

---

# **Summary Table**

|Type of Merge|When It Happens|Creates New Commit?|Log Appearance|
|---|---|---|---|
|**Fast-Forward**|Target branch has no new commits|❌ No|Straight line|
|**3-Way (Non-FF)**|Both branches have unique commits|✔ Yes|Merge commit with two parents|

---



git diff, compares staging area and working directory (all unstagged changes)

a/File.txt b/File.txt

@ 3,5 4,5
+++
--
git diff HEAD -> head/branch and working directory (all changes stagged and un-stagged since head )
 

what will be shown in git diff head, i have created  a new file, in working directory 
shows one file

when we commit it and see ,git diff head,
will comparing it will list as 



git diff -- cached / --staged

staged area and the branch/HEAD(i.e last committed)


```git diff --cached <filename>``` 

just this file


comparing branches
```
git diff <branch1>..<branh2>
git diff <branch1> <branh2>
a<- branch1
b<- branch2
```


comparing commits

```
git diff <commithash1>..<commithash2>
git diff <commithash1> <commithash2>

order matters
```



# What will happen if i dont push my changes and try to switch the branch

- if no conflicts , the changes will come along with the branch  u want to switch to
- else git wont allow,unless u commit the changes etc