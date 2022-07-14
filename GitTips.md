# Git Tips

1. check local modification

      1. `git stash` temporally store modification in stash.
      2. `git stash pop` restore modification from stash.
      3. `git checkout .` cancel all local modification.
      4. `git reset --hard HASH` reset to certain `HASH` commit, losing all local modification.
2. `ssh -T git@github.com` test your ssh connection with github.
3. for certain case: you may need to last commitment ;create another branch, then go back to master branch`git cherry-pick <commit id>`
    1. `git cherry-pick` is a powerful command that enables arbitrary git commits to be picked by reference and appended to the current working branch HEAD. It is the act of picking commit from a branch and applying it to another branch.
4. show your git remote repository
    1. `git remote -v` or `git remote show orgin`
5. modified git commit comments
    1. if you just want to modify the comment that you just committed.
        1. `git commit --amend` (please use vim as default in terminal)
        2. `git push -f`

    2. if you just want to modify the last $N^{th}$ comment that you just committed.
        1. `git rebase -i HEAD~N` first you go back
        2. modify the comment and replace `pick` with `edit` in corresponding line
        3. `git commit --amend` do it again
        4. `git rebase --continue` you can come back now
        5. `git push -f`

    3. if you have local modification, try `git stash` (to archive modifications) and `git stash pop` (restore)


