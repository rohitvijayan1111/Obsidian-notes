
difference between switch and checkout

| Action          | switch                | checkout                  |
| --------------- | --------------------- | ------------------------- |
| Switch branches | Safer                 | Might overwrite files     |
| Create branch   | Clear                 | Mixed with other features |
| Restore files   | ❌ Not supported       | ✔ Yes                     |
| Checkout commit | ✔ Yes (with --detach) | ✔ Yes                     |

git switch -c "branch names" ->create an branch and moves to it


Switching to another branch before commiting:
- it will throw a warning to commit /stash the changes
- if not then the changes would be lost
will not throw warning if the file that was changed/created is unique
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
