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