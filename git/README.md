# Git exercises

To make each assignment, run the `setup.sh` file and examine the git repository in the `exercise` folder.

You need to provide the git commands you need to solve the task, as well as a copy of the following command from each repository:

`git log --oneline --graph --decorate --all`

# 1

The git commit history looks like a developers internal "I gotta save this" work. Not suited for public.
All work belongs to a task called "#321"

### Task

1. _Squash_ the five relevant commits into one, with the commit message of "close #321"
1. How does `git log` look now?

<br>

### Solution

To solve the problem, an interactive rebase is made with the first commit. The commits are sqashed into one and thereafter commited as one with a new commit message.  

#### steps

1. find the commit rebase on:  
```git log --oneline```  

2. rebase on commit:  
```git rebase -i 5905DFD```

3. pick a commit and squash the rest

4. commit with the new commit message: "close #321"

#### commands used

* git log --oneline
* git rebase -i  \<sha-1>


#### log result

```bash
Vedsted@DESKTOP-5ERSC7Q MINGW64 ~/Desktop/DevOps/git/1/exercise (master)
$ git flog
* 75b19b1 (HEAD -> master) Close #321
* 3c2afd6 initial file
```


<br><br>

# 2

You develop a new feature on the branch `new-feature`. You have already
implemented the first part of a feature, when you are notified of a critical
bug that has to be fixed right away on the `master` branch.

After the bug fix, you continue to work on the new feature. After you committed the second part of the feature, you realize that you have done your commit on the `master` branch instead of the feature branch.

### Task

1. Move the faulty commit from the `master` branch to the `new-feature` branch.
1. Copy the bugfix to your feature branch as well

<br>

### Solution

To solve the problem, the master branch is rebased onto the new-feature branch. This results in a merge problem that needs to be fixed.  

#### steps
1. change to the new-feature branch  
```git checkout new-feature```
2. rebase the master branch into the new-feature branch  
```git rebase master```
3. fix merge problem in myapp.txt and continue the rebase (commit the changes)  
```git rebase --continue```
4. change back to the master branch  
```git checkout master```
5. revert master to before the wrong commit  
```git revert HEAD``` OR ```git revert master```


#### commands used
* git checkout
* git rebase master
  * --continue 
* git revert HEAD
* git status
* git branch
* git log --oneline --graph

#### log result
```bash
* 8bf600c (master) Revert "Implement second part of feature"
| * 2e15dfb (HEAD -> new-feature) Implement first part of feature
|/
* 45a21a7 Implement second part of feature
* f42bec7 Fix bug
* b532231 Initial commit
```

<br>

# 3

You have developed a new feature, and wants to commit it to master:

```bash
* 1f37b43 (HEAD -> master) Add readme
| * a824913 (uppercase) Change greeting to uppercase
|/  
* b84f28f Add content to greeting.txt
* efb74a6 Add file greeting.txt
```

Instead of just merging the commit, you like a straight line of commits like the example below

```bash
* 47558e0 (HEAD -> uppercase) Change greeting to uppercase
* 1f37b43 (master) Add readme
* b84f28f Add content to greeting.txt
* efb74a6 Add file greeting.txt
```

### Task

* Show the commands in order to achieve this position of commits.
* Why does the commit with message "Change greeting to uppercase" change sha, when the others do not?

<br>


### Solution

To solve the problem, the master branch is merged onto the feature branch. This ensures a straight graph in the log. If it's desired to merge the feature branch into the master branch, then a fast-forward merge is now possible.

#### steps
* switch to the feature branch  
```git checkout feature```
* rebase the master branch onto the feature branch  
```git rebase master```

*if it's desired to merge the changes from the feature branch into the master branch, do the following*:
* switch to the master branch  
```git checkout master```
* merge the feature into master  
```git merge feature```

#### commands
* git checkoutfeature
* git rebase master
* git status
* git log
* git merge


#### log result
```bash
* 709d53d (HEAD -> feature) Change greeting to uppercase
* cd33227 (master) Add readme
* 4f23a42 Add content to greeting.txt
* 29cd11f Add file greeting.txt

```

#### questions
* *Why does the commit with message "Change greeting to uppercase" change sha, when the others do not?*
    * the rebase applies the changes from the master branch to the feature branch, resulting in a new commit with a new sha-1.

<br>

# 4

Look at the git graph and status of the created repository to find out the state.

### Task

* In words, describe what you are seeing in the repository. Use the git terminology when applicable.

Show the list of commands you need to do the following (in the given order).

* remove the work in progress using git.
* remove the staged change
* make master go back to the commit before the bad commit
* does git track bfile.txt? Reason your answer. 

<br>


### Solution

The first thing to see in this repo's log, is that a file has been edited, staged and then edited again.

#### commands
* git log --graph --oneline
* git status
* git checkout
* git reset
* git revert
* cat

#### log result
```bash
* 8592d0c (HEAD -> master) Revert "Add bad content to afile.txt"
* b53d4cc Add bad content to afile.txt
* ee67078 first commit
```

#### questions
* *describe what you are seeing in the repository.*
    * the master branch contains a file that has been staged and edited again, which results in the following ```git status``` output:

```bash
    On branch master
    Changes to be committed:
        (use "git reset HEAD <file>..." to unstage)

            modified:   afile.txt

    Changes not staged for commit:
        (use "git add <file>..." to update what will be committed)
        (use "git checkout -- <file>..." to discard changes in   working directory)

            modified:   afile.txt

```

* *remove the work in progress using git.*
    * the command below, removes the changes in the workspace:  
    ```git checkout afile.txt```


* *remove the staged change*
    * the command below, moves the changes from the staging area back to the workspace area:  '
    ```git reset afile.txt```    
    There after will the next command discard all changes in the workspace:  
    ```git checkout afile.txt```


* *make master go back to the commit before the bad commit*
    * the command below, reverts the master branch back one commit. This results in the bad commit being removed:  
    ```git revert master```


* *does git track bfile.txt? Reason your answer.*
    * No.  The .gitignore file clearly states that the bfile.txt is ignored. Below is a 'cat' of the .gitignore file:    
```
$ cat .gitignore
bfile.txt
```



