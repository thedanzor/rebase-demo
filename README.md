

# Introduction

To summarize the difference between Rebasing and Merging:

**Merging:** Puts changes on top of your branch
**Rebase:** Puts the changes from your target branch underneath the changes in your current branch.

Understanding how this affects git history is very important to avoid problems and confusion.

### What are the benefits of using rebase over merge?

 1. You are not potentially putting older work ontop of newer work, thus not regressing the software or feature backwards in time.
 2. When you are merging you create a 'merge' commit, if there was a conflict with getting this into your branch. The developer who fixes the conflict becomes author to all the changes in all the files, regardless if those files had merge conflicts in them and thus removing a big part of the git history (who authored the change).

### Things to be aware of when using rebase

 1. Rebase changes the history of your local branch, if you're working on a feature and you rebase against dev, all the changes you do not have from dev will appear before the changes in your branch. If you have already pushed your feature to origin, after a rebase you will get git errors when pushing again to origin. Because origin and local have different histories and the hashes of the commits have changed. To resolve this you need to force push to your origin branch, this can be scary and problematic if you're not careful and do not state your correct origin branch.
 2. You cannot as easily rollback from a rebase, when you use merge you can `git reset HEAD~1 --hard` but this wouldn't work with a rebase. You need to use other mechanisms of git or keep origin up-to-date and use that to revert your local branch in the case of a mistake

### Practises to help protect you

1. When you push it's always good to restate the origin branch, even if you're upstream is set correctly. This practises is good thing to get into for when you're working on other peoples branches and when force pushing. - `git push origin <TargetBranch>`

# Task 1 - Rebasing your changes and merging them to master

Lets get used to using rebase and seeing how it works, there is a branch feature/task1 which we will rebase against master and then merge it in.

    `git checkout feature/task1`

    `git rebase -i master`

    `git checkout master`

    `git merge feature/task1`


# Task 2 - Rebasing your changes and resolving the merge conflict

You have now successfully rebased your changes onto of master, then merged them back into the master branch.

We will now `checkout feature/task2` and follow the same steps as above, but this time we will resolve the merge conflict.

##You have successfully rebased and resolved the merge conflicts##

# We are done

This process has shown you the basics of rebase, the important part is understanding the impact and what is happening under the hood - That it is changing the history and the hashes of the commits.

I would advise to make sure important branches like dev / master cannot be pushed too directly - to avoid people accidently force pushing to the wrong branch.

The rebasing of release branches is done no differently then above, but probably best left to people with more experience in rebasing.

Something you can do to make your git workflow easier, is squashing your commits when your done. The history of your changes remains intact but it's then part of bigger and fewer commits - or even a single big commit if you would like.
