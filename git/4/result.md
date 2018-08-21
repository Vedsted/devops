# task 4

#### commands
* git log --graph --oneline
* git status
* git checkout
* git reset
* git revert

#### steps
1. 


#### result
```
* 8592d0c (HEAD -> master) Revert "Add bad content to afile.txt"
* b53d4cc Add bad content to afile.txt
* ee67078 first commit
```

#### questions
* *describe what you are seeing in the repository.*
    * the master branch contains a file that has been staged and edited again, wich results in the following ```git status``` output:

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
    * the following command moves the changes from the staging area back to the workspace area: ```git reset afile.txt```. There after the following command will discard all changes in the workspace: ```git checkout afile.txt```


* *make master go back to the commit before the bad commit*
    * the following command reverts the master branch back one commit. This results in the bad commit being removed: ```git revert master```


* *does git track bfile.txt? Reason your answer.*
    * No.  The .gitignore file clearly states that the bfile.txt is ignored.  
    ```
    $ cat .gitignore
    bfile.txt
    ```