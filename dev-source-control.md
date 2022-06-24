# source control

## git

- foss, written in shell + c
- text ui: tig, lazygit

- useful commands
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

  - stage changed files with detecting renamed ones
    > git -A add .
  
  - register nccommit alias
    > git config --global alias.nccommit 'commit -a --allow-empty-message -m ""'

  - hard reset to previous commit
    > git log
    > git reset --hard <commit>


## mercurial

- foss, written in python
- repository https://www.mercurial-scm.org/repo/hg/


## servers

- gitlab (foss)
- gitea (foss)
- bitbucket server