
1. Describe what is the output of the following commands



```
   git branch list the branches in current repo.
   git checkout BRANCH_NAME lets us to go to the branch with the name BRANCH_NAME 
   git log --decorate shows us the structure of the commits 
```
2. Try `git log --graph --all` to see the commit tree. What do you see?
```
It shows all the latest commits to the branches nicely

```
3. Use git diff BRANCH_NAME to view the differences from a branch and the current branch. Summarize the difference from master to the other branch.
```
The green lines are in the current branch (master), and the red lines are in the other branch not in the current branch. 
```
4. Write a command sequence to merge the non-master branch into `master`

```
git merge BRANCH_NAME

```


5. Write a command (or sequence) to (i) create a new branch called math (from the master) and (ii) change to this branch 
(yes, math is already there, just report what you've done, the error and the reason you got the error. If you deleted and recreated the branch, you are fine too)

```
git branch math
git checkout math


```
   
6. Edit B.py adding the following source code below the content you have there
```
print 'I know math, look:'
print 2+2
```

7. Write a command (or sequence) to commit your changes
```
git add B.py
git commit -m "change made"

```

8. Change back to the `master` branch and change B.py adding the following source code (commit your change to `master`):
```
print 'hello world!'
```

9. Write a command sequence to merge the `math` branch into `master` and describe what happened
```
git merge math
There happens a conflict and to avoid the conflict I have to change the file manually.

```
   
10. Write a set of commands to abort the merge
```
git merge --abort

```
   
11. Now repeat item 9, but proceed with the manual merge (Editing B.py). All implemented methods are needed. Explain your procedure
```
 I opened the B.py in editor and deleted 2 lines and then use add command and merge command in git, To avoid conflict

```

12. Write a command (or set of commands) to proceed with the merge and make `master` branch up-to-date
```
git add B.py
git commit -m "conflict  in mergin solved"

```

Report your experience of making this submission, including the steps followed, commands used, and hurdles faced (within the file you created for the **Part 1**.
```
It wasn't hard. It is the first time I am using git though. 
```
