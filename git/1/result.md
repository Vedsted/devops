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