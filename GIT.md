GIT cheat sheet
===


General aspects
-----------------
```
git help  or  git  --help
git help <command>

git status

git log
git log -p <file>         #history for a given file

exit

```
Comments to the commits:
- the Pandas project uses various three-letter keys to indicate the type of commit, such as (ENH)ancement, BUG, and (DOC)umentation.


Local repos
-----------
```
git init                  #create repo

git add <file>            #stage file
git add .                 #adds all new files
git add -u                #updates tracking for deleted or renamed files
git add -A                # same as previous two ones

git commit -m "message"   #commit to local repo
git commit -a             #automatically stage tracked files that have been modified or deleted

git diff                  #changes in working directory not yet staged for a commit.
git diff --cached         #changes that are  staged

git tag <tag>             #mark current commit with a tag

```

Undoing things
```
git checkout <commit> <file> #restore local file to a previous 
git checkout master       #return to the most advanced point after chckout of a previous
git checkout HEAD <file>  #restore local files to the last commited state (does not affect new files)commit

git reset HEAD             #make index same as HEAD (discarding staged files)
git reset HEAD <stagedfile>#make index same as HEAD; remove file from the index
git reset --hard <commit>  #discard all local changes permamently

git revert <commit>       #remove given commit from history

git rm --cached <file>    #removes the file from index alone and keeps it in your working copy: exact opposite of git add file

```

Diagram: git data transport commands (by Oliver Steele)
![Git data transport commands (by Oliver Steele)](http://blog.osteele.com/images/2008/git-transport.png)


Branches
--------
```
git branch                #see branches, and what branch you are in
git branch -d brnchname   #delete

git checkout branch       #create or move HEAD to the branch
git checkout master       #switch back to the master

git merge branch          #merge branch into the current branch (typically, master)
git merge --abort

git rebase <branch>       #rebase current HEAD into branch
```


Remote repos
------------

```
git clone ssh://...

git push <branch>         #take local changes to remote repo
git fetch <remote>        #download changes but don't integrate into HEAD
git pull <remote>         #download changes and integrate/merge into HEAD

git remote add origin https://github.com/... : links local to remote repo
git remote -v             #list configured remotes
git remote show <remote>  #
```


Git configuration
-----------------

```
git config --global user.name "name"
git config --global user.email "email"
git config --global core.editor "nano"
git config --list

```

---


Github
------

 - Fork another user's repo: creates a copy of their repo; can clone into your local desktop
 - Pull request


---

References
-----------
 - Diagram by Oliver Steele: http://blog.osteele.com/images/2008/git-transport.png
 - http://www.git-tower.com/blog/git-cheat-sheet/
 - http://git-scm.com/book/en/v2
