
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

# over
d

Git status-> used to see the status of github repository

Git init -> used to intialize a git repository in the current working directory

what if i use git init, already in a folder that is already inited

so when we do git init:
the data is stored in .git folder



git add-> add the data to the stagged area, to be commited
> we can add every folder, or be selective

git add <f1><f2>
	git add . (possible?)
git commit-> commits the stagged data

git commit -> some pop up comes
git commit -m "messages heere"


after commiting -> it will tell working tree clean,nothing to commit



git log -> shows commit histroy (name, email,mesage)

dd