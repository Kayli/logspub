# notes related to software that matters to me atm


## basics

- types that matter
  - free open source (foss)
  - closed-source
  - everything-in-between


## game theory

- even in closed-source software
  - solutions are reverse-engineered
  - source codes eventually are getting solen
  - patents expire

- tbd: consider reviewing related studies and materials
  - https://onlinelibrary.wiley.com/doi/10.1002/smj.3222


## fos software

- nix oses
- rockbox
  - gitlab mirror: https://gitlab.com/mi-mi-mirrors/rockbox
- openwrt https://openwrt.org
- shinobi https://shinobi.video
- music production [^1]
  - lmms https://lmms.io
  - ardour https://ardour.org
  - vital: spectral warping table synth plugin https://vital.audio
  - zynaddsubfx: musical software synthesizer https://github.com/zynaddsubfx/zynaddsubfx 
  - drums plugin: https://drumgizmo.org/
  - noise repellent https://github.com/lucianodato/noise-repellent
  - and more, see [^1]
- security
  - bitwarden
    - Donyelle Werner, Attorney Bitwarden Inc. 1 North Calle Cesar Chavez, Suite 102 Santa Barbara, California 93103
      donyelle@donyellewernerlaw.com Phone: (415) 307-7492


## hardware with foss firmware support

- pine64
  - alt names: pine store limited
  - devices: pinebook, pinephone, pinepower, pinecil

- rockbox
  - ipod classic 5 gen
    - https://www.ebay.com/itm/352615082200
    - price: 150 USD (as of 2021/07)
  - xDuoo X3
    - https://www.ebay.com/itm/353574355506
    - price: 125 USD (as of 2021/07)
  - FiiO M3K
    - https://www.amazon.ca/gp/product/B07JDR5SYZ
    - builds https://download.rockbox.org/daily/fiiom3k/
    - bootloader instructions https://forums.rockbox.org/index.php/topic,53858.0.html
    - price: 95 CAD (as of 2021/09)
    - bootloader instructions
      - pull and run build cluster container overriding default entrypoint
        $ docker pull built1n/rbclient
        $ docker run -it --entrypoint=/bin/bash built1n/rbclient:latest
      - build rockbox
        - pull latest version from github and follow standard instructions
      - build bootloader similar way you built rockbox
        - just select 'bootloader' option after choosing your platform while running configure script
      - copy bootloader and rockbox files to host machine
        - docker cp <container-id>:/home/rb/rockbox/build/bootloader.m3k /home/illiak/projects/rockbox/
        - docker cp <container-id>:/home/rb/rockbox/build/rockbox.zip /home/illiak/projects/rockbox/
      - make sure sdcard formatted in fat32
      - copy bootloader and rockbox to sdcard
          $ cp ./bootloader.m3k /run/media/illiak/MUSIC/
          $ unzip ./rockbox.zip -d <sdcard-folder-path>
      - build jztool for your platform
        - make sure libusb is installed by running
          $ apt-get install libusb-1.0-0-dev
        - run make in a tool folder
          $ cd /home/rb/rockbox/rbutil/jztool
          $ make
        - copy built jztool binary to host machine
          $ docker cp <container-id>:/home/rb/rockbox/rbutil/jztool/jztool /home/illiak/projects/rockbox/
      - to connect the player in USB boot mode, follow these steps
        - ensure the player is fully powered off
        - plug one end of the USB cable into your player
        - hold down your player's USB boot key: volume down
        - plug the other end of the USB cable into your computer
        - let go of the USB boot key
      - run jztool on the host, it will start bootloader on a device without flashing it
        $ sudo ./jztool fiiom3k load bootloader.m3k
      - backup your original bootloader and save the file
      - install rockbox bootloader
      - run player as usual, everything should work


## references

[^1]: https://www.youtube.com/watch?v=qistxioVgMw
