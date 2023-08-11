# Git

- `git pull --rebase origin master` - pull the current branch and rebase it on `master`
- `git branch --force SOME_BRANCH [COMMIT]` - reset a branch to a commit (by default the commit is HEAD)
- `git rebase --onto <newparent> <oldparent> [until]`
    - `git rebase --onto TARGET_BRANCH HEAD~5` - rebase last five commits on TARGET_BRANCH, current branch pointer is set on top
- `git log --oneline ..FETCH_HEAD` - see what's coming the your branch
- `--force-with-lease` - safer option to `--force`
    - it fails when someone else pushed new commits/changed the branch somehow
    - it doesn't fail when you are the only person making changes (rebasing, squashing, changing commit messages) - the remote branch must be somewhere in your Git history