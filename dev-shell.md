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
- conditionals
  - string equality check: spaces around = operator are very important!!!
    > if [ $my_var = test ] ; then echo yes ; else echo no ; fi
  - substring pattern check, double brackets are very important!
    > if [[ $my_var = *my_substring* ]] ; then echo yes ; else echo no ; fi
  - string is null check (has zero length)
    > if [ -z $my_var ]
  - string is not null
    > if [ -n $my_var ]

- string substitution
  - substring substitution
    > my_var=test
    > echo ${my_var/est/bla}
    tbla
  - removes .tar.gz extension from the value of my_var variable
    > echo "${my_var/.tar.gz/}"

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


## zsh

- zshell is a default shell on macos since macOS Catalina (2019)
- default shebang #!/bin/zsh

- get folder in which current script is running
  > mydir=${0:a:h}
