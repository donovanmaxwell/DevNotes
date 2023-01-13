# **GIT**

Version Control System  
[Git Website] (https://git-scm.com)  

### **Branches**  
By default, all code is located on **master** branch. Can think of branches as different files. Allows working on one file without affecting a different file.Branches can later be merged to combine their code.

Point to branches: Multiple collaborators can work on a project, each working on separeate branches, and merge changes once complete into main branch, all while allowing work to be done independently on other branches.

### **Workflow Analogy:** 
Commits are storage boxes. Commits represent sealed changes, like a box containing items to be stored. Things get put into boxes, labeled, and sent somewhere to be stored. 
1. Select items to be stored `git add [box]`
2. Put items into box, label the box, and seal it `git commit -m "label"`
3. Send box to storage location `git push`  

### **Pull Requests**
A "pull request" (essentially a request to merge) is not the same as the "pull" commmand (which retrieves the latest version from the remote repo).

A "pull request" is basically a note (request) to others to notify the that you have made changes on a branch and want (request) those changes be merged into the main or other relevant branch. Merges to relevant branch usually happen, if approved, after a short discussion & quality check & inspection of updated code.

## **Commands**  

### **Setup & Initialize**  
  
Clone A Project  
`git clone [url]`

Initialize Folder/Project  
`git init`

### **Stages & Snapshots**  
  
Add a file as it looks now to next commit (stage)  
`git add [file]`  
`git add .` adds everything

Commit staged content as new commit snapshot  
`git commit -m 'helpful message goes here'`  

### **Branches & Merging**  

List branches  
`git branch`  
  
Switch to another branch & check it out to your working directly  
`git checkout`  
`git checkout [hash code]` checkout as specific point in history to working directory  

Create new branch named main  
`git branch -M main`  

Create new branch  
`git checkout -b new-branch`  

Rename local *master* branch into *main*  
`git branch --move master main`

### **Share & Update**  

Add a git URL as an alias  
`git remote add origin [URL]`

Fetch and merge any commits from the tracking remote branch  
`git pull origin master`  

### **Inspect & Compare**  
  
Show commit history for currently active branch  
`git log` *can use hash codes found here in 'git checkout' command to restore one of these points*  

## **Procedures**

### **Changing Master Branch Name**  
Example: Change Master to Main
1. Rename local *master* branch into *main*  
`git branch --move master main`
2. Push new branch to remote so branch is available and visible  
   `git push --set-upstream origin main`  
    *Remote will still show a master branch and other collaborators will still be able to use the master branch.*
3. Complete following tasks to remove any references to master branch:
    - Any projects that depend on this one will need to update their code and/or configuration
    - Update any test-runner config files
    - Adjust build & release scripts
    - Redirect settings on your repo host for things like the repo's default branch, merge rules, and other things that match branch names
    - Update references to the old branch in documentation
4. Once Step 3 tasks are complete, can delete master branch.  
`git push origin --delete master`

