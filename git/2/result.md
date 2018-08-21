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