
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


## Git log

# ATOMIC Commit

- each commit must focus on one thing

MEssage text:
- in present tense not past
- write like order to the codebase to change the behaviour


## Seeing the shorten version of commit logs (Since commit message could be big and we cant see the id easily)

- git logs --pretty=online