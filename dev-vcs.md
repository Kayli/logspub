# source control

## git

- foss, written in shell + c
- text ui: tig, lazygit

- useful commands
  - recursively get latest version
    > git pull --recurse-submodules     # may not update submodules to latest branch commit3
    > git submodule update --recursive  

  
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
