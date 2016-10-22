GIT
====


Configuring git
===============

git stores configuration at three levels.

1. System : 
    
     git config --system

2.  User: 

     git config --global

3.  from project to project : 

     git config 

To configure properties at any level 

 git config --global propertyname propertyvalue

 Ex: git config --global user.name "satya"

     git config --global user.email "$userEmail"

     git config --list # list the all the configuration properties set

     git config --list propertyname #gives the propertyvalue of the property name


These files are stored in .gitconfig at global level.

To use colors in git:

      git config --global color.ui true



git init #initiate the git repository

git log #show the commit history

git log -n $No #shows only recent $No of commits.

git log --since=2016-06-15 #shows the commits since that date

git log --until=2016-06-14 #show the commits until that date

git log --author="kevin" #show the commits made by kevin

git log --grep="Init" #shows the commits filtered with grep expression



Git Key Concepts 
-----------------

 There are three stages

    1. repository

    2. Staging index

    3. working 


 push changes 3 ---> 2--->1

 pull changes 1--------->3




 git add $fileName #pushes the file to the staging index

 git commit -m "This is the commit message " #pushes to the repository

 
 HEAD pointer
 
 =============

point to the tip of the current branch in the "repository" not in the staging index or working.

It refers to what was the last checked out in the repository

points to the parent of the next commit.
  


Commands

========

git status # reports the difference between working  directory, staging index and repository

touch second.txt third.txt


 git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	second.txt
	third.txt

nothing added to commit but untracked files present (use "git add" to track)



git add $fileName # add the file to the staging index

git add . #adds all the files in the present directory 


git diff $fileName # shows the differences between the file that is in repository(where the head is pointing at) vs the one with working directory


--- ==> old version
+++ ==> new version


git diff --staged $fileName #shows the differences between the file in staging index and in the repository

git diff --color-word $fileName #shows the differences side by side between the file in the repository and working directory  

git rm $fileName #removes the file from the working directory completely(without moving to trash directory)

git add $fileName 

git commit -m "remove the file $fileName"

git mv $fileName $renameFile #renames the file from fileName to renameFile


git add $renameFile

git commit -m "rename the file $renameFileName"


 git diff contact.html
diff --git a/contact.html b/contact.html
index fd9eb7a..8291d24 100644
--- a/contact.html
+++ b/contact.html
@@ -104,7 +104,7 @@
                                                free to call us at<span class="phone"> <strong>866.555.4310</strong>.
                                                        Please note that this is not the support line, for support you
                                                        could call
-                                               </span><strong>866.555.4315</strong>. Thanks for getting in touch!
+                                               </span><strong>866.555.4314</strong>. Thanks for getting in touch!
                                        </p>
                                </div>
 
@@ -345,7 +345,7 @@
                                        5605 Nota Street<br /> Ventura, CA 93003
                                </p>
                                <p>
-                                       866.555.4310<br />866.555.4315 <em>(24 hour support)</em>
+                                       866.555.4310<br />866.555.4314 <em>(24 hour support)</em>
                                </p>
                        </div>
                </div>




Undo the changes for an older version

======================================

git checkout -- $fileName #go to the repository and look for fileName in the repository and make that particular file in working directory just like the file in the repository

git reset HEAD $fileName #go look to the Head pointer, go look at the fileName in the repository and set the same file in staging area to that of corresponding file in repository

Ammending commits

=================

git commit --amend $commitMessage  #modify the latest Commit that we made at last with this commit that we are going to make now.


Retrieving old version of the file

=====================================

git checkout $SHA_OF_OLD_COMMIT $fileName #checkout from a particular revision will put into a staged index. 

git reset HEAD $fileName # then put that particular old version file to the working directory


Revert Command

===============

git revert $HEAD_REV_NAME #Reverts the HEAD_REV_NAME to its previous version

git revert 68c3a395df4eb648d7744e0f2e0467e051b2246a #Reverts the head which is 68c3a395df4eb648d7744e0f2e0467e051b2246a to its previous version

it opens an notepad and asks us for the commit message and once we save it it automatically revert the working directory and repository to the previous version.

git revert -n 68c3a395df4eb648d7744e0f2e0467e051b2246a #Reverts the head which is 68c3a395df4eb648d7744e0f2e0467e051b2246a to its previous version but put the changes to staging index.


Using reset to undo multiple commits

=====================================

git reset #rewind back to previous commit and then start recording from there now on. It always move the head pointer.

  --soft : moves the head pointer to specific commit and doesn't change staging index or working directory at the same time. It is safest of all options.
           Thus what ever we have in the staging index/working directory is the latest one and that of in repository is the oldest one.

  --mixed: head pointer to the specific commit and also changes the staging index to match with the repository and doesn't change the working directory.

  --hard: moves not only the head pointer of the repository but also make sure that staging index and working directory matches the repository as well.

git reset --soft $oldCommitId

git reset --mixed $oldCommitId

On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   resources.html

no changes added to commit (use "git add" and/or "git commit -a")
 
 git reset --hard $oldCommitId 


 Remove untracked files

======================

Remove all the files that are not in the repository.


 git clean -n   #dry run to remove the untracked files in the present directory from git

 git clean -f  #forcefully remove the untracked files which are not present in the repository


 Ignore git files globally

=========================

 git config --global core.excludes file $fileName #sets the global ignore to all the projects as per the $fileName

 
 Ignore the files that are already tracked

==========================================
 
 git rm --cached $fileName #will cause the file not being tracked.
 
 
 Track empty directories

========================
 
 By default, git doesn't track empty directories.
 
 touch .gitKeep in the empty directory to keep track of empty directory
 
 
 Referencing commits

====================
 
 tree-ish: 

  it is something used to refer a commit.
  
  A treeish can be following
  
  1. full sha-1 hash
  2. short sha-1 hash
  3. Head pointer
  4. branch reference
  5. tag reference
  6. ancestry
  
  parent commit : commit^
  
  
  head^=head~1
  
  head^^=head~2
  
  
  Explore tree listings

====================
  
  git ls-tree $treeish #will give the list of the files that are available that treeish which is referring to a commit.
  
  
  git ls-tree $treeish $directoryName/ #will give the list of files in that directory that are available at that treeish
  
  
  git ls-tree $treeNumber #will give the files inside the tree(which is nothing but a directory)
  

Getting more from commit log
===============================

git log --oneline #gives oneline description of each commits.

git log --oneline -$n #limits the number of commits to n for display

git log --since="2012-06-20" #gives the commits since that date

git log --until="2012-06-20" #gives commits until that date

git log --since="2 weeks ago" --until="3 days ago" #gives commits since 2 weeks up to 3 days ago

git log --since=2.weeks --until=3.days #gives the commits since 2 weeks up to 3 days ago

git log --author="kevin" #gives the commits made by author kevin

git log --grep="temp" #grep for temp word in the comit messages of log list and return it to the end user

git log $SHA1..$SHA2 # give the log from $SHA1 to $SHA2

git log  $SHA1..$SHA2 $fileName #give me the log that is from $SHA1 to $SHA2

git log -p $SHA1..$SHA2 #show the changes that were made between SHA1 and SHA2

git log --oneline --graph --all --decorate #nice way to see the commits

git log --oneline $fileName

git log $SHA1.. $fileName

viewing commits
===============

git show $SHA #show the changes made in that SHA and show the differences between this SHA 
               and its previous SHA
               
git show $treeNameofDirectory equivalent to git ls-tree $treeIdofDirectory

Comparing commits
=================

git diff $treeIsh

git diff $treeIsh $fileName

git diff $treeIsh1..$treeIsh2

git diff 

git diff --staged

git diff $treeIsh1..$treeIsh2 fileorDirectoryName

git log --oneline

git diff --stat --summary $treeIsh1..$treeIsh2

git diff -b -w $treeIsh1..$treeIsh2


Branches
=========

git branch #shows list of branches in current repository

git branch $newBranch #creates new branch.

git checkout $branchName #switch to the branch with branchName

git checkout -b $branchName #create and checkout this branch 

Compare branches
================

git diff $treeish1..$treeish2 #Each treeish can be branch name or the ancestor of the branch name

git branch --merged #check if the current branch include all the changes of other branch, if not we need to merge it.

Rename branches
===============

git branch --move $branchName $newBranchName #rename the current branch to new Branch

git branch --delete $branchName #deletes the current branch name 

Note: you should not be on the same branch that you are deleting it.
 
git branch -D $branchName #delete the branch name forcefully


Configure command prompt to show up the branch
==============================================

see the .bashrc file


Merge the branches
==================

To merge the branch 'a' with branch 'b'

git checkout b

git merge a

git merge --no-ff branchName #forces git not to do fast forward merge

git merge --ff-only branchName #forces git to do a merge only if it can do a fast forward merge

to resolve the merge conflicts, do the manual way to remove the conflicts.

git merge $b #to merge b on to a


Saving changes to stash
=========================

git stash save "$Message" #changes are stashed in and it is not an actual messages

git stash list #shows the items in the stash

git stash show $StashName #show the information about the item in the stash

ex: git stash stash@{0} #show the information about stash@{0} 

git stash show -p $stashName #give more details about the stash item  

Retrieving stashed changes
===========================

git stash apply $stashItem #will apply the stash changes in the current directory and keep a copy of it in the stash

git stash pop $stashItem #will apply stash changes and remove the item from the stash area

git stash drop $stashItem #will delete the stashItem in the list

git stash clear #clear all the items in the stash


Remotes
=======
git remote # lists all the remote branches

git remote add $alias $url 

where $alias is the alias of the URL
and $url is the url of the repository in the github

git remote rm $alias #removes the alias

git push -u $alias $branchName #push up the branchName to the remote branch through alias

git branch -r #show the remote branches

git branch -a #show all the branches

git clone  $remoteRepositoryURL #clone the remote repository locally with remote repository name from default branch

git clone $remoteRepositoryURL $directory #clone the remote repository locally with the directory name from default branch

git clone -b $remoteRepositoryURL $branchName #clone the remote repository locally from the specified branch

for non tracking branch push

git push $alias $branchName

if we want to track non tracking branch then

git config branch.$branchname.remote 

git config branch.$branchName.merge refs/heads/$branchName 

--------------
git push #push changes to the tracking branch

git fetch #fetch changes from remote repository

git pull #git fetch + git push

git branch $newBranchName $pointtoBranch #creates a new branch from pointtoBranch

git branch myChange origin/master #creates a new branch from origin/master branch

git checkout myChange #switch to myChange branch

git push $alias $localBranch:$remoteBranchName #push changes from localBranch to remoteBranch

git push origin non_tracking:non_tracking #push changes from non_tracking local to non_tracking remote

git push origin :non_tracking #delete the non tracking branch in git remote repository

git push $alias --delete $branchName #delete the non tracking branch in git remote repository


Daily Routine
============

git checkout master

git fetch

git merge origin/master

git checkout -b feedback_form

git add feedback.html

git commit -m "Add feedback form"

git fetch

git push-u origin fedback_form

 
Tools
=====

git config --global alias.$shortcutName $commandName #set the alias for the commandname



