

git config --global user.name "Username"
git config --email user.email "Email"

Git commands
************
cd-change directory
 syntax---cd "filename"

>git clone <repo link>-bring a repository that is hosted somewhere like Github into folder on your local machine.

>add-track your files and changes in Git(putting all the changed files in a staged area).
--git add . -->to add all the files thats changed
--git add filename-->to add the changes in a specific filename.

>git commit -m "<Message>"-save ur files in Git.(-m means message)

------>[we can also use git commit -am "<message>"-->it will (a->add,m->message) stage and commit at the same time.
**this will only work if the file is just modified not created.**]

>git status -to check what changes we make is applied or not.

>git checkout -b <branchname> -create a new separate branch from the master branch

>git checkout master -it is just to move to the master branch from the new branch. 

>**first be on the master branch** then enter
 git merge <branch name>


>****push-upload Git commits to a remote repo like Github.****
>git remote add origin <remote URL from github> --this will connect git local with the git remote repository.

***before pushing to remote repository please verify that we are in master branch*** 
>git push -u origin master -to push the files in our local repo to the remote repo.
	[the "-u" is knowm as "upstream" as it sets the origin master as default]

>pull-download changes from remote repo to your local machine,the opposite of push.
>git pull origin master-it will pull the changes from remote repo to local repo (origin(where) from master branch).

>git push origin <branch name>-to push a branch to the remote repo.
**first we need to move to the branch then use the above command.

>git remote -v --->it showes any remote repositories that i have connected to this repo.

>git diff --->it showes all the changes i have made.

>git branch -d <branch> ---this will delete the branch.

>git reset <hash code>---it will remove that perticular commit from the staged area.
         OR
 git reset <file name>---here it will remove the file with the given name  from the staged area.
          OR
 git reset -- hard <hashcode>----it will not only remove the file from the staged area but also delete it permanently.

>change the origin link----->git remote set-url origin <link>
git questions
-------------
1>What is the command to write a commit message in Git?
  --->git commit -m "message"
2>How will you squash the last N commits into a single commit?

3>In Git how do you revert a commit that has already been pushed and made public?
---->To do this, first identify the commit you want to revert using the `git log` command and note down its hash. 
Then use the `git revert` command followed by the commit hash, which will create a new commit that undoes those 
changes. Finally, push these changes to your remote repository with the `git push` command.

4>What is the difference between git pull and git fetch?
-->git pull-downloads the changes in the remote repositories and merge those changes and store them in the local repositories.

5>why do we use git init?
  Most other Git commands are not available outside of an initialized repository, so this is usually the first command you'll run in a new project. Executing git init creates a . git   
subdirectory in the current working directory, which contains all of the necessary Git metadata for the new repository.