# self education course on foss laptop oses


- manjaro 
  - version
    - desktop: plasma 5.20.4
    - kernel 5.10.2-1-MANJARO-ARM
  - positive
    - looks great
    - ui elements are intuitive and configurable
    - downloadable wallpapers with rating system
  - problems
    - window snapping/resizing is not trivial to do using only a keyboard
      - people with disabilities (e.g. cerebral palsy) may appreciate this function
      - one variant of reasonable defaults could be
        - super + arrows - snapping to edges
        - super + shift + alt+  arrows - resize by 20px
        - super + shift + arrows - move by 20px
        - fn + '+'/'-' - grow window (resize in all four directions)
        - ctrl + super + arrows - switching virtual desktops
          - handy for a 'cube' mode
    - virtual desktops are half broken in "cube" mode
      - adding more than 1 rows does nothing and disappears after reopening settings window 
    - terminal startup time is about 1.5 sec, which is huge for such simple app
      - ideally should happen immediately without any visible delay
      - even if prompt slowed down by startup shell scripts ... window itself should appear much faster
    - boot log is not really visible on a startup/shutdown after user presses esc key


- garuda
  - version: dragonized edition, installed around Dec 2020
  - positive
    - pretty damn good looking os, very good job!
    - better modularity: latte dock is a separate app (from the rest of kde ui?)
    - nice cube animation of virtual desktops (but there is a room for improvement)
  - problems
    - distro gets bloated
      - boot times are slower and slower
      - nonsense splashscreens with anemic spinners are killing me
    - boot log could be better
      - shows nothing for a while and then displays lots of messages (probably cached in some buffer?)
        - better way: show boot messages one by one immediately after they spitted out
      - has 2 splash screens, with 2nd one not having any intuitive way to view detailed progress log
    - "cube" virtual desktop animation
      - is inconsistent 
        - cube is actually not a cube, but faked animation without actual model of a cube
        - instead, they are using NxM grid as a model, which is fundamentally inconsistent with cube animation
          - should be polyhedron net of sorts https://en.wikipedia.org/wiki/Net_(polyhedron)
      - cube settings menu is broken
        - after adding/removing rows starts glitching
        - apply button stays disabled even after changing stuff
        - default name for new rows start containing error messages
      - okay, they removed cube haha, so funny, like gave up on trying to fix it )))))
    - setting wifi password is a pain
      - editbox gets swapped for a new one with someone elses network as list refreshes
      - that issue is at least 6 months old already (writing this at dec 9 2021)
    
    
- systemd based distros
  - lack of modularity/diversity: may hinder development of ecosystem
  - bloated software is akin to 
    - huge human egos (creator's projections?) with all good and bad consequences
    - political parties
    - ideologies
  - good aspects
    - successful integration project
    - high cohesion of components being driven/evolved towards the same consistent goal
    - suggests that there may be a need for additional os "system" layer between "core" and "interface" ones 
  - bad aspects
    - gives single "systemd" name to lots of tools, which steals recognition/visibility from authors of individual components
    - has ambition of a separate linux distro without actually being one   
    - may be harder to swap components
    
    
  
