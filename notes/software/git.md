# Git

- `git pull --rebase origin master` - pull the current branch and rebase it on `master`
- `git branch --force SOME_BRANCH [COMMIT]` - reset a branch to a commit (by default the commit is HEAD)
- `git rebase --onto <newparent> <oldparent> [until]`
  - `git rebase --onto TARGET_BRANCH HEAD~5` - rebase last five commits on TARGET_BRANCH, current branch pointer is set on top
- `git log --oneline ..FETCH_HEAD` - see what's coming the your branch 