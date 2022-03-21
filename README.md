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
#### git clean 
-df - to delete




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
