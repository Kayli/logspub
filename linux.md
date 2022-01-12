# self learning course notes on linux

## managing processes

display all running processes
```bash
ps -aux
```

To kill process with the specified name
```bash
pkill -f <process_name>
```

## working with archives

Zip file on linux with highest compression rate
```bash
zip -9 archive-name.zip file1 file2 file3 ...
```

Zip files in a folder recursively
```bash
zip -r myfiles.zip mydir
```

## system logs

Log files for
- global activity 
  - Debian /var/log/syslog
  - RedHat /var/log/messages
- kernel events, errors, and warning logs
  - /var/log/kern.log stores 

Follow system log. Can be useful when connecting new devices, like thumb-drives
```bash
tail -f /var/log/messages
```

To access more advanced/structured logs, use syslog https://tools.ietf.org/html/rfc5424#section-6


## services

How to restart services in Linux
- https://www.techrepublic.com/article/how-to-start-stop-and-restart-services-in-linux/

```bash
sudo systemctl stop httpd
sudo systemctl start httpd
sudo systemctl restart httpd
sudo service httpd start
​sudo service httpd stop
​sudo service httpd restart
```

## working with git 

Show log and commit details
```bash
git log
git show <hash>
```

Amend last commit
```bash
git commit --amend -m'message'
```

List all git lfs files 
```bash
git lfs ls-files --all
```

Stage changed files with detecting renamed ones
```bash
git -A add .
```


## flashing images

List partitions for the devices matched by a pattern sdi*
```bash
fdisk -l /dev/sdi
```
List block devices
```bash
lsblk
```
- using dd
  - sudo dd of=/dev/mmcblk1 status=progress oflag=direct bs=16M && sync

Backup boot sector area of emmc drive where manjaro was installed
```bash
sudo dd if=/dev/mmcblk2 of=boot-sector-manjaro-emmc.img bs=512 count=62500
```
Command to restore boot sector back
```bash
sudo dd if=boot-sector-manjaro-emmc.img of=/dev/mmcblk2 bs=512
```


## regular expression pattern matching

- this will search/match 'test' and 'hui' strings within a <filename> document
  - case insesitive search is enabled with -i argument

```bash
cat <filename> | egrep -i '^(test|hui)'
```


## networking

- there are several tools that you can use to check for open ports: netstat, ss, lsof, nmap
- open port doesn’t mean anyone from outside can access those ports
  - those ports can still be blocked by software, cloud, or hardware firewall.

```bash
sudo netstat -tulpn | grep LISTEN
sudo ss -tulpn
sudo lsof -i -P -n | grep LISTEN
sudo nmap -sT -O localhost
```

- to scan all network devices in your local segment
  $ sudo nmap -sn 192.168.1.0/24


### firewall

'ufw' is a system firewall with simple and intuitive cli
https://askubuntu.com/questions/448836/how-do-i-with-ufw-deny-all-outgoing-ports-excepting-the-ones-i-need#

```bash
sudo ufw default deny outgoing
sudo ufw default deny incoming
sudo ufw allow 6969               # qbittorent
sudo ufw allow out dns
sudo ufw allow out http
sudo ufw allow out https
sudo ufw enable
```


## copying/syncing/backup

- to sync folders in archival mode
  - this command performs recursive sync of folders preserving timestamps, symlinks, etc.
    $ rsync -a <src> <dst>
  - to restore
    $ rsync -aruv <src> <dst>

- on-demand snapshot using timeshift
  $ sudo timeshift --create --comments "before omf install"

- create snapshot using snapper
  $ ?


## kernel related

- UserMode Linux (UML)
  - allows to run the kernel as a userspace application - this is called 


## robotic operation system (ROS) related commands

To run "roscore" process from the "ros:latest" docker image named as "rosmaster" container use the following command: 

```bash
docker run -itd --rm \
    --name rosmaster \
    ros:latest  \
    roscore
```

Attach to already running ROS container via interactive shell:

```bash
docker exec -ti rosmaster /opt/ros/melodic/env.sh bash
```

To list topics inside ROS container:

```bash
rostopic list
```


## frequently encountered terms

- loop device, vnd (vnode disk), or lofi (loop file interface)
  - pseudo-device that makes a file accessible as a block device


## editors

- debian-specific
  - add micro editor to the list of selectable ones via 'select-editor' command
    - register
    ```bash 
    sudo update-alternatives --install /usr/bin/editor editor /usr/bin/micro 50
    ```
    - interactively select default among different alternatives
    ```bash
    sudo update-alternatives --config editor
    ```


## misc file operations

- determines type of a file, checks some file attributes, etc
  - will notify about result of the operation with an exit code
  - e.g. to check if file exists use -e flag and watch for return codes: 0 exists, 1 no such file
  $ test -e <filename>

- check for exit code of the last executed command
  $ echo $?

- flatten files in a folder hierarchy command
  $ find /dir1 -mindepth 2 -type f -exec mv -t /dir1 -i '{}' +

- watch changes in fs [^1]
  - inotify
    - creates a kernel object for every watched file
      - therefore not usable to monitor all changes happening in fs
  - fanotify
    - requires kernel patch to be usable 

- disk usage analyzers
  - ncdu: ncurses interface, fast

- recursively delete files of specific type in a folder
  $ find <path> -name "*.bak" -type f -delete


## containers

- To run portainer on desktop-old machine as illiak user us the following command:
```bash
cd ~/portainer
./portainer --template-file "${PWD}/templates.json" --data "${PWD}/data" -p :8080
```
This command implies that portainer installed in home directory. 
After that browse to http://localhost:8080/#/home and login using your user password as admin
See this link for more details: https://portainer.readthedocs.io/en/latest/deployment.html

- copy file from inside of the running docker container
```bash
docker ps -alq # get last container id
docker cp <containerId>:/file/path/within/container /host/path/target
```

## audio

- set default audio sink using alsa
  - list sinks available 
    $ pactl list short
  - set default sink by id
    $ pactl set-default-sink 45


## music

- from youtube
  - using following command to download audio
    - $ youtube-dl -f 'bestaudio[ext=m4a]' <playlist id or url>
  - using the following command to download video of the best quality
    - $ youtube-dl -f 'best' <playlist id or url>
  - with a sequence number in filename, add 
    - $ youtube-dl -o "%(playlist_index)s-%(title)s.%(ext)s" -f 'bestaudio[ext=m4a]' <playlist id or url>


# documents

- to read office, pdf and bunch of other preproessed documents from command line
  you can use lesspipe like the following:
  $ lesspipe.sh <filename> | less


## fish shell

- omf (plugin manager) useful plugins
  - archlinux
  - bang-bang

- indexer loop
  $ for i in (seq 1 20); echo "test$i.wav"; end


## video encoding

- convert webm to mp4 without transcoding media streams
  $ ffmpeg -i video.webm -c:v copy -c:a copy video.mkv
  
- fix broken/truncated file index
  $ ffmpeg -i <broken> -vcodec copy -acodec copy <fixed>


## arch specific

- to figure out fastest mirrors 
  - generate list for your country https://archlinux.org/mirrorlist/
  - update /etc/pacman.d/mirrorlist
  - use tool to rank mirrors by actual connection speed
    - rankmirrors -v /etc/pacman.d/mirrorlist
- update trusted gpg keys
  - sudo packman -Sy archlinux-keyring


## garuda specific

- after fresh install 
  - make sure to disable following services
    $ sudo systemctl stop smb.service && sudo systemctl disable smb.service
    $ sudo systemctl stop saned.socket && sudo systemctl disable saned.socket
  - scan local ports with nmap
    $ sudo nmap -sT -O 192.168.0.102
  - update system
    $ sudo pacman -Syu
  - install a bunch of software
    $ sudo pacman -S pamac kitty 


## xfce specific

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
