# source control

## git

- foss, written in shell + c
- text ui: tig, lazygit

- useful commands
  - checkout remote feature branch
    > git checkout --track origin/feature/<name>
  - switch to another existing local branch
  - list branches
    > git branch
    > git branch -r  # list remote branches
  - switch to another existing branch
    > git checkout <name>
  - git checkout local branch
    > git checkout --track origin/feat/ryan-devcontainer
  - create new branch
    > git checkout -b <name>
  - merge changes from upstream origin/main branch
    > git fetch                 # fetch changes from remote branches
    > git merge origin/main 
  - delete branch
    > git branch -d <name>      # removes branch locally
    > git push origin -d <name> # removes branch on a remote
  - push local branch to remote for the first time
    > git push --set-upstream origin <name>

  - recursively update to latest version
    - will use submodule's parent repository to determine specific commit in a child
      > git pull --recurse-submodules
    - will use submodule's latest commit of default branch
      > git submodule foreach --recursive git pull  
  
  - show log and commit details
    > git log
    > git show <hash>

  - amend last commit
    > git commit --amend -m'message'

  - list all git lfs files 
    > git lfs ls-files --all

  - prune lfs cache
    > git lfs prune

  - stage changed files with detecting renamed ones
    > git -A add .
  
  - register nccommit alias
    > git config --global alias.nccommit 'commit -a --allow-empty-message -m ""'

  - hard reset 
    - to previous commit
      > git log
      > git reset --hard <commit>
    - to remote origin
      > git fetch origin
      > git reset --hard origin/<branch>

  - stash/unstash changes
    > git stash
    > git stash pop

  - get repo size
    > git count-objects -vH | grep 'size-pack'


## mercurial

- foss, written in python
- repository https://www.mercurial-scm.org/repo/hg/


## svn

- migrate svn repository to git


## servers

- gitlab (foss)
  - problems observed
    - 'pipeline run details' page sometimes doesn't get updated during run
      - so that task may be finished by still displayed as pending
      - need to refresh the page to update

- gitea (foss)
- bitbucket server


## branching strategies

- trunk-based development
  - everyone commits to a main branch and that thing goes to production
- feature branches or github flow
  - work performed in feature branches and then PRs a issued into main
- forking
  - pull requests from forked repo to main repo
  - open source projects
- release branches
  - teams work on specific releases in separate release branches
- gitflow
  - main always has same code as in production
  - develop is integration branch
  - feature branches created from develop and merged back into it
  - release branches created from develop and hotfixes applied there
- environment branches
  - its like gitflow, but with additional branhces for specific environments
