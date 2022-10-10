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



## useful folders

- startup C:\Users\<username>\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup


## useful apps

- AutoHotkey https://www.autohotkey.com/ (source code https://github.com/Lexikos/AutoHotkey_L)


## useful commands

- echo path in powershell
  > $env:path.split(";")


## related products

- outlook: selected tree menu item (left) is too pale and hard to see
- onedrive does not recognize @microsoft account, such a nonsense
