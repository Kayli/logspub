# notes related to windows os, likely windows 11 and above


## windows 11

- impressions
  - its scary to see how many glitches this os has when just installed
  - some windows are rendered blurry on my secondary monitor
    - fucking nonsense. how much time they need to fix this shit?
  - while resizing 'windows terminal' app window, blinking white stripes appear
  - on a first startup windows were rendered broken
    - as some drivers installations were changing resolution in background
  - during installation hotkeys were not available to choose right value from long combo-boxes
    - so i had to scroll throgh the whole thing
  - explorer process crashes/restarts regularily
  - my secondary keyboard layout was selected by default after reboot despite it was last in priority list
  - app updates and systems updates are two different things
    - while updates are happenning in a background, your app process may just be killed without your permission
  - hyper-v virtual machine has a way to select from preconfigured linux ubuntu distributives, but
    - ubuntu interface is lagging
    - was hanging with black screen several times during installation, so had to hard reset vm
  - system tray was renamed to "taskbar corner" which is weird
    - it also no longer support option for always showing all tray icons, you need to enable each icon manually
  - synaptics trackpoint started moving mouse cursor on its own
    - wanted to turn it off, but trackpoint settings were unavailable/greyed-out
    - in device manager there was no option to disable this specific device
    - initiated system update, after which trackpoint stopped working
    - but touchpad buttons stopped working as well! (or they're part of trackpoint??)
    - trackpoint settings are still greyed-out, which doesn't make much sense
  - notepad does not repaint contents of it screen sometimes, when window is inactive
    - so visually it looks like there is an empty notepad window in the background, until you click on it
    - only after activating this window its contents get repainted
  - edge browser forces me to look at market ticker on a new tab page
    - to remove this option you have to guess that its called 'show greeting'
  - windows button menu takes 5-7 seconds to load and be responsive after reboot
    - this lag is fucking nonsesne, don't they have automated tests to catch shit like that?

- its 2023 and issue with different dpi monitors still haven't been solved
  - if you choose high-dpi monitor as your main one and other monitors are standard dpi - some text becomes blurred
    - 'clear type' mode is enabled, but doesn't help
  - workaround
    - select low-dpi monitor as a main one
    - make sure to reboot

- strange 'there is nothing to show here' bug when opening pictures in standard photos app
  - happens when you open files from 'recent' folder
    - picture opens but then suddenly disappears displaying 'there is nothing to show here'
  - likely reason: those files are likely temporary/short-living
  - solution: open same files from 'pictures' folder, should be fine


## windows 10

- virtual desktops 
  - switching from one vd to another is visually glitchy (fixed as of aug 2023)
  - wallpaper is the same for every vd, there is no way to set a different one

- onedrive does not recognize @microsoft account, such a nonsense


## managed service account

- managed service accounts are identified by ending in a dollar sign ($)
  - they allow to run programs as an account that doesn't require a password while still having the security of a strong password
  - example: IIS may use managed service accounts to impersonate app that connects to sql database using windows authentication


## useful folders

- startup C:\Users\<username>\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup


## useful apps

- AutoHotkey https://www.autohotkey.com/ (source code https://github.com/Lexikos/AutoHotkey_L)


## useful powershell commands

- echo path in powershell
  > $env:path.split(";")

- test if port opened
  > tnc <hostname> -Port <port>

- check service running
  > Get-Service <servicename>

- zip/unzip file from command line (no max file size limitation)
  - compress file or folder into a tar.gz archive
    > tar -czvf name-of-archive.tar.gz /path/to/directory-or-file
  - extract into a folder
    > tar -xzvf database/LSMP.tar.gz -C C:projects/lsmp-git/compose/database

- unblock executable file downloaded from internet
  > Unblock-File -Path <filepath>

- getting credentials interactively
  ```powershell
    $username="EU8I" //default user name
    $cred=Get-Credential $username
    $passwd=[Runtime.InteropServices.Marshal]::PtrToStringAuto([Runtime.InteropServices.Marshal]::SecureStringToBSTR( $cred.Password ))
  ```


## wsl

- security considerations
  - WSL is as secure as any other program running in your Windows user account
  - only the Windows security model matters
    - running as root inside WSL doesn't actually give more permissions than running as a standard user the things that you can do from that perspective are 100% exactly the same (in either case) as the things that the user who ran the Windows wsl.exe program (or other WSL-launching command) could do


## related products

- outlook: selected tree menu item (left) is too pale and hard to see
- onedrive does not recognize @microsoft account, such a nonsense
- outlook and calendar in office 365 are snappier than old app at first glance
