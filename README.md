# GitCommands

#### .git is the hidden repository in working directory which has staging area and commits

### Basic Git Commands:

#### git init 
- to initialize .git repository in working directory

#### git status 
- to get some inportant information about files in the directory

#### git add file_name 
- to add an untracked file to staging area

#### git add . 
- to add all untracked files to staging area

#### git commit -m "message - (first commit)" 
- to commit new changes linked to files

To authourize with your identity so that other people know who created any changes or commits
#### git config --global user.email "you@email.com"
#### git config --global user.name "your name"

#### git log 
- to get all the information about commits in that specific branch


Checkout is used to move around branches and commits
#### git checkout commit_id 
- to go to a particular commit

#### git checkout branch_name 
- to go to a particular branch

Branches
#### git branch - will show all branches and current branch with asterisk on it

#### git branch "branch-name" 
- it will create a new branch with name "branch-name"

#### git checkout -b "branch-name" 
- it will create a new branch and move us to that branch(we can check that using "git branch" command)

Merges : if a branch is ahead of main branch and we want to add merge its changes to main branch
#### git merge "branch-name" 
- if we want to merge we should checkout to that branch on which we want to merge and then merge from "branch-name"


- if we use 'git log', we see
- commit id (Head -> main, second-branch) : in which this head points to the lastest commit of current branch
- if we checkout to a commit using commit_id then it will show us detached head (check that using 'git branch' after checkout to commit)



Switching:
#### git switch "branch-name" 
- to switch to other brach just like checkout command
#### git switch -c "new-branch-name" 
- to create and switch to new branch 





Deleting tracked files with latest commit:
#### git ls-files 
- to check which files are currently there in unstaged from the latest commit or all file in staging area refering to a commit

#### git rm "file-name" 
- then if we delete a specific file we need to put that change in staged area for that we will use command and commit the change. Recheck that using git ls-files command.

To undo changes for tracked files at unstaged level:
#### git checkout "file-name"
#### git checkout -- "file-name" 
- here '--' represents current branch we can ignore that as well
#### git checkout . 
- to undo all file's changes

To undo changes for tracked files at unstaged level (to avoid use of checkout):
#### git restore "file-name"
#### git restore -- "file-name" 
- here '--' represents current branch we can ignore that as well
#### git restore . 
- to undo all file's changes

Deleting untracked files :
#### git clean -dn 
- to get all the entries we want to delete
#### git clean -df 
- to delete




Undoing the chages after staging:
1.  one way:
#### git reset "file-name" 
- it copies the latest commit file to the staging area so basically unstaging the file
#### git checkout "file-name" or git restore "file-name" 
- after reset command we use this to undo changes to file.

2.  another way (better way):
#### git restore --staged "file-name" 
- it copies the latest commit file to the staging area so basically unstaging the file
#### git checkout "file-name" or git restore "file-name" 
- after reset command we use this to undo changes to file.




Undoing changes after commit:
#### git reset --soft HEAD~1 
- it will remove the latest commit from the branch head will go to the previous commit but it wont remove file from staging area. check that using 'git ls-files'
#### git reset HEAD~1 
- it will remove the lastest commit and also will remove it from staging area but wont delete the file.
#### git reset --hard HEAD~1 
- it will remove the lastest commit and will remove it from staging area but will also delete the file.
#### git commit --amend
- this wont delete the last commmit instead it will merge changes in the commit that we did.
- example: if we did added 2 line of code into a file and commit that. soon after we realise we wanted 3 line of code so we add new line and then use commit --amend to merge those changes in latest/last commit we created instead of creating new commit.


Deleting Branch:
#### git branch -d/-D "branch-name" 
- this will delete the branch
#### git branch -d/-D "first-branch" "second-branch" 
- this will be used to delete multiple branches here two




Detached branch:
#### git checkout "commit_id" 
- to go to detached-head

after doing some changes we add and commit at detached-head
#### git add .
#### git commit -m "changes in detached-head"

#### git branch "detached-head-branch" 
- now we need to make another branch that will save the changes from detached-head otherwise if try to switch other branch it will show warning and changes wont we updated.

#### git switch master 
- then we switch
#### git merge "detached-head-branch" 
- and merge it with main branch to have those changes
#### git branch -d "detached-head-branch" 
- then we can delete that "detached-head-branch"



### Other Deep Dive commands:

'git stash':
#### git stash 
- can be used to save unstaged changes if we ant to go back to latest committed changes.
#### git stash apply 
- to bring back those saved unstaged changes
#### git stash list 
- to list all saved changes in stash (top one will be latest stashed data)
#### git stash apply {number} 
- to go to specific stashed change we need to go back to staged area with latest commmit for that we need to use 'git stash' again. then we can use this command.
#### git stash push -m "message" 
- it is better to use it with message to make it easier to know about stashed changes.
#### git stash pop {number} 
- to remove n add this stashed change from stashed area to unstaged area. (as in apply data stays in stash)
#### git stash drop {number} 
- to drop data from stash
#### git stash clear 
- to drop the whole stash


'git reflog'
#### git refolg 
- can show us the overview of all the changes that we applied in this branch.

if we want to bring back some changes deleted
#### git reset --hard "hash" 
- to bring back the head to a commit

reflog can work well when we need to bring back deleted branch
for ex:
#### git checkout -b feature
#### git add .
#### git commit -m "added a file"
#### git switch master
#### git brnach -D feature

now the branch is deleted.
#### git reflog

to recreate the branch we need two steps:
1. take the hash value of the change/commit that we did in feature branch
git checkout "hash" - checkout to that commit (basically detached head will form)
2. create a branch with either switch or checkout command
git swtich -c feature / git checkout -b feature

after this changes will be back with new branch




MERGES - fast-forward and Non-fastforward
1. fast-forward merge - is done when there is no additional commit in master branch after feature branch was created. this merge moves HEAD forward but does not create new commit.
simply switching to master/main branch and merging feature branch will work.
#### git switch master
#### git merge feature

to go back to inital state we need to go back to a specific commit in master but in feature those commits will still stay the same.
#### git reset --hard HEAD~{number}

we can use --squash, which collects all the commits in feature branch which doesn't belong to master and create a single commit for all those changes. But we need to commit these changes by ourself after using the merge --squash command
#### git merge --squash feature
#### git commmit -m "message"
#### git log 
- to check what happened there

2. No-fast-forward merge (Recursive merge) - it used normally when both branches have differnet commit after base commit
git merge --no-ff "branch" - after merging an additional commit was created in master branch we can check that with git log
if we want to go back to previous state we just need hard rest only one commit that is the latest merge commit by using command 'git reset --hard HEAD~1'
we can squash command for the commit as well which will collect all the commits of feature branch into single commit but we have to commit it by ouself
#### git merge --squash merge
#### git commit -m "message(merged master and feature)"





REBASE:
rebase does not move commit but instead it create new commits with same content in the branch without having merge commits.
let m2 be the base commit for master and feature branches. m3 is latest commit in master and f1 and f2 in feature.
so now if we use rebase command while present on feature branch, firstly it will create m3 to be the base commit for both branches and then add f1 and f2 over it but as commits with new hash value but same content. then we can switch to master branch use merge command to merge feature branch in ff mode.

#### git swtich feature
#### git rebase master 
- (from m1,m2,f1,f2 to m1,m2,m3,f1*,f2* in feature branch) (* means different hash values but same content)
#### git switch master
#### git merge feature 
- (it will be ff merge automatically)

Q. when can we apply rebase command?
A.
1. new commits in master branch while working in feature branch
2. feature relies on additional commits in master branch but it will affect the id of feature commits.
3. when feature is fininshed - implementation into master without merge commit (rebase master into feature, merge (in ff mode) feature into master)


Conflicts in MERGE:
#### git merge --abort 
- can be used to undo merge command when we have conflicts while merging.
otherwise we can just fix conflicts and commmit and it will create a merge commit in master branch at the end.


Cherry-Picking: with this method we can use the changes of the specific commit without including other commits. ex - if we have a typo in some txt file in master branch, and we created a new branch for new feature and then we worked on that feature branch with few commits. suddenly realising that there is a typo mistake in some txt file and we fixed it (and commit it). and worked on our features in that ffeature branch. and with cherry picking method we can resilve that issue.

#### git cherry-pic "commit_id(hash)" 
- although it will fix the issue but will create a new commit with different id(hash).



TAGS : are used to tag important stages in history
1. lightweight tag - a pointer towards a commit in a branch like (HEAD in a branch)
2. annotated tag - it can have information like email of the person who commited

to get all the tags
#### git tag

to add a lightweight tag (if we dont specifiy commit_id then it will tag latest commit)
#### git tag 1.0 "commit_id"

#### git show 1.0 
- allows us to show the details linked to that tag

to delete a tag
#### git tag -d 1.0


to add a annotated tag (if we dont specifiy commit_id then it will tag latest commit)
#### git tag -a 2.0 "commit_id" -m "message"




##### readme u.11
