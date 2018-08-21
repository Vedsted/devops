# task 1

#### commands used

* git log --oneline
* git rebase -i  \<sha-1>


#### steps

1. find the commit rebase on:  
```git log --oneline```  

2. rebase on commit:  
```git rebase -i 5905DFD```

3. pick a commit and squash the rest

4. commit with the new commit message: "close #321"


#### log result

```
Vedsted@DESKTOP-5ERSC7Q MINGW64 ~/Desktop/DevOps/git/1/exercise (master)
$ git flog
* 75b19b1 (HEAD -> master) Close #321
* 3c2afd6 initial file
```


<br><br>
# task 2


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



<br><br>
# task 3

#### commands
* git checkoutfeature
* git rebase master
* git status
* git log
* git merge

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


#### log result
```bash
* 709d53d (HEAD -> feature) Change greeting to uppercase
* cd33227 (master) Add readme
* 4f23a42 Add content to greeting.txt
* 29cd11f Add file greeting.txt

```

#### questions
* *Show the commands in order to achieve this position of commits.*
    * see steps section

* *Why does the commit with message "Change greeting to uppercase" change sha, when the others do not?*
    * the rebase applies the changes from the master branch to the feature branch, resulting in a new commit with a new sha-1 



<br><br>
# task 4

#### commands
* git log --graph --oneline
* git status
* git checkout
* git reset
* git revert
* cat

#### result
```
* 8592d0c (HEAD -> master) Revert "Add bad content to afile.txt"
* b53d4cc Add bad content to afile.txt
* ee67078 first commit
```

#### questions
* *describe what you are seeing in the repository.*
    * the master branch contains a file that has been staged and edited again, which results in the following ```git status``` output:

    ```
    On branch master
    Changes to be committed:
        (use "git reset HEAD <file>..." to unstage)

            modified:   afile.txt

    Changes not staged for commit:
        (use "git add <file>..." to update what will be committed)
        (use "git checkout -- <file>..." to discard changes in working directory)

            modified:   afile.txt
    ```

* *remove the work in progress using git.*
    * the following command removes the changes in the workspace: ```git checkout afile.txt```


* *remove the staged change*
    * the following command moves the changes from the staging area back to the workspace area: ```git reset afile.txt```.  
    There after the following command will discard all changes in the workspace: ```git checkout afile.txt```


* *make master go back to the commit before the bad commit*
    * the following command reverts the master branch back one commit. This results in the bad commit being removed: ```git revert master```


* *does git track bfile.txt? Reason your answer.*
    * No.  The .gitignore file clearly states that the bfile.txt is ignored.  
    ```
    $ cat .gitignore
    bfile.txt
    ```



