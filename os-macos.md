# macos related useful information

## terminal commands

- list block devices (like lsblk on linux)
  > diskutil list

- flash image to a thumb drive
  > sudo dd if=/Users/illiak/Downloads/someos.iso of=/dev/disk2 bs=16777216

- clean clipboard 
  > pbcopy < /dev/null

## system extensions

- pieces of code that can run independently of any user
- network extensions can monitor and filter network traffic
- needs developer subscription which costs 100 bucks a year
- running/debugging system extensions without subscription is a pain, as you need to
  - reset all previous System Extensions
    > systemextensionsctl reset
  - turn on developer mode and disable some of the restrictions like having to run from /Applications
    > systemextensionsctl developer on
  - disable system integrity protection (sip) by running command from terminal in recovery mode
    > csrutil disable
  - disabling apple mobile file integrity (amfi) by running command from terminal in recovery mode
    > nvram boot-args="amfi_get_out_of_my_way=0x1"



## useful libraries

- kernel sources mirror https://github.com/apple/darwin-xnu
- python bindings for macos api https://github.com/ronaldoussoren/pyobjc/


## useful applications

- opensource application firewall https://objective-see.com/products/lulu.html
  - warning: posts some user data to a third-party service


## references

[^1]: https://stackoverflow.com/questions/60674561/how-to-run-un-signed-system-extensions-in-osx-catalina
