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