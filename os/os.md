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
  - world's most advanced, most highly assured operating-system kernel (marketing blurb?)
  - it is also a hypervisor
    - supports virtual machines that can run a fully fledged guest os such as linux
  - member of the L4 family of microkernels
  - written in asm, c, isabelle
  - comes with a formal, mathematical, machine-checked proof of implementation correctness


## ssh

- user configuration folder is ~/.ssh
- known_hosts file lets the client authenticate the server, to check that it isn't connecting to an impersonator
  - user: ~/.ssh/known_hosts
  - system-wide: /etc/ssh/known_hosts
- ~/.ssh/authorized_keys file lets the server authenticate the user

- scp tool allows to copy files using ssh
  - copy file from remote ssh to host
    > scp 'username@ipaddress:/home/username/Downloads/*.pdf' ~/Downloads

- install ssh key to remote server
  - you need to already have ssh connection to the target machine
    - most likely scenario is that you're admin who already has ssh access to machine B
    - and you want to allow access from machine A to machine B
  - run the following command, to add your public key to authorized_keys on a server machine
    > ssh-copy-id -i ~/.ssh/id_ed25519.pub username@ipaddress


## popular executable library formats

- pe: on microsoft windows
- elf: on linux and most other versions of unix
- mach-o: on macos and ios
- mz: on dos

- fat binary (or multiarchitecture binary)
  - is a computer executable program or library which has been expanded (or "fattened") with code native to multiple instruction sets which can consequently be run on multiple processor types


## references

[^1]: https://en.wikipedia.org/wiki/Real-time_operating_system
