# notes related to writing shell scripts

## basics

- shell is a computer program which exposes an operating system's services to a human user or other programs
- popular shells: bash, zsh, fish


## debugging

- enables a mode of the shell where all executed commands are printed to the terminal
  > set -x

- enables a mode of the shell that will make the script exit with an error whenever an error occurs
  > set -e


## bash

- bash is a default shell on many nix systems
- default shebang #!/bin/bash


## zsh

- zshell is a default shell on macos since macOS Catalina (2019)
- default shebang #!/bin/zsh

- get folder in which current script is running
  > mydir=${0:a:h}
