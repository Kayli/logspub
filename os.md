# notes on operating systems

## basics

- operating system (OS)
  - is system software that manages computer hardware, software resources
  - provides common services for computer programs

- categorization based on
  - source code availability 
    - open source: linux, freebsd
    - closed source: windows, macos
  - system resources sharing approach [^1]
    - realtime
      - are usually event-driven
      - switch between tasks based on their priorities
    - time-sharing
      - switch between tasks based on clock interrupts


## nix

- pipeline
  - mechanism for inter-process communication using message passing
    - set of processes chained together by their standard streams, 
      - output text of each process (stdout) is passed directly as input (stdin) to the next one
    - second process is started as the first process is still executing
      - so they are executed concurrently


## provable kernels

- seL4 [ess-e-ell-four]
  - world's most advanced, most highly assured operating-system kernel
  - it is also a hypervisor
    - supports virtual machines that can run a fully fledged guest os such as linux
  - member of the L4 family of microkernels
  - written in asm, c, isabelle
  - comes with a formal, mathematical, machine-checked proof of implementation correctness



### useful commands

- copy file from remote ssh to host
  > scp 'username@ipaddress:/home/username/Downloads/*.pdf' ~/Downloads

- install ssh key to remote server from client
  - make sure password authentication is enabled
  - run the following command
    > ssh-copy-id -i ~/.ssh/id_ed25519.pub username@ipaddress
  - this adds your public key to authorized_keys on a server machine
    - it means you can add key to this file on a server manually if password authentication is disabled
  - you can disable password authentication after installing a key


## references

[^1]: https://en.wikipedia.org/wiki/Real-time_operating_system
