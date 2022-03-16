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


## references

[^1]: https://en.wikipedia.org/wiki/Real-time_operating_system
