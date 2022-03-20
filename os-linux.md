# notes related to linux os

## basics

- kernel source code: https://github.com/torvalds/linux

- popular distributives
  - debian
    - package manager: apt
    - forks
      - ubuntu
        - mint (de: cinnamon, mate, xfce)
      - pop!_os (de: cosmic)
  - arch
    - package manager: pacman
    - forks: garuda, manjaro
  - alpine
    - package manager: apk

- popular desktop environments
  - gnome (versions 2.x, 3.x)
    - forks: mate, cinnamon, cosmic
    - gtk: multi-platform toolkit for creating graphical user interfaces
  - kde
  - xfce

- system level components
  - systemd

- cross-distribution package managers
  - flatpack
  - snap
  - homebrew


## frequently encountered terms

- loop device, vnd (vnode disk), or lofi (loop file interface)
  - pseudo-device that makes a file accessible as a block device


## useful commands

- managing processes
  - display all running processes
    > ps -aux
  - kill process with the specified name
    > pkill -f <process_name>

- working with archives
  - zip file on linux with highest compression rate
    > zip -9 archive-name.zip file1 file2 file3 ...
  - zip files in a folder recursively
    > zip -r myfiles.zip mydir

- system logs
  - log files for
    - global activity (everything except auth-related messages)
      - debian /var/log/syslog
      - redhat /var/log/messages
    - kernel events, errors, and warnings
      > less /var/log/kern.log
  
  - follow system log (can be useful when connecting new devices, like thumb-drives)
    > tail -f /var/log/messages
  
  - to access more advanced/structured logs, use syslog https://tools.ietf.org/html/rfc5424#section-6

- systemd-journald
  - view logs for specific service journalctl -u <servicename>

- system services  [^3]
  - basic commands
    > sudo systemctl stop <servicename>
    > sudo systemctl start <servicename>
    > sudo systemctl restart <servicename>
    > sudo service <servicename> start
    ​> sudo service <servicename> stop
    ​> sudo service <servicename> restart
  - creating your own service [^4]

- git version control
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

- flashing images
  - list partitions for the devices matched by a pattern sdi*
    > fdisk -l /dev/sdi
  - list block devices
    > lsblk
  - using dd
    > sudo dd of=/dev/mmcblk1 status=progress oflag=direct bs=16M && sync
  - backup boot sector area of emmc drive where manjaro was installed
    > sudo dd if=/dev/mmcblk2 of=boot-sector-manjaro-emmc.img bs=512 count=62500
  - command to restore boot sector back
    > sudo dd if=boot-sector-manjaro-emmc.img of=/dev/mmcblk2 bs=512

- regular expression pattern matching
  - this will search/match 'test' and 'hui' strings within a <filename> document, ignoring case
    > cat <filename> | egrep -i '^(test|hui)'

- networking
  - there are several tools that you can use to check for open ports: netstat, ss, lsof, nmap
  - open port doesn’t mean anyone from outside can access those ports
    - those ports can still be blocked by software, cloud, or hardware firewall.
      > sudo netstat -tulpn | grep LISTEN
      > sudo ss -tulpn
      > sudo lsof -i -P -n | grep LISTEN
      > sudo nmap -sT -O localhost

  - to scan all network devices in your local segment
    > sudo nmap -sn 192.168.1.0/24

  - list established tcp connections
    > sudo lsof | grep TCP | grep ESTAB

  - firewall
    - 'ufw' is a system firewall with simple and intuitive cli
    - 'deny all except' example: [5]
      > sudo ufw default deny outgoing
      > sudo ufw default deny incoming
      > sudo ufw allow 6969               # qbittorent
      > sudo ufw allow out dns
      > sudo ufw allow out http
      > sudo ufw allow out https
      > sudo ufw enable

- copying/syncing/backup
  - to sync folders in archival mode
    - this command performs recursive sync of folders preserving timestamps, symlinks, etc.
      > rsync -a <src> <dst>
    - to restore
      > rsync -aruv <src> <dst>

  - on-demand snapshot using timeshift
    > sudo timeshift --create --comments "before omf install"

- kernel related
  - usermode linux (UML)
    - allows to run the kernel as a userspace application

- editors
  - debian-specific
    - add micro editor to the list of selectable ones via 'select-editor' command
      - register
        > sudo update-alternatives --install /usr/bin/editor editor /usr/bin/micro 50
      - interactively select default among different alternatives
        > sudo update-alternatives --config editor

- misc file operations
  - determines type of a file, checks some file attributes, etc
    - will notify about result of the operation with an exit code
    - e.g. to check if file exists use -e flag and watch for return codes: 0 exists, 1 no such file
      > test -e <filename>

  - check for exit code of the last executed command
      > echo $?

  - flatten files in a folder hierarchy command
      > find /dir1 -mindepth 2 -type f -exec mv -t /dir1 -i '{}' +

  - watch changes in fs [^1]
    - inotify
      - creates a kernel object for every watched file
        - therefore not usable to monitor all changes happening in fs
    - fanotify
      - requires kernel patch to be usable 

  - disk usage analyzers
    - ncdu: ncurses interface, fast

  - recursively delete files of specific type in a folder
    > find <path> -name "*.bak" -type f -delete

  - merge two files
    > diff --unchanged-group-format="" src1 src2 > dst

- containers
  - copy file from inside of the running docker container
    > docker ps -alq # get last container id
    > docker cp <containerId>:/file/path/within/container /host/path/target

- audio
  - alsa
    - list sinks available 
      > pactl list short
    - set default sink by id
      > pactl set-default-sink 45

- music
  - download from youtube
    - using following command to download audio
      > youtube-dl -f 'bestaudio[ext=m4a]' <playlist id or url>
    - using the following command to download video of the best quality
      > youtube-dl -f 'best' <playlist id or url>
    - with a sequence number in filename, add 
      > youtube-dl -o "%(playlist_index)s-%(title)s.%(ext)s" -f 'bestaudio[ext=m4a]' <playlist id or url>

- documents
  - read office, pdf and other preproessed documents
    > lesspipe.sh <filename> | less

- fish shell
  - omf (plugin manager) useful plugins: archlinux, bang-bang
  - indexer loop
    > for i in (seq 1 20); echo "test$i.wav"; end

- video encoding
  - convert webm to mp4 without transcoding media streams
    > ffmpeg -i video.webm -c:v copy -c:a copy video.mkv
    
  - fix broken/truncated file index
    > ffmpeg -i <broken> -vcodec copy -acodec copy <fixed>

- arch specific
  - to figure out fastest mirrors 
    - generate list for your country https://archlinux.org/mirrorlist/
    - update /etc/pacman.d/mirrorlist
    - use tool to rank mirrors by actual connection speed
      > rankmirrors -v /etc/pacman.d/mirrorlist
  - update trusted gpg keys
    > sudo packman -Sy archlinux-keyring

- garuda specific
  - after fresh install 
    - make sure to disable following services
      > sudo systemctl stop smb.service && sudo systemctl disable smb.service
      > sudo systemctl stop saned.socket && sudo systemctl disable saned.socket
    - scan local ports with nmap
      > sudo nmap -sT -O 192.168.0.102
    - update system
      > sudo pacman -Syu
    - install a bunch of software
      > sudo pacman -S pamac kitty 

- popos specific
  - install touche from popshop to invert touchpad 4-finger gestures [^6]
  


- xfce specific
  - windows resize
    - alt + right mouse button
    - incasing the size of resize border area by editing ~/.gtkrc-2.0 [^2]
    - hotkeys + mouse
      - alt + space to invoke a window's menu then R to run resize 
      - then Left Right Top or Bottom Arrow Key to chose direction
      - use touch pad to actually resize a window


## references

[^1]: https://superuser.com/questions/118642/recursive-filesystem-notifications-inotify-for-ubuntu-karmic-koala
[^2]: https://unix.stackexchange.com/questions/156435/how-can-i-make-windows-easier-to-resize-in-xfce
[^3]: https://www.techrepublic.com/article/how-to-start-stop-and-restart-services-in-linux/
[^4]: https://medium.com/codex/setup-a-python-script-as-a-service-through-systemctl-systemd-f0cc55a42267
[^5]: https://askubuntu.com/questions/448836/how-do-i-with-ufw-deny-all-outgoing-ports-excepting-the-ones-i-need
[^6]: https://www.reddit.com/r/pop_os/comments/oin0ev/invert_workspace_touchpad_gestures/h4wjyz0/
