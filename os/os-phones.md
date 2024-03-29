# self education course on foss mobile oses

## design

- there are 4 essential layers
  - arm chip hardware
  - firmware
    - ATF (arm trusted firmware)
      - for ATF to correctly interact with p-boot, ATF needs to be patched, in order not to run U-Boot specific code
      - loaded into A64 SRAM A2
        - rk3399 chip has 192KB total, 4KB of which is used by bootrom when bootup
      - uses reference implementation available at https://github.com/ARM-software/arm-trusted-firmware
    - SCP (system control processor firmware) 
      - libre implementation is called "crust", improves battery life and thermal performance by implementing 
        a deep sleep state. During deep sleep, the CPU cores, the DRAM controller, and most onboard peripherals are 
        powered down, reducing power consumption by 80% or more compared to an idle device. 
      - on boards without a PMIC, Crust is also responsible for orderly power-off and power-on of the device
        For this to work, Crust runs outside the main CPU and DRAM, on a dedicated always-on microprocessor called SCP
    - ATF and SCP share the same SRAM, packaged into a single binary
  - bootloader software
    - u-boot https://github.com/u-boot/u-boot (installed by default)
    - p-boot https://xnux.eu/p-boot/ (more lightweight and friendly implementation)
  - os software
    - rk3399 ported linux kernel https://github.com/rockchip-linux/kernel

- terminology
  - ATF stands for ARM Trusted Firmware
    - goal: develop and maintain reference software (firmware) for SoCs which provides trusted boot, 
            secure runtime interface and secure services
  - SCP stands for System Control Processor
    - a dedicated processor that is used to abstract power and system management tasks away from application processors
    - read more at https://developer.arm.com/tools-and-software/open-source-software/firmware/scp-firmware
  - SoC developers stands for system on chip developers


## android [1]

- runtimes
  - dalvik vm: used till 2013
  - android runtime (art)
    - application runtime environment used by the android operating system
    - unlike dalvik, art introduces the use of ahead-of-time (aot) compilation by compiling entire applications into native machine code upon their installation
    - once an application is compiled by using art's on-device dex2oat utility, it is run solely from the compiled elf executable

- “плацебо” обновления
  - были случаи, когда вендоры отправляли патчи пустышки – обновления по факту приходят, а в нем нет ничего. такие обновления можно назвать “плацебо”, т.к. часть пользователей верит, что они делают их устройства быстрее и безопаснее

- механизм direct boot
  - позволяет приложениям работать до ввода пароля на устройстве. 
  - приложение сможет использовать часть хранилища, которая не требует разблокировки пользователем, а достаточно загрузить устройство. так вы без проблем получите sms, телефонные звонки, будильники, пуш уведомления и др.

- project treble
  - гарантирует обратную совместимость с 3 предыдущими версиями реализации вендора
  - это значит, что gsi android 13 можно будет установить на любое устройство с android 12, 11 и 10.



## oses tested

- ubuntu touch 
  - tested on Jan 24, 2021
  - managed to make a phonecall, configure lte internet

- sailfish
  - good
    - very good looking interface, original design idea
  - problems
    - setting initial pin screen is broken 
    - mobile data is not working (maybe its my device's hardware issue?)
    - wifi is not working
      - despite showing my connection, allowing me to enter password
    - orientation switch doesn't work
    - camera is not working
    - no reboot button, only power-off

- ubuntu touch same version but latest build
  - good
    - front camera started working!
      - its slow as hell, but still ...
    - no way to skip interactive tutorial at first boot
    - cell lte data doesn't work
      - checked in "morph browser" and "open store" apps
    - sound started working!!
      - tested in "phone" and "morph browser" apps
  - problems
    - didn't find a build number in menu
      - downloaded file name has no number as well
      - jenkins shows build #97
    - gallery app 
      - is not detecting orientation of the image properly
        - vertical photo shown horizontally
      - thumbnails are not displayed
      - not obvious how to enter "edit mode" for an album to change title, subtitle
      - there is one image in the gallery app that fails to load
      - phone
        - tried calling 3 numbers and both calls faileds 
        - those 3 attempts were not saved in "recent calls"
  - problems expected
    - video recording isn't working
    - camera orientation is messed up
      - its reversed horizontally
    - recorder app is not recording: fails with "data flow" error

- ubuntu touch 16.04 2020-09-18
  - good
    - well polished, nice looking and consistent initial setup wizard experience
    - interactive tutorial is helpful, organically integrated with the main ui flow
    - empty screens contain helpful messages suggesting most likely next action
      - messages app -> new message, contacts, etc
    - open store with apps and updates
      - lots of apps available for download
    - overall ui design is great, well thought-through, production quality
    - ability to select between different update channels: stable and edge?
    - morph browser worked good for a couple of sites i was browsing
      - embedded video played well (but no sound, see problems section)
    - storage screen is really cool
    - vpn support
    - app permissions management
    - sound indicator shows that there is no sound!! 
      - thats great, as system is able to detect its own problems
    - free-text search throughout system menus
    - rich choice of keyboard settings/layouts  

  - problems
    - blank screens on boot for too long 
      - after first pine64 splash, before second ubuntu touch splash 6-7 sec
      - after restart been initiated
    - no way to see detailed log instead of splash screen by pressing a button
      - would be better: press 'up' button to hide splash screen and see a detailed log messages
    - no sample photos in a photos app by default, unable to test this app further
    - fetching channels screen takes forever to load
      - progress indicator is of anemic kind: spinning wheel of suffering
        - gave up after waiting 1-2 minutes
    - checking for updates spinning wheel didn't stop for 3 minutes of me watching it spinning
      - kinda useless invention, not a real progress/timeout indicator 
    - long press on app navigates to store screen instead of more logical action ... 
      - like suggesting to drop it on a desktop
    - why desktop is empty and its not clear how to move app icons to it? 
      - i thought that it is maybe utilized for some desktop widgets ... but wasn't able to find any
      - really strange design decision to leave desktop empty, surprised to see that
    - why quick launch panel is on the left of the screen?
      - ui designer must be lefty of something 
      - is it configurable at least? wasn't able to find this option
   
    - minor
      - vertical/horizontal orientation switch is lagging
      - can't find "system update" button, only app updates 
      - small inconsistency
        - pictures for wallpaper available via system settings but not visible in gallerey 
      - no message indicating that camera is not working 
        - but for disabled/not-implemented sound there is a crossed-out speaker icon
      - expected
        - camera app is not working, blank screen for both cameras
        - no sound in multidistro version
        - animations are lagging a bit (as there is no GPU support yet)
    - overall impression
      - best foss mobile os ive seen so far
      - will seriously consider moving to it from android once sound is fixed
        - phone app should work as well
    - a stretch
      - would be ideal os if "recording calls app" is available
        - i don't even know if its possible hardware-wise, need to research a bit more  
- kde neon
  - problems
    - unable to login
      - default pins from official websites don't work, tried: 1234 and 123456
      - root passwords don't work, tried empty one, 1234 and 123456
      - phablet/1234 didn't work
    - screen breaks when changing orientation in locked mode
      - horizontal mode renders only half of the screen and another half is broken
      - after switching modes couple of times it breaks completely, so that only reboot helps
    - minor
      - blank screen on boot for too long
  - summary: 
    - wasn't able to really test it, failed to login
    - maybe its a side-effect of multidistro packaging process ... 
      - not sure, need to verify that hypothesis
- maemo leste
  - slovenian team project? translates as 'we have the best'
  - positive 
    - openrc as a service manager
    - clean and detailed boot log
    - animations are sexy, despite of small visual artifacts here and there
    - ui design is simple and original, feels good and usable
    - virtual desktops
  - problems
    - where is a "phone" app?
    - shows blank screen for a while, when loading graphical user interface
      - user may be confused if os failed to load or what ...
      - no progress indicators or trace messages when loading gui 
    - internet connection
      - keeps asking for wifi connection even after connecting to a dock with ethernet cable
        - shows "not connected" in system menu (tap on clock)
      - unable to use password-protected wifi 
        - after entering password nothing happens and i got prompted to connect to wifi once again
      - booting up with lan connected via dock has no positive effect
        - still "no connection" message displayed
    - terminal
      - pressing "enter" key on external keyboard does some freaky shit: virtual keyboard shows up with empty editbox
        - i have no way of entering commands using external keyboard 
      - very strange choice of default colors (black text on white background) for preinstalled terminal app
    - horizontal orientation is not sensitive to g-force? sensors: will not rotate 180 if usb-c is on the left
    - tana_ap_user button does nothing
    - system menu location is not obvious
      - tapping on a clock opens the menu
      - there are plenty of space available on a screen to come up with some dedicated "system menu" button 
    - pdf reader
      - no sample pdf file provided, so that i can quickly check how the app works
    - after using os for some time it just blacked out and became unresponsive
    - htop crashed when i've tried to run preinstalled htop app by tapping on an app icon
    - switches off with a blank screen showing no shutdown progress messages
      - so you don't know if its still in the process or done
      - i have a suspicion that it just hangs with the black screen, as pressing power button doesn't turn on device
        - so i have to do a longpress to hard-reset a thing
    - minor: 
      - no vertical orientation
      - no reboot button, only a switch-off one
      - some rendering glitches/artifacts when swiping on a calendar form (pulling form beyond the edges of the screen)
        - behavior is correct: feels springy and returns back to consistent position
        - rendering is flaky: 
          - animation is full of visual artifacts
          - sometimes artifacts remain after animation is finished and user is not doing anything
      - "debian" icon name is confusing, consider changing to "debian apps"
    - "add shortcut" button is too deep in a menu tree
      - consider showing "add shortcut" button near the "options (gear) button when tapping on a desktop  
  - summary: good impression overall, distribution is original enough and has a potential
  

- multidistro https://xnux.eu/p-boot-demo/
  - written on their website: designed to allow users to try all available pinephone oses without too much hassle
  - suppose to play on 'unification' side of unification-diversity duality
  - good
    - superfast startup of a bootloader with oses selection
    - sleek ui
    - supports jumpdrive 
    - supports booting from internal emmc
    - night and day when comparing to u-boot
  - problems
    - very minor one: touching screen does not resetting shutdown timer
      - i was confused at first when tried to use device without back cover
      - after some time i realized that touchscreen is not envolved at all and i should use physical up-down keys 
    - next day pboot stopped booting into selection menu
      - showing "arch pinephone p-boot" splash screen and then tty login prompt
      - i should consider learning how to build multidistro with latest os images by myself
    - no git repository in a public hosting like github/gitlab
      - self-hosted is fine, but no mirrors is kinda weird
  - notes
    - all passwords were changed to 1111 where possible 
    - manjaro password is 123456. Root passwords are 1111
    - sxmo login/password is mo/1111

- pinephone oses already tried in Dec 2020
  - overall impression
    - can't really use any of reviewed oses
    - lies on project websites about state/readiness of their software was really killing me 
      - ... so disappointing :(
      - my only explanation of the phenomenon: 
        - there is some kind of money laundering happenning
        - or maybe just unprofessional management teams in charge
        - so they were just overblowing marketing side, while making barely demoable alpha previews
    - you can't call management irresponsible, as you can fake 'responsible' behavior
      - so on a surface it will look like person/team is responsible
      - but in practice they will feed you will bullshit every fucking time
      - i've seen so many instances of that happenning on commercial projects
        - caused lots of pain and suffering for technical people involved
  - manjaro, mobian
    - was hard to do basic menu navigation operations 
      - e.g. switching between menus/different apps
    - felt like an alpha preview of software
  - postmarketos (alpine linux derivative)
    - most adequate (usable) of 3 i've tried
    - but still needs more polish to be a real replacement for android


## references

[1]: https://habr.com/ru/companies/broadcast/articles/763094/