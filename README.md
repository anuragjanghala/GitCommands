# GitCommands

####.git is the hidden repository in working directory which has staging area and commits

###Basic Git Commands:

git init - to initialize .git repository in working directory

git status - to get some inportant information about files in the directory

git add file_name - to add an untracked file to staging area

git add . - to add all untracked files to staging area

git commit -m "message - (first commit)" - to commit new changes linked to files

- To authourize with your identity so that other people know who created any changes or commits
git config --global user.email "you@email.com"
git config --global user.name "your name"

git log - to get all the information about commits in that specific branch


- Checkout is used to move around branches and commits
git checkout commit_id - to go to a particular commit

git checkout branch_name - to go to a particular branch

- Branches
git branch - will show all branches and current branch with asterisk on it

git branch "branch-name" - it will create a new branch with name "branch-name"

git checkout -b "branch-name" - it will create a new branch and move us to that branch(we can check that using "git branch" command)

- Merges : if a branch is ahead of main branch and we want to add merge its changes to main branch
git merge "branch-name" - if we want to merge we should checkout to that branch on which we want to merge and then merge from "branch-name"

- if we use 'git log', we see
- commit id (Head -> main, second-branch) : in which this head points to the lastest commit of current branch
- if we checkout to a commit using commit_id then it will show us detached head (check that using 'git branch' after checkout to commit)
