# Git

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

