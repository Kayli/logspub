# macos related useful information

## startup configuration

- check Preferences > Users & Groups > Login Items
- startup items can also be located in one of the following folders
  - /Library/StartupItems
  - /Library/LaunchAgents
  - /Library/LaunchDaemons
  - ~/Library/LaunchAgents

- commands from following files are executed on every shell start
  - ~/.zprofile
  - ~/.zshrc


## executable binary format

- mach-o (mach object)
  - format for executables, object code, shared libraries, dynamically loaded code, and core dumps
  - like 'elf' on linux, 'pe' on windows


## useful terminal commands

- list block devices (like lsblk on linux)
  > diskutil list

- flash image to a thumb drive
  > sudo dd if=/Users/illiak/Downloads/someos.iso of=/dev/disk2 bs=16777216

- clean clipboard 
  > pbcopy < /dev/null

- test remote port
  > nc -vz <ip> <port>

- view shell commands full history
  > less ~/.zsh_history


## system extensions

- pieces of code that can run independently of any user
- network extensions can monitor and filter network traffic
- needs developer subscription which costs 100 bucks a year
- running/debugging system extensions without subscription is a pain, as you need to [1]
  - reset all previous System Extensions
    > systemextensionsctl reset
  - turn on developer mode and disable some of the restrictions like having to run from /Applications
    > systemextensionsctl developer on
  - disable system integrity protection (sip) by running command from terminal in recovery mode
    > csrutil disable
  - disabling apple mobile file integrity (amfi) by running command from terminal in recovery mode
    > nvram boot-args="amfi_get_out_of_my_way=0x1"


## screen sharing

- sidecar: sharing screen on macos with ipad


## finder

- show hidden files: command + shift + . (the period key)


## useful libraries

- kernel sources mirror https://github.com/apple/darwin-xnu
- python bindings for macos api https://github.com/ronaldoussoren/pyobjc/


## useful applications

- opensource application firewall https://objective-see.com/products/lulu.html
  - warning: posts some user data to a third-party service


## security [2]

- gatekeeper
  - verifies that the software 
    - from an identified developer
    - notarized by Apple to be free of known malicious content
    - and hasn’t been altered
  - requests user approval before opening downloaded software for the first time to make sure the user hasn’t been tricked into running executable code they believed to simply be a data file

- system integrity protection (sip) 
  - is a security technology designed to help prevent potentially malicious software from modifying protected files and folders
  - introduced in OS X El Capitan (2015)
  - does not allow root user to change certain system folders

- XProtect
  - identifies and blocks malware when its just copied/downloaded
  - acts to remediate malware that has managed to successfully execute
  - scans only apps that have been changed or apps at first launch


## references

[1]: https://stackoverflow.com/questions/60674561/how-to-run-un-signed-system-extensions-in-osx-catalina
[2]: https://habr.com/ru/companies/bastion/articles/763468/