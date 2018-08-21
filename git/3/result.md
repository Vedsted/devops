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