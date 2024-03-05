# notes related to writing shell scripts

## basics

- shell is a computer program which exposes an operating system's services to a human user or other programs
- popular shells: bash, zsh, fish
- symbolic link to executable file is also executable


## debugging

- enables a mode of the shell where all executed commands are printed to the terminal
  > set -x

- enables a mode of the shell that will make the script exit with an error whenever an error occurs
  > set -e


## bash

- bash is a default shell on many nix systems
- default shebang #!/bin/bash

- single quotes results in non-interpolated string

- generate random number
  > echo $RANDOM

- generate hash
  > cat file | md5sum

- get first n characters from a stream
  > cat file | head -c <n>

- inplace substitution in a file by string match
  > sed -i "s|old string|new string,|" <filename>

- create file from a script with specified content
  ```bash
    cat << EoF > ./my-document.txt
    Hello world
    Have a nice day
    EoF
  ```

- pause script execution
  > read -s -n 1 -p "Press any key to continue . . ."

- conditionals
  - string equality check: spaces around = operator are very important!!!
    > if [ $my_var = test ] ; then echo yes ; else echo no ; fi
  - substring pattern check, double brackets are very important!
    > if [[ $my_var = *my_substring* ]] ; then echo yes ; else echo no ; fi
  - string is null check (has zero length)
    > if [ -z $my_var ]
  - string is not null
    > if [ -n $my_var ]

- check if folder 
  - is empty
    > if [ -z "$(ls -A -- "$dir")" ]; then echo yes ; else echo no ; fi
  - exists
    > if [ -d "$dir" ]; then echo 'exists'; else echo 'not found'; fi
  - does not exist
    > if [ ! -e "$TWOHAT_DIR" ]; then echo 'not found'; else echo 'exists'; fi

- string substitution
  - substring substitution
    > my_var=test
    > echo ${my_var/est/bla}
    tbla
  - removes .tar.gz extension from the value of my_var variable
    > echo "${my_var/.tar.gz/}"

- stdin
  - single dash "-", when not part of an option, is often used by convention to signify that a program should process stdin, as opposed to a file

- loops
  - user-defined list of files
    DOCKERFILES=(
      docker/client-connector/Dockerfile-client-connector-base
      docker/client-connector/Dockerfile-client-connector-code
      docker/client-connector/Dockerfile-client-connector-no-config
    )
    for f in ${DOCKERFILES[*]}; do
      docker run -i --rm $(DEFAULT_ACR).azurecr.io/tools/hadolint:20220310 hadolint --ignore DL3059 - < $f
    done

- run command as a different user
  > su [username] -c "[command]"

- export [name[=value]] ...
  - the supplied names are marked for automatic export to the environment of subsequently executed commands



## zsh

- zshell is a default shell on macos since macOS Catalina (2019)
- default shebang #!/bin/zsh

- get folder in which current script is running
  > mydir=${0:a:h}


## batch files (.bat)

- comments
  - 'rem' command
  - colon symbol ":" at the beginning of the line

- fail fast
  - neither 'cmd' nor 'powershell' don't have 'fail fast' mode for commands execution
  - while bash provides a `set -eo pipefail` exit code handling mode

- to run scripts as admin use
  > runas /user:Administrator <my-script.bat>

- create local user
  > net user <username> <password> /add
- delete local user
  > net user <username> /delete
- grant full access to folder
  > icacls <path> /grant <username>:(OI)(CI)F /T
- remove folder recursively
  > rmdir <mydir> /s /q

- common exit codes
  - 0	Program successfully completed
  - 1	Incorrect function. Indicates that Action has attempted to execute non-recognized command
  - 2	The system cannot find the file specified
  - 3	The system cannot find the path specified
  - 5	Access is denied


## task runners

- gnu make
- just https://github.com/casey/just
  - written in rust
