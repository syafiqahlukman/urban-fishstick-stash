# urban-fishstick-stash

Demonstration on how git stash works and when you can actually use it

Firstly, I created a repository in GitHub and I use git clone to have a copy of the repository in my local computer
Then I initialize the git repository using ```git init``` so that Git can track any changes done in this repo

Then I create a new file, add content into it, adds it to the staging area, and commit to the repository
```
 echo "Initial content" > stash.txt
 git add stash.txt
 git commit -m "Initial commit"
```

Let say now I want to work on a new feature. So, for isolation from the main branch, I created a new branch to experiment on the new feature
```
 git checkout -b Feature1
 echo "In this branch, I would like to work on this new feature" >> stash.txt
 git add stash.txt
 git commit -m "Work in progress to add new feature"
```

Then suddenly I got and idea where I need to add something in the main branch. So I switch to main branch and work on it
However, I am not sure yet wether to commit this new feature or not. So I didnt stages the changes yet nor commit it
```
 git checkout main
 echo "Back in main branch to add something that I forgot during inital commit. But I am not sure yet wether this need to be added or not, yet" suddenly got issue on branch Feature1 that need to be fixed" >> stash.txt
```

Then suddenly there's issue on the branch Feature1 that needs me to qucikly fix it. So I switch to branch Feature1
```
git checkout Feature1
```
After I run this command, there will be an error
```
error: Your local changes to the following files would be overwritten by checkout:
	stash.txt
Please commit your changes or stash them before you switch branches.
Aborting
```
This error is because Git prevents the switch to protect my work in progress on the main branch. The changes I made to stash.txt on main branch are not committed yet, and switching to Feature1 branch would require merging these changes into Feature1 branch (which might not be what I want because I have not completed working on the new feature yet) or discarding them (this also might not be what I want because it will lead to potential data loss)

So to handle this situation and proceed to fix in Feature1 branch, I can stash my uncommitted changes on main branch using the command 
```
git stash push -m "Work in progress: main branch"
Saved working directory and index state On main: Work in progress: main branch
```

Then now I am able to switch to branch Feature1 and fix the issue
```
 git checkout Feature1
 echo "The bug is fixed" >> stash.txt
 git add stash.txt
 git commit -m "Fix applied"
```

Then, after commiting the fix in branch Feature1, I can switch back to main branch and continue to work on the idea that I have just now
```
 git checkout main
 git stash pop
 echo "Now I am ready to commit this to main" >> stash.txt
 git add stash.txt
 git commit -m "Update on main"
```

And finally, we need to merge both branch by using VS Code and choose ```Accept Both Changes```

Then, stage the changes that have been made after resolving the merge conflict, then commit it
```
 git add stash.txt
 git commit -m "Resolve merge conflicts"
```
Last but not least, push to remote repository 





