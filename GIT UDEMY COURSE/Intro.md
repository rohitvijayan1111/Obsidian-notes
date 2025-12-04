
## What is Git:
- Git is just one of the many version control systems available today. Other well-known ones include Subversion, CVS, and Mercurial.


## how does Git help us
- Track changes across multiple files
- Compare versions of a project
- "Time travel" back to old versions
- Revert to a previous version
- Collaborate and share changes
- Combine changes

ANALOGY:
similar to checkpoints in game, where if anything happens the game will be loaded from that point

- Checkpoints
- Branching
## Who uses GIT

- Developer/engineering team
- others non tech people
- government
- scientist 
- Writers
## Difference between GIT and Github

### GIT
- Git is the version control software that runs locally on your machine. You don't need to register for an account.
- You don't need the internet to use it. You can use Git without ever touching GitHub.

### Github

- Github is a service that hosts Git repositories in the cloud and makes it easier to collaborate with Other people.
- You do need to sign up for an account to use GitHub. It's an online place to share work that is done using Git.

## Various ways to interact with GIT

- commandline
- GUI-> gitKraken


> Git requires UNIX based interface, so we need to install git bash for windows

## Download & Setup 

- Default branch name is "master", but you could use any
- try to install the git usage in VSC,rather than VIM (for text editor)

## configuring git
- To configure the name that Git will associate with your work, run this command:
	- git config --global user . name "Tom Hulce"
- Do the same thing for your email using the following command. When we get to Github, you'll want your Git email address to match your Github account.
	- git config --global user . email blah@blah.com

> TO CHECK THE USER NAME
> git config user.name

# Commandline knowledge
## 🧩 **1. Opening File Manager from Terminal**

### **Windows**

`start .`

✔ Opens File Explorer in the current folder.

### **macOS / Linux**

`open .`

✔ Opens Finder / Files in the current folder.

---

## 📄 **2. Creating Files**

### **touch**

`touch filename.txt touch file1 file2 file3`

✔ Creates empty files  
✔ Also updates the “last modified” timestamp

---

## 📁 **3. Creating Folders**
### **mkdir**

`mkdir folder1 mkdir folderA folderB`

✔ Creates one or multiple directories

---

## 📂 **4. Listing Files**

### **ls -a**

`ls -a`

✔ Shows all files including hidden files (`.git`, `.env`, etc.)

---

## 🗑️ **5. Deleting Files/Folders**

### ⚠️ Dangerous Command

`rm -rf foldername`

**-r** → recursive (delete inside folders)  
**-f** → force (no confirmation)

✔ Used to delete folders permanently  
⚠️ No recycle bin → irreversible

---

## 🧭 **6. Navigation Commands**

`pwd        # show current path cd folder  # move into folder cd ..      # go back one level cd /       # go to root cd ~       # go to home directory`

# Basics

- Repository:
	- A Git "Repo" is a workspace which tracks and manages files within a folder.
- Committing:
	- Making a commit is similar to making a save in a video game. We're taking a snapshot of a git repository in time.
	- When saving a file, we are saving the state of a single file. With Git, we can save the state of multiple files and folders together.

# 🧩 **1. `git init` — Initialize Git Repository**
## ✔ What it does:
- Creates a hidden `.git` folder inside your project
- Converts normal folder → Git-controlled folder
- Starts version control
### 🔧 Command:
`git init`
### 🎯 When to use:
- At the **very beginning** of a new project
- Before you start tracking any files
### 🧠 Internal working:
- Creates `.git` folder
- Inside it: commits, branches, logs, configurations
- Entire Git magic happens here
### 📌 Example:
`mkdir myproject cd myproject git init`

Output:
`Initialized empty Git repository...`

---

# 🟦 **2. `git status` — See What’s Happening**

## ✔ What it does:
- Shows files you changed
- Shows untracked files
- Shows which branch you're on
- Shows what’s staged and unstaged
### 🔧 Command:
`git status`
### 🎯 Use this every time:
- Before adding files
- Before committing
- To understand what Git sees
### 📌 Example output:
`Untracked files:   index.html`
---
# 🟩 **3. `git add` — Move Files to Staging Area**
## ✔ What it does:
- Selects the files you want to include in next commit
- Sends them to **staging area**
### 🔧 Commands:
`git add file.txt       # add specific file git add folder/        # add folder git add .              # add EVERYTHING`

### 🎯 Why staging area exists?
- So you can choose **which changes** go into commit
- Gives fine control
- Prevents accidental commits
### 🧠 Internal working:
- Git takes a snapshot of the file
- Stores it temporarily in staging area
- after git add ., it indicates to commit 
---
# 🟥 **4. `git commit` — Create a Checkpoint**
## ✔ What it does:
Creates a **permanent snapshot** of your project.

### 🔧 Command:
`git commit -m "message"`

### 🎯 Good commit messages:
- “Added login page”
- “Fixed home page UI bug”
- “Updated database config”
### 🧠 Internal working:
- Git creates a **commit object**
- Stores:
    - Snapshot of files
    - Your name/email
    - Time
    - Commit message
    - Unique ID (SHA)
- After committing it says "Working tree clean. no changes to commit"

### 📌 Example:
`git add . git commit -m "Initial commit"`

## Doubts that i got:
- What is Untracked files-> files that are newly created and not already in git
- Why do we need staging area-> coz sometime we may not commit all the files

---


## Git log

`git log` shows:
- All commits
- Commit IDs (SHA)
- Author name
- Email
- Commit date/time
- Commit message
### **Command:**
`git log`
### **Sample Output:**
`commit a3dfd1234e89c91cbe58fa12e65e67cd1ab2234a Author: Rohit <rohit@example.com> Date:   Sun Feb 16 10:52:21 2025      Added user authentication feature`

You’ll see commits from latest → oldest.
It is like the **timeline / history viewer** of your Git project.

|Command|Meaning|
|---|---|
|`git log`|Full commit history|
|`git log --oneline`|One-line summary of commits|
|`git log --graph`|Visual tree of branches|
|`git log -p`|Log with code diff|
|`git log file.txt`|History of a specific file|
|`git log --author=""`|Filter by author|
|`git log --since=""`|Filter by date|

# ATOMIC Commit

### ✅ **Definition**
An **Atomic Commit** is a commit that focuses on _one single purpose_ or _one single logical change_.

### 📌 **Meaning:**
- Each commit should do **ONE thing only**, not many.
- The commit should be **small, understandable, and reversible**. 
- If something goes wrong, you can revert that one small unit without affecting unrelated code.

## 📝 **Commit Message Style Guidelines**
## 1. **Present tense, not past**
- ❌ “Fixed bug”
- ✔ “Fix bug”
    
## 2. **Imperative style**
Write like **an instruction or command to the codebase**.
Examples:
- “Add login authentication”
- “Update dashboard route”

**Think of it as:**  
“What should this commit _do_ to the code?”
Because tools like Git auto-generate messages like:

**"This commit will…"**

So your message should complete the sentence:
- **This commit will _Add login page_** ✔
- **This commit will _Fixed login page_** ❌ (wrong tense)

# **Shortened Commit Logs in Git**
By default, `git log` shows **big, detailed commit messages**, author, date, and full SHA (40 characters).  
This becomes hard to read when history grows.
So Git provides a way to show a **clean, one-line, shortened version** of each commit.

---
# 🧩 **Command:**
`git log --pretty=oneline --abbrev-commit`
# ⭐ What This Command Does
### ✔ `--pretty=oneline`
- Shows every commit in **one single line**
- Removes author, date, extra details
- Gives you a cleaner history
### ✔ `--abbrev-commit`
- Shortens the long 40-char commit ID (SHA) to ~7 characters
- Easier to read
- Easier to copy/paste
- Still unique enough to identify commits
---
# 🎯 **Example Output**
`a1b2c3d Fix user login bug 
d4e5f6a Add JWT authentication`

Gitkraken
- use it do in a GUI

## **Amending a Commit in Git**
Sometimes after making a commit, you realize:
- You forgot to add a file
- You made a typo in the commit message
- You want to update the commit message
- You forgot to stage a change
    
Git allows you to **fix ONLY the previous commit** using:
`git commit --amend`
# ⭐ What `git commit --amend` Does
When you run amend:
- It **replaces** the previous commit
- It does NOT create a new commit
- It becomes a **new edited version** of the old commit
- The commit **SHA changes** (important)
  
**Only amend commits that you haven’t pushed yet—amending pushed commits rewrites history and can break your team’s work.**



## **`.gitignore`**
- Tells Git which files/folders NOT to track
- Prevents pushing unwanted files to GitHub
- Keeps repo clean and secure
- Use template generators like Toptal/gitignore.io
### 🧠 Important Note
If a file was **already tracked by Git**, adding it to `.gitignore` won’t stop Git from tracking it.
You must untrack it manually:
`git rm --cached filename`




	

GITHUB-> creates a branchh called main and not master

HEAD->current locatio


Git branches-> pointer for each branch to point to the latest commit


git branches ->lists branches


to create branches
git branches <branch_name>-> 
- but pointer (head) still in the previous branch
- does it have the data of the previous branch???

git switch <branch name>



git status -> shows the status of all the branches
- how does it show in the pov in each branch same result?


git commit -a -m "messgw"



difference between switch and checkout


git switch -c "branch names" ->create an branch and moves to it


Switching to another branch before commiting:

- it will throw a warning to commit /stash the changes
- if not then the changes would be lost
will not throw warning if the file that was changed/creaated is unique
if conflicts it will throw warning 


git branch --delete/--d <branch name>
?does it allow delete the branch in the same branch, should i have to switch to other branch?
it shows some conflict like the branch is not fully merged, are sure to delete it
(anywhere but not in the branch)


for rename->u have to be inside that brach
git branch -m <renamed name>


HEad:
- in .git it stores a head, file where it would refer to a file, which will have the latest commit code for each branch, so we switch branches this file path changes in the head



# Git merge

move to the branch where u have to merge the code
git switch
	git merge <other branch nae>

> fast forward merge(no)
> how will the logs look like it

if it isnt a fast forward commit,means there is change in the main branch and the new branch, then git automatically, creates a commit,which merges these two, and the parent of this would be both the branches


merge conflicts

COnflict markers -> <<<<hEad

if merge branching is done, will both the repo will hve the same code or only the main repo?
