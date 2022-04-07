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
  - member of the L4 family of microkernels
  - written in asm, c, isabelle
  - comes with a formal, mathematical, machine-checked proof of implementation correctness



### useful commands

- copy file from remote ssh to host
  > scp 'ilichpost_gmail_com@35.233.131.109:/home/ilichpost_gmail_com/Downloads/*.pdf' ~/Downloads


## references

[^1]: https://en.wikipedia.org/wiki/Real-time_operating_system
